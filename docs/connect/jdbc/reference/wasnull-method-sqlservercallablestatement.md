---
description: wasNull メソッド (SQLServerCallableStatement)
title: wasNull メソッド (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerCallableStatement.wasNull
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1a27b2fe-ae12-46a9-9bca-2c5ca66b9eb3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 517abf6fc57fa890b058f18300e4fc502aa270e4
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99181125"
---
# <a name="wasnull-method-sqlservercallablestatement"></a>wasNull メソッド (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  最後に読み取られた OUT パラメーターが SQL NULL かどうかを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean wasNull()  
```  
  
## <a name="return-value"></a>戻り値  
 最後に読み取られたパラメーターが null である場合は、**true** です。 それ以外の場合は、 **false** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 wasNull メソッドは、java.sql.CallableStatement インターフェイスの wasNull メソッドで規定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerCallableStatement のメンバー](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement クラス](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
