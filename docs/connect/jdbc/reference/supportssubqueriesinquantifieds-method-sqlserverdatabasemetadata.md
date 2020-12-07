---
description: supportsSubqueriesInQuantifieds メソッド (SQLServerDatabaseMetaData)
title: supportsSubqueriesInQuantifieds メソッド (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsSubqueriesInQuantifieds
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6749e14c-0f8a-4f1f-8583-dd5cc79b24fe
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d7c10719052590399c4716a7b38f85444da8b6c9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466974"
---
# <a name="supportssubqueriesinquantifieds-method-sqlserverdatabasemetadata"></a>supportsSubqueriesInQuantifieds メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  データベースが定量化された式でサブクエリをサポートするかどうかを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean supportsSubqueriesInQuantifieds()  
```  
  
## <a name="return-value"></a>戻り値  
 サポートされている場合は、**true** です。 それ以外の場合は、 **false**です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この supportsSubqueriesInQuantifieds メソッドは、java.sql.DatabaseMetaData インターフェイスの supportsSubqueriesInQuantifieds メソッドで指定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメソッド](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
