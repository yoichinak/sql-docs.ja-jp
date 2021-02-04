---
description: getMaxRows メソッド (SQLServerStatement)
title: getMaxRows メソッド (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerStatement.getMaxRows
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6aece4e5-027d-434e-a8cf-a67c0484f189
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: af3a66f1ebcc4487c4ed74db06e3e1d949e65535
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99175550"
---
# <a name="getmaxrows-method-sqlserverstatement"></a>getMaxRows メソッド (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトによって生成される [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトが含むことのできる最大行数を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final int getMaxRows()  
```  
  
## <a name="return-value"></a>戻り値  
 最大行数を示す **int** です。制限しない場合は 0 です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この getMaxRows メソッドは、java.sql.Statement インターフェイスの getMaxRows メソッドで指定されています。  
  
 getMaxRows メソッドは、スクロール可能な動的カーソルに対して常に 0 を返します。  
  
## <a name="see-also"></a>参照  
 [SQLServerStatement のメンバー](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement クラス](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
