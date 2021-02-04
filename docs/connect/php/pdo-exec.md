---
title: PDO::exec
description: SQL Server 用 Microsoft PDO_SQLSRV Driver for PHP の PDO::exec 関数の API リファレンス。
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.assetid: 359a87c6-c13a-4518-8f23-a922e7f3b171
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ad79792d21e9b097f6aee681b1097c8aacfa44fa
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99202018"
---
# <a name="pdoexec"></a>PDO::exec
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

1 回の関数呼び出しで SQL ステートメントを準備および実行し、ステートメントの影響を受けた行数を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
int PDO::exec ($statement)  
```  
  
#### <a name="parameters"></a>パラメーター  
*$statement*: 実行する SQL ステートメントを含む文字列です。  
  
## <a name="return-value"></a>戻り値  
影響を受けた行数を報告する整数です。  
  
## <a name="remarks"></a>解説  
*$statement* に複数の SQL ステートメントが含まれる場合、最後のステートメントの影響を受ける行数のみを返します。  
  
PDO::exec では SELECT ステートメントの結果は返しません。  
  
PDO::exec の動作に影響する属性は次のとおりです。  
  
-   PDO::ATTR_DEFAULT_FETCH_MODE  
  
-   PDO::SQLSRV_ATTR_ENCODING  
  
-   PDO::SQLSRV_ATTR_QUERY_TIMEOUT  
  
詳細については、「 [PDO::setAttribute](../../connect/php/pdo-setattribute.md)」を参照してください。 
  
PDO のサポートは [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]のバージョン 2.0 で追加されました。  
  
## <a name="example"></a>例  
この例では、Table1 の col1 に 'xxxyy' がある行を削除します。 次いで例では削除した行数を報告します。  
  
```  
<?php  
   $c = new PDO( "sqlsrv:server=(local)");  
  
   $c->exec("use Test");  
   $ret = $c->exec("delete from Table1 where col1 = 'xxxyy'");  
   echo $ret;  
?>  
```  
  
## <a name="see-also"></a>参照  
[PDO クラス](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
