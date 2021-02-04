---
description: supportsTableCorrelationNames メソッド (SQLServerDatabaseMetaData)
title: supportsTableCorrelationNames メソッド (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerDatabaseMetaData.supportsTableCorrelationNames
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 85d4eb84-6d0a-4671-b6e5-a7085e086fcf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b9add281ebae028fce20b2f8e499652257ce82a5
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99189112"
---
# <a name="supportstablecorrelationnames-method-sqlserverdatabasemetadata"></a>supportsTableCorrelationNames メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  データベースがテーブルの相関名をサポートするかどうかを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean supportsTableCorrelationNames()  
```  
  
## <a name="return-value"></a>戻り値  
 サポートされている場合は、**true** です。 それ以外の場合は、 **false** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この supportsTableCorrelationNames メソッドは、java.sql.DatabaseMetaData インターフェイスの supportsTableCorrelationNames メソッドで指定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメソッド](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
