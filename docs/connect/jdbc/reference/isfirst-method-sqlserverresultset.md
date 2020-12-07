---
description: isFirst メソッド (SQLServerResultSet)
title: isFirst メソッド (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.isFirst
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2ff94b95-32ad-4378-8bb1-970030527bb2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 05892bce86471733edca6a19a163603dc2a6bbce
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433574"
---
# <a name="isfirst-method-sqlserverresultset"></a>isFirst メソッド (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  カーソルが、この [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの先頭行にあるかどうかを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean isFirst()  
```  
  
## <a name="return-value"></a>戻り値  
 カーソルが最初の行にある場合は **true** です。 カーソルがそれ以外の位置にある場合、または結果セットに行が含まれていない場合は、**false** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この isFirst メソッドは、java.sql.ResultSet インターフェイスの isFirst メソッドで規定されています。  
  
 このメソッドを順方向カーソルおよび動的カーソルで使用すると、例外がスローされます。  
  
## <a name="see-also"></a>参照  
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
