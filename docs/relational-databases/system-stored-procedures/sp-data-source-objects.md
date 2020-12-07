---
description: sp_data_source_objects (Transact-sql)
title: sp_data_source_objects |Microsoft Docs
ms.custom: ''
ms.date: 11/14/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sp_data_source_objects
helpviewer_keywords:
- PolyBase
ms.assetid: 48066431-fed2-4a8a-85af-ac704689e183
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: d30a5190d88a0b3714f670f5f253c2a31e98f69e
ms.sourcegitcommit: 2e7154475ba1f31d1aeebc8f48ac05846f793736
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126608"
---
# <a name="sp_data_source_objects-transact-sql"></a>sp_data_source_objects (Transact-sql)

[!INCLUDE [sqlserver2019](../../includes/applies-to-version/sqlserver2019.md)]

仮想化できるテーブルオブジェクトの一覧を返します。

> [!NOTE]
> この手順は、 [SQL 2019 CU5](../../big-data-cluster/release-notes-big-data-cluster.md#cu5)で導入されました。

![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

## <a name="syntax"></a>構文  

```syntaxsql
sp_data_source_objects  
         [ @data_source = ] 'data_source'
     [ , [ @object_root_name = ] 'object_root_name' ]
     [ , [ @max_search_depth = ] max_search_depth ]
     [ , [ @search_options = ] 'search_options' ]
[ ; ]
```  
  
## <a name="arguments"></a>引数  

`[ @data_source = ] 'data_source'`   
メタデータの取得元となる外部データソースの名前。 `@data_source` は `sysname` です。  

`[ @object_root_name = ] 'object_root_name'`   
このパラメーターは、検索対象のオブジェクトの名前のルートです。 `@object_root_name``nvarchar(max)`,、既定値は `NULL` です。

この呼び出しは、に設定された値で始まる外部オブジェクトのみを返し `@object_root_name` ます。

ODBC データソースが3つの部分で構成される名前を使用するリレーショナルデータベース管理システム (RDBMS) に接続する場合、に `@object_root_name` はデータベース名の一部を含めることはできません。 このような場合、パラメーターには `@object_root_name` 3 つの部分がすべて含まれている必要があります。3番目の部分は検索するオブジェクト名です。
> [!CAUTION]
> 外部データプラットフォームの違いにより、の既定値が指定されている場合、一部のプラットフォームでは結果が返されません `NULL` 。 `NULL`フィルターの欠如として扱われるものもあります。 たとえば、がに指定されている場合、Oracle RDMBS は結果を返しません `NULL` `@object_root_name` 。

`[ @max_search_depth = ] max_search_depth`   
この値は、検索対象のの最大の深さ (部分単位) を指定し `@object_root_name` ます。 `@max_search_depth` の型は `int` で、既定値は1です。

たとえば、が `@max_search_depth` 1 で `@object_root_name` SQL Server データベースの名前がである場合、データベース内に含まれるスキーマが返されます。

`@max_search_depth` `NULL` `@object_root_name` カタログまたはスキーマの場合、のは、存在するかどうかに関する情報を返します。

`[ @search_options = ] 'search_options'`   
`search_options`パラメーターは nvarchar (max) で、既定値は `NULL` です。

このパラメーターは使用されませんが、将来実装される可能性があります。

## <a name="result-sets"></a>結果セット

| 列名 | データ型 | 説明 |
|--|--|--|
| OBJECT_TYPE | nvarchar(200) | オブジェクトの種類 (例: テーブルまたはデータベース)。 |
| OBJECT_NAME | nvarchar(max) | オブジェクトの完全修飾名。 バックエンド固有の引用符を使用してエスケープされます。 |
| OBJECT_LEAF_NAME | nvarchar(max) | 修飾されていないオブジェクト名。 |
| TABLE_LOCATION | nvarchar(max) | CREATE EXTERNAL TABLE ステートメントに使用できる有効なテーブルの場所の文字列。 適用されない場合は、になり `NULL` ます。 |
  
## <a name="permissions"></a>アクセス許可

ALTER ANY EXTERNAL DATA SOURCE 権限が必須です。  

## <a name="remarks"></a>解説  

SQL Server インスタンスに  [PolyBase](../../relational-databases/polybase/polybase-guide.md) 機能がインストールされている必要があります。

このストアドプロシージャは、次のコネクタをサポートしています。

- SQL Server
- Oracle
- Teradata
- MongoDB
- Cosmos DB

ストアドプロシージャは、汎用 ODBC dta ソースコネクタをサポートしていません。

Empty と non empty の概念は、ODBC ドライバーと[ `SQLTables` 関数](../native-client-odbc-api/sqltables.md)の動作に関連しています。 空以外の場合は、行ではなくテーブルがオブジェクトに含まれていることを示します。 たとえば、空のスキーマには SQL Server にテーブルが含まれていません。 空のデータベースには、Teradata 内にテーブルが含まれていません。

オブジェクトの種類は、外部データソースの ODBC ドライバーによって決定されます。 各外部データソースによって、テーブルとして修飾される対象が決まります。 これには、TeraData の関数などのデータベースオブジェクトや、Oracle のシノニムを含めることができます。 PolyBase は一部の ODBC オブジェクトに外部テーブルとして接続できないため、TABLE_LOCATION 列に値がありません。 これらのオブジェクトのいずれかが存在する場合は、データベースまたはスキーマが空でない可能性があります。

`sp_data_source_objects` [`sp_data_source_table_columns`](sp-data-source-table-columns.md) 外部オブジェクトを検出するには、およびを使用します。 これらのシステムストアドプロシージャは、仮想化が可能なテーブルのスキーマを返します。 Azure Data Studio は、これらの2つのストアドプロシージャを使用して、 [データの仮想化](../../azure-data-studio/extensions/data-virtualization-extension.md)をサポートします。 [Sp_data_source_table_columns](sp-data-source-table-columns.md)を使用すると、SQL Server データ型で表される外部テーブルスキーマを検出できます。

### <a name="data-source-type-specific-remarks"></a>データソースの種類に固有の解説

* Teradata

   Teradata システムビューでは、行レベルのセキュリティ (RLS) が使用されないため、ユーザーはクエリできないテーブルが存在するかどうかを確認できます。

* MongoDB

   以前のバージョンの MongoDB では、すべてのデータベースを管理者のようなユーザーに一覧表示する機能が制限されていました。 このアクセス許可を持たないユーザーは、null でこのプロシージャを実行しようとすると、認証エラーが発生する可能性があり `@object_root_name` ます。

## <a name="examples"></a>例  

### <a name="sql-server"></a>SQL Server

次の例では、すべてのデータベース、スキーマ、およびテーブル/ビューを返します。

```sql
DECLARE @data_source SYSNAME = N'ExternalDataSourceName';
DECLARE @object_root_name NVARCHAR(MAX) = NULL;
DECLARE @max_search_depth INT = 3;
EXEC sp_data_source_objects @data_source, @object_root_name, @max_search_depth;
```

| OBJECT_TYPE | OBJECT_NAME | OBJECT_LEAF_NAME | TABLE_LOCATION |
|--|--|--|--|
| DATABASE | "database" | database | NULL |
| SCHEMA | "データベース"。dbo | dbo | NULL |
| TABLE | "データベース"。dbo "."お | 顧客 | [データベース]。[dbo]。お |
| TABLE | "データベース"。dbo "."品 | item | [データベース]。[dbo]。品 |
| TABLE | "データベース"。dbo "."貴国 | 貴国 | [データベース]。[dbo]。貴国 |

次の例では、すべてのデータベースが返されます。

```sql
DECLARE @data_source SYSNAME = N'ExternalDataSourceName';
DECLARE @object_root_name NVARCHAR(MAX) = NULL;
EXEC sp_data_source_objects @data_source, @object_root_name;
```

| OBJECT_TYPE | OBJECT_NAME | OBJECT_LEAF_NAME | TABLE_LOCATION |
|--|--|--|--|
| DATABASE | "UserDatabase" | UserDatabase | NULL |
| DATABASE | "master" | master | NULL |
| DATABASE | 満杯 | msdb | NULL |
| DATABASE | データベース | tempdb | NULL |
| DATABASE | "database" | database | NULL |

次の例では、データベース内のすべてのスキーマを返します。

```sql
DECLARE @data_source SYSNAME = N'ExternalDataSourceName'; 
DECLARE @object_root_name NVARCHAR(MAX) = N'[database]'; 
EXEC sp_data_source_objects @data_source, @object_root_name;
```

| OBJECT_TYPE | OBJECT_NAME | OBJECT_LEAF_NAME | TABLE_LOCATION |
|--|--|--|--|
| SCHEMA | "データベース"。dbo | dbo | NULL |
| SCHEMA | "データベース"。INFORMATION_SCHEMA " | INFORMATION_SCHEMA | NULL |
| SCHEMA | "データベース"。sys.databases | sys | NULL |

次の例では、スキーマ内のすべてのテーブルを返します。 

```sql
DECLARE @data_source SYSNAME = N'ExternalDataSourceName'; 
DECLARE @object_root_name NVARCHAR(MAX) = N'[database].[dbo]'; 
EXEC sp_data_source_objects @data_source, @object_root_name;
```

| OBJECT_TYPE | OBJECT_NAME | OBJECT_LEAF_NAME | TABLE_LOCATION |
|--|--|--|--|
| TABLE | "データベース"。dbo "."お | 顧客 | [データベース]。[dbo]。お |
| TABLE | "データベース"。dbo "."品 | item | [データベース]。[dbo]。品 |
| TABLE | "データベース"。dbo "."貴国 | 貴国 | [データベース]。[dbo]。貴国 |
| TABLE | "データベース"。dbo "."注文 | 注文 | [データベース]。[dbo]。注文 |
| TABLE | "データベース"。dbo "."一部 | のコンポーネント | [データベース]。[dbo]。一部 |

### <a name="oracle"></a>Oracle

次の例では、完全なスキーマとテーブル、関数、ビューなどが返されます。

```sql
DECLARE @data_source SYSNAME = N'ExternalDataSourceName'; 
DECLARE @object_root_name NVARCHAR(MAX) = N'[OracleObjectRoot]'; 
DECLARE @max_search_depth INT = 2; 
EXEC sp_data_source_objects @data_source, @object_root_name, @max_search_depth;
```

| OBJECT_TYPE | OBJECT_NAME | OBJECT_LEAF_NAME | TABLE_LOCATION |
|--|--|--|--|
| VIEW | "SYS"。 "ALL_SQLSET_STATEMENTS " | ALL_SQLSET_STATEMENTS | [ORACLEOBJECTROOT].[SYS]。[ALL_SQLSET_STATEMENTS] |
| SYSTEM TABLE | "SYS"。 "BOOTSTRAP $ " | ブートストラップ $ | [ORACLEOBJECTROOT].[SYS]。[BOOTSTRAP $] |
| SYNONYM | "PUBLIC"。 "ALL_ALL_TABLES " | ALL_ALL_TABLES | NULL |
| SCHEMA | "database" | database | NULL |
| TABLE | "データベース"。お | 顧客 | [ORACLEOBJECTROOT].[データベース]。お |

### <a name="teradata"></a>Teradata

次の例では、すべてのデータベースとテーブル、関数、ビューなどが返されます。

```SQL
DECLARE @data_source SYSNAME = N'ExternalDataSourceName';
DECLARE @object_root_name NVARCHAR(MAX) = NULL;
DECLARE @max_search_depth INT = 2;
EXEC sp_data_source_objects @data_source, @object_root_name, @max_search_depth;
```

| OBJECT_TYPE | OBJECT_NAME | OBJECT_LEAF_NAME | TABLE_LOCATION |  
|--|--|--|--|
| FUNCTION | "SYSLIB"."ExtractRoles" | ExtractRoles | NULL |  
| SYSTEM TABLE | "DBC"。 "UDTCast " | UDTCast | [DBC]。[UDTCast] |  
| TYPE | "SYSUDTLIB"."XML | XML | NULL |  
| DATABASE | "database" | database | NULL |
| TABLE | "データベース"。お | 顧客 | [データベース]。お |  

### <a name="mongo-db"></a>Mongo DB

次の例では、すべてのデータベースとテーブルを返します。

```SQL
DECLARE @data_source SYSNAME = N'ExternalDataSourceName';
DECLARE @object_root_name NVARCHAR(MAX) = NULL;
DECLARE @max_search_depth INT = 2;
EXEC sp_data_source_objects @data_source, @object_root_name, @max_search_depth;
```

| OBJECT_TYPE | OBJECT_NAME | OBJECT_LEAF_NAME | TABLE_LOCATION |
|--|--|--|--|
| DATABASE | "database" | database | NULL |
| TABLE | "データベース"。お | 顧客 | [データベース]。お |
| TABLE | "データベース"。品 | item | [データベース]。品 |
| TABLE | "データベース"。貴国 | 貴国 | [データベース]。貴国 |
| TABLE | "データベース"。注文 | 注文 | [データベース]。注文 |

## <a name="see-also"></a>関連項目

- [sp_data_source_columns](/sql/relational-databases/system-stored-procedures/sp-data-source-table-columns)   
- [CREATE EXTERNAL TABLE AS SELECT (Transact-SQL)](../../t-sql/statements/create-external-table-as-select-transact-sql.md)
- [CREATE EXTERNAL TABLE (Transact-SQL)](../../t-sql/statements/create-external-table-transact-sql.md)
- [Azure Data Studio 用のデータ仮想化の拡張機能](../../azure-data-studio/extensions/data-virtualization-extension.md)   
- [PolyBase の概要](../polybase/polybase-guide.md)   
- [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)
