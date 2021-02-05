---
description: setFetchSize メソッド (SQLServerStatement)
title: setFetchSize メソッド (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerStatement.setFetchSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 760e555e-9667-4b40-b0ba-778026ff2923
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c66e978e0f1bc2233e2359a5fd92f4a94e96fbd4
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99178934"
---
# <a name="setfetchsize-method-sqlserverstatement"></a>setFetchSize メソッド (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  さらに行が必要な場合にデータベースからフェッチする必要がある行数について、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] にヒントを示します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final void setFetchSize(int rows)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *rows*  
  
 フェッチする行数を示す **int** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この setFetchSize メソッドは、java.sql.Statement インターフェイスの setFetchSize メソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerStatement のメンバー](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement クラス](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
