---
description: position (java.lang.String, long) メソッド
title: position メソッド (java.lang.String, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerClob.position (java.lang.String, long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 86fad8ed-375a-42e1-b40e-1fa085957a2c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c2017c991eb080a6684b2cb24dc7d90f9b585c52
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99176912"
---
# <a name="position-method-javalangstring-long"></a>position (java.lang.String, long) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  渡された開始位置に基づいて、CLOB 内の指定された部分文字列の文字位置を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public long position(java.lang.String searchstr,  
                     long start)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *searchstr*  
  
 検索対象の部分文字列。  
  
 *start*  
  
 検索を開始する位置です。最初の位置は 1 です。  
  
## <a name="return-value"></a>戻り値  
 部分文字列が現れる位置です。部分文字列がない場合は -1 が返されます。最初の位置は 1 です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この position メソッドは、java.sql.Clob インターフェイスの position メソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [position メソッド &#40;SQLServerClob&#41;](../../../connect/jdbc/reference/position-method-sqlserverclob.md)   
 [SQLServerClob のメソッド](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob メンバー](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob クラス](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
