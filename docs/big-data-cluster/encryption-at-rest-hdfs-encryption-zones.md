---
title: SQL Server ビッグ データ クラスター HDFS 暗号化ゾーンの使用ガイド
titleSuffix: SQL Server big data clusters
description: この記事では、BDC の SQL Server HDFS 暗号化ゾーン機能の使用方法について説明します。
author: DaniBunny
ms.author: dacoelho
ms.reviewer: mihaelab
ms.date: 10/19/2020
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 904b07913a63e226e5e45876f2fc520226411223
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92199590"
---
# <a name="sql-server-big-data-clusters-hdfs-encryption-zones-usage-guide"></a>SQL Server ビッグ データ クラスター HDFS 暗号化ゾーンの使用ガイド

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

このガイドでは、SQL Server ビッグ データ クラスターの保存時の暗号化機能を使用し、暗号化ゾーンを使用して HDFS フォルダーを暗号化する方法について説明します。

使用できる状態になっている、マウントされた既定の暗号化ゾーンが __```/securelake```__ に既に存在することに注意してください。 これは、 __securelakekey__ という名前のシステム生成の 256 ビット キーを使用して作成されました。 このキーは、追加の暗号化ゾーンを作成するために使用できます。

## <a name="prerequisites"></a><a id="prereqs"></a> 前提条件

- Active Directory 統合を使用する [SQL Server ビッグ データ クラスター CU8 以降](release-notes-big-data-cluster.md)。
- 管理特権を持つユーザー。

## <a name="login-into-the-name-node"></a>name ノードにログインする

[Active Directory の接続手順](active-directory-connect.md)に関するページを参照して、クラスターのログインを実行します。 namenode (nmnode-0-0) にログインして、キーおよび暗号化ゾーン コマンドを発行します。

   ```console
   kubectl exec -it -c hadoop -n <cluster_namespace> nmnode-0-0 -- /bin/bash
   ```

## <a name="create-an-encryption-zone-using-the-provided-system-managed-key"></a>指定されたシステム マネージド キーを使用して暗号化ゾーンを作成する

1. HDFS フォルダーを作成します

   ```console
   hdfs dfs -mkdir -p /user/zone/folder
   ```

1. encryption zone create コマンドを発行して、 __securelakekey__ キーを使用してフォルダーを暗号化します。

   ```console
   hdfs crypto -createZone -keyName securelakekey -path /user/zone/folder
   ```

## <a name="create-a-custom-new-key-and-encryption-zone"></a>カスタムの新しいキーと暗号化ゾーンを作成する

1. 次のパターンを使用して、256 ビットのキーを作成します。

   ```console
   kinit hdfs
   hadoop key create mydatalakekey -size 256
   ```

1. ユーザー キーを使用して、新しい HDFS パスを作成し、暗号化します。

   ```console
   hdfs dfs -mkdir -p /user/mydatalake
   hdfs crypto -createZone -keyName mydatalakekey -path /user/mydatalake
   ```
