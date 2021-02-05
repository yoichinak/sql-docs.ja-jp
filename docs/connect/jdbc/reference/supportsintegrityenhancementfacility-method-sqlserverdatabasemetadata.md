---
description: supportsIntegrityEnhancementFacility メソッド (SQLServerDatabaseMetaData)
title: supportsIntegrityEnhancementFacility メソッド | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerDatabaseMetaData.supportsIntegrityEnhancementFacility
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: edee084b-9a8c-4167-9e13-66fc3ed1ecaa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3c7eab951eb1c4587f81ab8ed728954171f828d4
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99185550"
---
# <a name="supportsintegrityenhancementfacility-method-sqlserverdatabasemetadata"></a>supportsIntegrityEnhancementFacility メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  データベースが SQL Integrity Enhancement Facility をサポートするかどうかを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean supportsIntegrityEnhancementFacility()  
```  
  
## <a name="return-value"></a>戻り値  
 サポートされている場合は、**true** です。 それ以外の場合は、 **false** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この supportsIntegrityEnhancementFacility メソッドは、java.sql.DatabaseMetaData インターフェイスの supportsIntegrityEnhancementFacility メソッドで規定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメソッド](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
