---
description: setTransactionIsolation メソッド (SQLServerConnection)
title: setTransactionIsolation メソッド (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerConnection.setTransactionIsolation
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6a8fa4d3-5237-40f8-8a02-b40a3d7a1131
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f391337a0034fa7feeb284352d8c3d677a3c3fa7
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99178488"
---
# <a name="settransactionisolation-method-sqlserverconnection"></a>setTransactionIsolation メソッド (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) オブジェクトのトランザクション分離レベルについて、渡されたレベルへの変更を試行します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setTransactionIsolation(int level)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *level*  
  
 次のいずれかの分離レベルを含む **int** 値です。  
  
 TRANSACTION_READ_UNCOMMITTED  
  
 TRANSACTION_READ_COMMITTED  
  
 TRANSACTION_REPEATABLE_READ  
  
 TRANSACTION_SERIALIZABLE  
  
 TRANSACTION_SNAPSHOT = 0x1000  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この setTransactionIsolation メソッドは、java.sql.Connection インターフェイスの setTransactionIsolation メソッドによって指定されます。  
  
 トランザクションの実行中にこのメソッドが呼び出された場合、トランザクションはコミットされません。  
  
## <a name="see-also"></a>参照  
 [SQLServerConnection のメンバー](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection クラス](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
