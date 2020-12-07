---
description: sp_data_source_table_columns (Transact-sql)
title: sp_data_source_table_columns |Microsoft Docs
ms.custom: ''
ms.date: 11/10/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sp_data_source_table_columns
helpviewer_keywords:
- PolyBase
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4153b7546dfce226cb056b7a548efb69f5175e06
ms.sourcegitcommit: 4c3949f620d09529658a2172d00bfe37aeb1a387
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2020
ms.locfileid: "96128777"
---
# <a name="sp_data_source_table_columns-transact-sql"></a>sp_data_source_table_columns (Transact-sql)

[!INCLUDE [sqlserver2019](../../includes/applies-to-version/sqlserver2019.md)]

外部データソーステーブル内の列の一覧を返します。
  
> [!NOTE]
> この手順は、 [SQL 2019 CU5](../../big-data-cluster/release-notes-big-data-cluster.md#cu5)で導入されました。

![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sqlsyntax
sp_data_source_table_columns
         [ @data_source = ] 'data_source'
       , [ @table_location = ] 'table_location'
[ ; ]
```  

## <a name="arguments"></a>引数

`[ @data_source = ] 'data_source'`   
メタデータの取得元となる外部データソースの名前。 型は `sysname` です。

`[ @table_location = ] 'table_location'`   
テーブルを識別するテーブルの場所を示す文字列です。 `table_location` 型は `nvarchar(max)` です。

## <a name="returns"></a>戻り値

このストアドプロシージャは、次の情報を返します。

|列名 |データ型 |説明|
|---|---|---|
|NAME|nvarchar(max)|列の名前。
|TYPE|nvarchar(200)|SQL Server 型名
|LENGTH|INT|列の長さ
|PRECISION|INT|列の有効桁数
|SCALE|INT|列の小数点以下桁数
|COLLATION|nvarchar(200)|列の SQL Server 照合順序
|IS_NULLABLE|bit|この列は null 値を許容します。
|SOURCE_TYPE_NAME|nvarchar(max)|バックエンド固有の型名。 ほとんどはデバッグに使用されます。 ODBC ソースの場合は、SQLColumns () の TYPE_NAME 結果列に対応します。
|REMARKS|nvarchar(max)|列の一般的なコメントまたは説明。 現在は常に NULL です。|

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

Empty と non empty の概念は、ODBC ドライバーと[ `SQLTables` 関数](../native-client-odbc-api/sqltables.md)の動作に関連しています。 空以外の場合は、行ではなくテーブルがオブジェクトに含まれていることを示します。 たとえば、空のスキーマには SQL Server にテーブルが含まれていません。 空のデータベースには、Teradata 内のテーブルが含まれていません。結果は、バックエンドの PolyBase コネクタによって解釈されるバックエンドスキーマの SQL Server 表現になります。 ここでの違いは、ODBC 呼び出しの結果をバックエンドに渡すだけでなく、PolyBase の型マッピングコードの結果に基づいていることです。

[`sp_data_source_objects`](sp-data-source-objects.md) `sp_data_source_table_columns` 外部オブジェクトを検出するには、およびを使用します。 これらのシステムストアドプロシージャは、仮想化が可能なテーブルのスキーマを返します。 Azure Data Studio は、これらの2つのストアドプロシージャを使用して、 [データの仮想化](../../azure-data-studio/extensions/data-virtualization-extension.md)をサポートします。 `sp_data_source_table_columns`SQL Server のデータ型で表される外部テーブルスキーマを検出するために使用します。

SQL Server 2019 では、Hadoop ソースデータの照合順序とサポートされている照合順序の違いにより、外部テーブルの varchar データ型の列に推奨されるデータ型の長さは、予想よりもはるかに大きくなる可能性があります。 これは仕様です。

## <a name="example"></a>例  

次の例では、という名前のスキーマに属するという名前の SQL Server 内の外部テーブルのテーブル列を返し `server` `schema` ます。
  
```sql
DECLARE @data_source SYSNAME = N'ExternalDataSourceName';
DECLARE @table_location NVARCHAR(400) = N'[database].[schema].[table]';
EXEC sp_data_source_table_columns @data_source, @table_location
```  
  
## <a name="see-also"></a>関連項目

- [PolyBase の概要](../polybase/polybase-guide.md)
- [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)
- [CREATE EXTERNAL TABLE AS SELECT (Transact-SQL)](../../t-sql/statements/create-external-table-as-select-transact-sql.md)
- [CREATE EXTERNAL TABLE (Transact-SQL)](../../t-sql/statements/create-external-table-transact-sql.md)