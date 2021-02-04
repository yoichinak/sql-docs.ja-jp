---
description: truncate メソッド (SQLServerClob)
title: truncate メソッド (SQLServerClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerClob.truncate
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ea3b2a03-387e-49d7-a4d6-ca6a6a354c90
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 40c8285312ee7129d4d6af24d329d9ee64fa3ca4
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99189768"
---
# <a name="truncate-method-sqlserverclob"></a>truncate メソッド (SQLServerClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  CLOB を指定された長さに切り捨てます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void truncate(long len)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *len*  
  
 CLOB を切り捨てた後に残す長さ (文字数) です。  
  
## <a name="exceptions"></a>例外  
 java.sql.SQLException  
  
## <a name="remarks"></a>解説  
 この truncate メソッドは、java.sql.Clob インターフェイスの truncate メソッドで規定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerClob のメソッド](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob メンバー](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob クラス](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
