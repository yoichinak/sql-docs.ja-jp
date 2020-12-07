---
title: カーソルの種類 (SQLSRV ドライバー)
description: SQL Server 用 Microsoft Drivers for PHP を利用し、順序に関係なくアクセスできる結果セットをカーソルの種類を使用して作成する方法について説明します。
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8472d839-8124-4a62-a83c-7e771b0d4962
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8e72381eed4aa89ccd9656d3eabadb22bccd357d
ms.sourcegitcommit: 620a868e623134ad6ced6728ce9d03d7d0038fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87411468"
---
# <a name="cursor-types-sqlsrv-driver"></a>カーソルの種類 (SQLSRV ドライバー)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

SQLSRV ドライバーでは、カーソルの種類に基づき、任意の順番で行にアクセスできる結果セットを作成できます。  このトピックでは、クライアント側 (バッファーされる) およびサーバー側 (バッファーされない) カーソルについて説明します。  
  
## <a name="cursor-types"></a>カーソルの種類  
[sqlsrv_query](../../connect/php/sqlsrv-query.md) を使用して、または [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) を使用して結果セットを作成する場合は、カーソルの種類を指定できます。 既定では、順方向専用カーソルが使用されます。これにより、結果セットの先頭行から開始し、結果セットの末尾に達するまで、一度に 1 行ずつ移動することができます。  
  
スクロール可能なカーソルを使用して結果セットを作成すると、結果セット内の任意の行に任意の順序でアクセスできます。 次の表は、sqlsrv_query または sqlsrv_prepare において **Scrollable** オプションに渡すことができる値を示しています。  
  
|オプション|説明|  
|----------|---------------|  
|SQLSRV_CURSOR_FORWARD|結果セットの先頭行から開始し、結果セットの末尾に達するまで、一度に 1 行ずつ移動することができます。<br /><br />これは、既定のカーソルの種類です。<br /><br />[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md) からは、このカーソルの種類で作成された結果セットに関するエラーが返されます。<br /><br />**forward** は SQLSRV_CURSOR_FORWARD の省略形です。|  
|SQLSRV_CURSOR_STATIC|任意の順序で行にアクセスできますが、変更内容はデータベースに反映されません。<br /><br />**static** は SQLSRV_CURSOR_STATIC の省略形です。|  
|SQLSRV_CURSOR_DYNAMIC|任意の順序で行にアクセスでき、変更内容はデータベースに反映されます。<br /><br />[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md) からは、このカーソルの種類で作成された結果セットに関するエラーが返されます。<br /><br />**dynamic** は、SQLSRV_CURSOR_DYNAMIC の省略形です。|  
|SQLSRV_CURSOR_KEYSET|任意の順序で行にアクセスできます。 ただし、行がテーブルから削除される場合 (削除された行は、値なしで返されます)、キーセット カーソルは行の数を更新しません。<br /><br />**keyset** は SQLSRV_CURSOR_KEYSET の省略形です。|  
|SQLSRV_CURSOR_CLIENT_BUFFERED|任意の順序で行にアクセスできます。 クライアント側のカーソル クエリを作成します。<br /><br />**buffered** は SQLSRV_CURSOR_CLIENT_BUFFERED の省略形です。|  
  
クエリによって複数の結果セットが生成された場合は、すべての結果セットに **[スクロール可能]** オプションが適用されます。  
  
## <a name="selecting-rows-in-a-result-set"></a>結果セット内のすべての行を選択する  
結果セットを作成したら、[sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md)、[sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)、または [sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md) を使用して行を指定できます。  
  
次の表では、*row* パラメーターで指定できる値について説明します。  
  
|パラメーター|説明|  
|-------------|---------------|  
|SQLSRV_SCROLL_NEXT|次の行を指定します。 これは、スクロール可能な結果セットに対して *row* パラメーターを指定しない場合、既定値となります。|  
|SQLSRV_SCROLL_PRIOR|現在の行の前の行を指定します。|  
|SQLSRV_SCROLL_FIRST|結果セットの最初の行を指定します。|  
|SQLSRV_SCROLL_LAST|結果セットの最後の行を指定します。|  
|SQLSRV_SCROLL_ABSOLUTE|*offset* パラメーターで指定された行を指定します。|  
|SQLSRV_SCROLL_RELATIVE|現在の行から *offset* パラメーターで指定された行を指定します。|  
  
## <a name="server-side-cursors-and-the-sqlsrv-driver"></a>サーバー側カーソルと SQLSRV ドライバー  
次の例は、さまざまなカーソルの効果を示します。 例の 33 行目には、それぞれ異なるカーソルを指定する 3 つのクエリ ステートメントのうちの 1 番目が表示されています。  2 つのクエリ ステートメントはコメント化されています。 プログラムを実行するたびに、別の種類のカーソルを使用して、データベースの更新の結果を 47 行目で表示します。  
  
