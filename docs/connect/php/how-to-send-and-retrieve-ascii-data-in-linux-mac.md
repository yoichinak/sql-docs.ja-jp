---
title: 方法:Linux および macOS での ASCII データの送信と取得 (SQL)
description: このトピックでは、Microsoft Drivers for PHP for SQL Server を使用する場合に Linux および macOS で ASCII データを送信および取得する方法について説明します
ms.custom: ''
ms.date: 01/16/2018
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving data, ASCII data
- sending data
- linux
- macOS
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 015562e9a783cef79a9466778b89edecffee5fe0
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680427"
---
# <a name="how-to-send-and-retrieve-ascii-data-in-linux-and-macos"></a>方法:Linux および macOS での ASCII データの送信と取得 
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

この記事では、お使いの Linux または macOS システムで ASCII (UTF-8 以外) ロケールが生成されている、あるいはインストールされているものと想定しています。 

ASCII 文字セットをサーバーに送信するには (またはサーバーから取得するには):  

1.  目的のロケールがお使いのシステム環境の既定値ではない場合、最初の接続を行う前に必ず `setlocale(LC_ALL, $locale)` を呼び出します。 PHP setlocale() 関数では、現在のスクリプトに対してのみロケールが変更されます。最初の接続後に呼び出された場合、無視されることがあります。
 
2.  SQLSRV ドライバーを使用するとき、接続オプションとして `'CharacterSet' => SQLSRV_ENC_CHAR` を指定できますが、既定のエンコードであるため、この手順は任意です。

3.  PDO_SQLSRV ドライバーを使用するとき、2 つの方法があります。 まず、接続するとき、`PDO::SQLSRV_ATTR_ENCODING` を `PDO::SQLSRV_ENCODING_SYSTEM` に設定します (接続オプションの設定例については、「[PDO::__construct](../../connect/php/pdo-construct.md)」を参照してください)。 あるいは、正常に接続された後、この行 `$conn->setAttribute(PDO::SQLSRV_ATTR_ENCODING, PDO::SQLSRV_ENCODING_SYSTEM);` を追加します 
  
接続リソース (SQLSRV) または接続オブジェクト (PDO_SQLSRV) のエンコードを指定するとき、このドライバーでは、他の接続オプション文字列でその同じエンコードが使用されるものと想定されます。 サーバー名およびクエリ文字列も同じ文字セットを使用すると見なします。  
  
PDO_SQLSRV ドライバーの既定のエンコードは、SQLSRV ドライバーとは異なり、UTF-8 (PDO::SQLSRV_ENCODING_UTF8) です。 これらの定数の詳細については、「[定数 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)」を参照してください。 
  
## <a name="example"></a>例  
次の例からは、PHP Drivers for SQL Server を使用し、接続前に特定のロケールを指定するという方法で ASCII データを送信および取得する方法がわかります。 各種 Linux プラットフォームのロケールには、macOS の同じロケールとは異なる名前が付いている場合があります。 たとえば、US ISO-8859-1 (Latin 1) ロケールは Linux では `en_US.ISO-8859-1` で、macOS では名前が `en_US.ISO8859-1` になります。
  
例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がサーバーにインストールされているものと想定しています。 ブラウザーからこの例を実行すると、すべての出力はブラウザーに書き込まれます。  
  
