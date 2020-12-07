---
title: SQL Server のデータ型のマッピング
description: SQL Server と .NET Framework の異なる型システム間のマッピングについて説明します。 この記事では、Microsoft SqlClient Data Provider for SQL Server でシステムが相互作用する方法をまとめます。
ms.date: 11/13/2020
ms.assetid: fafdc31a-f435-4cd3-883f-1dfadd971277
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 0b12445989fd044a39ab88b2d840368aec206025
ms.sourcegitcommit: debaff72dbfae91b303f0acd42dd6d99e03135a2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/01/2020
ms.locfileid: "96419713"
---
# <a name="sql-server-data-type-mappings"></a>SQL Server のデータ型のマッピング

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

SQL Server と .NET Framework は異なる型システムを使用しています。 たとえば、.NET Framework の <xref:System.Decimal> 構造体の最大小数点以下桁数は 28 ですが、SQL Server の decimal データ型と numeric データ型の最大小数点以下桁数は 38 です。 データを読み書きするときにデータの整合性を保つために、<xref:Microsoft.Data.SqlClient.SqlDataReader> では、.NET Framework の型を返すアクセサー メソッドと共に、<xref:System.Data.SqlTypes> のオブジェクトを返す SQL Server 固有の型指定されたアクセサー メソッドを公開しています。 SQL Server の型と .NET Framework の型は、両方とも <xref:System.Data.DbType> および <xref:System.Data.SqlDbType> クラスの列挙によって表されます。これらは <xref:Microsoft.Data.SqlClient.SqlParameter> データ型を指定するときに使用できます。

推論される .NET Framework 型、<xref:System.Data.DbType> 列挙型と <xref:System.Data.SqlDbType> 列挙型、<xref:Microsoft.Data.SqlClient.SqlDataReader> のアクセサー メソッドを、次の表に示します。

