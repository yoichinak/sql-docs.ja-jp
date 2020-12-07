---
description: setFloat メソッド (SQLServerPreparedStatement)
title: setFloat メソッド (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setFloat
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 870d0031-6871-4dc0-b03a-fb0a9ff6ab98
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2a4ea923e29eeff00164e889320b1c32f4f1c028
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431804"
---
# <a name="setfloat-method-sqlserverpreparedstatement"></a>setFloat メソッド (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定されたパラメーターを、渡された **float** 値に設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final void setFloat(int n,  
                           float x)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *n*  
  
 パラメーターの番号を示す **int** です。  
  
 *x*  
  
 **float** 値。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この setFloat メソッドは、java.sql.PreparedStatement インターフェイスの setFloat メソッドで規定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerPreparedStatement のメンバー](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement クラス](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
