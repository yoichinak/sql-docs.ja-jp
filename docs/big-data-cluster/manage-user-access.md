---
title: Active Directory モードでビッグ データ クラスター アクセスを管理する
description: ビッグ データ クラスターへのアクセスを管理する
author: NelGson
ms.author: negust
ms.reviewer: mikeray
ms.date: 08/04/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ef2df0bec343d73de90a43e411da92530c3c50c8
ms.sourcegitcommit: 6ab28d954f3a63168463321a8bc6ecced099b247
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/05/2020
ms.locfileid: "87790270"
---
# <a name="manage-big-data-cluster-access-in-active-directory-mode"></a>Active Directory モードでビッグ データ クラスター アクセスを管理する

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

この記事では、*clusterUsers* 構成設定を介して展開中に提供されるグループに加え、*bdcUser* ロールを持つ新しい Active Directory グループを追加する方法について説明します。

>[!IMPORTANT]
>*bdcAdmin* ロールを持つ新しい Active Directory グループはこの手順で追加しないでください。 HDFS や Spark などの Hadoop コンポーネントによって、BDC の *bdcAdmin* ロールに相当するスーパーユーザー グループとして Active Directory グループが 1 つだけ許可されます。 展開後にビッグ データ クラスターに、*bdcAdmin* アクセス許可を持つ追加の Active Directory グループを与えるには、展開時に登録済みのグループにユーザーとグループを追加する必要があります。 *bdcUsers* ロールを持つグループ メンバーシップを同じ手順で更新できます。

## <a name="two-overarching-roles-in-the-big-data-cluster"></a>ビッグ データ クラスターの 2 つの主要なロール

ビッグ データ クラスター内の承認に使用する 2 つの主要なロールの一部として、展開プロファイルのセキュリティ セクションで Active Directory グループを指定することができます。

* `clusterAdmins`:このパラメーターは、1 つの Active Directory グループを受け取ります。 このグループのメンバーには *bdcAdmin* ロールが与えられます。つまり、クラスター全体の管理者アクセス許可が与えられます。 SQL Server に *sysadmin* アクセス許可、Hadoop 分散ファイル システム (HDFS) および Spark には *superuser* アクセス許可、コントローラーには *administrator* 権限が付与されます。

* `clusterUsers`:これらの Active Directory グループは BDC で *bdcUsers* ロールにマッピングされます。 これらは、クラスターに管理者アクセス許可のない通常のユーザーです。 SQL Server マスター インスタンスにログインするアクセス許可が付与されますが、既定では、オブジェクトまたはデータに対するアクセス許可はありません。 これらは、*superuser* アクセス許可のない、HDFS と Spark の通常のユーザーです。 コントローラー エンドポイントに接続するとき、これらのユーザーはエンドポイントにのみクエリを実行できます (*azdata bdc endpoints list* を使用します)。

Active Directory 内のグループ メンバーシップを変更せずに追加の Active Directory グループの *bdcUser* アクセス許可を付与するには、次のセクションの手順を完了します。

## <a name="grant-bdcuser-permissions-to-additional-active-directory-groups"></a>追加の Active Directory グループに *bdcUser* アクセス許可を付与する

### <a name="create-a-login-for-the-active-directory-user-or-group-in-the-sql-server-master-instance"></a>SQL Server マスター インスタンスで Active Directory ユーザーまたはグループのログインを作成する

1. 好みの SQL クライアントを使用して、マスター SQL エンドポイントに接続します。 任意の管理者のログイン (たとえば、展開時に提供された `AZDATA_USERNAME`) を使用します。 または、セキュリティ構成で `clusterAdmins` として提供された Active Directory グループに属する任意の Active Directory アカウントを使用できます。

1. Active Directory ユーザーまたはグループのログインを作成するには、次の TSQL コマンドを実行します。

   ```sql
   CREATE LOGIN [<domain>\<principal>] FROM WINDOWS;
   ```

   SQL Server インスタンスで目的のアクセス許可を付与する:

   ```sql
   ALTER SERVER ROLE <server role> ADD MEMBER [<domain>\<principal>];
   GO
   ```

サーバー ロールの完全一覧が必要であれば、[こちら](../relational-databases/security/authentication-access/server-level-roles.md)でそれに対応する SQL Server セキュリティ トピックをご覧ください。

### <a name="add-the-active-directory-user-or-group-to-the-roles-table-in-the-controller-database"></a>コントローラー データベースの roles テーブルに Active Directory ユーザーまたはグループを追加します。

1. 次のコマンドを実行して、コントローラーの SQL server 資格情報を取得します。

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

1. 前の接続を使用し、*roles* テーブルと *active_directory_principals* テーブルに新しい行を挿入します。 大文字で「*REALM*」という値を入力します。

   ```sql
   USE controller;
   GO

   INSERT INTO [controller].[auth].[roles] VALUES (N'<user or group name>@<REALM>', 'bdcUser')
   GO

   INSERT INTO [controller].[auth].[active_directory_principals] VALUES (N'<user or group name>@<REALM>', N'<SID>')
   GO
   ```

   追加されるユーザーまたはグループの SID を見つけるには、[Get-ADUser](/powershell/module/addsadministration/get-aduser/) または [Get-ADGroup](/powershell/module/addsadministration/get-adgroup/) PowerShell コマンドを使用できます。

2. コントローラー エンドポイントにログインするか、SQL Server マスター インスタンスに認証することで、追加したグループのメンバーに、想定どおりの *bdcUser* アクセス許可が与えられていることを確認します。 次に例を示します。

   ```bash
   azdata login
   azdata bdc endpoints list
   ```

## <a name="next-steps"></a>次のステップ

- [SQL Server 2019 ビッグ データ クラスターのセキュリティの概念](concept-security.md)
