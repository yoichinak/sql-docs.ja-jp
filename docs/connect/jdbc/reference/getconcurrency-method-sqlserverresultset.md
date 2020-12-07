---
description: getConcurrency メソッド (SQLServerResultSet)
title: getConcurrency メソッド (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getConcurrency
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 207e25f4-769c-4ff3-913c-3517b06208e4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b8cb92a019c9c65e867be023fab9bc299a7a8bc8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88436554"
---
# <a name="getconcurrency-method-sqlserverresultset"></a>getConcurrency メソッド (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの同時実行モードを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public int getConcurrency()  
```  
  
## <a name="return-value"></a>戻り値  
 コンカレンシーの種類を示す **int** です。次のいずれかの値になります。  
  
 ResultSet.CONCUR_READ_ONLY  
  
 ResultSet.CONCUR_UPDATABLE  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この getConcurrency メソッドは、java.sql.ResultSet インターフェイスの getConcurrency メソッドによって指定されます。  
  
 使用されるコンカレンシーは、結果セットを作成した [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトによって決定されます。  
  
 このメソッドを使用すると、実際のコンカレンシーを確認できます。 アプリケーションが CONCUR_READ_ONLY または CONCUR_UPDATABLE を選択した場合は、これらが返されます。 アプリケーションが既定のコンカレンシーを使用した場合は、CONCUR_READ_ONLY が返されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
