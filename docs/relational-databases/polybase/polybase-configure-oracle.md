---
title: 外部データへのアクセス:Oracle - PolyBase
description: この記事では、PolyBase を使用して Oracle のデータにアクセスする外部データ ソースを作成する方法を示します。
ms.date: 12/13/2019
ms.custom: seo-lt-2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: 29a8d7074d88af68605831529ca0e92e58a6129e
ms.sourcegitcommit: 757b827cf322c9f792f05915ff3450e95ba7a58a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2020
ms.locfileid: "92134820"
---
# <a name="configure-polybase-to-access-external-data-in-oracle"></a>Oracle 上の外部データにアクセスするための PolyBase の構成

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

この記事では、SQL Server インスタンス上で PolyBase を使用して、Oracle 上の外部データに対してクエリを実行する方法について説明します。

## <a name="prerequisites"></a>前提条件

PolyBase をインストールしていない場合は、「[PolyBase のインストール](polybase-installation.md)」をご覧ください。

  データベース スコープ資格情報より前に、[マスター キー](../../t-sql/statements/create-master-key-transact-sql.md)を作成しておく必要があります。 

## <a name="configure-an-oracle-external-data-source"></a>Oracle の外部データ ソースを構成する

Oracle データ ソースのデータに対してクエリを実行するには、外部テーブルを作成して外部データを参照する必要があります。 このセクションでは、これらの外部テーブルを作成するサンプル コードを示します。

このセクションでは以下の Transact-SQL コマンドが使用されます。

- [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
- [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 
- [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)


1. Oracle ソースにアクセスするために、データベース スコープ資格情報を作成します。

    ```sql
    /*  specify credentials to external data source
    *  IDENTITY: user name for external source. 
    *  SECRET: password for external source.
    */
    CREATE DATABASE SCOPED CREDENTIAL credential_name WITH IDENTITY = 'username', Secret = 'password';
    ```
    
   > [!IMPORTANT] 
   > PolyBase 用の Oracle ODBC コネクタでサポートされるのは、Kerberos 認証ではなく、基本認証のみです。 

1. [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md) を使用して外部データ ソースを作成します。

    ```sql
    /* 
    * LOCATION: Location string should be of format '<vendor>://<server>[:<port>]'.
    * PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
    * CONNECTION_OPTIONS: Specify driver location
    * CREDENTIAL: the database scoped credential, created above.
    */  
    CREATE EXTERNAL DATA SOURCE external_data_source_name
    WITH ( LOCATION = 'oracle://<server address>[:<port>]',
    -- PUSHDOWN = ON | OFF,
    CREDENTIAL = credential_name)
    ```

1. **省略可能:** 外部テーブルの統計を作成します。

    最適なクエリのパフォーマンスを得るために、外部テーブルの列、特に結合、フィルター、集計に使用される列に対して統計を作成することをお勧めします。

    ```sql
    CREATE STATISTICS statistics_name ON customer (C_CUSTKEY) WITH FULLSCAN; 
    ```

>[!IMPORTANT] 
>外部データ ソースを作成すると、[CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) コマンドを使用して、そのソース上でクエリ可能なテーブルを作成することができます。 

詳細と例については、次の記事を参照してください。

- [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md)
- [SQL Server PolyBase の概要](polybase-guide.md)
