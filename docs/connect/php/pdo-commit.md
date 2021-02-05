---
title: PDO::commit
description: SQL Server 用 Microsoft PDO_SQLSRV Driver for PHP の PDO::commit 関数の API リファレンス。
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.assetid: a0db4a00-9700-4f49-ab16-6522dd1101d3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2a498e78ce994907d666e8fdc01a494234d858d2
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99202065"
---
# <a name="pdocommit"></a>PDO::commit
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) を呼び出した後に発行されたデータベースにコマンドを送信し、接続を自動コミット モードに戻します。  
  
## <a name="syntax"></a>構文  
  
```  
  
bool PDO::commit();  
```  
  
## <a name="return-value"></a>戻り値  
メソッドの呼び出しに成功した場合は true、それ以外の場合は false。  
  
## <a name="remarks"></a>解説  
PDO::commit は PDO::ATTR_AUTOCOMMIT の値によって影響を受けず、PDO::ATTR_AUTOCOMMIT の値に影響を与えません。  
  
PDO::commit の使用例については、「 [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) 」を参照してください。  
  
PDO のサポートは [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]のバージョン 2.0 で追加されました。  
  
## <a name="see-also"></a>参照  
[PDO クラス](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
