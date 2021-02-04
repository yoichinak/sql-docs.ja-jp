---
description: getMaxStatements メソッド (SQLServerDatabaseMetaData)
title: getMaxStatements メソッド (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerDatabaseMetaData.getMaxStatements
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 71d58431-b671-49c5-939a-f581d1fef7cd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2ca07db52c71e12a1ffa3866b6b3cd05f55fceda
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99175504"
---
# <a name="getmaxstatements-method-sqlserverdatabasemetadata"></a>getMaxStatements メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  データベースの同時に開くことができるアクティブなステートメントの最大数を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public int getMaxStatements()  
```  
  
## <a name="return-value"></a>戻り値  
 許容されるアクティブなステートメントの最大数を示す **int** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この getMaxStatements メソッドは、java.sql.DatabaseMetaData インターフェイスの getMaxStatements メソッドで指定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメソッド](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
