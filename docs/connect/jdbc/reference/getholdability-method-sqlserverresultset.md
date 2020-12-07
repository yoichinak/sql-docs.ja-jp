---
description: getHoldability メソッド (SQLServerResultSet)
title: getHoldability メソッド (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4508d90f-c3c4-4eac-8001-fb0b93b66734
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fa94ee80f73dfcc21f519d62c4f29f2bda6b3eb2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435894"
---
# <a name="getholdability-method-sqlserverresultset"></a>getHoldability メソッド (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの保持機能を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public int getHoldability()  
```  
  
## <a name="return-value"></a>戻り値  
 次のいずれかの保持機能レベルを含む **int** 値です。  
  
 HOLD_CURSORS_OVER_COMMIT  
  
 CLOSE_CURSORS_AT_COMMIT  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この getHoldability メソッドは、java.sql.ResultSet インターフェイスの getHoldability メソッドで指定されています。  
  
 結果セットの保持機能を設定するには、アプリケーションで [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) クラスの [setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) メソッドを使用できます。 [setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) メソッドが呼び出され、ステートメント オブジェクトとその結果セット オブジェクトが作成され、ステートメントが実行された後、アプリケーションで保持機能をもう一度変更しなければならない場合があります。  
  
 サーバー側のカーソルについては、SQL Server 2005 以降に接続されている場合に、保持機能の設定が、その接続でこれから作成される新しい結果セットの保持機能にのみ影響を与えます。 ただし、SQL Server 2000 の場合は、保持機能の設定が、既存の結果セットとその接続でこれから作成される新しい結果セットの両方の保持機能に影響を与えます。  
  
 保持機能がリセットされ、getHoldability メソッドが以前に作成された結果セット オブジェクトで呼び出された場合、このメソッドによって返される値は、次のメソッドによって返される保持機能値と異なる可能性があります: Statement.getResultSetHoldability、Connection.getHoldability、または DatabaseMetaData.getResultSetHoldability。  
  
## <a name="see-also"></a>参照  
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
