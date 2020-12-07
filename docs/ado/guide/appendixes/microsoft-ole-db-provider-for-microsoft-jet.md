---
description: Microsoft OLE DB Provider for Microsoft Jet の概要
title: Microsoft OLE DB Provider for Microsoft Jet |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Jet provider for OLE DB [ADO]
- providers [ADO], OLE DB provider for Microsoft Jet
- OLE DB provider for Microsoft Jet [ADO]
ms.assetid: fd956da1-5203-40af-aa7e-fc13a6c6581f
author: rothja
ms.author: jroth
ms.openlocfilehash: bc04cce33d3a1170c01b604ef8b71ef82bc98fe2
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991033"
---
# <a name="microsoft-ole-db-provider-for-microsoft-jet-overview"></a>Microsoft OLE DB Provider for Microsoft Jet の概要
Microsoft Jet の OLE DB プロバイダーにより、ADO は Microsoft Jet データベースにアクセスできます。

## <a name="connection-string-parameters"></a>接続文字列パラメーター
 このプロバイダーに接続するには、 [ConnectionString](../../reference/ado-api/connectionstring-property-ado.md)プロパティの*provider*引数を次のプロパティに設定します。

```vb
Microsoft.Jet.OLEDB.4.0
```

 [プロバイダー](../../reference/ado-api/provider-property-ado.md)プロパティを読み取ると、この文字列も返されます。

## <a name="typical-connection-string"></a>一般的な接続文字列
 このプロバイダーの一般的な接続文字列は次のとおりです。

```vb
"Provider=Microsoft.Jet.OLEDB.4.0;Data Source=databaseName;User ID=MyUserID;Password=MyPassword;"
```

 文字列は、次のキーワードで構成されています。

|キーワード|説明|
|-------------|-----------------|
|**プロバイダー**|Microsoft Jet の OLE DB プロバイダーを指定します。|
|**データ ソース**|データベースパスとファイル名 (など) を指定し `c:\Northwind.mdb` ます。|
|**[ユーザー ID]**|ユーザー名を指定します。 このキーワードが指定されていない場合、 `admin` 既定では "" という文字列が使用されます。|
|**パスワード**|ユーザーのパスワードを指定します。 このキーワードが指定されていない場合、既定では空の文字列 ("") が使用されます。|

> [!NOTE]
>  Windows 認証をサポートするデータソースプロバイダーに接続する場合は、接続文字列にユーザー ID とパスワードの情報ではなく、 **Trusted_Connection = yes** または **INTEGRATED Security = SSPI** を指定する必要があります。

## <a name="provider-specific-connection-parameters"></a>プロバイダー固有の接続パラメーター
 OLE DB Provider for Microsoft Jet では、ADO によって定義されているものに加えて、いくつかのプロバイダー固有の動的プロパティがサポートされています。 他のすべての **接続** パラメーターと同様に、接続オブジェクトの **Properties** コレクションまた **は接続文字列** の一部として設定できます。

 次の表は、これらのプロパティと、対応する OLE DB プロパティ名をかっこで示しています。

