---
description: getClientConnectionID メソッド (SQLServerConnection)
title: getClientConnectionID メソッド (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: bee39c11-733a-461f-92cc-33efcb2af87d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 18bd2254052364c746ad88e972a57bdfc7bfbf5f
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725443"
---
# <a name="getclientconnectionid-method-sqlserverconnection"></a>getClientConnectionID メソッド (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  接続に成功したか失敗したかにかかわらず、直近に試行された接続の ID を取得します。  
  
## <a name="syntax"></a>構文  
  
``` 
public Java.util.UUID SQLServerConnection.getClientConnectionID();  
```  
  
## <a name="return-value"></a>戻り値  
 直近に試行された接続の ID を表す、16 バイトの GUID。 接続要求の開始後にエラーが発生し、ログイン前ハンドシェイクに失敗した場合は NULL。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 拡張イベント ログの診断情報へのアクセスの詳細については、「[拡張イベント ログの診断情報へのアクセス](../../../connect/jdbc/accessing-diagnostic-information-in-the-extended-events-log.md)」を参照してください。  
  
 次のサンプルは、接続 ID の取得方法を示しています。  
  
```  
Connection con = DriverManager.getConnection(connectionUrl);  
UUID id = ((ISQLServerConnection)con).getClientConnectionId();  
```  
  
 次のサンプルは、接続 ID を取得する別の方法を示しています。  
  
```  
SQLServerConnectionPoolDataSource ds = new SQLServerConnectionPoolDataSource();  
ds.setUser("...");  
ds.setPassword("...");  
ds.setServerName("...");  
PooledConnection pcon= ds.getPooledConnection();  
Connection cn = pcon.getConnection();  
UUID conid = ((ISQLServerConnection)cn).getClientConnectionId();  
```  
  
 **getClientConnectionID** は、接続先のサーバーのバージョンに関係なく使用できますが、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2008 R2 以前のサーバーの場合は、拡張イベント ログと、接続リング バッファー エラーに関するエントリが提供されません。  
  
 接続 ID のログ記録に関する拡張イベントが有効になっている場合は、拡張イベント ログ内で接続 ID を探し、エラーがサーバー上のものであるかどうかを確認できます。 また、一部の接続エラーについては、接続リング バッファー ([接続リング バッファーによる SQL Server 2008 での接続トラブルシューティング](/archive/blogs/sql_protocols/connectivity-troubleshooting-in-sql-server-2008-with-the-connectivity-ring-buffer)) 内で接続 ID を検索することもできます。 接続 ID が接続リング バッファー内にない場合は、ネットワーク エラーであると考えることができます。  
  
## <a name="see-also"></a>参照  
 [SQLServerConnection のメンバー](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection クラス](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
