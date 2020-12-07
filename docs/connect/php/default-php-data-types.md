---
title: 既定の PHP データ型
description: このトピックでは、Microsoft SQLSRV Driver for PHP for SQL Server の使用時の既定の全 PHP データ型とそれに対応する SQL Server データ型をリストアップします
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- default data types
- converting data types
ms.assetid: b66c301d-3d20-45b8-a112-225d8f01c0bd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c1e1cf91baf80fd6298eaaca9c9e12a0b5858d9f
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680793"
---
# <a name="default-php-data-types"></a>既定の PHP データ型
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

サーバーからデータを取得するとき、ユーザーが PHP のデータ型を指定しないと、 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] はデータを既定の PHP データ型に変換します。  
  
PDO_SQLSRV ドライバーを使用してデータが返される場合、データ型は int または string になります。  
  
このトピックでは、SQLSRV ドライバーを使用するときの既定のデータ型について説明します。  
  
次の表では、SQL Server のデータ型 (サーバーから取得されるデータ型)、PHP の既定のデータ型 (データが変換されるデータ型)、およびストリームと文字列の既定のエンコードを示します。 サーバーからデータを取得するときにデータ型を指定する方法の詳細については、「 [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)」を参照してください。  
  
|SQL Server 型|PHP の既定の型|既定のエンコード|  
|-------------------|--------------------|--------------------|  
|bigint|String|8 ビット文字<sup>1</sup>|  
|binary|Stream<sup>2</sup>|バイナリ<sup>3</sup>|  
|bit|Integer|8 ビット文字<sup>1</sup>|  
|char|String|8 ビット文字<sup>1</sup>|  
|date<sup>4</sup>|Datetime|適用なし|  
|datetime<sup>4</sup>|Datetime|適用なし|  
|datetime2<sup>4</sup>|Datetime|適用なし|  
|datetimeoffset<sup>4</sup>|Datetime|適用なし|  
|decimal|String|8 ビット文字<sup>1</sup>|  
|float|Float|8 ビット文字<sup>1</sup>|  
|geography|STREAM|バイナリ<sup>3</sup>|  
|geometry|STREAM|バイナリ<sup>3</sup>|  
|image<sup>5</sup>|Stream<sup>2</sup>|バイナリ<sup>3</sup>|  
|INT|Integer|8 ビット文字<sup>1</sup>|  
|money|String|8 ビット文字<sup>1</sup>|  
|nchar|String|8 ビット文字<sup>1</sup>|  
|numeric|String|8 ビット文字<sup>1</sup>|  
|nvarchar|String|8 ビット文字<sup>1</sup>|  
|nvarchar(MAX)|Stream<sup>2</sup>|8 ビット文字<sup>1</sup>|  
|ntext<sup>6</sup>|Stream<sup>2</sup>|8 ビット文字<sup>1</sup>|  
|real|Float|8 ビット文字<sup>1</sup>|  
|smalldatetime|Datetime|8 ビット文字<sup>1</sup>|  
|smallint|Integer|8 ビット文字<sup>1</sup>|  
|smallmoney|String|8 ビット文字<sup>1</sup>|  
|sql_variant<sup>7</sup>|String|8 ビット文字<sup>1</sup>|  
|text<sup>8</sup>|Stream<sup>2</sup>|8 ビット文字<sup>1</sup>|  
|time<sup>4</sup>|Datetime|適用なし|  
|timestamp|String|8 ビット文字<sup>1</sup>|  
|tinyint|Integer|8 ビット文字<sup>1</sup>|  
|UDT|Stream<sup>2</sup>|バイナリ<sup>3</sup>|  
|UNIQUEIDENTIFIER|String<sup>9</sup>|8 ビット文字<sup>1</sup>|  
|varbinary|Stream<sup>2</sup>|バイナリ<sup>3</sup>|  
|varbinary (max)|Stream<sup>2</sup>|バイナリ<sup>3</sup>|  
|varchar|String|8 ビット文字<sup>1</sup>|  
|varchar(MAX)|Stream<sup>2</sup>|8 ビット文字<sup>1</sup>|
|xml|Stream<sup>2</sup>|8 ビット文字<sup>1</sup>|  
  

1.  データは、システムの Windows ロケール設定のコード ページで指定されている 8 ビット文字で返されます。 任意のマルチバイト文字またはこのコード ページにマップされていない文字は、1 バイトの疑問符 (?) 文字に置き換えられます。  
  
2.  [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md) または [sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md) を使用して既定の PHP 型が Stream であるデータを取得する場合、データはストリームと同じエンコードの文字列として返されます。 たとえば、**sqlsrv_fetch_array** を使用して SQL Server の binary 型を取得した場合、既定の戻り値の型はバイナリ文字列です。  
  
3.  データは、エンコードまたは変換されず、生のバイト ストリームとしてサーバーから返されます。  

4.  日付と時刻の型は、文字列として取得できます。 詳細については、「 [方法: SQLSRV ドライバーを利用し、日付/時刻型を取得する](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md)」を参照してください。  

5.  これは、varbinary(max) 型にマップされる従来の型です。

6. これは、nvarchar(max) 型にマップされる従来の型です。

7.  sql_variant は、双方向パラメーターまたは出力パラメーターではサポートされていません。

8.  これは、varchar(max) 型にマップされる従来の型です。  
  
9.  UNIQUEIDENTIFIER は、次の正規表現によって表される GUID です。  
  
    [0-9a-fA-F]{8}-[0-9a-fA-F]{4}-[0-9a-fA-f]{4}-[0-9a-fA-f]{4}-[0-9a-fA-F]{12}  
 
 
## <a name="other-new-sql-server-2008-data-types-and-features"></a>SQL Server 2008 でのその他の新しいデータ型と機能  
SQL Server 2008 の新しいデータ型で、列の外部に存在するもの (テーブル値パラメーターなど) は、[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] ではサポートされていません。 次の表は、SQL Server 2008 の新機能の PHP によるサポートをまとめたものです。  
  
|機能|PHP のサポート|  
|-----------|---------------|  
|テーブル値パラメーター|いいえ|  
|スパース列|Partial|  
|Null ビット圧縮|はい|  
|大きな CLR ユーザー定義型 (UDT)|はい|  
|サービス プリンシパル名|いいえ|  
|MERGE|はい|  
|FILESTREAM|Partial|  
  
部分的な型のサポートとは、その列の型をプログラムでクエリできないことを意味します。  
  
## <a name="see-also"></a>参照  
[定数 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)

[データ型の変換](../../connect/php/converting-data-types.md)

[PHP の型](https://php.net/manual/en/language.types.php)

[データ型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)

[sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md)  
  
