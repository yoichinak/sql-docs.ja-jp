---
title: AZDATA_PASSWORD を更新する
description: '`AZDATA_PASSWORD` を手動で更新する'
author: NelGson
ms.author: negust
ms.reviewer: mikeray
ms.date: 12/19/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7fe856ae92c198d44ed0b11d1d2ce808e87fb4eb
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100039682"
---
# <a name="manually-update-azdata_password"></a>`AZDATA_PASSWORD` を手動で更新する

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

クラスターが Active Directory 統合で動作しているかどうかにかかわらず、展開時に `AZDATA_PASSWORD` が設定されます。 これにより、クラスター コントローラーとマスター インスタンスに基本認証が提供されます。 このドキュメントでは、`AZDATA_PASSWORD` を手動で更新する方法について説明します。

## <a name="change-azdata_password-for-controller"></a>コントローラーの `AZDATA_PASSWORD` を変更する

クラスターが非 Active Directory モードで動作している場合は、次の手順を実行して、Apache Knox ゲートウェイのパスワードを更新します。

1. 次のコマンドを実行して、コントローラーの SQL Server 資格情報を取得します。

   a. Kubernetes 管理者として次のコマンドを実行します。

   ```bash
   kubectl get secret controller-sa-secret -n <cluster name> -o yaml | grep password
   ```

   b. シークレットを Base64 でデコードします。
   
   ```bash
   echo <password from kubectl command>  | base64 --decode && echo
   ```

1. 別のコマンド ウィンドウで、コントローラー データベースのサーバー ポートを公開します。

   ```bash
   kubectl port-forward controldb-0 1433:1433 --address 0.0.0.0 -n <cluster name>
   ```
 
1. 先ほど取得したシステム管理者パスワードを使用して、SQL クライアント ツールからコントローラー データベース サーバーに接続します。

1. `AZDATA_USERNAME` の新しい複雑なパスワードを生成して、既存の `AZDATA_PASSWORD` を置き換えます。

   生成されるパスワードは "newPassword" なので、この例を簡単にするために、次の手順では "newPassword" を使用します。 

1. users テーブルから `hexsalt` を取得します。

   ```sql
   SELECT hexsalt FROM [auth].[users] WHERE username = '<username>'
   ```

   `hexsalt` からランダムな 16 進文字列が返されます (たとえば、`64FC59DF31244FFEE02F457BC0750226`)。

1. `hexsalt` を使用して、新しい複雑なパスワードを暗号化します。

   参考までに、パスワードを暗号化するための事前に構築されたツール `pbkdf2` が用意されています。 [`pbkdf2`](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/security/password-hashing/pbkdf2/prebuilt-binaries) 用のプラットフォームに適した .NET Core アプリをダウンロードします。

   アプリは自己完結型であり、.NET ランタイムなどの必須コンポーネントは必要ありません。 パスワードを暗号化するには、以下を実行します。

   ```bash
   pbkdf2 <password> <hexsalt>
   J2y4E4dhlgwHOaRr3HKiiVAKBfjuGDyYmzn88VXmrzM=
   ```

1. users テーブルのパスワードを更新します。

   ```SQL
   UPDATE [auth].[users] SET password = 'J2y4E4dhlgwHOaRr3HKiiVAKBfjuGDyYmzn88VXmrzM=' WHERE username = '<username>'
   ```

## <a name="change-azdata_password-in-the-sql-server-master-instance"></a>SQL Server マスター インスタンスの `AZDATA_PASSWORD` を変更する

1. 任意の管理者ユーザーを使用して、マスター SQL エンドポイントに接続します。

1. パラメーター `AZDATA_USERNAME` で展開時に定義したログイン資格情報のパスワードを変更するには、次の TSQL コマンドを実行します。

   ```sql
   ALTER LOGIN <AZDATA_USERNAME> WITH PASSWORD = 'newPassword'
   ```