|パラメーター|説明|
|---------------|-----------------|
|Jet OLEDB: コンパクトに回収した領域の量 (DBPROP_JETOLEDB_COMPACTFREESPACESIZE)|データベースを圧縮することによって再利用できる領域の容量をバイト単位で示します。 この値は、データベース接続が確立された後にのみ有効です。|
|Jet OLEDB: 接続制御 (DBPROP_JETOLEDB_CONNECTIONCONTROL)|ユーザーがデータベースに接続できるかどうかを示します。|
|Jet OLEDB: システムデータベースの作成 (DBPROP_JETOLEDB_CREATESYSTEMDATABASE)|新しいデータソースの作成時にシステムデータベースを作成するかどうかを示します。|
|Jet OLEDB: データベースロックモード (DBPROP_JETOLEDB_DATABASELOCKMODE)|このデータベースのロックモードを示します。 データベースを開く最初のユーザーは、データベースを開いているときに使用されるモードを決定します。|
|Jet OLEDB: データベースパスワード (DBPROP_JETOLEDB_DATABASEPASSWORD)|データベースのパスワードを示します。|
|Jet OLEDB: Compact でロケールをコピーしない (DBPROP_JETOLEDB_COMPACT_DONTCOPYLOCALE)|データベースの圧縮時に Jet がロケール情報をコピーする必要があるかどうかを示します。|
|Jet OLEDB: Encrypt Database (DBPROP_JETOLEDB_ENCRYPTDATABASE)|圧縮されたデータベースを暗号化する必要があるかどうかを示します。 このプロパティが設定されていない場合、元のデータベースも暗号化されている場合は、圧縮されたデータベースが暗号化されます。|
|Jet OLEDB: エンジンの種類 (DBPROP_JETOLEDB_ENGINE)|現在のデータストアにアクセスするために使用するストレージエンジンを示します。|
|Jet OLEDB: 排他的な非同期遅延 (DBPROP_JETOLEDB_EXCLUSIVEASYNCDELAY)|データベースを排他的に開いたときに、Jet がディスクへの非同期書き込みを遅延する最大時間 (ミリ秒単位) を示します。<br /><br /> このプロパティは、 **JET OLEDB: Flush Transaction Timeout** が0に設定されている場合を除き、無視されます。|
|Jet OLEDB: Flush Transaction Timeout (DBPROP_JETOLEDB_FLUSHTRANSACTIONTIMEOUT)|非同期書き込みのためにキャッシュに格納されたデータがディスクに書き込まれるまでの待機時間を示します。 この設定は、 **JET oledb: Shared Async delay** および **Jet Oledb: Exclusive async delay**の値よりも優先されます。|
|Jet OLEDB: グローバル一括トランザクション (DBPROP_JETOLEDB_GLOBALBULKNOTRANSACTIONS)|SQL 一括トランザクションがトランザクション処理されるかどうかを示します。|
|Jet OLEDB: グローバル部分一括操作 (DBPROP_JETOLEDB_GLOBALBULKPARTIAL)|データベースを開くために使用するパスワードを示します。|
|Jet OLEDB: 暗黙のコミット同期 (DBPROP_JETOLEDB_IMPLICITCOMMITSYNC)|内部の暗黙のトランザクションで行われた変更が、同期モードと非同期モードのどちらで作成されたかを示します。|
|Jet OLEDB: ロック遅延 (DBPROP_JETOLEDB_LOCKDELAY)|前回の試行が失敗した後にロックを取得しようとするまでの待機時間をミリ秒単位で示します。|
|Jet OLEDB: ロックの再試行 (DBPROP_JETOLEDB_LOCKRETRY)|ロックされたページにアクセスしようとした回数を示します。|
|Jet OLEDB: Max Buffer Size (DBPROP_JETOLEDB_MAXBUFFERSIZE)|ディスクへの変更のフラッシュを開始する前に Jet が使用できる最大メモリ量 (kb 単位) を示します。|
|Jet OLEDB: 1 ファイルあたりの最大ロック数 (DBPROP_JETOLEDB_MAXLOCKSPERFILE)|Jet がデータベースに配置できるロックの最大数を示します。 既定値は9500です。|
|Jet OLEDB: 新しいデータベースパスワード (DBPROP_JETOLEDB_NEWDATABASEPASSWORD)|このデータベースに対して設定される新しいパスワードを示します。 古いパスワードは、 **JET OLEDB: Database password**に格納されています。|
|Jet OLEDB: ODBC コマンドのタイムアウト (DBPROP_JETOLEDB_ODBCCOMMANDTIMEOUT)|Jet からのリモート ODBC クエリがタイムアウトするまでのミリ秒数を示します。|
|Jet OLEDB: テーブルロックへのページロック (DBPROP_JETOLEDB_PAGELOCKSTOTABLELOCK)|Jet がロックをテーブルロックに昇格させようとする前に、トランザクション内でロックする必要があるページ数を示します。 この値が0の場合、ロックは昇格されません。|
|Jet OLEDB: ページタイムアウト (DBPROP_JETOLEDB_PAGETIMEOUT)|データベースファイルでキャッシュが古くなっているかどうかを確認する前に Jet が待機するミリ秒数を示します。|
|Jet OLEDB: 長い値ページのリサイクル (DBPROP_JETOLEDB_RECYCLELONGVALUEPAGES)|Jet が解放されたときに BLOB ページを積極的に再利用する必要があるかどうかを示します。|
|Jet OLEDB: レジストリパス (DBPROP_JETOLEDB_REGPATH)|Jet データベースエンジンの値を含む Windows レジストリキーを示します。|
|Jet OLEDB: ISAM の統計をリセットする (DBPROP_JETOLEDB_RESETISAMSTATS)|パフォーマンス情報を返した後に、スキーマ **レコードセット** DBSCHEMA_JETOLEDB_ISAMSTATS がパフォーマンスカウンターをリセットするかどうかを示します。|
|Jet OLEDB: Shared Async Delay (DBPROP_JETOLEDB_SHAREDASYNCDELAY)|データベースがマルチユーザーモードで開かれた場合に、Jet がディスクへの非同期書き込みを遅延する最大時間をミリ秒単位で示します。|
|Jet OLEDB: システムデータベース (DBPROP_JETOLEDB_SYSDBPATH)|ワークグループ情報ファイル (システムデータベース) のパスとファイル名を示します。|
|Jet OLEDB: トランザクションコミットモード (DBPROP_JETOLEDB_TXNCOMMITMODE)|トランザクションがコミットされたときに、Jet がデータを同期的にまたは非同期的に書き込むかどうかを示します。|
|Jet OLEDB: User Commit Sync (DBPROP_JETOLEDB_USERCOMMITSYNC)|トランザクションで行われた変更を同期モードまたは非同期モードのどちらで作成するかを示します。|

