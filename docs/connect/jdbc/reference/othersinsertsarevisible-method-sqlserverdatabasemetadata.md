---
description: othersInsertsAreVisible メソッド (SQLServerDatabaseMetaData)
title: othersInsertsAreVisible メソッド (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerDatabaseMetaData.othersInsertsAreVisible
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: aa32f059-bb59-47f8-bac1-292f314df730
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae7a993b02e49b5c8e9a4bdf74bd00a0afec9f65
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99174217"
---
# <a name="othersinsertsarevisible-method-sqlserverdatabasemetadata"></a>othersInsertsAreVisible メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  他で行われた挿入が可視かどうかを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean othersInsertsAreVisible(int type)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *type*  
  
 結果セットの種類を示す **int** です。java.sql.ResultSet または SQLServerResultSet での定義に従って、次のいずれかの値を指定できます。  
  
## <a name="javasqlresultset-types"></a>java.sql.ResultSet の種類  
 TYPE_FORWARD_ONLY  
  
 TYPE_SCROLL_SENSITIVE  
  
 TYPE_SCROLL_INSENSITIVE  
  
## <a name="sqlserverresultset-types"></a>SQLServerResultSet の種類  
 TYPE_SS_SCROLL_STATIC  
  
 TYPE_SS_SCROLL_KEYSET  
  
 TYPE_SS_DIRECT_FORWARD_ONLY  
  
 TYPE_SS_SERVER_CURSOR_FORWARD_ONLY  
  
 TYPE_SS_SCROLL_DYNAMIC  
  
## <a name="return-value"></a>戻り値  
 挿入が可視の場合は **true** です。 それ以外の場合は、 **false** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この othersInsertsAreVisible メソッドは、java.sql.DatabaseMetaData インターフェイスの othersInsertsAreVisible メソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメソッド](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
