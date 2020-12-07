---
description: setDouble メソッド (SQLServerPreparedStatement)
title: setDouble メソッド (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setDouble
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 295c16b7-1532-40e1-93ef-64462a2c0ab6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f2f7b770e5bd8561990cf1e6b209d8d70fae5afc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431934"
---
# <a name="setdouble-method-sqlserverpreparedstatement"></a>setDouble メソッド (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定されたパラメーターを、渡された **double** 値に設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final void setDouble(int n,  
                            double x)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *n*  
  
 パラメーターの番号を示す **int** です。  
  
 *x*  
  
 **double** 値。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この setDouble メソッドは、java.sql.PreparedStatement インターフェイスの setDouble メソッドで指定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerPreparedStatement のメンバー](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement クラス](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
