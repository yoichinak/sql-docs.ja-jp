---
description: getTableName メソッド (SQLServerResultSetMetaData)
title: getTableName メソッド (SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerResultSetMetaData.getTableName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9a077b50-cc5a-4301-9398-49ea68544e89
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a8e97b0a43cdc9f8b25c3d0519da2bfb940b5c32
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99174873"
---
# <a name="gettablename-method-sqlserverresultsetmetadata"></a>getTableName メソッド (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定された列のテーブル名を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.lang.String getTableName(int column)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *column*  
  
 列インデックスを示す **int** です。  
  
## <a name="return-value"></a>戻り値  
 テーブル名を含む **文字列** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この getTableName メソッドは、java.sql.ResultSetMetaData インターフェイスの getTableName メソッドで規定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerResultSetMetaData メソッド](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData メンバー](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData クラス](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
