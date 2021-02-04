---
description: getShort (java.lang.String) メソッド (SQLServerResultSet)
title: getShort (java.lang.String) メソッド (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerResultSet.getShort (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 183af414-b0a3-4ca7-b160-d199bcf469b0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c25233a2ab9bb029949e4ed3a0b1ca5279654c23
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99175039"
---
# <a name="getshort-method-javalangstring-sqlserverresultset"></a>getShort (java.lang.String) メソッド (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列名の値を、Java プログラミング言語の **short** として取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public short getShort(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *columnName*  
  
 列名を含む **文字列** です。  
  
## <a name="return-value"></a>戻り値  
 **short** 値です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この getShort メソッドは、java.sql.ResultSet インターフェイスの getShort メソッドで規定されています。  
  
 このメソッドは、smallint、tinyint、bit などの整数値を安全に返すことができる [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ型でのみサポートされます。 このメソッドを他のデータ型で使用すると、例外がスローされます。  
  
## <a name="see-also"></a>参照  
 [getShort メソッド &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getshort-method-sqlserverresultset.md)   
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
