---
description: getArray (java.lang.String) メソッド
title: getArray メソッド (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerCallableStatement.getArray (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4610cbaf-5638-4a66-bd83-70aefca40e58
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1e32dbdbb73b58fdba28950b7c322a5eda7d9f55
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99168369"
---
# <a name="getarray-method-javalangstring"></a>getArray (java.lang.String) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  パラメーターに渡された名前を使用して、指定されたパラメーターの値を Array オブジェクトとして取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.sql.Array getArray(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *sCol*  
  
 パラメーターの名前を含む **文字列** です。  
  
## <a name="return-value"></a>戻り値  
 Array オブジェクトです。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この getArray メソッドは、java.sql.CallableStatement インターフェイスの getArray メソッドで指定されています。  
  
## <a name="see-also"></a>参照  
 [getArray メソッド &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getarray-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement のメンバー](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement クラス](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
