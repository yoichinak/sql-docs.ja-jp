---
description: sqlsrv_field_metadata
title: sqlsrv_field_metadata | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_field_metadata
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_field_metadata
- sqlsrv_field_metadata
ms.assetid: c02f6942-0484-4567-a78e-fe8aa2053536
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c6f2e0f7eefdfe78d1058d839c3e5a4fa9404e77
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2020
ms.locfileid: "92080571"
---
# <a name="sqlsrv_field_metadata"></a>sqlsrv_field_metadata
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

準備されたステートメントのフィールドのメタデータを取得します。 ステートメントの準備については、「 [sqlsrv_query](../../connect/php/sqlsrv-query.md) 」または「 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)」を参照してください。 **sqlsrv_field_metadata** は、実行前または実行後の任意の準備されたステートメントで呼び出すことができます。  
  
## <a name="syntax"></a>構文  
  
```  
  
sqlsrv_field_metadata( resource $stmt)  
```  
  
#### <a name="parameters"></a>パラメーター  
*$stmt*: フィールドのメタデータを要求するステートメント リソース。  
  
## <a name="return-value"></a>戻り値  
配列の **array** 、または **false**。 array は、結果セット内のフィールドごとに 1 つの配列で構成されます。 各サブ配列には、次の表で示すようなキーがあります。 フィールド メタデータの取得中にエラーが発生した場合は、 **false** が返されます。  
  
|Key|説明|  
|-------|---------------|  
|名前|フィールドが対応する列の名前。|  
|種類|SQL 型に対応する数値。|  
|サイズ|文字型 (char(n)、varchar(n)、nchar(n)、nvarchar(n)、XML) のフィールドの文字数。 バイナリ型 (binary(n)、varbinary(n)、UDT) のフィールドのバイト数。 他の SQL Server データ型の場合は**NULL** 。|  
|有効桁数|可変精度の型 (real、numeric、decimal、datetime2、datetimeoffset、time) の有効桁数。 他の SQL Server データ型の場合は**NULL** 。|  
|スケール|可変スケールの型 (numeric、decimal、datetime2、datetimeoffset、time) のスケール。 他の SQL Server データ型の場合は**NULL** 。|  
|Nullable|列が null 値許容か (**SQLSRV_NULLABLE_YES**)、null 値許容ではないか (**SQLSRV_NULLABLE_NO**)、または null 値許容かどうかわからないか (**SQLSRV_NULLABLE_UNKNOWN**) を示す列挙値。|  
  
次の表では、各サブ配列のキーについての詳細を示します (これらの型の詳細については、SQL Server のマニュアルを参照してください)。  
  
|SQL Server 2008 のデータ型|種類|最小/最大有効桁数|最小/最大スケール|サイズ|  
|-----------------------------|--------|----------------------|------------------|--------|  
|bigint|SQL_BIGINT (-5)|||8|  
|binary|SQL_BINARY (-2)|||0 < *n* < 8000 <sup>1</sup>|  
|bit|SQL_BIT (-7)||||  
|char|SQL_CHAR (1)|||0 < *n* < 8000 <sup>1</sup>|  
|日付|SQL_TYPE_DATE (91)|10/10|0/0||  
|DATETIME|SQL_TYPE_TIMESTAMP (93)|23/23|3/3||  
|datetime2|SQL_TYPE_TIMESTAMP (93)|19/27|0/7||  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET (-155)|26/34|0/7||  
|decimal|SQL_DECIMAL (3)|1/38|0/有効桁数の値||  
|float|SQL_FLOAT (6)|4/8|||  
|image|SQL_LONGVARBINARY (-4)|||2 GB|  
|INT|SQL_INTEGER (4)||||  
|money|SQL_DECIMAL (3)|19/19|4/4||  
|nchar|SQL_WCHAR (-8)|||0 < *n* < 4000 <sup>1</sup>|  
|ntext|SQL_WLONGVARCHAR (-10)|||1 GB|  
|numeric|SQL_NUMERIC (2)|1/38|0/有効桁数の値||  
|nvarchar|SQL_WVARCHAR (-9)|||0 < *n* < 4000 <sup>1</sup>|  
|real|SQL_REAL (7)|4/4|||  
|smalldatetime|SQL_TYPE_TIMESTAMP (93)|16/16|0/0||  
|smallint|SQL_SMALLINT (5)|||2 バイト|  
|Smallmoney|SQL_DECIMAL (3)|10/10|4/4||  
|sql_variant|SQL_SS_VARIANT (-150)|||変数|  
|text|SQL_LONGVARCHAR (-1)|||2 GB|  
|time|SQL_SS_TIME2 (-154)|8/16|0/7||  
|timestamp|SQL_BINARY (-2)|||8 バイト|  
|tinyint|SQL_TINYINT (-6)|||1 バイト|  
|udt|SQL_SS_UDT (-151)|||変数|  
|UNIQUEIDENTIFIER|SQL_GUID (-11)|||16|  
|varbinary|SQL_VARBINARY (-3)|||0 < *n* < 8000 <sup>1</sup>|  
|varchar|SQL_VARCHAR (12)|||0 < *n* < 8000 <sup>1</sup>|  
|xml|SQL_SS_XML (-152)|||0|  
  
(1) 0 は最大サイズが許容されることを示します。  
  
Nullable キーは yes または no です。  
  
## <a name="example"></a>例  
次の例では、ステートメント リソースを作成した後、フィールド メタデータを取得して表示します。 この例では、ローカル コンピューターに SQL Server および [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) データベースがインストールされていることを前提にしています。 コマンド ラインからこの例を実行すると、すべての出力はコンソールに書き込まれます。  
  
