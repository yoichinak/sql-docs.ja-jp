---
description: getObject (java.lang.String) メソッド (SQLServerResultSet)
title: getObject (java.lang.String) メソッド (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getObject (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 59a975e8-bea8-42fe-8f34-5f18f2bbd415
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b0ec424269200feb0325449953eec91917ff5a70
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435104"
---
# <a name="getobject-method-javalangstring-sqlserverresultset"></a>getObject (java.lang.String) メソッド (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  この [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列名の値を、Java プログラミング言語のオブジェクトとして取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.lang.Object getObject(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *columnName*  
  
 列名を含む**文字列**です。  
  
## <a name="return-value"></a>戻り値  
 **Object** 値。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この getObject メソッドは、java.sql.ResultSet インターフェイスの getObject メソッドで規定されています。  
  
 このメソッドは、指定された列の値を Java オブジェクトとして返します。 この Java オブジェクトの型は、JDBC 仕様に指定されている組み込み型のマッピングに基づく、列の SQL 型に対応する既定の Java オブジェクト型です。 値が SQL NULL の場合、ドライバーは Java の null を返します。  
  
 このメソッドは、データベース固有の抽象データ型を読み取る場合にも使用できます。 JDBC 2.0 API では、SQL のユーザー定義型のデータを具体化するよう、getObject メソッドの動作が拡張されています。 列に構造化された値または個別の値が含まれている場合、このメソッドの動作は `getObject(columnIndex, this.getStatement().getConnection().getTypeMap())` を呼び出した場合と同様です。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 以降:  
  
-   date 型の値は java.sql.Date オブジェクトとして返されます。  
  
-   time 型の値は java.sql.Time オブジェクトとして返されます。  
  
-   datetime2 型の値は java.sql.Timestamp オブジェクトとして返されます。  
  
-   datetimeoffset 型の値は microsoft.sql.DateTimeOffset オブジェクトとして返されます。  
  
## <a name="see-also"></a>参照  
 [getObject メソッド &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getobject-method-sqlserverresultset.md)   
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
