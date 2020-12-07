---
description: getType メソッド (SQLServerResultSet)
title: getType メソッド (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getType
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ffbc4a02-e851-431c-bc1a-7ab381d982bb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0c01dc19b6f9dfd1f1816c209f7c2168a68ceb85
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433964"
---
# <a name="gettype-method-sqlserverresultset"></a>getType メソッド (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトのカーソルの種類を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public int getType()  
```  
  
## <a name="return-value"></a>戻り値  
 現在のカーソルの種類を示す **int** です。次のいずれかの値になります。  
  
 ResultSet.TYPE_FORWARD_ONLY  
  
 ResultSet.TYPE_SCROLL_INSENSITIVE  
  
 ResultSet.TYPE_SCROLL_SENSITIVE  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この getType メソッドは、java.sql.ResultSet インターフェイスの getType メソッドで規定されています。  
  
 このメソッドを使用すると、実際のカーソルの種類を確認できます。 アプリケーションで TYPE_FORWARD_ONLY を選択した場合、または既定のカーソルの種類を使用した場合は、TYPE_FORWARD_ONLY が返されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
