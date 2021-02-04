---
description: getServerPreparedStatementDiscardThreshold メソッド (SQLServerConnection)
title: getServerPreparedStatementDiscardThreshold メソッド (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerConnection.getServerPreparedStatementDiscardThreshold
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ce985283a033c7942b2bca1cb7475a5b1813bcd0
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99175023"
---
# <a name="getserverpreparedstatementdiscardthreshold-method-sqlserverconnection"></a>getServerPreparedStatementDiscardThreshold メソッド (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 **serverPreparedStatementDiscardThreshold** 接続プロパティの値が返されます。 この設定では、サーバー上の未処理のハンドルをクリーンアップする呼び出しが実行される前に 1 回の接続あたりに未処理にできる、未処理の準備されたステートメントの破棄アクション (sp_unprepare) の数を制御できます。 設定が 1 以下の場合、準備解除アクションは、準備されたステートメントの終了時に直ちに実行されます。 1 より大きく設定した場合、これらの呼び出しは、sp_unprepare を頻繁に呼び出すことによるオーバーヘッドを回避するためにまとめてバッチ処理されます。 このオプションの既定値は、getDefaultServerPreparedStatementDiscardThreshold() を呼び出して変更することができます。

## <a name="syntax"></a>構文  
  
```  
  
public int getServerPreparedStatementDiscardThreshold()  
```  

## <a name="return-value"></a>戻り値
 **serverPreparedStatementDiscardThreshold** 接続プロパティの値を含む **int** です。

## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>解説  
 このメソッドは、JDBC ドライバー バージョン 6.4 以降で使用できます。
 
## <a name="see-also"></a>参照  
 [SQLServerConnection のメンバー](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection クラス](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
