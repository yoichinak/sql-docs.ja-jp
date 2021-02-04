---
description: insertRow メソッド (SQLServerResultSet)
title: insertRow メソッド (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerResultSet.insertRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 363d1008-1396-4fc0-8e27-c9ba2499e7f1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c8571bb1e069be74de9ec93890606b887d247e5d
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99177518"
---
# <a name="insertrow-method-sqlserverresultset"></a>insertRow メソッド (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  挿入行の内容を [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトとデータベースに追加します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void insertRow()  
```  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この insertRow メソッドは、java.sql.ResultSet インターフェイスの insertRow メソッドで指定されています。  
  
 このメソッドを呼び出すときに、カーソルが挿入行にある必要があります。 このメソッドが呼び出された後も、カーソルは挿入行に残り、結果セットは挿入モードのままになります。  
  
## <a name="see-also"></a>参照  
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
