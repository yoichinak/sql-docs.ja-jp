---
description: closeUnreferencedPreparedStatementHandles メソッド (SQLServerConnection)
title: closeUnreferencedPreparedStatementHandles メソッド (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerConnection.closeUnreferencedPreparedStatementHandles
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3dc6b5a8284216d09cececaeb5e439709f8af504
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99168588"
---
# <a name="closeunreferencedpreparedstatementhandles-method-sqlserverconnection"></a>closeUnreferencedPreparedStatementHandles メソッド (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 破棄された未処理の準備されたステートメントに対して、実行されるように準備解除要求が強制的に実行されます。

## <a name="syntax"></a>構文  
  
```  
  
public void closeUnreferencedPreparedStatementHandles()  
```  


## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  

## <a name="remarks"></a>解説  
 このメソッドは、JDBC ドライバー バージョン 6.4 以降で使用できます。
 
## <a name="see-also"></a>参照  
 [SQLServerConnection のメンバー](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection クラス](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
