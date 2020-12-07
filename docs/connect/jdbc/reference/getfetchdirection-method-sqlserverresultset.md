---
description: getFetchDirection メソッド (SQLServerResultSet)
title: getFetchDirection メソッド (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5ab385c2-e18c-4b75-ac2d-2402af5c52a5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 50b0ec2751f2a6cabe852be3e8610b3a97328c13
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88436054"
---
# <a name="getfetchdirection-method-sqlserverresultset"></a>getFetchDirection メソッド (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトのフェッチ方向を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public int getFetchDirection()  
```  
  
## <a name="return-value"></a>戻り値  
 現在のフェッチ方向を示す **int** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この getFetchDirection メソッドは、java.sql.ResultSet インターフェイスの getFetchDirection メソッドによって指定されます。  
  
 このメソッドは、順方向専用カーソルの場合は FETCH_FORWARD を返し、他の種類のカーソルの場合は [setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverresultset.md) メソッドの呼び出しによって行われた直前の設定を返し、setFetchDirection メソッドが呼び出されていないときは FETCH_UNKNOWN を返します。  
  
## <a name="see-also"></a>参照  
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