```
<?php
/* Connect to the local server using Windows Authentication and
specify the AdventureWorks database as the database in use. */
$serverName = "(local)";
$connectionInfo = array("Database"=>"AdventureWorks");
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
    echo "Could not connect.\n";
    die( print_r( sqlsrv_errors(), true));
}

/* Prepare the statement. */
$tsql = "SELECT ReviewerName, Comments FROM Production.ProductReview";
$stmt = sqlsrv_prepare( $conn, $tsql);
  
/* Get and display field metadata. */
foreach( sqlsrv_field_metadata( $stmt) as $fieldMetadata) {
    foreach( $fieldMetadata as $name => $value) {
        echo "$name: $value\n";
    }  
    echo "\n";
}  
  
/* Note: sqlsrv_field_metadata can be called on any statement
resource, pre- or post-execution. */
  
/* Free statement and connection resources. */
sqlsrv_free_stmt($stmt);
sqlsrv_close($conn);
?>
```

## <a name="sensitivity-data-classification-metadata"></a>秘密度データ分類のメタデータ

バージョン5.8.0 では、Microsoft SQL Server 2019 上で `sqlsrv_field_metadata` を使用して、ユーザーが[秘密度データ分類のメタデータ](../../relational-databases/security/sql-data-discovery-and-classification.md?tabs=t-sql#subheading-4)にアクセスするために、新しいオプション `DataClassification` が導入されています。Microsoft ODBC Driver 17.4.2 以降が必要になります。

既定で、オプション `DataClassification` は `false` になっていますが、`true` に設定されると、秘密度データ分類のメタデータがある場合には、`sqlsrv_field_metadata` によって返された配列には、そのデータが入力されます。 

たとえば、次のように Patients テーブルを取得します。

```
CREATE TABLE Patients 
      [PatientId] int identity,
      [SSN] char(11),
      [FirstName] nvarchar(50),
      [LastName] nvarchar(50),
      [BirthDate] date)
```

次に示すように、SSN と BirthDate 列を分類できます。

```
ADD SENSITIVITY CLASSIFICATION TO [Patients].SSN WITH (LABEL = 'Highly Confidential - secure privacy', INFORMATION_TYPE = 'Credentials')
ADD SENSITIVITY CLASSIFICATION TO [Patients].BirthDate WITH (LABEL = 'Confidential Personal Data', INFORMATION_TYPE = 'Birthdays')
```

メタデータにアクセスするには、次のスニペットに示すように、`sqlsrv_field_metadata` を呼び出します。

```
$tableName = 'Patients';
$tsql = "SELECT * FROM $tableName";
$stmt = sqlsrv_prepare($conn, $tsql, array(), array('DataClassification' => true));
if (sqlsrv_execute($stmt)) {
    $fieldmeta = sqlsrv_field_metadata($stmt);

    foreach ($fieldmeta as $f) {
        if (count($f['Data Classification']) > 0) {
            echo $f['Name'] . ": \n";
            print_r($f['Data Classification']); 
        }
    }
}
```

次のように出力されます。

```
SSN: 
Array
(
    [0] => Array
        (
            [Label] => Array
                (
                    [name] => Highly Confidential - secure privacy
                    [id] => 
                )

            [Information Type] => Array
                (
                    [name] => Credentials
                    [id] => 
                )

        )

)
BirthDate: 
Array
(
    [0] => Array
        (
            [Label] => Array
                (
                    [name] => Confidential Personal Data
                    [id] => 
                )

            [Information Type] => Array
                (
                    [name] => Birthdays
                    [id] => 
                )

        )

)
```

`sqlsrv_prepare` ではなく `sqlsrv_query` を使用する場合、上記のスニペットは次のように変更できます。

```
$tableName = 'Patients';
$tsql = "SELECT * FROM $tableName";
$stmt = sqlsrv_query($conn, $tsql, array(), array('DataClassification' => true));
$fieldmeta = sqlsrv_field_metadata($stmt);

foreach ($fieldmeta as $f) {
    $jstr = json_encode($f);
    echo $jstr . PHP_EOL;
}
```

次の JSON 表現でわかるように、列に関連付けられている場合は、データ分類メタデータが表示されます。

```
{"Name":"PatientId","Type":4,"Size":null,"Precision":10,"Scale":null,"Nullable":0,"Data Classification":[]}
{"Name":"SSN","Type":1,"Size":11,"Precision":null,"Scale":null,"Nullable":1,"Data Classification":[{"Label":{"name":"Highly Confidential - secure privacy","id":""},"Information Type":{"name":"Credentials","id":""}}]}
{"Name":"FirstName","Type":-9,"Size":50,"Precision":null,"Scale":null,"Nullable":1,"Data Classification":[]}
{"Name":"LastName","Type":-9,"Size":50,"Precision":null,"Scale":null,"Nullable":1,"Data Classification":[]}
{"Name":"BirthDate","Type":91,"Size":null,"Precision":10,"Scale":0,"Nullable":1,"Data Classification":[{"Label":{"name":"Confidential Personal Data","id":""},"Information Type":{"name":"Birthdays","id":""}}]}
```

## <a name="see-also"></a>参照  
[SQLSRV ドライバー API リファレンス](../../connect/php/sqlsrv-driver-api-reference.md)  

[定数 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  

[ドキュメントのコード例について](../../connect/php/about-code-examples-in-the-documentation.md)  
