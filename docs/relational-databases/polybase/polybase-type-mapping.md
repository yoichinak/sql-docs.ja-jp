---
title: PolyBase を使用した型マッピング | Microsoft Docs
description: PolyBase 外部データ ソースと SQL Server 間のマッピングについては、次の表を参照してください。 Transact-SQL CREATE EXTERNAL TABLE を使用して外部テーブルを定義します。
ms.date: 09/24/2018
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
ms.openlocfilehash: 107e25f9d4307532e4d1bd6d413e05347fc5209b
ms.sourcegitcommit: c4d6804bde7eaf72d9233d6d43f77d77d1b17c4e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2020
ms.locfileid: "91624739"
---
# <a name="type-mapping-with-polybase"></a>PolyBase を使用した型マッピング

[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

この記事では、PolyBase 外部データ ソースと SQL Server 間のマッピングについて説明します。 この情報を使用して、[CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) Transact-SQL コマンドで外部テーブルを正しく定義できます。

## <a name="overview"></a>概要

PolyBase を使用して外部テーブルを作成する場合、データ型と列の数を含む列の定義は、外部ファイル内のデータと一致している必要があります。 不一致がある場合、実際のデータに対してクエリを実行するときに、ファイルの行が拒否されます。  
  
外部データ ソース内のファイルを参照する外部のテーブルでは、列と型の定義は、外部ファイルの正確なスキーマにマップする必要があります。 Hadoop/Hive に格納されているデータを参照するデータの種類を定義する場合は、SQL、および Hive のデータ型の間では、次のマッピングを使用し、そこから選択するときに、SQL のデータ型に型をキャストします。 型には、特にそれ以外の場合に記されていない、Hive のすべてのバージョンが含まれます。

> [!NOTE]  
> SQL Server では、いずれの変換でも Hive の *infinity*のデータ値をサポートしていません。 PolyBase はデータ型変換エラーで失敗します。

## <a name="hadoop-type-mapping-reference"></a>Hadoop 型マッピング リファレンス

| SQL データ型 | .NET データ型            | Hive データ型 | Hadoop と Java のデータ型 | 説明                       |
| ------------- | ------------------------- | -------------- | --------------------- | ------------------------------ |
| tinyint       | Byte                      | tinyint        | ByteWritable          | 符号なし数値の場合のみです。     |
| smallint      | Int16                     | smallint       | ShortWritable         |
| INT           | Int32                     | INT            | IntWritable           |
| bigint        | Int64                     | bigint         | LongWritable          |
| bit           | Boolean                   | boolean        | BooleanWritable       |
| float         | Double                    | double         | DoubleWritable        |
| real          | Single                    | float          | FloatWritable         |
| money         | Decimal                   | double         | DoubleWritable        |
| smallmoney    | Decimal                   | double         | DoubleWritable        |
| nchar         | String<br /><br /> Char[] | string         | Varchar               |
| nvarchar      | String<br /><br /> Char[] | string         | Varchar               |
| char          | String<br /><br /> Char[] | string         | Varchar               |
| varchar       | String<br /><br /> Char[] | string         | Varchar               |
| binary        | Byte[]                    | binary         | BytesWritable         | Hive 0.8 以降に適用されます。 |
| varbinary     | Byte[]                    | binary         | BytesWritable         | Hive 0.8 以降に適用されます。 |
| date          | DateTime                  | timestamp      | TimestampWritable     |
| smalldatetime | DateTime                  | timestamp      | TimestampWritable     |
| datetime2     | DateTime                  | timestamp      | TimestampWritable     |
| DATETIME      | DateTime                  | timestamp      | TimestampWritable     |
| time          | TimeSpan                  | timestamp      | TimestampWritable     |
| decimal       | Decimal                   | decimal        | BigDecimalWritable    | Hive0.11 以降が適用されます。 |

<!--SQL Server 2019-->
::: moniker range=">= sql-server-ver15 || =sqlallproducts-allversions"

## <a name="oracle-type-mapping-reference"></a>Oracle 型マッピング リファレンス

| Oracle データ型 | SQL Server の型 | 
| -------------    | --------------- |
|Float             |Float            |
|NUMBER            |Float            |
|NUMBER (p,s)      |Decimal (p, s)   |
|LONG              |nvarchar         |
|BINARY_FLOAT      |Real             | 
|BINARY_DOUBLE     |Float            | 
|CHAR              |Char             |
|VARCHAR2          |Varchar          | 
|NVARCHAR2         |nvarchar         | 
|RAW               |Varbinary        |
|LONG RAW          |Varbinary        | 
|BLOB              |Varbinary        |
|CLOB              |Varchar          |
|NCLOB             | nvarchar        | 
|ROWID             |Varchar          |
|UROWID            |Varchar          | 
|DATE              |Datetime2        |
|timestamp         |Datetime2        | 

**型の不一致** 

**Float:** Oracle では、126 の精度の浮動小数点がサポートされます。これは SQL Server でサポートされる精度 (53) よりも低くなっています。 そのため、**Float (1-53)** は直接マップできますが、それを超えると切り捨てによるデータ損失が発生します。

**Timestamp:** Oracle の Timestamp と Timestamp with local timezone では、秒の小数部に 9 桁の有効桁数がサポートされますが、SQL Server の DateTime2 では秒の小数部に 7 桁の有効桁数がサポートされます。 




## <a name="mongodb-type-mapping"></a>MongoDB 型のマッピング

| BSON データ型     | SQL Server の型 |
| ------------------ | --------------- |
| Double             | Float           |
| String             | nvarchar        |
| Binary Data        | nvarchar        |
| Object ID          | nvarchar        |
| ブール型            | ビット             |
| Date               | Datetime2       |
| 32-bit integer     | int             |
| Timestamp          | nvarchar        |
| 64 ビット整数     | BigInt          |
|Decimal 128         | Decimal         | 
| DBPointer          | nvarchar        |
| JavaScript         | nvarchar        |
| Max Key            | nvarchar        |
| Min Key            | nvarchar        |
| Symbol             | nvarchar        |
| Regular Expression | nvarchar        |
| 未定義/NULL     | nvarchar        |


MongoDB では、BSON ドキュメントを使用して、データ レコードを格納します。 前のシナリオとは異なり、BSON はスキーマがなく、ドキュメントおよび他のドキュメント内の配列の埋め込みをサポートしています。 これによりユーザーに柔軟性を提供します。 


## <a name="teradata-type-mapping-reference"></a>Teradata 型マッピング リファレンス

| Teradata データ型 | SQL Server の型 | 
| -------------      | -------------   |
|INTEGER             |int              |
|SMALLINT            |SmallInt         |
|bigint              |BigInt           |
|BYTEINT             |SmallInt         |
|DECIMAL             |Decimal          |
|FLOAT               |Decimal          |
|BYTE                |Binary           |
|VARBYTE             |Varbinary        |
|BLOB                |varbinary        |
|CHAR                |Nchar            |
|CLOB                |nvarchar         |
|VARCHAR             |nvarchar         |
|Graphic             |Nchar            |
|JSON                |nvarchar         |
|VARGRAPHIC          |nvarchar         |
|DATE                |Date             |
|timestamp           |Datetime2        |
|TIME                |Time             |
|TIME WITH TIME ZONE |Time             |
|TIMESTAMP WITH TIME ZONE|時刻         |

::: moniker-end

## <a name="next-steps"></a>次の手順

これを使用する方法について詳しくは、[CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) に関する Transact-SQL 参照記事をご覧ください。
