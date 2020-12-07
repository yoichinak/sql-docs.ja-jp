---
description: SQLServerConnection のメンバー
title: SQLServerConnection のメンバー | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3115a533-756b-4c78-aee9-4ba7253c85e0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 75a3670a0f7e958f1976e387acdaa02a8449d202
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458284"
---
# <a name="sqlserverconnection-members"></a>SQLServerConnection のメンバー
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  次の表は、[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) クラスによって公開されるメンバーを示しています。  
  
## <a name="constructors"></a>コンストラクター  
 [なし] :  
  
## <a name="fields"></a>フィールド  
  
|名前|説明|  
|----------|-----------------|  
|[TRANSACTION_SNAPSHOT](../../../connect/jdbc/reference/transaction-snapshot-field-sqlserverconnection.md)|スナップショット トランザクションの分離レベルを指定する場合に使用します。|  
  
## <a name="inherited-fields"></a>継承されたフィールド  
  
|継承元のクラス|説明|  
|---------------------------|-----------------|  
|java.sql.Connection|TRANSACTION_NONE、TRANSACTION_READ_COMMITTED、TRANSACTION_READ_UNCOMMITTED、TRANSACTION_REPEATABLE_READ、TRANSACTION_SERIALIZABLE|  
  
## <a name="methods"></a>メソッド  
  