```  
<?php  
  
// SQLSRV Example
//
// Setting locale for the script is only necessary if Latin 1 is not the default 
// in the environment
$locale = strtoupper(PHP_OS) === 'LINUX' ? 'en_US.ISO-8859-1' : 'en_US.ISO8859-1';
setlocale(LC_ALL, $locale);
        
$serverName = 'MyServer';
$database = 'Test';
$connectionInfo = array('Database'=>'Test', 'UID'=>$uid, 'PWD'=>$pwd);
$conn = sqlsrv_connect($serverName, $connectionInfo);
  
if ($conn === false) {
    echo "Could not connect.<br>";  
    die(print_r(sqlsrv_errors(), true));
}  
  
// Set up the Transact-SQL query to create a test table
//   
$stmt = sqlsrv_query($conn, "CREATE TABLE [Table1] ([c1_int] int, [c2_varchar] varchar(512))");

// Insert data using a parameter array 
//
$tsql = "INSERT INTO [Table1] (c1_int, c2_varchar) VALUES (?, ?)";
  
// Execute the query, $value being some ASCII string
//   
$stmt = sqlsrv_query($conn, $tsql, array(1, array($value, SQLSRV_PARAM_IN, SQLSRV_PHPTYPE_STRING(SQLSRV_ENC_CHAR))));
  
if ($stmt === false) {
    echo "Error in statement execution.<br>";  
    die(print_r(sqlsrv_errors(), true));  
}  
else {  
    echo "The insertion was successfully executed.<br>";  
}  
  
// Retrieve the newly inserted data
//   
$stmt = sqlsrv_query($conn, "SELECT * FROM Table1");
$outValue = null;  
if ($stmt === false) {  
    echo "Error in statement execution.<br>";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
// Retrieve and display the data
//   
if (sqlsrv_fetch($stmt)) {  
    $outValue = sqlsrv_get_field($stmt, 1, SQLSRV_PHPTYPE_STRING(SQLSRV_ENC_CHAR));
    echo "Value: " . $outValue . "<br>";
    if ($value !== $outValue) {
        echo "Data retrieved, \'$outValue\', is unexpected!<br>";
    }
}  
else {  
    echo "Error in fetching data.<br>";  
    die(print_r(sqlsrv_errors(), true));  
}  

// Free statement and connection resources
//   
sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  
?>  
```  
  
```
<?php  
  
// PDO_SQLSRV Example:
//
// Setting locale for the script is only necessary if Latin 1 is not the default 
// in the environment
$locale = strtoupper(PHP_OS) === 'LINUX' ? 'en_US.ISO-8859-1' : 'en_US.ISO8859-1';
setlocale(LC_ALL, $locale);
        
$serverName = 'MyServer';
$database = 'Test';

try {
    $conn = new PDO("sqlsrv:Server=$serverName;Database=$database;", $uid, $pwd);
    $conn->setAttribute(PDO::SQLSRV_ATTR_ENCODING, PDO::SQLSRV_ENCODING_SYSTEM);
    
    // Set up the Transact-SQL query to create a test table
    //   
    $stmt = $conn->query("CREATE TABLE [Table1] ([c1_int] int, [c2_varchar] varchar(512))");
    
    // Insert data using parameters, $value being some ASCII string
    //
    $stmt = $conn->prepare("INSERT INTO [Table1] (c1_int, c2_varchar) VALUES (:var1, :var2)");
    $stmt->bindValue(1, 1);
    $stmt->bindParam(2, $value);
    $stmt->execute();
    
    // Retrieve and display the data
    //
    $stmt = $conn->query("SELECT * FROM [Table1]");
    $outValue = null;
    if ($row = $stmt->fetch()) {
        $outValue = $row[1];
        echo "Value: " . $outValue . "<br>";
        if ($value !== $outValue) {
            echo "Data retrieved, \'$outValue\', is unexpected!<br>";
        }
    }
} catch (PDOException $e) {
    echo $e->getMessage() . "<br>";
} finally {
    // Free statement and connection resources
    //
    unset($stmt);
    unset($conn);
}

?>  
```  

## <a name="see-also"></a>参照  
[データの取得](../../connect/php/retrieving-data.md)  
[UTF-8 データの使用](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)
[データの更新 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)  
[SQLSRV ドライバー API リファレンス](../../connect/php/sqlsrv-driver-api-reference.md)  
[定数 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
[サンプル アプリケーション &#40;SQLSRV ドライバー&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
  
