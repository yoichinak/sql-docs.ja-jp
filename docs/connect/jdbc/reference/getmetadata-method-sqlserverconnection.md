---
description: getMetaData メソッド (SQLServerConnection)
title: getMetaData メソッド (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerConnection.getMetaData
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 86223cb5-3bf4-489a-8c82-669a91764f2b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0480d1852c55806f09391be330d9c286f40a3389
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99175502"
---
# <a name="getmetadata-method-sqlserverconnection"></a>getMetaData メソッド (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  この [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) オブジェクトが表す接続の接続先データベースについてのメタデータを含む [SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) オブジェクトを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.sql.DatabaseMetaData getMetaData()  
```  
  
## <a name="return-value"></a>戻り値  
 DatabaseMetaData オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この getMetaData メソッドは、java.sql.Connection インターフェイスの getMetaData メソッドで規定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerConnection のメンバー](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection クラス](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
