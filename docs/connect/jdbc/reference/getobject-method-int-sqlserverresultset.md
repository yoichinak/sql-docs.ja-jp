---
description: getObject (int) メソッド (SQLServerResultSet)
title: getObject メソッド (int) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerResultSet.getObject (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 94e59366-ca34-4cd5-a6ec-ae32d475ef36
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e73ed303f034c7f46cfbca0f6f76b4b660d3835d
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99175372"
---
# <a name="getobject-method-int-sqlserverresultset"></a>getObject (int) メソッド (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列インデックスの値を、Java プログラミング言語のオブジェクトとして取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.lang.Object getObject(int columnIndex)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *columnIndex*  
  
 列インデックスを示す **int** です。  
  
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
  
  
