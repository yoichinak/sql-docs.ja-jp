---
description: setDisableStatementPooling メソッド (SQLServerDataSource)
title: setDisableStatementPooling メソッド (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2aab090785dda921cb1061f5ab59e90136fc3b3d
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99173494"
---
# <a name="setdisablestatementpooling-method-sqlserverdatasource"></a>setDisableStatementPooling メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  **disableStatementPooling** 接続プロパティの値を設定します。 false の場合、0 より大きい statementPoolingCacheSize 値との結合でステートメント プールを使用できます。  

## <a name="syntax"></a>構文  
  
```
public void setDisableStatementPooling(boolean disableStatementPooling);  
```  
  
#### <a name="parameters"></a>パラメーター  
 *disableStatementPooling*  
  
 **disableStatementPooling** 接続プロパティの新しい値です。  

## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>解説  
 このメソッドは、JDBC ドライバー バージョン 6.4 以降で使用できます。
 
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