## <a name="provider-specific-recordset-and-command-properties"></a>プロバイダー固有のレコードセットとコマンドのプロパティ
 Jet プロバイダーでは、いくつかのプロバイダー固有の **レコードセット** と **コマンド** プロパティもサポートされています。 これらのプロパティにアクセスして設定するには、**レコードセット**または**コマンド**オブジェクトの**properties**コレクションを使用します。 このテーブルには、ADO プロパティ名とそれに対応する OLE DB プロパティ名がかっこで囲まれて表示されます。

|プロパティ名|説明|
|-------------------|-----------------|
|Jet OLEDB: 一括トランザクション (DBPROP_JETOLEDB_BULKNOTRANSACTIONS)|SQL 一括操作がトランザクション処理されるかどうかを示します。 大量の一括操作は、リソースの遅延のため、トランザクション処理時に失敗する可能性があります。|
|Jet OLEDB: Fat カーソルを有効にする (DBPROP_JETOLEDB_ENABLEFATCURSOR)|リモート行ソースのレコードセットを作成するときに Jet が複数の行をキャッシュするかどうかを示します。|
|Jet OLEDB: Fat カーソルキャッシュサイズ (DBPROP_JETOLEDB_FATCURSORMAXROWS)|リモートデータストアの行キャッシュを使用しているときにキャッシュする行の数を示します。 **JET OLEDB: Enable Fat カーソル**が True の場合を除き、この値は無視されます。|
|Jet OLEDB: 一貫性がありません (DBPROP_JETOLEDB_INCONSISTENT)|クエリ結果が不整合な更新を許可するかどうかを示します。|
|Jet OLEDB: ロックの粒度 (DBPROP_JETOLEDB_LOCKGRANULARITY)|行レベルのロックを使用してテーブルを開くかどうかを示します。|
|Jet OLEDB: ODBC パススルーステートメント (DBPROP_JETOLEDB_ODBCPASSTHROUGH)|Jet が **Command** オブジェクト内の SQL テキストを変更せずにバックエンドに渡す必要があることを示します。|
|Jet OLEDB: 部分一括操作 (DBPROP_JETOLEDB_BULKPARTIAL)|SQL DML 操作が失敗したときの Jet の動作を示します。|
|Jet OLEDB: パススルークエリ Bulk Op (DBPROP_JETOLEDB_PASSTHROUGHBULKOP)|**レコードセット**を返さないクエリをデータソースに変更せずに渡すかどうかを示します。|
|Jet OLEDB: パススルークエリの接続文字列 (DBPROP_JETOLEDB_ODBCPASSTHROUGHCONNECTSTRING)|リモートデータストアへの接続に使用される Jet 接続文字列を示します。 **JET OLEDB: ODBC パススルーステートメント**が True でない限り、この値は無視されます。|
|Jet OLEDB: ストアドクエリ (DBPROP_JETOLEDB_STOREDQUERY)|コマンドテキストを SQL コマンドではなく、ストアドクエリとして解釈するかどうかを示します。|
|Jet OLEDB: Set で規則を検証する (DBPROP_JETOLEDB_VALIDATEONSET)|列データが設定されたとき、または変更がデータベースにコミットされたときに、Jet 検証ルールを評価するかどうかを示します。|

 既定では、microsoft Jet の OLE DB プロバイダーは、Microsoft Jet データベースを読み取り/書き込みモードで開きます。 データベースを読み取り専用モードで開くには、ADO**接続**オブジェクトの[Mode](../../reference/ado-api/mode-property-ado.md)プロパティを**adModeRead**に設定します。

