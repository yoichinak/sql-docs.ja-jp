---
title: 手順 4:PHP を使用して SQL に弾性的に接続する
description: 手順 4 は、接続試行中の一時的なエラーによって再試行が行われる方法がわかるように設計されていデモ プログラムです。
ms.custom: ''
ms.date: 01/22/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8013474f-48e9-43d5-ab89-7b0504044468
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b2222c72be6a499e9a60424d1a7cc508904b8f33
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726653"
---
# <a name="step-4-connect-resiliently-to-sql-with-php"></a>手順 4:PHP を使用して SQL に弾性的に接続する
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

  
デモ プログラムは、接続の試行時に一時的なエラー (この[付録](../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)に記載されているプレフィックス "08" が付くエラー コード) が発生すると再試行されるように設計されています。 しかし、クエリ コマンドの実行中に一時的なエラーが生じると、プログラムによって接続が破棄され、新しい接続が作成された後、クエリ コマンドが再試行されます。 この設計は選択しないことをお勧めします。 デモ プログラムは、使用可能な設計上の柔軟性をいくつか示しています。  
  
このコード サンプルの内容の大部分は、例外キャッチのロジックの記述です。   
  
[sqlsrv_query()](../../connect/php/sqlsrv-query.md) 関数は、SQL Database に対するクエリから結果セットを取得するために使用できます。 この関数では基本的に任意のクエリと接続オブジェクトを受け入れ、[sqlsrv_fetch_array()](../../connect/php/sqlsrv-fetch-array.md) を使用して反復処理できる結果セットを返します。 
  
```php

    <?php  
        // Variables to tune the retry logic.    
        $connectionTimeoutSeconds = 30;  // Default of 15 seconds is too short over the Internet, sometimes.  
        $maxCountTriesConnectAndQuery = 3;  // You can adjust the various retry count values.  
        $secondsBetweenRetries = 4;  // Simple retry strategy.  
        $errNo = 0;  
        $serverName = "tcp:yourdatabase.database.windows.net,1433";  
        $connectionOptions = array("Database"=>"AdventureWorks",  
           "Uid"=>"yourusername", "PWD"=>"yourpassword", "LoginTimeout" => $connectionTimeoutSeconds);  
        $conn = null;  
        $arrayOfTransientErrors = array('08001', '08002', '08003', '08004', '08007', '08S01'); 
        for ($cc = 1; $cc <= $maxCountTriesConnectAndQuery; $cc++) {  
            // [A.2] Connect, which proceeds to issue a query command.  
            $conn = sqlsrv_connect($serverName, $connectionOptions);    
            if ($conn === true) {  
                echo "Connection was established";  
                echo "<br>";  
  
                $tsql = "SELECT Name FROM Production.ProductCategory";  
                $stmt = sqlsrv_query($conn, $tsql);  
                if ($stmt === false) {
                    echo "Error in query execution";  
                    echo "<br>";  
                    die(print_r(sqlsrv_errors(), true));  
                }
                while($row = sqlsrv_fetch_array($stmt, SQLSRV_FETCH_ASSOC)) {     
                    echo $row['Name'] . "<br/>" ;
                }  
                sqlsrv_free_stmt($stmt);  
                sqlsrv_close( $conn); 
                break;  
            } else {    
                // [A.4] Check whether the error code is on the list of allowed transients.  
                $isTransientError = false;  
                $errorCode = '';
                if (($errors = sqlsrv_errors()) != null) {
                    foreach ($errors as $error) {  
                        $errorCode = $error['code'];
                        $isTransientError = in_array($errorCode, $arrayOfTransientErrors);
                        if ($isTransientError) {
                            break;
                        }
                    }
                }  
                if (!$isTransientError) { 
                    // it is a static persistent error...
                    echo("Persistent error suffered with error code = $errorCode. Program will terminate.");  
                    echo "<br>";  
                    // [A.5] Either the connection attempt or the query command attempt suffered a persistent error condition.  
                    // Break the loop, let the hopeless program end.  
                    exit(0);  
                }  
                // [A.6] It is a transient error from an attempt to issue a query command.  
                // So let this method reloop and try again. However, we recommend that the new query  
                // attempt should start at the beginning and establish a new connection.  
                if ($cc >= $maxCountTriesConnectAndQuery) {  
                    echo "Transient errors suffered in too many retries - $cc. Program will terminate.";  
                    echo "<br>";  
                    exit(0);  
                }  
                echo("Transient error encountered with error code = $errorCode. Program might retry by itself.");    
                echo "<br>";  
                echo "$cc attempts so far. Might retry.";  
                echo "<br>";  
                // A very simple retry strategy, a brief pause before looping.  
                sleep(1*$secondsBetweenRetries);  
            }  
            // [A.3] All has gone well, so let the program end.  
        }  
    ?>
```