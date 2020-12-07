---
title: PDO::quote
description: SQL Server 用 Microsoft PDO_SQLSRV Driver for PHP の PDO::quote 関数の API リファレンス。
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ab9ddc48-42f8-4edf-aa8b-b0fc66706161
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31756cbc2f0ede497ea34077f1bdd760412c716c
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081841"
---
# <a name="pdoquote"></a>PDO::quote
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

基になる SQL Server データベースでの必要に応じて、入力文字列を引用符で囲むことにより、クエリで使用できるように文字列を処理します。 PDO::quote は、SQL Server に適した引用符スタイルを使用して、入力文字列内の特殊文字をエスケープします。  
  
## <a name="syntax"></a>構文  
  
```  
  
string PDO::quote( $string[, $parameter_type ] )  
```  
  
#### <a name="parameters"></a>パラメーター  
$*string*: 引用符で囲む文字列。  
  
$*parameter_type*:データ型を示す省略可能な (整数) シンボル。  既定は PDO::PARAM_STR です。  

[Unicode および非 Unicode 文字列のバインド](https://wiki.php.net/rfc/extended-string-types-for-pdo)のサポートを追加するために、PHP 7.2 で新しい PDO 定数が導入されました。 Unicode 文字列は、プレフィックスとして N を使用して引用符で囲むことができます (つまり、'string' ではなく N'string')。

1. PDO::PARAM_STR_NATL - ビット単位の OR として PDO::PARAM_STR に適用される、Unicode 文字列の新しい種類
1. PDO::PARAM_STR_CHAR - ビット単位の OR として PDO::PARAM_STR に適用される、非 Unicode 文字列の新しい種類
1. PDO::ATTR_DEFAULT_STR_PARAM - PDO::PARAM_STR_NATL または PDO::PARAM_STR_CHAR のいずれかに設定して、既定で PDO::PARAM_STR に対してビット単位 OR を行う値を示します

バージョン 5.8.0 以降では、PDO::quote でこれらの定数を使用できます。
  
## <a name="return-value"></a>戻り値  
SQL ステートメントに渡すことができる引用符で囲まれた文字列、または失敗した場合は false。  
  
## <a name="remarks"></a>解説  
PDO のサポートは [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]のバージョン 2.0 で追加されました。  
  
## <a name="string-escape-example"></a>文字列エスケープの例  
  
```  
<?php  
$database = "test";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$param = 'a \' g';  
$param2 = $conn->quote( $param );  
  
$query = "INSERT INTO Table1 VALUES( ?, '1' )";  
$stmt = $conn->prepare( $query );  
$stmt->execute(array($param));  
  
$query = "INSERT INTO Table1 VALUES( ?, ? )";  
$stmt = $conn->prepare( $query );  
$stmt->execute(array($param, $param2));  
?>  
```  
  
## <a name="pdo-quote-example"></a>PDO::quote の例  

次のスクリプトでは、PHP 7.2 以降で拡張文字列型が PDO::quote() に与える影響の例をいくつか示します。

```
<?php
$database = "test";
$server = "(local)";
$db = new PDO("sqlsrv:server=$server; Database=$database", "", "");

$db->quote('über', PDO::PARAM_STR | PDO::PARAM_STR_NATL); // N'über'
$db->quote('foo'); // 'foo'

$db->setAttribute(PDO::ATTR_DEFAULT_STR_PARAM, PDO::PARAM_STR_NATL);
$db->quote('über'); // N'über'
$db->quote('foo', PDO::PARAM_STR | PDO::PARAM_STR_CHAR); // 'foo'
?>
```
  
## <a name="see-also"></a>参照  
[PDO クラス](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
