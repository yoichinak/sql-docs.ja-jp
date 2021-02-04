---
description: supportsNamedParameters メソッド (SQLServerDatabaseMetaData)
title: supportsNamedParameters メソッド (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerDatabaseMetaData.supportsNamedParameters
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 158be08f-387d-4c5b-b567-a1fe590d6f16
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2494fdccbcbeefa18eb5729604ba7361c9238751
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99167940"
---
# <a name="supportsnamedparameters-method-sqlserverdatabasemetadata"></a>supportsNamedParameters メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  データベースが呼び出し可能ステートメントで名前付きパラメーターをサポートするかどうかを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean supportsNamedParameters()  
```  
  
## <a name="return-value"></a>戻り値  
 サポートされている場合は、**true** です。 それ以外の場合は、 **false** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この supportsNamedParameters メソッドは、java.sql.DatabaseMetaData インターフェイスの supportsNamedParameters メソッドで規定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメソッド](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
