---
description: getSQLStateType メソッド (SQLServerDatabaseMetaData)
title: getSQLStateType メソッド (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerDatabaseMetaData.getSQLStateType
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ee4d6751-68a3-4d04-831c-e6d704c59e63
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 33b0553b18dc09306e7d84effa30b81b20b84768
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99162280"
---
# <a name="getsqlstatetype-method-sqlserverdatabasemetadata"></a>getSQLStateType メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  SQLException.getSQLState メソッドによって返される SQLSTATE が、X/Open (現在は Open Group)、SQL CLI、SQL99 (JDBC 3.0)、SQL:2003 (JDBC 4.0) のいずれであるかを示します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public int getSQLStateType()  
```  
  
## <a name="return-value"></a>戻り値  
 SQLSTATE の種類を示す **int** です。次のいずれかの値になります。  
  
-   Java Runtime Environment バージョン 5.0 の場合: **xopenStates** 接続プロパティが **true** に設定されている場合、このメソッドは DatabaseMetaData.sqlStateXOpen を返します。 それ以外の場合は、DatabaseMetaData.sqlStateSQL99 になります。  
  
-   Java Runtime Environment バージョン 6.0 の場合: **xopenStates** 接続プロパティが **true** に設定されている場合、このメソッドは DatabaseMetaData.sqlStateXOpen を返します。 それ以外の場合は、DatabaseMetaData.sqlStateSQL になります。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この getSQLStateType メソッドは、java.sql.DatabaseMetaData インターフェイスの getSQLStateType メソッドで指定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメソッド](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
