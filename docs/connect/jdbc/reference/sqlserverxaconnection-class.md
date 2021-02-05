---
description: SQLServerXAConnection クラス
title: SQLServerXAConnection クラス | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.assetid: 5ecb4bf1-b8d1-47cf-9cb1-7a18acc11ce2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 13d2ad39b4259d514c099e221961132336d152aa
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99179976"
---
# <a name="sqlserverxaconnection-class"></a>SQLServerXAConnection クラス
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  分散 (XA) トランザクションに参加できる JDBC 接続を表します。  
  
 **パッケージ:** com.microsoft.sqlserver.jdbc  
  
 **拡張:** [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)  
  
 **実装:** javax.sql.XAConnection  
  
## <a name="syntax"></a>構文  
  
```  
  
public class SQLServerXAConnection  
```  
  
## <a name="remarks"></a>解説  
 SQLServerXAConnection オブジェクトは、[SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) オブジェクトを使用して分散トランザクションに参加させることができます。 トランザクション マネージャー (通常は中間層サーバーの一部) では、SQLServerXAResource オブジェクトを使用して SQLServerXAConnection オブジェクトが管理されます。  
  
> [!NOTE]  
>  通常、アプリケーション プログラマがこのインターフェイスを直接使用することはありません。 このインターフェイスは主に、中間層サーバーで動作しているトランザクション マネージャーによって使用されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerXAConnection のメンバー](../../../connect/jdbc/reference/sqlserverxaconnection-members.md)   
 [JDBC Driver API リファレンス](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
