---
description: getServerPreparedStatementDiscardThreshold メソッド (SQLServerDataSource)
title: getServerPreparedStatementDiscardThreshold メソッド (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e779955f77be3891bb3f7479b4a40fb30b3d56ac
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434544"
---
# <a name="getserverpreparedstatementdiscardthreshold-method-sqlserverdatasource"></a>getServerPreparedStatementDiscardThreshold メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  **serverPreparedStatementDiscardThreshold** 接続プロパティの値が返されます。 この設定では、サーバー上の未処理のハンドルをクリーンアップする呼び出しが実行される前に 1 回の接続あたりに未処理にできる、未処理の準備されたステートメントの破棄アクション (sp_unprepare) の数を制御できます。 設定が 1 以下の場合、準備解除アクションは、準備されたステートメントの終了時に直ちに実行されます。 この値を 1 より大きく設定した場合、これらの呼び出しは、sp_unprepare を頻繁に呼び出すことによるオーバーヘッドを回避するためにまとめてバッチ処理されます。

  
## <a name="syntax"></a>構文  
  
```
public int getServerPreparedStatementDiscardThreshold();  
```  
  
## <a name="return-value"></a>戻り値  
 **serverPreparedStatementDiscardThreshold** 接続プロパティの **int** 値が返されます。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>解説  
 このメソッドは、JDBC ドライバー バージョン 6.4 以降で使用できます。
 
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
