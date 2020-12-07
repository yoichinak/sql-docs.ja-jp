---
title: JDBC ドライバーの準備されたステートメント メタデータ キャッシュ
description: SQL Server 用 JDBC Driver では、準備されたステートメントをキャッシュし、データベース呼び出しを最小限に抑えることでパフォーマンスを改善します。その方法とその動作を制御する方法について説明します。
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 67b35e04ede8608d222c8fc31d89bfd01b093ba7
ms.sourcegitcommit: 129f8574eba201eb6ade1f1620c6b80dfe63b331
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/30/2020
ms.locfileid: "87435395"
---
# <a name="prepared-statement-metadata-caching-for-the-jdbc-driver"></a>JDBC ドライバーの準備されたステートメント メタデータ キャッシュ
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

この記事では、ドライバーのパフォーマンスを向上させるために実装された 2 つの変更について説明します。

## <a name="batching-of-unprepare-for-prepared-statements"></a>準備されたステートメントに対する準備解除のバッチ処理
バージョン 6.1.6 プレビュー以降、SQL Server へのサーバーのラウンド トリップを最小限に抑えることでパフォーマンスの改善が実装されました。 以前は、すべての prepareStatement クエリに対して、準備解除の呼び出しも送信されていました。 6.1.6 プレビュー以降、ドライバーは、しきい値 "ServerPreparedStatementDiscardThreshold" (既定値は 10) まで準備解除クエリをバッチ処理するようになりました。

> [!NOTE]  
>  ユーザーは、setServerPreparedStatementDiscardThreshold(整数値) メソッドを使用して、この既定値を変更できます。

6.1.6 プレビューから導入されたもう 1 つの変更は、それまでドライバーは常に sp_prepexec を呼び出していた点です。 ドライバーは、準備されたステートメントの最初の実行で sp_executesql を呼び出し、それ以降は sp_prepexec を実行して、ハンドルを割り当てるようになりました。 詳細については、[こちら](https://github.com/Microsoft/mssql-jdbc/wiki/PreparedStatement-metadata-caching)をご覧ください。

> [!NOTE]  
>  ユーザーは、setEnablePrepareOnFirstPreparedStatementCall(ブール値) メソッドを使用して enablePrepareOnFirstPreparedStatementCall を **true** に設定することにより、この既定の動作を、常に sp_prepexec を呼び出すという以前のバージョンの動作に変更することができます。

### <a name="list-of-the-new-apis-introduced-with-this-change-for-batching-of-unprepare-for-prepared-statements"></a>準備されたステートメントに対する準備解除をバッチ処理するためのこの変更で新しく導入された API の一覧

 **SQLServerConnection**
 
|新しいメソッド|説明|  
|-----------|-----------------|  
|int getDiscardedServerPreparedStatementCount()|現在未処理の準備されたステートメントの unprepare アクションの数が返されます。|
|void closeUnreferencedPreparedStatementHandles()|破棄された未処理の準備されたステートメントに対する準備解除要求を強制的に実行します。|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|特定の接続インスタンスの動作を返します。 false の場合、最初の実行で sp_executesql が呼び出され、ステートメントは準備されません。2 回目が実行されると、sp_prepexec が呼び出され、準備されたステートメントのハンドルが実際に設定されます。 以降の実行では、sp_execute が呼び出されます。 そのため、ステートメントの実行が 1 回のみの場合、準備されたステートメントを閉じるときに sp_unprepare を行う必要はなくなります。 このオプションの既定値は、setDefaultEnablePrepareOnFirstPreparedStatementCall() を呼び出して変更することができます。|
|void setEnablePrepareOnFirstPreparedStatementCall(boolean value)|特定の接続インスタンスの動作を指定します。 値が false の場合、最初の実行で sp_executesql が呼び出され、ステートメントは準備されません。2 回目が実行されると、sp_prepexec が呼び出され、準備されたステートメントのハンドルが実際に設定されます。 以降の実行では、sp_execute が呼び出されます。 そのため、ステートメントの実行が 1 回のみの場合、準備されたステートメントを閉じるときに sp_unprepare を行う必要はなくなります。|
|int getServerPreparedStatementDiscardThreshold()|特定の接続インスタンスの動作を返します。 この設定では、サーバー上の未処理のハンドルをクリーンアップする呼び出しが実行される前に 1 回の接続あたりに未処理にできる、未処理の準備されたステートメントの破棄アクション (sp_unprepare) の数を制御できます。 設定が 1 以下の場合、準備解除アクションは、準備されたステートメントの終了時に直ちに実行されます。 {@literal >} 1 に設定すると、これらの呼び出しはバッチ処理され、sp_unprepare が頻繁に呼び出されることによるオーバーヘッドを回避します。 このオプションの既定値は、getDefaultServerPreparedStatementDiscardThreshold() を呼び出して変更することができます。|
|void setServerPreparedStatementDiscardThreshold(int value)|特定の接続インスタンスの動作を指定します。 この設定では、サーバー上の未処理のハンドルをクリーンアップする呼び出しが実行される前に 1 回の接続あたりに未処理にできる、未処理の準備されたステートメントの破棄アクション (sp_unprepare) の数を制御できます。 設定が 1 以下の場合、準備解除アクションは、準備されたステートメントの終了時に直ちに実行されます。 1 より大きい値に設定すると、これらの呼び出しはバッチ処理され、sp_unprepare が頻繁に呼び出されることによるオーバーヘッドを回避します。|

 **SQLServerDataSource**
 
|新しいメソッド|説明|  
|-----------|-----------------|  
|void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall)|この構成が false の場合、準備されたステートメントの最初の実行で sp_executesql が呼び出され、ステートメントは準備されません。2 回目が実行されると、sp_prepexec が呼び出され、準備されたステートメント ハンドルが実際に設定されます。 以降の実行では、sp_execute が呼び出されます。 そのため、ステートメントの実行が 1 回のみの場合、準備されたステートメントを閉じるときに sp_unprepare を行う必要はなくなります。|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|この構成で false が返される場合、準備されたステートメントの最初の実行で sp_executesql が呼び出され、ステートメントは準備されません。2 回目が実行されると、sp_prepexec が呼び出され、準備されたステートメント ハンドルが実際に設定されます。 以降の実行では、sp_execute が呼び出されます。 そのため、ステートメントの実行が 1 回のみの場合、準備されたステートメントを閉じるときに sp_unprepare を行う必要はなくなります。|
|void setServerPreparedStatementDiscardThreshold(int serverPreparedStatementDiscardThreshold)|この設定では、サーバー上の未処理のハンドルをクリーンアップする呼び出しが実行される前に 1 回の接続あたりに未処理にできる、未処理の準備されたステートメントの破棄アクション (sp_unprepare) の数を制御できます。 設定が 1 以下の場合、準備解除アクションは、準備されたステートメントの終了時に直ちに実行されます。 {@literal >} 1 に設定すると、これらの呼び出しはバッチ処理され、sp_unprepare が頻繁に呼び出されることによるオーバーヘッドを回避します。|
|int getServerPreparedStatementDiscardThreshold()|この設定では、サーバー上の未処理のハンドルをクリーンアップする呼び出しが実行される前に 1 回の接続あたりに未処理にできる、未処理の準備されたステートメントの破棄アクション (sp_unprepare) の数を制御できます。 設定が 1 以下の場合、準備解除アクションは、準備されたステートメントの終了時に直ちに実行されます。 {@literal >} 1 に設定すると、これらの呼び出しはバッチ処理され、sp_unprepare が頻繁に呼び出されることによるオーバーヘッドを回避します。|

