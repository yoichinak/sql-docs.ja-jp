---
title: 接続のプール (Microsoft SQL Server 用 Drivers for PHP)
description: Microsoft SQL Server 用 Drivers for PHP 使用時の接続のプールの詳細と、オペレーティング システムによって動作が異なる場合があることについて説明します。
ms.custom: ''
ms.date: 08/01/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection pooling support
ms.assetid: 4d9a83d4-08de-43a1-975c-0a94005edc94
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 147e744a69850a5c76b9706c03a96fa67d2efb5f
ms.sourcegitcommit: 129f8574eba201eb6ade1f1620c6b80dfe63b331
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/30/2020
ms.locfileid: "87435264"
---
# <a name="connection-pooling-microsoft-drivers-for-php-for-sql-server"></a>接続のプール (Microsoft SQL Server 用 Drivers for PHP)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]の接続のプールについて重要な点は、次のとおりです。  
  
-   [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] では ODBC 接続プールが使用されます。  
  
-   Windows の既定では、接続プールは有効になっています。 Linux と macOS では、接続プールが ODBC に対して有効になっている場合にのみ、接続がプールされます (「[接続プールの有効化と無効化](#enablingdisabling-connection-pooling)」を参照してください)。 接続プールが有効になっているときに、サーバーに接続すると、ドライバーでは、新しい接続を作成する前にプールされたものの使用が試みられます。 プールに同等の接続がない場合、新しい接続が構築され、プールに追加されます。 ドライバーは、接続文字列の比較に基づき、接続が同等かどうかを判断します。  
  
-   プールの接続が使用されると、接続状態がリセットされます (Windows のみ)。  
  
-   接続を閉じると、接続がプールに返されます。  
  
接続のプールについて詳しくは、「[ドライバー マネージャーの接続プール](../../odbc/reference/develop-app/driver-manager-connection-pooling.md)」をご覧ください。  
  
## <a name="enablingdisabling-connection-pooling"></a>接続プールの有効化と無効化
### <a name="windows"></a>Windows
(接続プールで同等の接続を探す代わりに) 新しい接続を構築するようにドライバーに強制できます。その場合、接続文字列の *ConnectionPooling* 属性を **false** (または 0) に設定します。  
  
接続文字列から *ConnectionPooling* 属性を省略する場合、あるいは **true** (または 1) に設定する場合、同等の接続が接続プールに存在しないときにのみ、ドライバーは新しい接続を構築します。  

> [!NOTE]  
> 複数のアクティブな結果セット (MARS) は既定では無効になっています。 MARS とプールの両方が使用されているとき、MARS を正しく機能させるため、"*最初の*" クエリでドライバーの接続リセットにかかる時間が長くなります。そのため、クエリ タイムアウトが指定されていても無視されます。 ただし、クエリのタイムアウト設定は後続のクエリで有効になります。
  
必要に応じて「[方法: 複数のアクティブな結果セット (MARS) を無効にする](../../connect/php/how-to-disable-multiple-active-resultsets-mars.md)」を参照してください。 その他の接続属性の詳細については、「 [Connection Options](../../connect/php/connection-options.md)」を参照してください。  

### <a name="linux-and-macos"></a>Linux と macOS
接続プールを有効または無効にする場合に、*ConnectionPooling* 属性を使用することはできません。 

接続プールを有効または無効にするには、odbcinst.ini 構成ファイルを編集します。 変更を有効にするには、ドライバーを再度読み込む必要があります。

dbcinst.ini ファイル内で `Pooling` を `Yes` に、`CPTimeout` を正の値に設定すると、接続プールが有効になります。 
```
[ODBC]
Pooling=Yes

[ODBC Driver 17 for SQL Server]
CPTimeout=<int value>
```
  
最低限、odbcinst.ini ファイルは次の例のようにする必要があります。

```
[ODBC]
Pooling=Yes

[ODBC Driver 17 for SQL Server]
Description=Microsoft ODBC Driver 17 for SQL Server
Driver=/opt/microsoft/msodbcsql17/lib64/libmsodbcsql-17.5.so.2.1
UsageCount=1
CPTimeout=120
```

odbcinst.ini ファイル内で `Pooling` を `No` に設定すると、ドライバーは新しい接続の作成を強制されます。
```
[ODBC]
Pooling=No
```

## <a name="remarks"></a>解説
- Linux または macOS では、2.3.7 以前の unixODBC で接続プールが推奨されていません。 odbcinst.ini ファイルでプールが有効になっている場合、つまり、ConnectionPooling 接続オプションが適用されない場合、すべての接続がプールされます。 プーリングを無効にするには、odbcinst.ini ファイル内で Pooling=No を設定し、ドライバーを再度読み込みます。 
  - unixODBC < = 2.3.4 (Linux および macOS) の場合、エラー メッセージ、警告、情報メッセージなどの適切な診断情報が返されない場合があります
  - このため、SQLSRV および PDO_SQLSRV ドライバーでは、長いデータ (xml やバイナリなど) を文字列として適切にフェッチできない可能性があります。 回避策として、長いデータをストリームとしてフェッチすることができます。 SQLSRV については、次の例を参照してください。

```
<?php
$connectionInfo = array("Database"=>"test", "UID"=>"username", "PWD"=>"password");

$conn1 = sqlsrv_connect("servername", $connectionInfo);

$longSample = str_repeat("a", 8500);
$xml1 = 
'<ParentXMLTag>
  <ChildTag01>'.$longSample.'</ChildTag01>
</ParentXMLTag>';

// Create table and insert xml string into it
sqlsrv_query($conn1, "CREATE TABLE xml_table (field xml)");
sqlsrv_query($conn1, "INSERT into xml_table values ('$xml1')");

// retrieve the inserted xml
$column1 = getColumn($conn1);

// return the connection to the pool
sqlsrv_close($conn1);

// This connection is from the pool
$conn2 = sqlsrv_connect("servername", $connectionInfo);
$column2 = getColumn($conn2);

sqlsrv_query($conn2, "DROP TABLE xml_table");
sqlsrv_close($conn2);

function getColumn($conn)
{
    $tsql = "SELECT * from xml_table";
    $stmt = sqlsrv_query($conn, $tsql);
    sqlsrv_fetch($stmt);
    // This might fail in Linux and macOS
    // $column = sqlsrv_get_field($stmt, 0, SQLSRV_PHPTYPE_STRING(SQLSRV_ENC_CHAR));
    // The workaround is to fetch it as a stream
    $column = sqlsrv_get_field($stmt, 0, SQLSRV_PHPTYPE_STREAM(SQLSRV_ENC_CHAR));
    sqlsrv_free_stmt($stmt);
    return ($column);
}
?>
```


## <a name="see-also"></a>参照  
[方法:Windows 認証を使用した接続](../../connect/php/how-to-connect-using-windows-authentication.md)

[方法: SQL Server 認証を使用して接続する](../../connect/php/how-to-connect-using-sql-server-authentication.md)  
  
