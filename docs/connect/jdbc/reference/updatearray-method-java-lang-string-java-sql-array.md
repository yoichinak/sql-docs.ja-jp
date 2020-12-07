---
description: updateArray (java.lang.String, java.sql.Array) メソッド
title: updateArray メソッド (java.lang.String, java.sql.Array) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateArray (java.lang.String, java.sql.Array)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6f2ced5a-1c7d-439a-aaa5-472b9f4fdeab
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1b40ee796c388c19796761eae067132862fddeb0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458047"
---
# <a name="updatearray-method-javalangstring-javasqlarray"></a>updateArray (java.lang.String, java.sql.Array) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  渡された列名を使用して、指定された列を Array オブジェクトで更新します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void updateArray(java.lang.String columnName,  
                        java.sql.Array x)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *columnName*  
  
 列名を含む**文字列**です。  
  
 *x*  
  
 Array オブジェクトです。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この updateArray メソッドは、java.sql.ResultSet インターフェイスの updateArray メソッドで規定されています。  
  
## <a name="see-also"></a>参照  
 [updateArray メソッド &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatearray-method-sqlserverresultset.md)   
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