|SQL Server データベース エンジンの型|.NET Framework 型|SqlDbType 列挙|SqlDataReader SqlTypes の型指定されたアクセサー|DbType 列挙|SqlDataReader DbType の型指定されたアクセサー|  
|-------------------------------------|-------------------------|---------------------------|-------------------------------------------|------------------------|-----------------------------------------|  
|bigint|Int64|<xref:System.Data.SqlDbType.BigInt>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlInt64%2A>|<xref:System.Data.DbType.Int64>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetInt64%2A>|  
|バイナリ|Byte[]|<xref:System.Data.SqlDbType.VarBinary>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlBinary%2A>|<xref:System.Data.DbType.Binary>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetBytes%2A>|  
|bit|ブール型|<xref:System.Data.SqlDbType.Bit>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlBoolean%2A>|<xref:System.Data.DbType.Boolean>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetBoolean%2A>|  
|char|String<br /><br /> Char[]|<xref:System.Data.SqlDbType.Char>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlString%2A>|<xref:System.Data.DbType.AnsiStringFixedLength>、<br /><br /> <xref:System.Data.DbType.String>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetString%2A><br /><br /> <xref:Microsoft.Data.SqlClient.SqlDataReader.GetChars%2A>|  
|date <sup>1</sup><br /><br /> (SQL Server 2008 以降)|DateTime|<xref:System.Data.SqlDbType.Date> <sup>1</sup>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlDateTime%2A>|<xref:System.Data.DbType.Date> <sup>1</sup>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetDateTime%2A>|  
|datetime|DateTime|<xref:System.Data.SqlDbType.DateTime>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlDateTime%2A>|<xref:System.Data.DbType.DateTime>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetDateTime%2A>|  
|datetime2<br /><br /> (SQL Server 2008 以降)|DateTime|<xref:System.Data.SqlDbType.DateTime2>|None|<xref:System.Data.DbType.DateTime2>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetDateTime%2A>|  
|datetimeoffset<br /><br /> (SQL Server 2008 以降)|DateTimeOffset|<xref:System.Data.SqlDbType.DateTimeOffset>|none|<xref:System.Data.DbType.DateTimeOffset>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetDateTimeOffset%2A>|  
|decimal|Decimal (10 進数型)|<xref:System.Data.SqlDbType.Decimal>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlDecimal%2A>|<xref:System.Data.DbType.Decimal>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetDecimal%2A>|  
|FILESTREAM 属性 (varbinary(max))|Byte[]|<xref:System.Data.SqlDbType.VarBinary>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlBytes%2A>|<xref:System.Data.DbType.Binary>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetBytes%2A>|  
|float|Double|<xref:System.Data.SqlDbType.Float>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlDouble%2A>|<xref:System.Data.DbType.Double>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetDouble%2A>|  
|イメージ|Byte[]|<xref:System.Data.SqlDbType.Binary>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlBinary%2A>|<xref:System.Data.DbType.Binary>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetBytes%2A>|  
|int|Int32|<xref:System.Data.SqlDbType.Int>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlInt32%2A>|<xref:System.Data.DbType.Int32>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetInt32%2A>|  
|money|Decimal (10 進数型)|<xref:System.Data.SqlDbType.Money>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlMoney%2A>|<xref:System.Data.DbType.Decimal>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetDecimal%2A>|  
|nchar|String<br /><br /> Char[]|<xref:System.Data.SqlDbType.NChar>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlString%2A>|<xref:System.Data.DbType.StringFixedLength>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetString%2A><br /><br /> <xref:Microsoft.Data.SqlClient.SqlDataReader.GetChars%2A>|  
|ntext|String<br /><br /> Char[]|<xref:System.Data.SqlDbType.NText>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlString%2A>|<xref:System.Data.DbType.String>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetString%2A><br /><br /> <xref:Microsoft.Data.SqlClient.SqlDataReader.GetChars%2A>|  
|数値|Decimal (10 進数型)|<xref:System.Data.SqlDbType.Decimal>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlDecimal%2A>|<xref:System.Data.DbType.Decimal>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetDecimal%2A>|  
|nvarchar|String<br /><br /> Char[]|<xref:System.Data.SqlDbType.NVarChar>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlString%2A>|<xref:System.Data.DbType.String>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetString%2A><br /><br /> <xref:Microsoft.Data.SqlClient.SqlDataReader.GetChars%2A>|  
|実数|Single|<xref:System.Data.SqlDbType.Real>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlSingle%2A>|<xref:System.Data.DbType.Single>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetFloat%2A>|  
|rowversion|Byte[]|<xref:System.Data.SqlDbType.Timestamp>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlBinary%2A>|<xref:System.Data.DbType.Binary>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetBytes%2A>|  
|smalldatetime|DateTime|<xref:System.Data.SqlDbType.DateTime>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlDateTime%2A>|<xref:System.Data.DbType.DateTime>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetDateTime%2A>|  
|smallint|Int16|<xref:System.Data.SqlDbType.SmallInt>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlInt16%2A>|<xref:System.Data.DbType.Int16>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetInt16%2A>|  
|smallmoney|Decimal (10 進数型)|<xref:System.Data.SqlDbType.SmallMoney>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlMoney%2A>|<xref:System.Data.DbType.Decimal>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetDecimal%2A>|  
|sql_variant|Object <sup>2</sup>|<xref:System.Data.SqlDbType.Variant>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValue%2A> <sup>2</sup>|<xref:System.Data.DbType.Object>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetValue%2A> <sup>2</sup>|  
|テキスト|String<br /><br /> Char[]|<xref:System.Data.SqlDbType.Text>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlString%2A>|<xref:System.Data.DbType.String>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetString%2A><br /><br /> <xref:Microsoft.Data.SqlClient.SqlDataReader.GetChars%2A>|  
|時間<br /><br /> (SQL Server 2008 以降)|TimeSpan|<xref:System.Data.SqlDbType.Time>|none|<xref:System.Data.DbType.Time>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetDateTime%2A>|  
|タイムスタンプ|Byte[]|<xref:System.Data.SqlDbType.Timestamp>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlBinary%2A>|<xref:System.Data.DbType.Binary>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetBytes%2A>|  
|tinyint|Byte|<xref:System.Data.SqlDbType.TinyInt>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlByte%2A>|<xref:System.Data.DbType.Byte>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetByte%2A>|  
|uniqueidentifier|GUID|<xref:System.Data.SqlDbType.UniqueIdentifier>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlGuid%2A>|<xref:System.Data.DbType.Guid>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetGuid%2A>|  
|varbinary|Byte[]|<xref:System.Data.SqlDbType.VarBinary>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlBinary%2A>|<xref:System.Data.DbType.Binary>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetBytes%2A>|  
|varchar|String<br /><br /> Char[]|<xref:System.Data.SqlDbType.VarChar>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlString%2A>|<xref:System.Data.DbType.AnsiString>、<xref:System.Data.DbType.String>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetString%2A><br /><br /> <xref:Microsoft.Data.SqlClient.SqlDataReader.GetChars%2A>|  
|xml|Xml|<xref:System.Data.SqlDbType.Xml>|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlXml%2A>|<xref:System.Data.DbType.Xml>|none|

<sup>1</sup> `SqlParameter` の `DbType` プロパティを `SqlDbType.Date` に設定することはできません。  
<sup>2</sup> `sql_variant` の基になる型がわかっている場合は、特定の型指定されたアクセサーを使用してください。

## <a name="sql-server-documentation"></a>SQL Server ドキュメント

SQL Server のデータ型について詳しくは、「[データ型 (Transact-SQL)](/sql/t-sql/data-types/data-types-transact-sql)」をご覧ください。

## <a name="see-also"></a>関連項目

- [SQL Server データ型と ADO.NET](./sql/sql-server-data-types.md)
- [SQL Server のバイナリ データと大きな値のデータ](./sql/sql-server-binary-large-value-data.md)
- [パラメーターの構成](configure-parameters.md)
- [ADO.NET でのデータ型のマッピング](data-type-mappings-ado-net.md)
