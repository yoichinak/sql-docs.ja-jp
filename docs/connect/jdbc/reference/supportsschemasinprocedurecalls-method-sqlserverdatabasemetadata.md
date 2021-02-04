---
description: supportsSchemasInProcedureCalls メソッド (SQLServerDatabaseMetaData)
title: supportsSchemasInProcedureCalls メソッド | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerDatabaseMetaData.supportsSchemasInProcedureCalls
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8955457a-b176-4674-9366-39a1942164a5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 760c3ab25277ca36dd46aeb53e5a4c189cbff26d
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99181402"
---
# <a name="supportsschemasinprocedurecalls-method-sqlserverdatabasemetadata"></a>supportsSchemasInProcedureCalls メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  プロシージャ呼び出しステートメントでスキーマ名を使用できるかどうかを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean supportsSchemasInProcedureCalls()  
```  
  
## <a name="return-value"></a>戻り値  
 サポートされている場合は、**true** です。 それ以外の場合は、 **false** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この supportsSchemasInProcedureCalls メソッドは、java.sql.DatabaseMetaData インターフェイスの supportsSchemasInProcedureCalls メソッドで指定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメソッド](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
