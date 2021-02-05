---
description: setFetchDirection メソッド (SQLServerStatement)
title: setFetchDirection メソッド (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerStatement.setFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 18176517-2fb3-4266-924d-0f01253083d2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fb12ef2dda38efe87bf9db4785c864f1bc89443f
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99178945"
---
# <a name="setfetchdirection-method-sqlserverstatement"></a>setFetchDirection メソッド (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  結果セットの行を処理する方向についてのヒントを [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] に示します。  
  
> [!NOTE]  
>  JDBC ドライバーは、現在、このメソッドによって提供されるヒントを無視しています。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final void setFetchDirection(int nDir)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *nDir*  
  
 行を処理する方向を示す **int** です。次のいずれかの値を指定します。  
  
 FETCH_FORWARD  
  
 FETCH_REVERSE  
  
 FETCH_UNKNOWN  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この setFetchDirection メソッドは、java.sql.Statement インターフェイスの setFetchDirection メソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerStatement のメンバー](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement クラス](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
