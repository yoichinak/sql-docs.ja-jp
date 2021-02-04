---
description: getRow メソッド (SQLServerResultSet)
title: getRow メソッド (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerResultSet.getRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a266e3bc-05c2-44e2-9346-125ae6780216
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 191cfad8b1610d3fb379b3893f478a849aa4f540
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99175128"
---
# <a name="getrow-method-sqlserverresultset"></a>getRow メソッド (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  現在の行番号を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public int getRow()  
```  
  
## <a name="return-value"></a>戻り値  
 現在の行番号を示す **int** です。行がない場合は 0 です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この getRow メソッドは、java.sql.ResultSet インターフェイスの getRow メソッドで規定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
