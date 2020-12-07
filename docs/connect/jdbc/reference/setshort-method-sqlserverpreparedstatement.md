---
description: setShort メソッド (SQLServerPreparedStatement)
title: setShort メソッド (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setShort
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6a9171a4-3e44-44ea-a453-23f57e5320e9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6caced92252eb8b9c4e9d50600df7846d44bd30e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458329"
---
# <a name="setshort-method-sqlserverpreparedstatement"></a>setShort メソッド (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定されたパラメーターを、渡された **short** 値に設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final void setShort(int index,  
                           short x)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *インデックス*  
  
 パラメーターの番号を示す **int** です。  
  
 *x*  
  
 **short** 値です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この setShort メソッドは、java.sql.PreparedStatement インターフェイスの setShort メソッドで規定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerPreparedStatement のメンバー](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement クラス](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