## <a name="command-object-usage"></a>コマンドオブジェクトの使用法
 [コマンド](../../reference/ado-api/command-object-ado.md)オブジェクトのコマンドテキストは、MICROSOFT Jet SQL 言語を使用します。 コマンドテキストで、行を返すクエリ、アクションクエリ、およびテーブル名を指定できます。ただし、ストアドプロシージャはサポートされていないため、指定しないでください。

## <a name="recordset-behavior"></a>レコードセットの動作
 Microsoft Jet データベースエンジンでは、動的カーソルはサポートされていません。 そのため、Microsoft Jet の OLE DB プロバイダーは、 **Adlockdynamic** カーソルの種類をサポートしていません。 動的カーソルが要求されると、プロバイダーはキーセットカーソルを返し、 [CursorType](../../reference/ado-api/cursortype-property-ado.md) プロパティをリセットして、返された [レコードセット](../../reference/ado-api/recordset-object-ado.md) の種類を示します。 さらに、更新可能な **レコードセット** が要求された場合 (**LockType** は **adlockoptimistic**、 **Adlockbatchオプティミスティック**、または **adlockoptimistic ペシミスティック**)、プロバイダーはキーセットカーソルも返し、 **CursorType** プロパティをリセットします。

## <a name="dynamic-properties"></a>動的プロパティ
 OLE DB Provider for Microsoft Jet は、開かれていない[接続](../../reference/ado-api/connection-object-ado.md)、[レコードセット](../../reference/ado-api/recordset-object-ado.md)、および[コマンド](../../reference/ado-api/command-object-ado.md)オブジェクトの**properties**コレクションに動的なプロパティをいくつか挿入します。

 次の表は、各動的プロパティの ADO と OLE DB 名のクロスインデックスです。 OLE DB プログラマーリファレンスでは、ADO プロパティ名を "Description" という用語で参照しています。 これらのプロパティの詳細については、OLE DB プログラマーリファレンスを参照してください。

## <a name="connection-dynamic-properties"></a>接続の動的プロパティ
 **接続**オブジェクトの**properties**コレクションには、次のプロパティが追加されます。

