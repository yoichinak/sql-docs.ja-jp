---
description: sqlsrv_server_info
title: sqlsrv_server_info | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- sqlsrv_server_info
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_server_info
- sqlsrv_server_info
ms.assetid: ef6fe2b7-d267-4379-b948-5626c4684367
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e1c263797c0f67751b5aa96899adadbf37017803
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99201038"
---
# <a name="sqlsrv_server_info"></a>sqlsrv_server_info
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

サーバーに関する情報を返します。 この関数を呼び出す前に、接続を確立する必要があります。  
  
## <a name="syntax"></a>構文  
  
```  
  
sqlsrv_server_info( resource $conn)  
```  
  
#### <a name="parameters"></a>パラメーター  
*$conn*: クライアントとサーバーを接続する接続リソース。  
  
## <a name="return-value"></a>戻り値  
次のキーを含む連想配列。  
  
|Key|説明|  
|-------|---------------|  
|CurrentDatabase|現在対象となっているデータベース。|  
|SQLServerVersion|SQL Server のバージョン。|  
|SQLServerName|サーバーの名前。|  
  
## <a name="example"></a>例  
次の例では、コマンドラインからこの例を実行すると、サーバー情報がコンソールに書き込まれます。  
  
```  
<?php  
/* Connect to the local server using Windows Authentication. */  
$serverName = "(local)";  
$conn = sqlsrv_connect( $serverName);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
$server_info = sqlsrv_server_info( $conn);  
if( $server_info )  
{  
      foreach( $server_info as $key => $value)  
      {  
             echo $key.": ".$value."\n";  
      }  
}  
else  
{  
      echo "Error in retrieving server info.\n";  
      die( print_r( sqlsrv_errors(), true));  
}  
  
/* Free connection resources. */  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>参照  
[SQLSRV ドライバー API リファレンス](../../connect/php/sqlsrv-driver-api-reference.md)  

[ドキュメントのコード例について](../../connect/php/about-code-examples-in-the-documentation.md)  
  
