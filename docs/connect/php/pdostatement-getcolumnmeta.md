---
title: PDOStatement::getColumnMeta
description: SQL Server 用 Microsoft PDO_SQLSRV Driver for PHP の PDOStatement::getColumnMeta 関数の API リファレンス。
ms.custom: ''
ms.date: 01/29/2021
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.assetid: c92a21cc-8e53-43d0-a4bf-542c77c100c9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bbfddcbf39dbbba3b63c6853ea7700e6a27a4614
ms.sourcegitcommit: 9413ddd8071da8861715c721b923e52669a921d8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "101837221"
---
# <a name="pdostatementgetcolumnmeta"></a>PDOStatement::getColumnMeta
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

列のメタデータを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
array PDOStatement::getColumnMeta ( $column );  
```  
  
#### <a name="parameters"></a>パラメーター  
*$conn*: (整数) メタデータを取得する列を示す 0 から始まる番号。  
  
## <a name="return-value"></a>戻り値  
列のメタデータを格納している連想配列 (キーと値)。 配列内のフィールドの詳細については「解説」セクションを参照してください。  
  
## <a name="remarks"></a>解説  
次の表では、getColumnMeta によって返される配列内のフィールドについて説明します。  
  
|名前|VALUES|  
|--------|----------|  
|native_type|列の PHP 型を指定します。 常に文字列です。|  
|driver:decl_type|データベースで列の値を表すために使用される SQL 型を指定します。 結果セット内の列が関数の結果である場合、この値は PDOStatement::getColumnMeta では返されません。|  
|flags|この列に設定されているフラグを指定します。 常に 0 です。|  
|name|データベースでの列の名前を指定します。|  
|table|データベースで列を含むテーブルの名前を指定します。 常に空白です。|  
|len|列の長さを指定します。|  
|精度|この列の数値の有効桁数を指定します。|  
|pdo_type|PDO::PARAM_* 定数によって表される、この列の型を指定します。 常に PDO::PARAM_STR (2) です。|  
  
PDO のサポートは [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]のバージョン 2.0 で追加されました。  
  
## <a name="example"></a>例  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$stmt = $conn->query("select * from Person.ContactType");  
$metadata = $stmt->getColumnMeta(2);  
var_dump($metadata);  
  
print $metadata['sqlsrv:decl_type'] . "\n";  
print $metadata['native_type'] . "\n";  
print $metadata['name'];  
?>  
```  
  
## <a name="sensitivity-data-classification-metadata"></a>秘密度データ分類のメタデータ

バージョン5.8.0 以降では、Microsoft SQL Server 2019 上で `PDOStatement::getColumnMeta` を使用して、ユーザーが[秘密度データ分類のメタデータ](../../relational-databases/security/sql-data-discovery-and-classification.md)にアクセスするために、新しいステートメント属性 `PDO::SQLSRV_ATTR_DATA_CLASSIFICATION` を利用できます。Microsoft ODBC Driver 17.4.2 以降が必要になります。

属性 `PDO::SQLSRV_ATTR_DATA_CLASSIFICATION` は既定で `false` になっていますが、`true` に設定されると、秘密度データ分類のメタデータがある場合には、前述の配列フィールド `flags` にはそのデータが入力されます。 

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

メタデータにアクセスするには、次のスニペットに示すように、`PDO::SQLSRV_ATTR_DATA_CLASSIFICATION` を true に設定した後に `PDOStatement::getColumnMeta` を使用します。

```
$options = array(PDO::SQLSRV_ATTR_DATA_CLASSIFICATION => true);
$tableName = 'Patients';
$tsql = "SELECT * FROM $tableName";
$stmt = $conn->prepare($tsql, $options);
$stmt->execute();
$numCol = $stmt->columnCount();

for ($i = 0; $i < $numCol; $i++) {
    $metadata = $stmt->getColumnMeta($i);
    $jstr = json_encode($metadata);
    echo $jstr . PHP_EOL;
}
```

すべての列のメタデータの出力は次のとおりです。

