---
description: rowUpdated メソッド (SQLServerResultSet)
title: rowUpdated メソッド (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerResultSet.rowUpdated
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 29303550-294e-4d43-b892-312b42e21271
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c09a12aa4a9ceabf1f4b5d26fe017b709368acec
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99174159"
---
# <a name="rowupdated-method-sqlserverresultset"></a>rowUpdated メソッド (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  現在の行が更新されたかどうかを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean rowUpdated()  
```  
  
## <a name="return-value"></a>戻り値  
 所有者または別のユーザーによって行が明確に更新され、かつ更新が検出された場合は **true** です。 それ以外の場合は、 **false** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この rowUpdated メソッドは、java.sql.ResultSet インターフェイスの rowUpdated メソッドによって指定されます。  
  
 返される値は、結果セットが更新を検出できるかどうかによって異なります。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、どの種類のカーソルに対しても更新された行は検出されません。  
  
## <a name="see-also"></a>参照  
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
