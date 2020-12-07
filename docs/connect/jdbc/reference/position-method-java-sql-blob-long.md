---
description: position (java.sql.Blob, long) メソッド
title: position メソッド (java.sql.Blob, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerBlob.position (java.sql.Blob.long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ebd005e5-f6c5-4789-87f9-d2fdacd35060
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 941996adfc1fb23340da173d2c7f28393c25e17e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433034"
---
# <a name="position-method-javasqlblob-long"></a>position (java.sql.Blob, long) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  渡されたパターンと開始インデックスに基づいて、BLOB 内の指定されたパターンの位置を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public long position(java.sql.Blob pattern,  
                     long start)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *pattern*  
  
 検索するパターンです。  
  
 *start*  
  
 検索の開始インデックスです。  
  
## <a name="return-value"></a>戻り値  
 パターンが見つかった場合は位置の **long** 値で、見つからなかった場合は -1 です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この position メソッドは、java.sql.Blob インターフェイスの position メソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [position メソッド &#40;SQLServerBlob&#41;](../../../connect/jdbc/reference/position-method-sqlserverblob.md)   
 [SQLServerBlob のメソッド](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob のメンバー](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob クラス](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