```
{"flags":{"Data Classification":[]},"sqlsrv:decl_type":"int identity","native_type":"string","table":"","pdo_type":2,"name":"PatientId","len":10,"precision":0}
{"flags":{"Data Classification":[{"Label":{"name":"Highly Confidential - secure privacy","id":""},"Information Type":{"name":"Credentials","id":""}}]},"sqlsrv:decl_type":"char","native_type":"string","table":"","pdo_type":2,"name":"SSN","len":11,"precision":0}
{"flags":{"Data Classification":[]},"sqlsrv:decl_type":"nvarchar","native_type":"string","table":"","pdo_type":2,"name":"FirstName","len":50,"precision":0}
{"flags":{"Data Classification":[]},"sqlsrv:decl_type":"nvarchar","native_type":"string","table":"","pdo_type":2,"name":"LastName","len":50,"precision":0}
{"flags":{"Data Classification":[{"Label":{"name":"Confidential Personal Data","id":""},"Information Type":{"name":"Birthdays","id":""}}]},"sqlsrv:decl_type":"date","native_type":"string","table":"","pdo_type":2,"name":"BirthDate","len":10,"precision":0}
```

`PDO::SQLSRV_ATTR_DATA_CLASSIFICATION` を `false` (既定のケース) に設定して上記のスニペットを変更した場合、次に示すように、`flags` フィールドは常に、以前と同様に `0` になります。

```
{"flags":0,"sqlsrv:decl_type":"int identity","native_type":"string","table":"","pdo_type":2,"name":"PatientId","len":10,"precision":0}
{"flags":0,"sqlsrv:decl_type":"char","native_type":"string","table":"","pdo_type":2,"name":"SSN","len":11,"precision":0}
{"flags":0,"sqlsrv:decl_type":"nvarchar","native_type":"string","table":"","pdo_type":2,"name":"FirstName","len":50,"precision":0}
{"flags":0,"sqlsrv:decl_type":"nvarchar","native_type":"string","table":"","pdo_type":2,"name":"LastName","len":50,"precision":0}
{"flags":0,"sqlsrv:decl_type":"date","native_type":"string","table":"","pdo_type":2,"name":"BirthDate","len":10,"precision":0}
```

## <a name="sensitivity-rank-using-a-predefined-set-of-values"></a>事前設定されている値セットを使用した秘密度順位

5\.9.0 以降、ODBC ドライバー 17.4.2 以上の使用時、PHP ドライバーによって分類順位の取得が追加されました。 ユーザーは [ADD SENSITIVITY CLASSIFICATION](../../t-sql/statements/add-sensitivity-classification-transact-sql.md) 使用時の順位を定義し、あらゆるデータ列を分類できます。 

たとえば、ユーザーが `NONE` と `LOW` をそれぞれ BirthDate と SSN に割り当てる場合、JSON 表記は次のようになります。

```
{"0":{"Label":{"name":"Confidential Personal Data","id":""},"Information Type":{"name":"Birthdays","id":""},"rank":0},"rank":0}
{"0":{"Label":{"name":"Highly Confidential - secure privacy","id":""},"Information Type":{"name":"Credentials","id":""},"rank":10},"rank":10}
```

[秘密度分類](../../relational-databases/system-catalog-views/sys-sensitivity-classifications-transact-sql.md)に示されているように、順位の数値は次のようになります。

```
0 for NONE
10 for LOW
20 for MEDIUM
30 for HIGH
40 for CRITICAL
```

したがって、`RANK=NONE` ではなく、ユーザーが列 BirthDate の分類時に `RANK=CRITICAL` を定義する場合、分類メタデータは次のようになります。

```
array(1) {
  ["Data Classification"]=>
  array(2) {
    [0]=>
    array(3) {
      ["Label"]=>
      array(2) {
        ["name"]=>
        string(26) "Confidential Personal Data"
        ["id"]=>
        string(0) ""
      }
      ["Information Type"]=>
      array(2) {
        ["name"]=>
        string(9) "Birthdays"
        ["id"]=>
        string(0) ""
      }
      ["rank"]=>
      int(40)
    }
    ["rank"]=>
    int(40)
  }
}
```

更新された JSON 表記は次のようになります。

```
{"0":{"Label":{"name":"Confidential Personal Data","id":""},"Information Type":{"name":"Birthdays","id":""},"rank":40},"rank":40}
```

## <a name="see-also"></a>参照  
[PDOStatement クラス](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)