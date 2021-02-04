---
description: setHoldability メソッド (SQLServerConnection)
title: setHoldability メソッド (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerConnection.setHoldability
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 552eebd0-4c38-43f0-961f-35244f99109b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3f5b35e755449c61aa8e9b23bc05b1b71ab16318
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99173421"
---
# <a name="setholdability-method-sqlserverconnection"></a>setHoldability メソッド (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) オブジェクトを使用して作成された [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの保持機能を、渡された保持機能に変更します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setHoldability(int nNewHold)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *nNewHold*  
  
 次のいずれかの保持機能レベルを含む **int** 値です。  
  
 HOLD_CURSORS_OVER_COMMIT  
  
 CLOSE_CURSORS_AT_COMMIT  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この setHoldability メソッドは、java.sql.Connection インターフェイスの setHoldability メソッドで指定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerConnection のメンバー](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection クラス](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
