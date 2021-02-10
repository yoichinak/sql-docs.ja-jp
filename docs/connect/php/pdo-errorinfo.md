---
title: PDO::errorInfo
description: SQL Server 用 Microsoft PDO_SQLSRV Driver for PHP の PDO::errorInfo 関数の API リファレンス。
ms.custom: ''
ms.date: 01/29/2021
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.assetid: 9d5481d5-13bc-4388-b3aa-78676c0fc709
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 46b57275d92f4eb6acb64c276e3b34ea67efb429
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99202027"
---
# <a name="pdoerrorinfo"></a>PDO::errorInfo
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

データベース ハンドルの最新の操作のエラーの詳細情報を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
array PDO::errorInfo();  
```  
  
## <a name="return-value"></a>戻り値  
データベース ハンドルの最新の操作に関するエラー情報の配列。 配列は、次のフィールドで構成されます。  
  
-   SQLSTATE エラー コード。  
  
-   ドライバー固有のエラー コード。  
  
-   ドライバー固有のエラー メッセージ。  
  
エラーがない場合、または SQLSTATE が設定されていない場合、ドライバー固有のフィールドは NULL になります。  
  
## <a name="remarks"></a>解説  
PDO::errorInfo は、データベースで直接実行された操作のエラー情報だけを取得します。 PDO::prepare または PDO::query を使用して PDOStatement インスタンスを作成する場合は、PDOStatement::errorInfo を使用します。  
  
PDO のサポートは [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]のバージョン 2.0 で追加されました。  
  
## <a name="example"></a>例  
この例では、列の名前が間違っており (`City` ではなく `Cityx`)、エラーが発生します。そのエラーは報告されます。  
  
```php
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks ", "");  
$query = "SELECT * FROM Person.Address where Cityx = 'Essen'";  
  
$conn->query($query);  
print $conn->errorCode();  
echo "\n";  
print_r ($conn->errorInfo());  
?>  
```  

## <a name="additional-odbc-messages"></a>追加の ODBC メッセージ

例外が発生すると、ODBC ドライバーから問題の診断に役立つ複数のエラーが返されることがあります。 ただし、PDO::errorInfo では常に最初のエラーのみが示されます。 この [バグ報告](https://bugs.php.net/bug.php?id=78196)に応じて、[PDO::errorInfo](https://www.php.net/manual/en/pdo.errorinfo.php) と [PDOStatement::errorInfo](https://www.php.net/manual/en/pdostatement.errorinfo.php) が更新され、ドライバーで "*少なくとも*" 次の 3 つのフィールドを表示する必要があることが示されるようになりました。
```
0   SQLSTATE error code (a five characters alphanumeric identifier defined in the ANSI SQL standard).
1   Driver specific error code.
2   Driver specific error message.
```

5\.9.0 以降での PDO::errorInfo の既定の動作では、追加の ODBC エラー (使用可能な場合) が表示されます。 以下に例を示します。

```php
<?php  
try {
    $conn = new PDO("sqlsrv:server=$server;", $uid, $pwd);
    $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    $stmt = $conn->prepare("SET NOCOUNT ON; USE $database; SELECT 1/0 AS col1");
    $stmt->execute();
} catch (PDOException $e) {
    var_dump($e->errorInfo);
}
?>  
```  

上記のスクリプトを実行すると、例外がスローされるはずです。その出力は次のようになります。

```
array(6) {
  [0]=>
  string(5) "01000"
  [1]=>
  int(5701)
  [2]=>
  string(91) "[Microsoft][ODBC Driver 17 for SQL Server][SQL Server]Changed database context to 'tempdb'."
  [3]=>
  string(5) "22012"
  [4]=>
  int(8134)
  [5]=>
  string(87) "[Microsoft][ODBC Driver 17 for SQL Server][SQL Server]Divide by zero error encountered."
}
```

ユーザーが前の方法を希望する場合は、`pdo_sqlsrv.report_additional_errors` という新しい構成オプションを使用して無効にすることができます。 php スクリプトの先頭に次の行を追加するだけです。

```
ini_set('pdo_sqlsrv.report_additional_errors', 0);
```

この場合、同じサンプル スクリプトを実行すると、表示されるエラー情報はこのようになります。

```
array(3) {
  [0]=>
  string(5) "01000"
  [1]=>
  int(5701)
  [2]=>
  string(91) "[Microsoft][ODBC Driver 17 for SQL Server][SQL Server]Changed database context to 'tempdb'."
}
```

必要に応じて、ユーザーはすべての php スクリプトでこの機能を無効にするために、php.ini ファイルに次の行を追加することを選択できます。

```
pdo_sqlsrv.report_additional_errors = 0
```

## <a name="warnings-and-errors"></a>警告とエラー

5\.9.0 以降では、ODBC の警告がエラーとしてログに記録されなくなります。 つまり、プレフィックスが "01" の[エラー コード](https://docs.microsoft.com/sql/odbc/reference/appendixes/appendix-a-odbc-error-codes)が警告としてログに記録されます。 言い換えると、ユーザーがエラーのみをログに記録する場合は、このように php.ini を更新します。

```
[pdo_sqlsrv]  
pdo_sqlsrv.log_severity = 1
```

この場合、ログ ファイルにはいずれの警告メッセージも含まれません。 pdo_sqlsrv ユーザーの[ログ記録](https://docs.microsoft.com/sql/connect/php/logging-activity#logging-activity-using-the-pdo_sqlsrv-driver)の動作を確認してください。

## <a name="see-also"></a>参照  
[PDO クラス](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  

[PDOStatement::errorInfo](../../connect/php/pdostatement-errorinfo.md)
