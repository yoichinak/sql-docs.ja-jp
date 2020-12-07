---
description: SQLServerXADataSource のメンバー
title: SQLServerXADataSource のメンバー | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 04178645-915f-4569-8907-d45e299bbe7d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ed2d2515dc742eca0ece6036dbf0b06dd9a9530c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458204"
---
# <a name="sqlserverxadatasource-members"></a>SQLServerXADataSource のメンバー
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  次の表は、[SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md) クラスによって公開されるメンバーを示しています。  
  
## <a name="constructors"></a>コンストラクター  
  
|名前|説明|  
|----------|-----------------|  
|[SQLServerXADataSource ()](../../../connect/jdbc/reference/sqlserverxadatasource-constructor.md)|[SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md) クラスの新しいインスタンスを初期化します。|  
  
## <a name="fields"></a>フィールド  
 [なし] :  
  
## <a name="inherited-fields"></a>継承されたフィールド  
 [なし] :  
  
## <a name="methods"></a>メソッド  
  
|名前|説明|  
|----------|-----------------|  
|[getApplicationIntent](../../../connect/jdbc/reference/getapplicationintent-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) **applicationIntent** 接続プロパティの値が返されます。|  
|[getApplicationName](../../../connect/jdbc/reference/getapplicationname-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) アプリケーション名が返されます。|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) この DataSource オブジェクトが示すデータ ソースとの接続の確立が試みられます。|  
|[getDatabaseName](../../../connect/jdbc/reference/getdatabasename-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) データベース名が返されます。|  
|[getFailoverPartner](../../../connect/jdbc/reference/getfailoverpartner-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) データベース ミラーリング構成で使用されるフェールオーバー サーバーの名前が返されます。|  
|[getInstanceName](../../../connect/jdbc/reference/getinstancename-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス名が返されます。|  
|[getLastUpdateCount](../../../connect/jdbc/reference/getlastupdatecount-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) lastUpdateCount プロパティが有効であるかどうかを示す **Boolean** 値が返されます。|  
|[getLockTimeout](../../../connect/jdbc/reference/getlocktimeout-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) データベースがロック タイムアウトを通知するまでに待機する時間 (ミリ秒) を示す **int** 値が返されます。|  
|[getLoginTimeout](../../../connect/jdbc/reference/getlogintimeout-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) 接続の試行中にこの DataSource オブジェクトが待機する秒数が返されます。|  
|[getLogWriter](../../../connect/jdbc/reference/getlogwriter-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) すべてのログ メッセージとトレース メッセージで使用される文字出力ストリームが返されます。|  
|[getMultiSubnetFailover](../../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) **multiSubnetFailover** 接続プロパティの値が取得されます。|  
|[getPooledConnection](../../../connect/jdbc/reference/getpooledconnection-method-sqlserverconnectionpooldatasource.md)|([SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md) から継承されます) プールされた接続として使用できる物理データベース接続の確立が試みられます。|  
|[getPortNumber](../../../connect/jdbc/reference/getportnumber-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] との通信に使用される現在のポート番号が返されます。|  
|[getReference](../../../connect/jdbc/reference/getreference-method-sqlserverxadatasource.md)|この [SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md) オブジェクトへの参照が返されます。|  
|[getSelectMethod](../../../connect/jdbc/reference/getselectmethod-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) この DataSource オブジェクトを使用して作成されるすべての結果セットで使用される、既定のカーソルの種類が返されます。|  
|[getSendStringParametersAsUnicode](../../../connect/jdbc/reference/getsendstringparametersasunicode-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) サーバーへの**文字列**パラメーターの UNICODE 形式による送信が有効になっているかどうかを示す、**Boolean** 値が返されます。|  
|[getServerName](../../../connect/jdbc/reference/getservername-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を実行しているコンピューターの名前が返されます。|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) データ ソースへの接続に使用される URL が返されます。|  
|[getUser](../../../connect/jdbc/reference/getuser-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) データ ソースへの接続に使用されるユーザー名が返されます。|  
|[getWorkstationID](../../../connect/jdbc/reference/getworkstationid-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) データ ソースへの接続に使用されるクライアント コンピューターの名前が返されます。|  
|[getXAConnection](../../../connect/jdbc/reference/getxaconnection-method-sqlserverxadatasource.md)|分散トランザクションで使用できる物理データベース接続の確立を試みます。|  
|[getXopenStates](../../../connect/jdbc/reference/getxopenstates-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) XOPEN 互換の状態への SQL 状態の変換が有効になっているかどうかを示す **Boolean** 値が返されます。|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverxadatasource.md)|このオブジェクトが指定されたインターフェイスのラッパーであるかどうかを示します。|  
|[setApplicationIntent](../../../connect/jdbc/reference/setapplicationintent-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) **applicationIntent** 接続プロパティの値が設定されます。|  
|[setApplicationName](../../../connect/jdbc/reference/setapplicationname-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) アプリケーション名が設定されます。|  
|[setAuthenticationSceme](../../../connect/jdbc/reference/setauthenticationscheme-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) ご利用のアプリケーションで使用する統合セキュリティの種類が示されます。|  
|[setDatabaseName](../../../connect/jdbc/reference/setdatabasename-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) 接続するデータベース名が設定されます。|  
|[setDescription](../../../connect/jdbc/reference/setdescription-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) データ ソースの記述が設定されます。|  
|[setFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) データベース ミラーリング構成で使用されるフェールオーバー サーバーの名前が設定されます。|  
|[setInstanceName](../../../connect/jdbc/reference/setinstancename-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス名が設定されます。|  
|[setIntegratedSecurity](../../../connect/jdbc/reference/setintegratedsecurity-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) integratedSecurity プロパティが有効であるかどうかを示す **Boolean** 値が設定されます。|  
|[setLastUpdateCount](../../../connect/jdbc/reference/setlastupdatecount-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) lastUpdateCount プロパティが有効であるかどうかを示す **Boolean** 値が設定されます。|  
|[setLockTimeout](../../../connect/jdbc/reference/setlocktimeout-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) データベースがロック タイムアウトを通知するまでに待機する時間 (ミリ秒) を示す **int** 値が設定されます。|  
|[setLoginTimeout](../../../connect/jdbc/reference/setlogintimeout-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) 接続の試行中に DataSource オブジェクトが待機する秒数が設定されます。|  
|[setLogWriter](../../../connect/jdbc/reference/setlogwriter-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) すべてのログ メッセージとトレース メッセージで使用される文字出力ストリームが設定されます。|  
|[setMultiSubnetFailover](../../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) **multiSubnetFailover** 接続プロパティの値を設定します。|  
|[setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] への接続に使用されるパスワードが設定されます。|  
|[setPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] との通信に使用されるポート番号が設定されます。|  
|[setSelectMethod](../../../connect/jdbc/reference/setselectmethod-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) DataSource オブジェクトを使用して作成されるすべての結果セットで使用される、既定のカーソルの種類が設定されます。|  
|[setSendStringParametersAsUnicode](../../../connect/jdbc/reference/setsendstringparametersasunicode-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) サーバーへの**文字列**パラメーターの UNICODE 形式による送信が有効になっているかどうかを示す、**Boolean** 値が設定されます。|  
|[setServerName](../../../connect/jdbc/reference/setservername-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を実行しているコンピューターの名前が設定されます。|  
|[setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) データ ソースへの接続に使用される URL が設定されます。|  
|[setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) データ ソースへの接続に使用されるユーザー名が設定されます。|  
|[setWorkstationID](../../../connect/jdbc/reference/setworkstationid-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) データ ソースへの接続に使用されるクライアント コンピューターの名前が設定されます。|  
|[setXopenStates](../../../connect/jdbc/reference/setxopenstates-method-sqlserverdatasource.md)|([SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) から継承されます) XOPEN 互換の状態への SQL 状態の変換が有効になっているかどうかを示す **Boolean** 値が設定されます。|  
|[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md)|指定されたインターフェイスを実装するオブジェクトを返します。このメソッドから返されたオブジェクトを使用することで、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 固有のメソッドにアクセスできます。|  
  
## <a name="inherited-methods"></a>継承されたメソッド  
  
|継承元のクラス|メソッド|  
|---------------------------|-------------|  
|com.microsoft.sqlserver.jdbc.SQLServerConnectionPoolDataSource|getPooledConnection|  
|com.microsoft.sqlserver.jdbc.SQLServerDataSource|getApplicationName、getConnection、getDatabaseName、getDescription、getFailoverPartner、getInstanceName、getLastUpdateCount、getLockTimeout、getLoginTimeout、getLogWriter、getPortNumber、getSelectMethod、getSendStringParametersAsUnicode、getServerName、getURL、getUser、getWorkstationID、getXopenStates、setApplicationName、setDatabaseName、setDescription、setFailoverPartner、setInstanceName、setIntegratedSecurity、setLastUpdateCount、setLockTimeout、setLoginTimeout、setLogWriter、setPassword、setPortNumber、setSelectMethod、setSendStringParametersAsUnicode、setServerName、setURL、setUser、setWorkstationID、setXopenStates|  
|java.lang.Object|clone、equals、finalize、getClass、hashCode、notify、notifyAll、toString、wait|  
|java.sql.Wrapper|isWrapperFor、unwrap|  
|javax.sql.XADataSource|getLoginTimeout、getLogWriter、setLoginTimeout、setLogWriter|  
|javax.sql.ConnectionPoolDataSource|getLoginTimeout、getLogWriter、setLoginTimeout、setLogWriter|  
  
## <a name="see-also"></a>参照  
 [SQLServerXADataSource クラス](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)  
  
  