|ADO プロパティ名|OLE DB プロパティ名|
|-----------------------|--------------------------|
|Active sessions|DBPROP_ACTIVESESSIONS|
|非同期で起こる Abort|DBPROP_ASYNCTXNABORT|
|非同期で起こるコミット|DBPROP_ASYNCTNXCOMMIT|
|自動コミット分離レベル|DBPROP_SESS_AUTOCOMMITISOLEVELS|
|カタログの場所|DBPROP_CATALOGLOCATION|
|カタログ用語|DBPROP_CATALOGTERM|
|列の定義|DBPROP_COLUMNDEFINITION|
|現在のカタログ|DBPROP_CURRENTCATALOG|
|Data Source|DBPROP_INIT_DATASOURCE|
|データ ソース名|DBPROP_DATASOURCENAME|
|データソースオブジェクトのスレッドモデル|DBPROP_DSOTHREADMODEL|
|DBMS 名|DBPROP_DBMSNAME|
|DBMS バージョン|DBPROP_DBMSVER|
|サポートによるグループ化|DBPROP_GROUPBY|
|異種テーブルのサポート|DBPROP_HETEROGENEOUSTABLES|
|識別子の大文字と小文字の区別|DBPROP_IDENTIFIERCASE|
|分離レベル|DBPROP_SUPPORTEDTXNISOLEVELS|
|分離の保持|DBPROP_SUPPORTEDTXNISORETAIN|
|[Locale Identifier]|DBPROP_INIT_LCID|
|インデックスの最大サイズ|DBPROP_MAXINDEXSIZE|
|行の最大サイズ|DBPROP_MAXROWSIZE|
|行の最大サイズに BLOB が含まれる|DBPROP_MAXROWSIZEINCLUDESBLOB|
|SELECT 内の最大テーブル数|DBPROP_MAXTABLESINSELECT|
|モード|DBPROP_INIT_MODE|
|複数のパラメーターセット|DBPROP_MULTIPLEPARAMSETS|
|複数の結果|DBPROP_MULTIPLERESULTS|
|複数のストレージオブジェクト|DBPROP_MULTIPLESTORAGEOBJECTS|
|複数テーブルの更新|DBPROP_MULTITABLEUPDATE|
|NULL 照合順序|DBPROP_NULLCOLLATION|
|NULL の連結動作|DBPROP_CONCATNULLBEHAVIOR|
|OLE DB のバージョン|DBPROP_PROVIDEROLEDBVER|
|OLE オブジェクトのサポート|DBPROP_OLEOBJECTS|
|行セットのサポートを開く|DBPROP_OPENROWSETSUPPORT|
|Select リスト内の列の並べ替え|DBPROP_ORDERBYCOLUMNSINSELECT|
|出力パラメーターの可用性|DBPROP_OUTPUTPARAMETERAVAILABILITY|
|Ref アクセサーで渡す|DBPROP_BYREFACCESSORS|
|Password|DBPROP_AUTH_PASSWORD|
|永続的な ID の種類|DBPROP_PERSISTENTIDTYPE|
|中止動作の準備|DBPROP_PREPAREABORTBEHAVIOR|
|コミット動作の準備|DBPROP_PREPARECOMMITBEHAVIOR|
|プロシージャ用語|DBPROP_PROCEDURETERM|
|Prompt|DBPROP_INIT_PROMPT|
|プロバイダーのフレンドリ名|DBPROP_PROVIDERFRIENDLYNAME|
|プロバイダー名|DBPROP_PROVIDERFILENAME|
|プロバイダーのバージョン|DBPROP_PROVIDERVER|
|読み取り専用データソース|DBPROP_DATASOURCEREADONLY|
|コマンドでの行セットの変換|DBPROP_ROWSETCONVERSIONSONCOMMAND|
|スキーマ用語|DBPROP_SCHEMATERM|
|スキーマの使用法|DBPROP_SCHEMAUSAGE|
|SQL サポート|DBPROP_SQLSUPPORT|
|構造化ストレージ|DBPROP_STRUCTUREDSTORAGE|
|サブクエリのサポート|DBPROP_SUBQUERIES|
|テーブル用語|DBPROP_TABLETERM|
|トランザクション DDL|DBPROP_SUPPORTEDTXNDDL|
|User ID|DBPROP_AUTH_USERID|
|[ユーザー名]|DBPROP_USERNAME|
|ウィンドウ ハンドル|DBPROP_INIT_HWND|

## <a name="recordset-dynamic-properties"></a>レコードセットの動的プロパティ
 次のプロパティが、**レコードセット**オブジェクトの**properties**コレクションに追加されます。

