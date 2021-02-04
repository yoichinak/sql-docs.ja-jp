---
description: supportsDataManipulationTransactionsOnly メソッド (SQLServerDatabaseMetaData)
title: supportsDataManipulationTransactionsOnly メソッド | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerDatabaseMetaData.supportsDataManipulationTransactionsOnly
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bdc182db-4518-4bf2-b63a-05f58fdb4eb8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9ede24aa8886e3a95d343e9a96a8cb995d7cd34f
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99159101"
---
# <a name="supportsdatamanipulationtransactionsonly-method-sqlserverdatabasemetadata"></a>supportsDataManipulationTransactionsOnly メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  データベースがトランザクション内でデータ操作ステートメントのみをサポートするかどうかを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean supportsDataManipulationTransactionsOnly()  
```  
  
## <a name="return-value"></a>戻り値  
 サポートされている場合は、**true** です。 それ以外の場合は、 **false** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この supportsDataManipulationTransactionsOnly メソッドは、java.sql.DatabaseMetaData インターフェイスの supportsDataManipulationTransactionsOnly メソッドで規定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメソッド](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
