---
description: setFetchSize メソッド (SQLServerResultSet)
title: setFetchSize メソッド (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.setFetchSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 233bf4f8-4758-42d0-a80b-33e34fa78027
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d984004b4d306462e2c1345344ebc8072f775a82
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431864"
---
# <a name="setfetchsize-method-sqlserverresultset"></a>setFetchSize メソッド (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトにさらに行が必要な場合にデータベースからフェッチする必要がある行数について、JDBC ドライバーにヒントを示します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setFetchSize(int rows)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *rows*  
  
 フェッチする行数を示す **int** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この setFetchSize メソッドは、java.sql.ResultSet インターフェイスの setFetchSize メソッドによって指定されます。  
  
 指定されたフェッチ サイズが 0 の場合、JDBC ドライバーはこの値を無視し、必要となるフェッチ サイズを推測します。 既定値は、結果セットを作成した [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトによって設定されます。 フェッチ サイズはいつでも変更できます。  
  
 このメソッドは、サーバー カーソルのブロック フェッチ サイズを変更します。この効果は、次回 JDBC ドライバーで sp_cursorfetch の呼び出しが必要となったときに有効となります。 フェッチ サイズを 0 に設定すると、現在使用しているカーソルの種類の既定のフェッチ サイズが復元されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