|ADO プロパティ名|OLE DB プロパティ名|
|-----------------------|--------------------------|
|アクセス順序|DBPROP_ACCESSORDER|
|追加専用の行セット|DBPROP_APPENDONLY|
|ブロッキングストレージオブジェクト|DBPROP_BLOCKINGSTORAGEOBJECTS|
|ブックマークの種類|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|ブックマークの順序付け|DBPROP_ORDEREDBOOKMARKS|
|遅延列をキャッシュする|DBPROP_CACHEDEFERRED|
|挿入された行の変更|DBPROP_CHANGEINSERTEDROWS|
|列の特権|DBPROP_COLUMNRESTRICT|
|列セットの通知|DBPROP_NOTIFYCOLUMNSET|
|書き込み可能列|DBPROP_MAYWRITECOLUMN|
|列の遅延|DBPROP_DEFERRED|
|ストレージオブジェクトの更新の遅延|DBPROP_DELAYSTORAGEOBJECTS|
|後方フェッチ|DBPROP_CANFETCHBACKWARDS|
|行の保持|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|ILockBytes|DBPROP_ILockBytes|
|Immobile 行|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetIndex|DBPROP_IRowsetIndex|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsestLocate|
|IRowsetResynch||
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|IStorage|DBPROP_IStorage|
|IStream|DBPROP_IStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|リテラルブックマーク|DBPROP_LITERALBOOKMARKS|
|リテラル行の Id|DBPROP_LITERALIDENTITY|
|開いている最大行数|DBPROP_MAXOPENROWS|
|保留中の最大行数|DBPROP_MAXPENDINGROWS|
|最大行数|DBPROP_MAXROWS|
|メモリ使用量|DBPROP_MEMORYUSAGE|
|通知の粒度|DBPROP_NOTIFICATIONGRANULARITY|
|通知フェーズ|DBPROP_NOTIFICATIONPHASES|
|トランザクション処理済みオブジェクト|DBPROP_TRANSACTEDOBJECT|
|その他の変更が表示される|DBPROP_OTHERUPDATEDELETE|
|その他の挿入を可視化|DBPROP_OTHERINSERT|
|独自の変更を表示|DBPROP_OWNUPDATEDELETE|
|独自の挿入を表示|DBPROP_OWNINSERT|
|中止時に保持する|DBPROP_ABORTPRESERVE|
|コミット時に保存|DBPROP_COMMITPRESERVE|
|クイック再起動|DBPROP_QUICKRESTART|
|再入イベント|DBPROP_REENTRANTEVENTS|
|削除された行の削除|DBPROP_REMOVEDELETED|
|複数の変更を報告する|DBPROP_REPORTMULTIPLECHANGES|
|保留中の挿入を返す|DBPROP_RETURNPENDINGINSERTS|
|行の削除通知|DBPROP_NOTIFYROWDELETE|
|行の最初の変更通知|DBPROP_NOTIFYROWFIRSTCHANGE|
|行の挿入通知|DBPROP_NOTIFYROWINSERT|
|行の特権|DBPROP_ROWRESTRICT|
|行の再同期の通知|DBPROP_NOTIFYROWRESYNCH|
|行のスレッドモデル|DBPROP_ROWTHREADMODEL|
|行の元に戻す変更通知|DBPROP_NOTIFYROWUNDOCHANGE|
|行の削除の取り消し通知|DBPROP_NOTIFYROWUNDODELETE|
|行の取り消し挿入通知|DBPROP_NOTIFYROWUNDOINSERT|
|行の更新通知|DBPROP_NOTIFYROWUPDATE|
|行セットのフェッチ位置の変更通知|DBPROP_NOTIFYROWSETFETCHPOSISIONCHANGE|
|行セットのリリース通知|DBPROP_NOTIFYROWSETRELEASE|
|後方にスクロール|DBPROP_CANSCROLLBACKWARDS|
|削除されたブックマークをスキップ|DBPROP_BOOKMARKSKIPPED|
|厳密な行の Id|DBPROP_STRONGITDENTITY|
|更新|DBPROP_UPDATABILITY|
|ブックマークを使用する|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>コマンドの動的プロパティ
 次のプロパティは、 **Command**オブジェクトの**properties**コレクションに追加されます。

