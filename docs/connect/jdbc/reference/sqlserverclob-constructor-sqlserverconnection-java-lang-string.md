---
description: SQLServerClob (SQLServerConnection, java.lang.String) コンストラクター
title: SQLServerClob コンストラクター (SQLServerConnection, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerConnection.SQLServerClob (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7058f4f7-ef3e-4d62-90d1-79299708b1eb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1b682ecf3dfc85415d8ca505be95fc65856bb465
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99178366"
---
# <a name="sqlserverclob-constructor-sqlserverconnection-javalangstring"></a>SQLServerClob (SQLServerConnection, java.lang.String) コンストラクター
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) オブジェクトとデータの文字列が渡されたときに、[SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md) クラスの新しいインスタンスを初期化します。  
  
> [!NOTE]  
>  このメソッドは、JDBC Driver Version 2.0 では非推奨とされました。 代わりに、[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) クラスの [createClob](../../../connect/jdbc/reference/createclob-method-sqlserverconnection.md) メソッドを使用してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
public SQLServerClob(SQLServerConnection connection,  
                     java.lang.String data)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *connection*  
  
 SQLServerConnection オブジェクト。  
  
 *data*  
  
 CLOB データです。  
  
## <a name="see-also"></a>参照  
 [SQLServerClob のコンストラクター](../../../connect/jdbc/reference/sqlserverclob-constructors.md)   
 [SQLServerClob メンバー](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob クラス](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
