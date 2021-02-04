---
description: getBigDecimal (java.lang.String, int) メソッド
title: getBigDecimal メソッド (java.lang.String, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerCallableStatement.getBigDecimal (java.lang.String, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6967ba55-9c9a-4f6f-a4d2-8ee9c9a82c14
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dd64f1f4856264e76ef17b717834a709a04dbcdb
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99165749"
---
# <a name="getbigdecimal-method-javalangstring-int"></a>getBigDecimal (java.lang.String, int) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  パラメーターに渡された名前と小数点以下桁数を使用して、指定されたパラメーターの値を java.math.BigDecimal として取得します。  
  
> [!NOTE]  
>  このメソッドは、JDBC 仕様では非推奨とされました。 代わりに、[getBigDecimal (java.lang.String)](../../../connect/jdbc/reference/getbigdecimal-method-java-lang-string.md) メソッドを使用してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.math.BigDecimal getBigDecimal(java.lang.String sCol,  
                                          int scale)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *sCol*  
  
 パラメーターの名前を含む **文字列** です。  
  
 *scale*  
  
 小数点以下の桁数を示す **int** です。  
  
## <a name="return-value"></a>戻り値  
 BigDecimal オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この getBigDecimal メソッドは、java.sql.CallableStatement インターフェイスの getBigDecimal メソッドで指定されています。  
  
## <a name="see-also"></a>参照  
 [getBigDecimal メソッド &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getbigdecimal-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement のメンバー](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement クラス](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
