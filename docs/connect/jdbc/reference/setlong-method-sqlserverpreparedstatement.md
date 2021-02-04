---
description: setLong メソッド (SQLServerPreparedStatement)
title: setLong メソッド (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerPreparedStatement.setLong
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 08223a62-6489-44e4-85e8-b45bfbb11cfc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f4c6c4c1d98ae1636b2bdf244eb40bc7bf424d57
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99178874"
---
# <a name="setlong-method-sqlserverpreparedstatement"></a>setLong メソッド (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定されたパラメーターを、渡された **long** 値に設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final void setLong(int n,  
                          long x)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *n*  
  
 パラメーターの番号を示す **int** です。  
  
 *x*  
  
 **long** 値です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この setLong メソッドは、java.sql.PreparedStatement インターフェイスの setLong メソッドで規定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerPreparedStatement のメンバー](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement クラス](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
