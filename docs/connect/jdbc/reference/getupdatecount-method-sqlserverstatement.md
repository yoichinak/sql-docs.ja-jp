---
description: getUpdateCount メソッド (SQLServerStatement)
title: getUpdateCount メソッド (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getUpdateCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e9570228-4500-44b6-b2f1-84ac050b5112
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19a4cfc7b9957d8ba4392477e6dcd3732f10bd7c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433904"
---
# <a name="getupdatecount-method-sqlserverstatement"></a>getUpdateCount メソッド (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  現在の結果を更新数として取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final int getUpdateCount()  
```  
  
## <a name="return-value"></a>戻り値  
 更新数を含む **int** です。 返された結果が結果セット オブジェクトである場合、または結果がなくなった場合は、-1 が返されます。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この getUpdateCount メソッドは、java.sql.Statement インターフェイスの getUpdateCount メソッドで指定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerStatement のメンバー](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement クラス](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
