---
title: PDOStatement::bindColumn
description: SQL Server 用 Microsoft PDO_SQLSRV Driver for PHP の PDOStatement::bindColumn 関数の API リファレンス。
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.assetid: bbdcea53-d23d-4769-89a0-95c7cf4d5390
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d9ed841aaf609178ee28b6340206421fa6d0eb81
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99195227"
---
# <a name="pdostatementbindcolumn"></a>PDOStatement::bindColumn
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

結果セット内の列に変数をバインドします。  
  
## <a name="syntax"></a>構文  
  
```  
  
bool PDOStatement::bindColumn($column, &$param[, $type[, $maxLen[, $driverdata ]]] );  
```  
  
#### <a name="parameters"></a>パラメーター  
$*column*: 結果セットの列 (1 から始まるインデックス) の (混合の) 番号または列の名前。  
  
&$*param*: 列をバインドする PHP 変数の (混合の) 名前。  
  
$*type*: (省略可能) PDO::PARAM_* 定数で表されたパラメーターのデータ型。  
  
$*maxLen*: (省略可能) 整数。Microsoft Drivers for PHP for SQL Server では使用されません。  
  
$*driverdata*: (省略可能) ドライバーに対する混合パラメーター。 たとえば、PDO::SQLSRV_ENCODING_UTF8 と指定すると、UTF-8 でエンコードされた文字列として列を変数にバインドできます。  
  
## <a name="return-value"></a>戻り値  
成功した場合は TRUE、それ以外の場合は FALSE。  
  
## <a name="remarks"></a>解説  
PDO のサポートは [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]のバージョン 2.0 で追加されました。  
  
## <a name="example"></a>例  
次の例では、結果セット内の列に変数をバインドする方法を示します。  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "SELECT Title, FirstName, EmailAddress FROM Person.Contact where LastName = 'Estes'";  
$stmt = $conn->prepare($query);  
$stmt->execute();  
  
$stmt->bindColumn('EmailAddress', $email);  
while ( $row = $stmt->fetch( PDO::FETCH_BOUND ) ){  
   echo "$email\n";  
}  
?>  
```  
  
## <a name="see-also"></a>参照  
[PDOStatement クラス](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
