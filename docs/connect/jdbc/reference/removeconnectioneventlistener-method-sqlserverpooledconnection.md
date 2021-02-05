---
description: removeConnectionEventListener メソッド (SQLServerPooledConnection)
title: removeConnectionEventListener メソッド (SQLServerPooledConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerPooledConnection.removeConnectionEventListener
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 46902e89-f512-40af-a2d9-a896f03d1200
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d2a145c8bc9ba4bd01dc837692a01908d4a75a15
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99176658"
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
  
  
