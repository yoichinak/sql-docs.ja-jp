---
description: SQLServerXAConnection のメンバー
title: SQLServerXAConnection のメンバー | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4b61dabd-369b-460c-8450-9fe424f76541
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9b0c1f613cfa44859c51bf4429939e93c157d75a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462544"
---
# <a name="sqlserverxaconnection-members"></a>SQLServerXAConnection のメンバー
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  次の表は、[SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) クラスによって公開されるメンバーを示しています。  
  
## <a name="constructors"></a>コンストラクター  
 [なし] :  
  
## <a name="fields"></a>フィールド  
 [なし] :  
  
## <a name="inherited-fields"></a>継承されたフィールド  
 [なし] :  
  
## <a name="methods"></a>メソッド  
  
|名前|説明|  
|----------|-----------------|  
|[addConnectionEventListener](../../../connect/jdbc/reference/addconnectioneventlistener-method-sqlserverpooledconnection.md)|([SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md) から継承されます) Connection オブジェクトでイベントが発生した場合に通知を受けるように、渡されたイベント リスナーを登録します。|  
|[close](../../../connect/jdbc/reference/close-method-sqlserverpooledconnection.md)|([SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md) から継承されます) Connection オブジェクトが表す物理的な接続を終了します。|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverpooledconnection.md)|([SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md) から継承されます) Connection オブジェクトが表す物理的な接続用のオブジェクト ハンドルを作成します。|  
|[getXAResource](../../../connect/jdbc/reference/getxaresource-method-sqlserverxaconnection.md)|[SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) オブジェクトの分散トランザクションへの参加を管理するため、トランザクション マネージャーが使用する [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) オブジェクトを取得します。|  
|[removeConnectionEventListener](../../../connect/jdbc/reference/removeconnectioneventlistener-method-sqlserverpooledconnection.md)|([SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md) から継承されます) 渡されたイベント リスナーを削除します。|  
  
## <a name="inherited-methods"></a>継承されたメソッド  
  
|継承元のクラス|メソッド|  
|---------------------------|-------------|  
|com.microsoft.sqlserver.jdbc.SQLServerPooledConnection|addConnectionEventListener、close、getConnection、removeConnectionEventListener|  
|java.lang.Object|clone、equals、finalize、getClass、hashCode、notify、notifyAll、toString、wait|  
|javax.sql.PooledConnection|addConnectionEventListener、close、getConnection、removeConnectionEventListener|  
  
## <a name="see-also"></a>参照  
 [SQLServerXAConnection クラス](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)  
  
  
