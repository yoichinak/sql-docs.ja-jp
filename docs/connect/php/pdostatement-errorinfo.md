---
title: PDOStatement::errorInfo
description: SQL Server 用 Microsoft PDO_SQLSRV Driver for PHP の PDOStatement::errorInfo 関数の API リファレンス。
ms.custom: ''
ms.date: 01/29/2021
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.assetid: e45bebe8-ea4c-49b6-93db-cf1ae65f530c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0474b0c1225a248b47f0892ac940f2e58ab0efa0
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99206357"
---
# <a name="pdostatementerrorinfo"></a>PDOStatement::errorInfo
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

ステートメント ハンドルの最新の操作に関する拡張エラー情報を取得します。  
  
## <a name="syntax"></a>構文  

```
array PDOStatement::errorInfo();
```
  
## <a name="return-value"></a>戻り値  
ステートメント ハンドルに対する最新の操作に関するエラー情報の配列。 配列は、次のフィールドで構成されます。  
  
-   SQLSTATE エラー コード  
  
-   ドライバー固有のエラー コード  
  
-   ドライバー固有のエラー メッセージ  
  
エラーがない場合、または SQLSTATE が設定されていない場合、ドライバー固有のフィールドは NULL になります。  
  
## <a name="remarks"></a>解説  
PDO のサポートは [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]のバージョン 2.0 で追加されました。  
  
## <a name="example"></a>例  
この例では、SQL ステートメントにエラーがあるので、そのエラーがレポートされます。  
  
```php
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks", "", "");  
$stmt = $conn->prepare('SELECT * FROM Person.Addressx');  
  
$stmt->execute();  
print_r ($stmt->errorInfo());  
?>  
```

## <a name="additional-odbc-messages"></a>追加の ODBC メッセージ

例外が発生すると、ODBC ドライバーから問題の診断に役立つ複数のエラーが返されることがあります。 ただし、PDOStatement::errorInfo では常に最初のエラーのみが示されます。 この [バグ報告](https://bugs.php.net/bug.php?id=78196)に応じて、[PDO::errorInfo](https://www.php.net/manual/en/pdo.errorinfo.php) と [PDOStatement::errorInfo](https://www.php.net/manual/en/pdostatement.errorinfo.php) が更新され、ドライバーで "*少なくとも*" 次の 3 つのフィールドを表示する必要があることが示されるようになりました。
```
0   SQLSTATE error code (a five characters alphanumeric identifier defined in the ANSI SQL standard).
1   Driver specific error code.
2   Driver specific error message.
```

5\.9.0 以降での PDOStatement::errorInfo の既定の動作では、追加の ODBC エラー (使用可能な場合) が表示されます。 詳細については、「[PDO::errorInfo](../../connect/php/pdo-errorinfo.md)」を参照してください。
  
## <a name="see-also"></a>参照  
[PDOStatement クラス](../../connect/php/pdostatement-class.md)

[PDO::errorInfo](../../connect/php/pdo-errorinfo.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
