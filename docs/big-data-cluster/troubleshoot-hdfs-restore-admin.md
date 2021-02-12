---
title: HDFS のアクセス許可の復元
titleSuffix: SQL Server Big Data Cluster
description: HDFS 管理者権限を復元します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.date: 04/21/2020
ms.topic: how-to
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d914b2006656162b233351815e238f282d73e913
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100045532"
---
# <a name="restore-hdfs-permissions"></a>HDFS のアクセス許可の復元

HDFS のアクセス制御リスト (ACL) の変更が HDFS 内の `/system` および `/tmp` フォルダーに影響する可能性があります。 ACL の変更の原因として、ユーザーがフォルダーの ACL を手動で操作することが考えられます。 /system フォルダーと /tmp/logs フォルダー内のアクセス許可を直接変更することはサポートされていません。

## <a name="symptom"></a>症状

spark ジョブを ADS 経由で送信すると、SparkContext の初期化エラーと AccessControlException で失敗します。

```
583 ERROR spark.SparkContext: Error initializing SparkContext.
org.apache.hadoop.security.AccessControlException: Permission denied: user=<UserAccount>, access=WRITE, inode="/system/spark-events":sph:BDCAdmin:drwxr-xr-x
```

Yarn UI には KILLED 状態のアプリケーション ID が表示されます。

ドメイン ユーザーとしてフォルダーに書き込もうとしても失敗します。 次の例を使用してテストすることができます。

```bash
kinit <UserAccount>
hdfs dfs -touch /system/spark-events/test
hdfs dfs -rm /system/spark-events/test
```

## <a name="cause"></a>原因

HDFS ACL が BDC ユーザー ドメイン セキュリティ グループ用に変更されました。 考えられる変更として、/system フォルダーと /tmp フォルダーの ACL があります。 これらのフォルダーの変更はサポートされていません。

Livy ログで効果を確認します。

```
INFO utils.LineBufferedStream: YYYY-MM-DD-HH:MM:SS,858 INFO yarn.Client: Application report for application_1580771254352_0041 (state: ACCEPTED)
...
WARN rsc.RSCClient: Client RPC channel closed unexpectedly.
INFO interactive.InteractiveSession: Failed to ping RSC driver for session <ID>. Killing application
```

YARN UI には、そのアプリケーション ID のアプリケーションが KILLED 状態で表示されます。

RPC 接続が閉じられる根本的な原因を取得するには、アプリケーションに対応するアプリの YARN アプリケーション ログを確認します。 前の例では、`application_1580771254352_0041` を参照しています。 `kubectl` を使用して sparkhead-0 ポッドに接続し、次のコマンドを実行します。

次のコマンドを使用すると、アプリケーションの YARN ログに対してクエリが実行されます。

```bash
yarn logs -applicationId application_1580771254352_0041
```

次の結果では、ユーザーのアクセス許可が拒否されています。 

```
YYYY-MM-DD-HH:MM:SS,583 ERROR spark.SparkContext: Error initializing SparkContext.
org.apache.hadoop.security.AccessControlException: Permission denied: user=user1, access=WRITE, inode="/system/spark-events":sph:BDCAdmin:drwxr-xr-x
```

BDC ユーザーが HDFS ルート フォルダーに再帰的に追加されたことが原因である可能性があります。 これは既定のアクセス許可に影響を与えた可能性があります。

## <a name="resolution"></a>解像度

次のスクリプトを使用してアクセス許可を復元します。管理者権限で `kinit` を使用します。

```bash
hdfs dfs -chmod 733 /system/spark-events
hdfs dfs -setfacl --set default:user:sph:rwx,default:other::--- /system/spark-events
hdfs dfs -setfacl --set default:user:app-setup:r-x,default:other::--- /system/appdeploy
hadoop fs -chmod 733 /tmp/logs
hdfs dfs -setfacl --set default:user:yarn:rwx,default:other::--- /tmp/logs
```
