---
description: setEnablePrepareOnFirstPreparedStatementCall Method (SQLServerConnection)
title: setEnablePrepareOnFirstPreparedStatementCall メソッド (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerConnection.setEnablePrepareOnFirstPreparedStatementCall
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0c96860c17e56857171c3f69f15bdd0c966d1c84
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99178985"
---
# <a name="setenableprepareonfirstpreparedstatementcall-method-sqlserverconnection"></a>setEnablePrepareOnFirstPreparedStatementCall Method (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 特定の接続インスタンスの動作を指定します。 値が false の場合、最初の実行では sp_executesql が呼び出され、ステートメントは準備されません。2 回目が実行されると、sp_prepexec が呼び出され、準備されたステートメント ハンドルが実際に設定されます。 次の実行では sp_execute が呼び出されます。 そのため、ステートメントの実行が 1 回のみの場合、準備されたステートメントを閉じるときに sp_unprepare を行う必要はなくなります。

## <a name="syntax"></a>構文  
  
```  
  
public void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *enablePrepareOnFirstPreparedStatementCall*  
  
 **enablePrepareOnFirstPreparedStatementCall** 接続プロパティの新しい値。  
 
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>解説  
 このメソッドは、JDBC ドライバー バージョン 6.4 以降で使用できます。
 
## <a name="see-also"></a>参照  
 [SQLServerConnection のメンバー](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection クラス](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
