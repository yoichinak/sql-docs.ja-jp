---
description: getGeneratedKeys メソッド (SQLServerStatement)
title: getGeneratedKeys メソッド (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerStatement.getGeneratedKeys
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a3325950-0e81-4ae8-aa0c-e1f6d371adcd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c55ef370ebc1413411dee4bfc951d6ce4c91cba6
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99175718"
---
# <a name="getgeneratedkeys-method-sqlserverstatement"></a>getGeneratedKeys メソッド (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトを実行した結果作成される自動生成キーを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final java.sql.ResultSet getGeneratedKeys()  
```  
  
## <a name="return-value"></a>戻り値  
 ResultSet オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この getGeneratedKeys メソッドは、java.sql.Statement インターフェイスの getGeneratedKeys メソッドで指定されています。  
  
 このメソッドの使用方法の詳細については、「[自動生成キーの使用](../../../connect/jdbc/using-auto-generated-keys.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQLServerStatement のメンバー](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement クラス](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
