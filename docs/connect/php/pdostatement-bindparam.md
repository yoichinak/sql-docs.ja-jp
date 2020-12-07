---
title: PDOStatement::bindParam
description: SQL Server 用 Microsoft PDO_SQLSRV Driver for PHP の PDOStatement::bindParam 関数の API リファレンス。
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 65212058-2632-47a4-ba7d-2206883abf09
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dd2d1feb1ae156d685dbd18595447a248836eba9
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081421"
---
# <a name="pdostatementbindparam"></a>PDOStatement::bindParam
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

SQL ステートメントで名前付きまたは疑問符プレースホルダーにパラメーターをバインドします。  
  
## <a name="syntax"></a>構文  
  
```  
  
bool PDOStatement::bindParam($parameter, &$variable[, $data_type[, $length[, $driver_options]]]);  
```  
  
#### <a name="parameters"></a>パラメーター  
$*parameter*: (混合) パラメーター識別子。 名前付きプレースホルダーを使用するステートメントの場合、パラメーター名 (:name) を使用します。 疑問符構文を使用する準備されたステートメントの場合、これはパラメーターの 1 から始まるインデックスになります。  
  
&$*variable*: SQL ステートメント パラメーターにバインドする PHP 変数の (混合の) 名前。  
  
$*data_type*: 省略可能な (整数の) PDO::PARAM_* 定数。 既定値は PDO::PARAM_STR です。  
  
$*length*: データ型の省略可能な (整数の) 長さ。 $*data_type* で PDO::PARAM_INT または PDO::PARAM_BOOL を使用している場合は、既定のサイズを示すように PDO::SQLSRV_PARAM_OUT_DEFAULT_SIZE を指定できます。  
  
$*driver_options*:省略可能な (混合の) ドライバー固有のオプション。 たとえば、PDO::SQLSRV_ENCODING_UTF8 と指定すると、UTF-8 でエンコードされた文字列として列を変数にバインドできます。  
  
## <a name="return-value"></a>戻り値  
成功した場合は TRUE、それ以外の場合は FALSE です。  
  
## <a name="remarks"></a>解説  
varbinary、binary、または varbinary(max) の各型のサーバー列に null データをバインドする場合は、$*driver_options* を使用してバイナリ エンコード (PDO::SQLSRV_ENCODING_BINARY) を指定する必要があります。 エンコード定数の詳細については、「[定数](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md) 」を参照してください。  
  
PDO のサポートは [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]のバージョン 2.0 で追加されました。  

## <a name="parameter-example"></a>パラメーターの例  
このコード例は、$contact をパラメーターにバインドした後に値を変更すると、クエリで渡される値が変更されることを示しています。  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO("sqlsrv:server=$server ; Database = $database", "", "");  
  
$contact = "Sales Agent";  
$stmt = $conn->prepare("select * from Person.ContactType where name = ?");  
$stmt->bindParam(1, $contact);  
$contact = "Owner";  
$stmt->execute();  
  
while ($row = $stmt->fetch(PDO::FETCH_ASSOC)) {  
   print "$row[Name]\n\n";  
}  
  
$stmt = null;  
$contact = "Sales Agent";  
$stmt = $conn->prepare("select * from Person.ContactType where name = :contact");  
$stmt->bindParam(':contact', $contact);  
$contact = "Owner";  
$stmt->execute();  
  
while ($row = $stmt->fetch(PDO::FETCH_ASSOC)) {  
   print "$row[Name]\n\n";  
}  
?>  
```  
  
## <a name="output-parameter-example"></a>出力パラメーターの例  
このコード サンプルは、出力パラメーターにアクセスする方法を示しています。  
  
```  
<?php  
$database = "Test";  
$server = "(local)";  
$conn = new PDO("sqlsrv:server=$server ; Database = $database", "", "");  
  
$input1 = 'bb';  
  
$stmt = $conn->prepare("select ? = count(*) from Sys.tables");  
$stmt->bindParam(1, $input1, PDO::PARAM_STR, 10);  
$stmt->execute();  
echo $input1;  
?>  
```  
  
> [!NOTE]
> 出力パラメーターを bigint 型にバインドする際に、値が[整数](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)の範囲外になる可能性がある場合、PDO::SQLSRV_PARAM_OUT_DEFAULT_SIZE と共に PDO::PARAM_INT を使用すると、"値が範囲外です" という例外が発生することがあります。 そのため、代わりに既定の PDO::P ARAM_STR を使用して、結果の文字列のサイズを指定します。最大は 21 です。 任意の bigint 値の最大桁数 (負の符号を含む) です。 

## <a name="inputoutput-example"></a>入力と出力の例  
このコード サンプルは、入力/出力パラメーターを使用する方法を示しています。  
  
```  
<?php  
   $database = "AdventureWorks";  
   $server = "(local)";  
   $dbh = new PDO("sqlsrv:server=$server ; Database = $database", "", "");  
  
   $dbh->query("IF OBJECT_ID('dbo.sp_ReverseString', 'P') IS NOT NULL DROP PROCEDURE dbo.sp_ReverseString");  
   $dbh->query("CREATE PROCEDURE dbo.sp_ReverseString @String as VARCHAR(2048) OUTPUT as SELECT @String = REVERSE(@String)");  
   $stmt = $dbh->prepare("EXEC dbo.sp_ReverseString ?");  
   $string = "123456789";  
   $stmt->bindParam(1, $string, PDO::PARAM_STR | PDO::PARAM_INPUT_OUTPUT, 2048);  
   $stmt->execute();  
   print $string;   // Expect 987654321  
?>  
```  

> [!NOTE]
> 値を [10 進数列または数値列](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)にバインドするときは、有効桁数と精度を保持するために、入力として文字列を使用することをお勧めします。これは、PHP には[浮動小数点数](https://php.net/manual/en/language.types.float.php)の有効桁数に制限があるためです。 値が[整数](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)の範囲外にある場合は特に、同じことが bigint 列にも適用されます。

## <a name="decimal-input-example"></a>10 進数の入力の例  
このコード サンプルでは、入力パラメーターとして 10 進数値をバインドする方法を示しています。  

```
<?php  
$database = "Test";  
$server = "(local)";  
$conn = new PDO("sqlsrv:server=$server ; Database = $database", "", "");  

// Assume TestTable exists with a decimal field 
$input = "9223372036854.80000";
$stmt = $conn->prepare("INSERT INTO TestTable (DecimalCol) VALUES (?)");
// by default it is PDO::PARAM_STR, rounding of a large input value may
// occur if PDO::PARAM_INT is specified
$stmt->bindParam(1, $input, PDO::PARAM_STR);
$stmt->execute();
```


## <a name="see-also"></a>参照  
[PDOStatement クラス](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
