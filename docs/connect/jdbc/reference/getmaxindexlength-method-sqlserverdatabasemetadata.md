---
description: getMaxIndexLength メソッド (SQLServerDatabaseMetaData)
title: getMaxIndexLength メソッド (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerDatabaseMetaData.getMaxIndexLength
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7c85d021-d466-4732-85f9-53903d297041
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2b6b66f9f8c9add68fa9e1f5f1869d84e805d477
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99175526"
---
# <a name="getmaxindexlength-method-sqlserverdatabasemetadata"></a>getMaxIndexLength メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  データベースで、インデックスのすべての部分を含めて、インデックスに許容される最大バイト数を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public int getMaxIndexLength()  
```  
  
## <a name="return-value"></a>戻り値  
 許容される最大バイト数を示す **int** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この getMaxIndexLength メソッドは、java.sql.DatabaseMetaData インターフェイスの getMaxIndexLength メソッドで指定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメソッド](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
