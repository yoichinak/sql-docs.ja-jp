---
description: removeConnectionEventListener メソッド (SQLServerPooledConnection)
title: removeConnectionEventListener メソッド (SQLServerPooledConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPooledConnection.removeConnectionEventListener
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 46902e89-f512-40af-a2d9-a896f03d1200
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ba6472207d42379a3c1d5fe04f4313db986ab0d2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88432744"
---
# <a name="removeconnectioneventlistener-method-sqlserverpooledconnection"></a>removeConnectionEventListener メソッド (SQLServerPooledConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  渡されたイベント リスナーを削除します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void removeConnectionEventListener(javax.sql.ConnectionEventListener listener)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *listener*  
  
 ConnectionEventListener オブジェクトです。  
  
## <a name="remarks"></a>解説  
 この removeConnectionEventListener メソッドは、javax.sql.PooledConnection インターフェイスの removeConnectionEventListener メソッドで規定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerPooledConnection のメソッド](../../../connect/jdbc/reference/sqlserverpooledconnection-methods.md)   
 [SQLServerPooledConnection のメンバー](../../../connect/jdbc/reference/sqlserverpooledconnection-members.md)   
 [SQLServerPooledConnection クラス](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)  
  
  
