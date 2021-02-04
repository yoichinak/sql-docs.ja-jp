---
description: getMaxColumnsInOrderBy メソッド (SQLServerDatabaseMetaData)
title: getMaxColumnsInOrderBy メソッド (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerDatabaseMetaData.getMaxColumnsInOrderBy
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d6af9bb4-c55d-41f4-a266-d10ebee61194
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6f07f16c948befa627f4d5bc72035fd062472a3c
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99175563"
---
# <a name="getmaxcolumnsinorderby-method-sqlserverdatabasemetadata"></a>getMaxColumnsInOrderBy メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  データベースで ORDER BY 句に許容される最大の列数を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public int getMaxColumnsInOrderBy()  
```  
  
## <a name="return-value"></a>戻り値  
 許容される最大の列数を示す **int** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この getMaxColumnsInOrderBy メソッドは、java.sql.DatabaseMetaData インターフェイスの getMaxColumnsInOrderBy メソッドで指定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメソッド](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
