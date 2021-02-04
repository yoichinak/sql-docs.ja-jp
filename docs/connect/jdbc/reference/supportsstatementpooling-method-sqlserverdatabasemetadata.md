---
description: supportsStatementPooling メソッド (SQLServerDatabaseMetaData)
title: supportsStatementPooling メソッド (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerDatabaseMetaData.supportsStatementPooling
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 83777807-5838-4f81-94ab-3ba4fc5aaa47
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 73cb80dfe29b04e034a1a4acb3441b892b194ba8
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99188672"
---
# <a name="supportsstatementpooling-method-sqlserverdatabasemetadata"></a>supportsStatementPooling メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  データベースがステートメントのプールをサポートするかどうかを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean supportsStatementPooling()  
```  
  
## <a name="return-value"></a>戻り値  
 サポートされている場合は、**true** です。 それ以外の場合は、 **false** です。  
  
## <a name="exceptions"></a>例外  
 java.sql.SQLException  
  
## <a name="remarks"></a>解説  
 この supportsStatementPooling メソッドは、java.sql.DatabaseMetaData interface インターフェイスの supportsStatementPooling method メソッドで指定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメソッド](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