|名前|説明|  
|----------|-----------------|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverconnection.md)|[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) オブジェクトについて報告されたすべての警告をクリアします。|  
|[close](../../../connect/jdbc/reference/close-method-sqlserverconnection.md)|[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) オブジェクト用のデータベースと JDBC リソースを、自動的に解放されるまで待たずに直ちに解放します。|  
|[closeUnreferencedPreparedStatementHandles](../../../connect/jdbc/reference/closeunreferencedpreparedstatementhandles-method-sqlserverconnection.md)|破棄された未処理の準備されたステートメントに対して、実行されるように準備解除要求が強制的に実行されます。| 
|[commit](../../../connect/jdbc/reference/commit-method-sqlserverconnection.md)|前回のコミットまたはロールバック以降のすべての変更を永続的にして、[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) オブジェクトによって現在保持されているデータベース ロックをすべて解除します。|  
|[createBlob](../../../connect/jdbc/reference/createblob-method-sqlserverconnection.md)|データが含まれていない **java.sql.Blob** オブジェクトが作成されます。|  
|[createClob](../../../connect/jdbc/reference/createclob-method-sqlserverconnection.md)|データが含まれていない **java.sql.Clob** オブジェクトが作成されます。|  
|[createNClob](../../../connect/jdbc/reference/createnclob-method-sqlserverconnection.md)|データが含まれていない **java.sql.NClob** オブジェクトが作成されます。|  
|[createStatement](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)|SQL ステートメントをデータベースに送信するための [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトを作成します。|  
|[createSQLXML](../../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md)|データが含まれていない **java.sql.SQLXML** オブジェクトが作成されます。|  
|[getAutoCommit](../../../connect/jdbc/reference/getautocommit-method-sqlserverconnection.md)|[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) オブジェクトの現在の自動コミット モードを取得します。|  
|[getCatalog](../../../connect/jdbc/reference/getcatalog-method-sqlserverconnection.md)|[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) オブジェクトの現在のカタログ名を取得します。|  
|[getClientConnectionID メソッド &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/getclientconnectionid-method-sqlserverconnection.md)|接続に成功したか失敗したかにかかわらず、直近に試行された接続の ID を取得します。|  
|[getClientInfo](../../../connect/jdbc/reference/getclientinfo-method-sqlserverconnection.md)|JDBC ドライバーでサポートされているクライアント情報のプロパティに関する情報を取得します。|  
|[getDisableStatementPooling](../../../connect/jdbc/reference/getdisablestatementpooling-method-sqlserverconnection.md)|**disableStatementPooling** 接続プロパティの値が返されます。 この設定により、この接続に対してステートメント プーリングを有効にするかどうかを制御します。|
|[getDiscardedServerPreparedStatementCount](../../../connect/jdbc/reference/getdiscardedserverpreparedstatementcount-method-sqlserverconnection.md)|現在未処理の準備されたステートメントの unprepare アクションの数が返されます。|
|[getEnablePrepareOnFirstPreparedStatementCall](../../../connect/jdbc/reference/getenableprepareonfirstpreparedstatementcall-method-sqlserverconnection.md)|**enablePrepareOnFirstPreparedStatementCall** 接続プロパティの値が返されます。|
|[getHoldability](../../../connect/jdbc/reference/getholdability-method-sqlserverconnection.md)|[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) オブジェクトを使用して作成された [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の保持機能を取得します。|  
|[getMetaData](../../../connect/jdbc/reference/getmetadata-method-sqlserverconnection.md)|この [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) オブジェクトが表す接続の接続先データベースについてのメタデータを含む [SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) オブジェクトを取得します。|  
|[getServerPreparedStatementDiscardThreshold](../../../connect/jdbc/reference/getserverpreparedstatementdiscardthreshold-method-sqlserverconnection.md)|**serverPreparedStatementDiscardThreshold** 接続プロパティの値が返されます。|  
|[getStatementHandleCacheEntryCount](../../../connect/jdbc/reference/getstatementhandlecacheentrycount-method-sqlserverconnection.md)|プール済みの準備されたステートメントの現在のハンドル数が返されます。|  
|[getStatementPoolingCacheSize](../../../connect/jdbc/reference/getstatementpoolingcachesize-method-sqlserverconnection.md)|この接続のために準備されたステートメント キャッシュのサイズが返されます。|  
|[getTransactionIsolation](../../../connect/jdbc/reference/gettransactionisolation-method-sqlserverconnection.md)|[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) オブジェクトの現在のトランザクション分離レベルを取得します。|  
|[getTypeMap](../../../connect/jdbc/reference/gettypemap-method-sqlserverconnection.md)|[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) オブジェクトに関連付けられている Map オブジェクトを取得します。|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverconnection.md)|[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) オブジェクトでの呼び出しによって報告された最初の警告を取得します。|  
|[isClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverconnection.md)|[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) オブジェクトが閉じられているかどうかを示します。|  
|[isReadOnly](../../../connect/jdbc/reference/isreadonly-method-sqlserverconnection.md)|[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) オブジェクトが読み取り専用モードかどうかを示します。|  
|[isStatementPoolingEnabled](../../../connect/jdbc/reference/isstatementpoolingenabled-method-sqlserverconnection.md)|この接続に対してステートメント プーリングが有効であるかどうかが返されます。|  
|[isValid](../../../connect/jdbc/reference/isvalid-method-sqlserverconnection.md)|[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) オブジェクトが閉じられておらず、有効であるかどうかを示します。|  
|[nativeSQL](../../../connect/jdbc/reference/nativesql-method-sqlserverconnection.md)|渡された SQL ステートメントを、データベース サーバーのネイティブな SQL 文法に変換します。|  
|[prepareCall](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)|データベースのストアド プロシージャを呼び出すための [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) オブジェクトを作成します。|  
|[prepareStatement](../../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md)|パラメーター化された SQL ステートメントをデータベースに送信するための [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) オブジェクトを作成します。|  
|[releaseSavepoint](../../../connect/jdbc/reference/releasesavepoint-method-sqlserverconnection.md)|現在のトランザクションから、指定された [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) オブジェクトを削除します。|  
|[rollback](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md)|現在のトランザクションで行われた変更をすべて元に戻し、[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) オブジェクトによって現在保持されているデータベース ロックをすべて解除します。|  
|[setAutoCommit](../../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md)|[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) オブジェクトの自動コミット モードを、渡された状態に設定します。|  
|[setCatalog](../../../connect/jdbc/reference/setcatalog-method-sqlserverconnection.md)|指定されたカタログ名を設定し、[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) オブジェクトのデータベースの作業用サブスペースを選択します。|  
|[setClientInfo](../../../connect/jdbc/reference/setclientinfo-method-sqlserverconnection.md)|クライアント情報のプロパティの値を設定します。|  
|[setDisableStatementPooling](../../../connect/jdbc/reference/setdisablestatementpooling-method-sqlserverconnection.md)|ステートメント プーリングが true または false に設定されます。|  
|[setEnablePrepareOnFirstPreparedStatementCall](../../../connect/jdbc/reference/setenableprepareonfirstpreparedstatementcall-method-sqlserverconnection.md)|**enablePrepareOnFirstPreparedStatementCall** 接続プロパティの新しい値が指定されます。|  
|[setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md)|[SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) オブジェクトを使用して作成された [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの保持機能を、渡された保持機能に変更します。|  
|[setReadOnly](../../../connect/jdbc/reference/setreadonly-method-sqlserverconnection.md)|[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) オブジェクトを読み取り専用モードにして、データベースの最適化を有効にするヒントを JDBC ドライバーに提供します。|  
|[setSavepoint](../../../connect/jdbc/reference/setsavepoint-method-sqlserverconnection.md)|名前を割り当てられていないセーブポイントを現在のトランザクションに作成し、そのセーブポイントを表す新しい [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) オブジェクトを返します。|  
|[setServerPreparedStatementDiscardThreshold](../../../connect/jdbc/reference/setserverpreparedstatementdiscardthreshold-method-sqlserverconnection.md)|**serverPreparedStatementDiscardThreshold** 接続プロパティの新しい値が設定されます。|  
|[setStatementPoolingCacheSize](../../../connect/jdbc/reference/setstatementpoolingcachesize-method-sqlserverconnection.md)|この接続のために準備されたステートメント キャッシュのサイズが設定されます。|  
|[setTransactionIsolation](../../../connect/jdbc/reference/settransactionisolation-method-sqlserverconnection.md)|[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) オブジェクトのトランザクション分離レベルについて、渡されたレベルへの変更を試行します。|  
|[setTypeMap](../../../connect/jdbc/reference/settypemap-method-sqlserverconnection.md)|[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) オブジェクトの型マップとして、渡された TypeMap オブジェクトをインストールします。|  
  
## <a name="inherited-methods"></a>継承されたメソッド  
  
|継承元のクラス|メソッド|  
|---------------------------|-------------|  
|java.lang.Object|clone、equals、finalize、getClass、hashCode、notify、notifyAll、toString、wait|  
|java.lang.Wrapper|isWrapperFor、unwrap|  
  
## <a name="see-also"></a>参照  
 [SQLServerConnection クラス](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
