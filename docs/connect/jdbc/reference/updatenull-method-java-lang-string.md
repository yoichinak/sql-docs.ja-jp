---
description: updateNull (java.lang.String) メソッド
title: updateNull メソッド (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerResultSet.updateNull (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fb3e5cde-30e1-4c95-adf0-d5b6c1f0da95
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0d870050347ab6d0d83ef8b5c55ebd5b20524262
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99181625"
---
# <a name="updatenull-method-javalangstring"></a>updateNull (java.lang.String) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  渡された列名を使用して、指定された列を null 値で更新します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void updateNull(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *columnName*  
  
 列名を含む **文字列** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この updateNull メソッドは、java.sql.ResultSet インターフェイスの updateNull メソッドで規定されています。  
  
## <a name="see-also"></a>参照  
 [updateNull メソッド &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatenull-method-sqlserverresultset.md)   
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