## <a name="prepared-statement-metadata-caching"></a>準備されたステートメントのメタデータ キャッシュ
6.3.0 プレビュー バージョン以降、SQL Server 用 Microsoft JDBC ドライバーは、準備されたステートメントのキャッシュをサポートします。 6.3.0 プレビュー以前は、既に準備され、キャッシュに格納されたクエリを実行すると、同じクエリを再度呼び出しても、準備は行われませんでした。 ドライバーは、キャッシュ内でクエリを検索し、ハンドルを見つけて、sp_execute でそれを実行するようになりました。
準備されたステートメント メタデータのキャッシュは、既定では**無効**に設定されます。 これを有効にするには、接続オブジェクトで次のメソッドを呼び出す必要があります。

`setStatementPoolingCacheSize(int value)   //value is the desired cache size (any value bigger than 0)`
`setDisableStatementPooling(boolean value) //false allows the caching to take place`

例: `connection.setStatementPoolingCacheSize(10)`
`connection.setDisableStatementPooling(false)`

### <a name="list-of-the-new-apis-introduced-with-this-change-for-prepared-statement-metadata-caching"></a>準備されたステートメント メタデータをキャッシュするためのこの変更で新しく導入された API の一覧

 **SQLServerConnection**
 
|新しいメソッド|説明|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean value)|ステートメント プーリングが true または false に設定されます。|
|boolean getDisableStatementPooling()|ステートメント プーリングが無効の場合、true を返します。|
|void setStatementPoolingCacheSize(int value)|この接続の準備されたステートメント キャッシュのサイズを指定します。 1 未満の値は、キャッシュしないことを意味します。|
|int getStatementPoolingCacheSize()|この接続のために準備されたステートメント キャッシュのサイズが返されます。 1 未満の値は、キャッシュしないことを意味します。|
|int getStatementHandleCacheEntryCount()|プール済みの準備されたステートメントの現在のハンドル数が返されます。|
|boolean isPreparedStatementCachingEnabled()|この接続に対してステートメント プーリングが有効であるかどうかを返します。|

 **SQLServerDataSource**
 
|新しいメソッド|説明|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean disableStatementPooling)|ステートメント プーリングを true または false に設定します。|
|boolean getDisableStatementPooling()|ステートメント プーリングが無効の場合、true を返します。|
|void setStatementPoolingCacheSize(int statementPoolingCacheSize)|この接続の準備されたステートメント キャッシュのサイズを指定します。 1 未満の値は、キャッシュしないことを意味します。|
|int getStatementPoolingCacheSize()|この接続のために準備されたステートメント キャッシュのサイズが返されます。 1 未満の値は、キャッシュしないことを意味します。|

## <a name="see-also"></a>関連項目  
 [JDBC ドライバーによるパフォーマンスと信頼性の強化](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
