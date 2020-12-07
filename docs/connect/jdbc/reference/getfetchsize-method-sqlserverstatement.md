---
description: getFetchSize メソッド (SQLServerStatement)
title: getFetchSize メソッド (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getFetchSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8115ca58-8ae9-46ce-8515-7905d7bb25fe
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2f1f57da836e5ce4d0b31e3d4a8e5f4fe283b5ff
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88436014"
---
# <a name="getfetchsize-method-sqlserverstatement"></a>getFetchSize メソッド (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  結果セットの行数を取得します。この行数は、[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトから生成される結果セット オブジェクトの既定のフェッチ サイズとなります。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final int getFetchSize()  
```  
  
## <a name="return-value"></a>戻り値  
 [setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverstatement.md) メソッドによって指定されるフェッチ サイズを示す **int** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この getFetchSize メソッドは、java.sql.Statement インターフェイスの getFetchSize メソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerStatement のメンバー](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement クラス](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
