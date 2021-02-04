---
description: setMaxFieldSize メソッド (SQLServerStatement)
title: setMaxFieldSize メソッド (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerStatement.setMaxFieldSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 38f7fc1d-acad-4d10-9fc8-3c0669d93b07
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a98cff7f25b30cc5bcb3cb22bd2aab342e790eac
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99173372"
---
# <a name="setmaxfieldsize-method-sqlserverstatement"></a>setMaxFieldSize メソッド (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  文字またはバイナリ値を格納する [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 列の最大バイト数の制限を、渡されたバイト数に設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final void setMaxFieldSize(int max)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *max*  
  
 最大バイト数を示す **int** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この setMaxFieldSize メソッドは、java.sql.Statement インターフェイスの setMaxFieldSize メソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerStatement のメンバー](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement クラス](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
