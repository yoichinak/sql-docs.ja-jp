---
description: setLoginTimeout メソッド (SQLServerDataSource)
title: setLoginTimeout メソッド (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setLoginTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b63d1cf4-dc1b-4e35-9a56-50436642eaaf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6c3b162d7280b82e532a418be41011730684250a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431734"
---
# <a name="setlogintimeout-method-sqlserverdatasource"></a>setLoginTimeout メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  接続の試行中に [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) オブジェクトが待機する秒数を設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setLoginTimeout(int loginTimeout)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *loginTimeout*  
  
 待機する秒数を表す **int** 値です。 0 は、タイムアウトが既定のシステム タイムアウトであることを示します。既定のシステム タイムアウトは、既定では 15 秒に指定されています。  
  
## <a name="remarks"></a>解説  
 この setLoginTimeout メソッドは、javax.sql.DataSource インターフェイスの setLoginTimeout メソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
