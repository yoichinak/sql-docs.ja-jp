---
title: アイドル状態の接続の回復性
description: アイドル状態の接続の回復性の概要と、Microsoft Drivers for PHP for SQL Server 内でのその動作について説明します。
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4008dd4f023170b50bdf28f1f026da9ee892f970
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726863"
---
# <a name="idle-connection-resiliency"></a>アイドル状態の接続の回復性
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[接続の回復性](../odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)は、特定の制約内で、切断されたアイドル状態の接続を再確立できるという原則です。 Microsoft SQL Server への接続に失敗した場合、接続の回復性により、クライアントは接続の再確立を自動的に試みることができます。 接続の回復性は、データソースのプロパティです。接続の回復性がサポートされているのは、SQL Server 2014 以降と Azure SQL Database のみです。

接続の回復性は、接続文字列に追加できる 2 つの接続キーワードを使用して実装されます: **ConnectRetryCount** と **ConnectRetryInterval**。

|Keyword|値|Default|説明|
|-|-|-|-|
|**ConnectRetryCount**| 0 から 255 までの整数|1|中止するまでに、切断された接続の再確立を試みる最大回数。 既定では、接続が切断されると、接続の再確立が 1 回試みられます。 値 0 は、再接続が試みられないことを意味します。|
|**ConnectRetryInterval**| 1 から 60 までの整数|1| 接続の再確立を試行する秒単位の時間間隔。 アプリケーションでは、接続途絶検出直後に再接続が試みられた後、**ConnectRetryInterval** 秒待ってから、再試行されます。 **ConnectRetryCount** が 0 の場合、このキーワードは無視されます。

**ConnectRetryCount** と **ConnectRetryInterval** を掛けた積が **LoginTimeout** より大きい場合、クライアントは **LoginTimeout** に達した時点で、接続の試みを停止します。そうしないと、**ConnectRetryCount** に達するまで再接続が試行され続けます。

#### <a name="remarks"></a>解説

接続の回復性は、接続がアイドル状態のときに適用されます。 たとえば、トランザクションの実行中にエラーが発生した場合は、再接続の試行はトリガーされません。他の場合と同様に失敗します。 復旧不可能なセッション状態と呼ばれる次の状況では、再接続の試行はトリガーされません。

* 一時テーブル
* グローバル カーソルとローカル カーソル
* トランザクション コンテキストとセッション レベルのトランザクション ロック
* アプリケーション ロック
* EXECUTE AS/REVERT セキュリティ コンテキスト
* OLE オートメーション ハンドル
* 準備済み XML ハンドル
* トレース フラグ

## <a name="example"></a>例

次のコードでは、データベースに接続してクエリが実行されます。 接続はセッションを強制終了することによって中断され、切断された接続を使用して新しいクエリが試行されます。 この例では、[AdventureWorks](/previous-versions/sql/sql-server-2008/ms124501(v=sql.100)) サンプル データベースを使用します。

この例では、接続を切断する前にバッファー カーソルを指定します。 バッファー カーソルを指定しない場合、アクティブなサーバー側カーソルが存在し、切断されたときに接続はアイドル状態にならないため、接続は再確立されません。 ただし、その場合でも、接続を断つ前に sqlsrv_free_stmt() を呼び出してカーソルを解放すると、接続が正常に再確立されます。

```php
<?php
// This function breaks the connection by determining its session ID and killing it.
// A separate connection is used to break the main connection because a session
// cannot kill itself. The sleep() function ensures enough time has passed for KILL
// to finish ending the session.
function BreakConnection( $conn, $conn_break )
{
    $stmt1 = sqlsrv_query( $conn, "SELECT @@SPID" );
    if ( sqlsrv_fetch( $stmt1 ) )
    {
        $spid=sqlsrv_get_field( $stmt1, 0 );
    }

    $stmt2 = sqlsrv_prepare( $conn_break, "KILL ".$spid );
    sqlsrv_execute( $stmt2 );
    sleep(1);
}

// Connect to the local server using Windows authentication and specify
// AdventureWorks as the database in use. Specify values for
// ConnectRetryCount and ConnectRetryInterval as well.
$databaseName = 'AdventureWorks2014';
$serverName = '(local)';
$connectionInfo = array( "Database"=>$databaseName, "ConnectRetryCount"=>10, "ConnectRetryInterval"=>10 );

$conn = sqlsrv_connect( $serverName, $connectionInfo );
if( $conn === false)  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}

// A separate connection that will be used to break the main connection $conn
$conn_break = sqlsrv_connect( $serverName, array( "Database"=>$databaseName) );

// Create a statement to retrieve the contents of a table
$stmt1 = sqlsrv_query( $conn, "SELECT * FROM HumanResources.Employee",
                       array(), array( "Scrollable"=>"buffered" ) );
if( $stmt1 === false )
{
     echo "Error in statement 1.\n";
     die( print_r( sqlsrv_errors(), true ));
}
else
{
    echo "Statement 1 successful.\n";
    $rowcount = sqlsrv_num_rows( $stmt1 );
    echo $rowcount." rows in result set.\n";
}

// Now break the connection $conn
BreakConnection( $conn, $conn_break );

// Create another statement. The connection will be reestablished.
$stmt2 = sqlsrv_query( $conn, "SELECT * FROM HumanResources.Department",
                       array(), array( "Scrollable"=>"buffered" ) );
if( $stmt2 === false )
{
     echo "Error in statement 2.\n";
     die( print_r( sqlsrv_errors(), true ));
}
else
{
    echo "Statement 2 successful.\n";
    $rowcount = sqlsrv_num_rows( $stmt2 );
    echo $rowcount." rows in result set.\n";
}

sqlsrv_close( $conn );
sqlsrv_close( $conn_break );
?>
```
予想される出力:
```
Statement 1 successful.
290 rows in result set.
Statement 2 successful.
16 rows in result set.
```

## <a name="see-also"></a>参照
[Windows ODBC ドライバーの接続の復元性](../odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)