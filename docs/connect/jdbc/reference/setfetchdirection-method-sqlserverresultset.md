---
description: setFetchDirection メソッド (SQLServerResultSet)
title: setFetchDirection メソッド (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.setFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4ee82290-508d-4bff-a5c5-8a56338deef8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1056136ec3f7cef61e22c237d250fd6709c23e22
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431894"
---
# <a name="setfetchdirection-method-sqlserverresultset"></a>setFetchDirection メソッド (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの行を処理する方向についてのヒントを示します。  
  
> [!NOTE]  
>  このメソッドは、現在 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] ではサポートされていません。 このメソッドを使用すると、JDBC ドライバーに設定が保存されますが、現時点ではドライバーはその設定に従って動作しません。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setFetchDirection(int direction)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *direction*  
  
 推奨されるフェッチ方向を示す **int** です。 次の値のいずれかです。  
  
 ResultSet.FETCH_FORWARD  
  
 ResultSet.FETCH_REVERSE  
  
 ResultSet.FETCH_UNKNOWN  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この setFetchDirection メソッドは、java.sql.ResultSet インターフェイスの setFetchDirection メソッドによって指定されます。  
  
 このメソッドの初期値は、SQLServerResultSet オブジェクトを生成した [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトによって決定されます。 フェッチ方向はいつでも変更できます。  
  
> [!NOTE]  
>  カーソルの種類が順方向専用の場合にこのメソッドを使用しても、効果はありません。  
  
## <a name="see-also"></a>参照  
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