```  
<?php  
$server = "server_name";  
$conn = sqlsrv_connect( $server, array( 'Database' => 'test' ));  
if ( $conn === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "DROP TABLE dbo.ScrollTest" );  
if ( $stmt !== false ) {   
   sqlsrv_free_stmt( $stmt );   
}  
  
$stmt = sqlsrv_query( $conn, "CREATE TABLE ScrollTest (id int, value char(10))" );  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "INSERT INTO ScrollTest (id, value) VALUES(?,?)", array( 1, "Row 1" ));  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "INSERT INTO ScrollTest (id, value) VALUES(?,?)", array( 2, "Row 2" ));  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "INSERT INTO ScrollTest (id, value) VALUES(?,?)", array( 3, "Row 3" ));  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "SELECT * FROM ScrollTest", array(), array( "Scrollable" => 'keyset' ));  
// $stmt = sqlsrv_query( $conn, "SELECT * FROM ScrollTest", array(), array( "Scrollable" => 'dynamic' ));  
// $stmt = sqlsrv_query( $conn, "SELECT * FROM ScrollTest", array(), array( "Scrollable" => 'static' ));  
  
$rows = sqlsrv_has_rows( $stmt );  
if ( $rows != true ) {  
   die( "Should have rows" );  
}  
  
$result = sqlsrv_fetch( $stmt, SQLSRV_SCROLL_LAST );  
$field1 = sqlsrv_get_field( $stmt, 0 );  
$field2 = sqlsrv_get_field( $stmt, 1 );  
echo "\n$field1 $field2\n";  
  
$stmt2 = sqlsrv_query( $conn, "delete from ScrollTest where id = 3" );  
// or  
// $stmt2 = sqlsrv_query( $conn, "UPDATE ScrollTest SET id = 4 WHERE id = 3" );  
if ( $stmt2 !== false ) {   
   sqlsrv_free_stmt( $stmt2 );   
}  
  
$result = sqlsrv_fetch( $stmt, SQLSRV_SCROLL_LAST );  
$field1 = sqlsrv_get_field( $stmt, 0 );  
$field2 = sqlsrv_get_field( $stmt, 1 );  
echo "\n$field1 $field2\n";  
  
sqlsrv_free_stmt( $stmt );  
sqlsrv_close( $conn );  
?>  
```  
  
## <a name="client-side-cursors-and-the-sqlsrv-driver"></a>クライアント側のカーソルと SQLSRV ドライバー  
クライアント側のカーソルはバージョン 3.0 の [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] で追加された機能です。これを使用すると、結果セット全体をメモリにキャッシュすることができます。 クライアント側のカーソルを使用すると、クエリを実行した後に行数を使用できます。  
  
クライアント側のカーソルは、小規模から中規模の結果セットに対して使用する必要があります。 大規模な結果セットには、サーバー側のカーソルを使用します。  
  
バッファーが結果セット全体を保持するために十分な大きさではない場合、クエリから false が返されます。 バッファーのサイズは PHP メモリの上限まで増やすことができます。  
  
SQLSRV ドライバーを使用すれば、[sqlsrv_configure](../../connect/php/sqlsrv-configure.md) の ClientBufferMaxKBSize 設定を使用して、結果セットを保持するバッファーのサイズを構成できます。 [sqlsrv_get_config](../../connect/php/sqlsrv-get-config.md) から、ClientBufferMaxKBSize の値が返されます。 php.ini ファイルで sqlsrv.ClientBufferMaxKBSize を使用して最大バッファー サイズを設定することもできます (たとえば、sqlsrv.ClientBufferMaxKBSize = 1024)。  
  
次のサンプルは以下を示しています。  
  
-   クライアント側のカーソルでは、常に行数が使用できます。  
  
-   クライアント側のカーソルとバッチ ステートメントの使用。  
  
```  
<?php  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if ( $conn === false ) {  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$tsql = "select * from HumanResources.Department";  
  
// Execute the query with client-side cursor.  
$stmt = sqlsrv_query($conn, $tsql, array(), array("Scrollable"=>"buffered"));  
if (! $stmt) {  
   echo "Error in statement execution.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// row count is always available with a client-side cursor  
$row_count = sqlsrv_num_rows( $stmt );  
echo "\nRow count = $row_count\n";  
  
// Move to a specific row in the result set.  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_FIRST);  
$EmployeeID = sqlsrv_get_field( $stmt, 0);  
echo "Employee ID = $EmployeeID \n";  
  
// Client-side cursor and batch statements  
$tsql = "select top 2 * from HumanResources.Employee;Select top 3 * from HumanResources.EmployeeAddress";  
  
$stmt = sqlsrv_query($conn, $tsql, array(), array("Scrollable"=>"buffered"));  
if (! $stmt) {  
   echo "Error in statement execution.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$row_count = sqlsrv_num_rows( $stmt );  
echo "\nRow count for first result set = $row_count\n";  
  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_FIRST);  
$EmployeeID = sqlsrv_get_field( $stmt, 0);  
echo "Employee ID = $EmployeeID \n";  
  
sqlsrv_next_result($stmt);  
  
$row_count = sqlsrv_num_rows( $stmt );  
echo "\nRow count for second result set = $row_count\n";  
  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_LAST);  
$EmployeeID = sqlsrv_get_field( $stmt, 0);  
echo "Employee ID = $EmployeeID \n";  
?>  
```  
  
次のサンプルでは、[sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) と、別のクライアント バッファー サイズを使用したクライアント側カーソルを示しています。
  
```  
<?php  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if ( $conn === false ) {  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$tsql = "select * from HumanResources.Employee";  
$stmt = sqlsrv_prepare( $conn, $tsql, array(), array("Scrollable" => SQLSRV_CURSOR_CLIENT_BUFFERED, "ClientBufferMaxKBSize" => 51200));
  
if (! $stmt ) {  
   echo "Statement could not be prepared.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
sqlsrv_execute( $stmt);  
  
$row_count = sqlsrv_num_rows( $stmt );  
if ($row_count)  
   echo "\nRow count = $row_count\n";  
  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_FIRST);  
if ($row ) {  
   $EmployeeID = sqlsrv_get_field( $stmt, 0);  
   echo "Employee ID = $EmployeeID \n";  
}  
?>  
```  
  
## <a name="see-also"></a>参照  
[カーソルの種類を指定し、行を選択する](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)  
  
