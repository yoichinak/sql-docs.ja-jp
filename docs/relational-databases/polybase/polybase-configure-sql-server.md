---
title: 外部データへのアクセス:SQL Server - PolyBase
description: SQL Server インスタンス上で PolyBase を使用して、別の SQL Server インスタンス上の外部データに対してクエリを実行する方法について説明します。 外部データを参照する外部テーブルを作成します。
ms.date: 10/06/2020
ms.custom: seo-lt-2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: 23eadb2089e3f692e5e054441b7617e09e71ac01
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "92005849"
---
# <a name="configure-polybase-to-access-external-data-in-sql-server"></a>SQL Server 上の外部データにアクセスするための PolyBase の構成

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

この記事では、SQL Server インスタンス上で PolyBase を使用して、別の SQL Server インスタンス上の外部データに対してクエリを実行する方法について説明します。

## <a name="prerequisites"></a>前提条件

PolyBase をインストールしていない場合は、「[PolyBase のインストール](polybase-installation.md)」をご覧ください。 インストールに関する記事では、前提条件について説明します。 また、インストールが完了したら、[PolyBase を有効にする](polybase-installation.md#enable)ようにしてください。

SQL Server の外部データ ソースによって、SQL 認証が使用されます。

データベース スコープ資格情報より前に、[マスター キー](../../t-sql/statements/create-master-key-transact-sql.md)を作成しておく必要があります。 

## <a name="configure-a-sql-server-external-data-source"></a>SQL Server の外部データ ソースを構成する

SQL Server データ ソースのデータに対してクエリを実行するには、外部テーブルを作成して外部データを参照する必要があります。 このセクションでは、これらの外部テーブルを作成するサンプル コードを示します。
 
最適なクエリのパフォーマンスを得るために、外部テーブルの列、特に結合、フィルター、集計に使用される列に対して統計を作成します。

このセクションでは以下の Transact-SQL コマンドが使用されます。

- [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
- [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 
- [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)

1. SQL Server ソースにアクセスするために、データベース スコープ資格情報を作成します。 次の例では、`IDENTITY = 'username'` および `SECRET = 'password'` を使用して、外部データ ソースに対する資格情報を作成します。

    ```sql
    CREATE DATABASE SCOPED CREDENTIAL SqlServerCredentials
    WITH IDENTITY = 'username', SECRET = 'password';
    ```
   >[!IMPORTANT]
   >PolyBase 用の SQL ODBC コネクタでサポートされるのは、Kerberos 認証ではなく、基本認証のみです。

1. [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md) を使用して外部データ ソースを作成します。 次のような例です。

   - `SQLServerInstance` という名前の外部データ ソースを作成します。
   - 外部のデータ ソースを識別します (`LOCATION = '<vendor>://<server>[:<port>]'`)。 この例では、SQL Server の既定のインスタンスを指しています。
   - 計算をソースにプッシュする必要があるかどうかを識別します (`PUSHDOWN`)。 `PUSHDOWN` は既定では `ON` です。

   最後に、この例では、前に作成した資格情報を使用します。

    ```sql
    CREATE EXTERNAL DATA SOURCE SQLServerInstance
        WITH ( LOCATION = 'sqlserver://SqlServer',
        PUSHDOWN = ON,
        CREDENTIAL = SQLServerCredentials);
    ```

1. 必要に応じて、外部テーブルの統計を作成します。

  最適なクエリのパフォーマンスを得るために、外部テーブルの列、特に結合、フィルター、集計に使用される列に対して統計を作成します。

  ```sql
    CREATE STATISTICS statistics_name ON customer (C_CUSTKEY)
    WITH FULLSCAN;
  ```

>[!IMPORTANT]
>外部データ ソースを作成すると、[CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) コマンドを使用して、そのソース上でクエリ可能なテーブルを作成することができます。

## <a name="sql-server-connector-compatible-types"></a>SQL Server コネクタの互換性のある型

SQL Server の接続を認識するその他のデータ ソースに接続することができます。 SQL Server PolyBase のコネクタを使用して、Azure Synapse Analytics と Azure SQL Database の両方の外部テーブルを作成します。 このタスクを実行するには、前に示したのと同じ手順に従います。 データベース スコープ資格情報、サーバーのアドレス、ポート、場所の文字列が接続先の互換データ ソースのものと関連付けられていることを確認してください。

## <a name="next-steps"></a>次のステップ

PolyBase の詳細については、[SQL Server PolyBase の概要](polybase-guide.md)に関する記事をご覧ください。
