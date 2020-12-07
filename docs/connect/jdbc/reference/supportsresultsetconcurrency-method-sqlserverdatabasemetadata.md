---
description: supportsResultSetConcurrency メソッド (SQLServerDatabaseMetaData)
title: supportsResultSetConcurrency メソッド (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsResultSetConcurrency
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8f7573b2-ac5c-4721-8a02-4b6cb60c74b2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f420aff2681495a8890a1c86841e124c73a98184
ms.sourcegitcommit: 80701484b8f404316d934ad2a85fd773e26ca30c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93243717"
---
# <a name="supportsresultsetconcurrency-method-sqlserverdatabasemetadata"></a>supportsResultSetConcurrency メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  データベースが、渡されたコンカレンシーの種類と結果セットの種類の組み合わせをサポートするかどうかを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean supportsResultSetConcurrency(int type,  
                                            int concurrency)  
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
  
 *concurrency*  
  
 結果セットのコンカレンシー レベルを示す **int** 。java.sql.ResultSet または SQLServerResultSet での定義に従って、次のいずれかの値を指定します。  
  
## <a name="concurrency-javasqlresultset-types"></a>コンカレンシー java.sql.ResultSet の種類  
 CONCUR_READ_ONLY  
  
 CONCUR_UPDATABLE  
  
## <a name="concurrency-sqlserverresultset-types"></a>コンカレンシーの SQLServerResultSet の種類  
 CONCUR_SS_OPTIMISTIC_CC  
  
 CONCUR_SS_SCROLL_LOCKS  
  
 CONCUR_SS_OPTIMISTIC_VAL  
  
## <a name="return-value"></a>戻り値  
 サポートされている場合は、 **true** です。 それ以外の場合は、 **false** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この supportsResultSetConcurrency メソッドは、java.sql.DatabaseMetaData インターフェイスの supportsResultSetConcurrency メソッドで指定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメソッド](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