|ADO プロパティ名|OLE DB プロパティ名|
|-----------------------|--------------------------|
|アクセス順序|DBPROP_ACCESSORDER|
|追加専用の行セット|DBPROP_APPENDONLY|
|ブロッキングストレージオブジェクト|DBPROP_BLOCKINGSTORAGEOBJECTS|
|ブックマークの種類|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|挿入された行の変更|DBPROP_CHANGEINSERTEDROWS|
|列の特権|DBPROP_COLUMNRESTRICT|
|列セットの通知|DBPROP_NOTIFYCOLUMNSET|
|列の遅延|DBPROP_DEFERRED|
|ストレージオブジェクトの更新の遅延|DBPROP_DELAYSTORAGEOBJECTS|
|後方フェッチ|DBPROP_CANFETCHBACKWARDS|
|行の保持|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|ILockBytes|DBPROP_ILockBytes|
|Immobile 行|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetIndex|DBPROP_IRowsetIndex|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsetLocate|
|IRowsetResynch||
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|IStorage|DBPROP_IStorage|
|IStream|DBPROP_IStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|リテラルブックマーク|DBPROP_LITERALBOOKMARKS|
|リテラル行の Id|DBPROP_LITERALIDENTITY|
|ロックモード|DBPROP_LOCKMODE|
|開いている最大行数|DBPROP_MAXOPENROWS|
|保留中の最大行数|DBPROP_MAXPENDINGROWS|
|最大行数|DBPROP_MAXROWS|
|通知の粒度|DBPROP_NOTIFICATIONGRANULARITY|
|通知フェーズ|DBPROP_NOTIFICATIONPHASES|
|トランザクション処理済みオブジェクト|DBPROP_TRANSACTEDOBJECT|
|その他の変更が表示される|DBPROP_OTHERUPDATEDELETE|
|その他の挿入を可視化|DBPROP_OTHERINSERT|
|独自の変更を表示|DBPROP_OWNUPDATEDELETE|
|独自の挿入を表示|DBPROP_OWNINSERT|
|中止時に保持する|DBPROP_ABORTPRESERVE|
|コミット時に保存|DBPROP_COMMITPRESERVE|
|クイック再起動|DBPROP_QUICKRESTART|
|再入イベント|DBPROP_REENTRANTEVENTS|
|削除された行の削除|DBPROP_REMOVEDELETED|
|複数の変更を報告する|DBPROP_REPORTMULTIPLECHANGES|
|保留中の挿入を返す|DBPROP_RETURNPENDINGINSERTS|
|行の削除通知|DBPROP_NOTIFYROWDELETE|
|行の最初の変更通知|DBPROP_NOTIFYROWFIRSTCHANGE|
|行の挿入通知|DBPROP_NOTIFYROWINSERT|
|行の特権|DBPROP_ROWRESTRICT|
|行の再同期の通知|DBPROP_NOTIFYROWRESYNCH|
|行のスレッドモデル|DBPROP_ROWTHREADMODEL|
|行の元に戻す変更通知|DBPROP_NOTIFYROWUNDOCHANGE|
|行の削除の取り消し通知|DBPROP_NOTIFYROWUNDODELETE|
|行の取り消し挿入通知|DBPROP_NOTIFYROWUNDOINSERT|
|行の更新通知|DBPROP_NOTIFYROWUPDATE|
|行セットのフェッチ位置の変更通知|DBPROP_NOTIFYROWSETFETCHPOSITIONCHANGE|
|行セットのリリース通知|DBPROP_NOTIFYROWSETRELEASE|
|後方にスクロール|DBPROP_CANSCROLLBACKWARDS|
|挿入時のサーバーデータ|DBPROP_SERVERDATAONINSERT|
|削除されたブックマークをスキップ|DBPROP_BOOKMARKSKIP|
|厳密な行の Id|DBPROP_STRONGIDENTITY|
|更新|DBPROP_UPDATABILITY|
|ブックマークを使用する|DBPROP_BOOKMARKS|

 Microsoft Jet の OLE DB プロバイダーの具体的な実装の詳細と機能については、OLE DB のドキュメントの「 [Jet プロバイダー](/previous-versions/windows/desktop/ms722791(v=vs.85)) 」を参照してください。
