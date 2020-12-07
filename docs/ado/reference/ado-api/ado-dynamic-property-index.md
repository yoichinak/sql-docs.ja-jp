---
description: ADO Dynamic プロパティ インデックス
title: ADO 動的プロパティインデックス |Microsoft Docs
ms.prod: sql
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- dynamic properties [ADO], index
ms.assetid: 80d389dd-46ef-459f-b0d4-6f712fc4f32d
author: rothja
ms.author: jroth
ms.openlocfilehash: bbf4cdae12da71f5fc4d3b8fbc11b7ca64c46c5b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976493"
---
# <a name="ado-dynamic-property-index"></a>ADO Dynamic プロパティ インデックス
データプロバイダー、サービスプロバイダー、およびサービスコンポーネントは、開かれていない[接続](./connection-object-ado.md)および[レコードセット](./recordset-object-ado.md)オブジェクトの**プロパティ**コレクションに動的なプロパティを追加できます。 また、これらのオブジェクトを開いたときに、指定したプロバイダーによって追加のプロパティが挿入される場合もあります。 これらのプロパティの一部は、「 [ADO Dynamic properties](./ado-dynamic-properties.md) 」セクションに一覧表示されています。 詳細については、 [「付録 a: providers](../../guide/appendixes/appendix-a-providers.md) 」セクションの特定のプロバイダーに記載されています。  
  
 次の表は、各標準 OLE DB プロバイダーの動的プロパティの ADO と OLE DB 名のクロスインデックスです。 プロバイダーは、ここに記載されているよりも多くのプロパティを追加できます。 プロバイダー固有の動的プロパティに関する具体的な情報については、プロバイダーのドキュメントを参照してください。  
  
 OLE DB プログラマーリファレンスでは、ADO プロパティ名を "Description" という用語で参照しています。 これらの標準プロパティの詳細については、 [OLE DB のドキュメント](/previous-versions/windows/desktop/ms722784(v=vs.85))で、OLE DB プロパティの名前でインデックスを検索または参照してください。  
  
## <a name="connection-dynamic-properties"></a>接続の動的プロパティ  
  
|ADO プロパティ名|OLE DB プロパティ名|  
|-----------------------|--------------------------|  
|Active sessions|DBPROP_ACTIVESESSIONS|  
|非同期で起こる Abort|DBPROP_ASYNCTXNABORT|  
|非同期で起こるコミット|DBPROP_ASYNCTNXCOMMIT|  
|自動コミット分離レベル|DBPROP_SESS_AUTOCOMMITISOLEVELS|  
|カタログの場所|DBPROP_CATALOGLOCATION|  
|カタログ用語|DBPROP_CATALOGTERM|  
|列の定義|DBPROP_COLUMNDEFINITION|  
|Connect Timeout|DBPROP_INIT_TIMEOUT|  
|現在のカタログ|DBPROP_CURRENTCATALOG|  
|Data Source|DBPROP_INIT_DATASOURCE|  
|データ ソース名|DBPROP_DATASOURCENAME|  
|データソースオブジェクトのスレッドモデル|DBPROP_DSOTHREADMODEL|  
|DBMS 名|DBPROP_DBMSNAME|  
|DBMS バージョン|DBPROP_DBMSVER|  
|Extended Properties|DBPROP_INIT_PROVIDERSTRING|  
|サポートによるグループ化|DBPROP_GROUPBY|  
|異種テーブルのサポート|DBPROP_HETEROGENEOUSTABLES|  
|識別子の大文字と小文字の区別|DBPROP_IDENTIFIERCASE|  
|Initial Catalog|DBPROP_INIT_CATALOG|  
|分離レベル|DBPROP_SUPPORTEDTXNISOLEVELS|  
|分離の保持|DBPROP_SUPPORTEDTXNISORETAIN|  
|[Locale Identifier]|DBPROP_INIT_LCID|  
|場所|DBPROP_INIT_LOCATION|  
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
|OLE DB サービス|DBPROP_INIT_OLEDBSERVICES|  
|OLE DB のバージョン|DBPROP_PROVIDEROLEDBVER|  
|OLE オブジェクトのサポート|DBPROP_OLEOBJECTS|  
|行セットのサポートを開く|DBPROP_OPENROWSETSUPPORT|  
|Select リスト内の列の並べ替え|DBPROP_ORDERBYCOLUMNSINSELECT|  
|出力パラメーターの可用性|DBPROP_OUTPUTPARAMETERAVAILABILITY|  
|Ref アクセサーで渡す|DBPROP_BYREFACCESSORS|  
|Password|DBPROP_AUTH_PASSWORD|  
|Persist Security Info|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|  
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
 **レコードセットオブジェクトの****動的プロパティ**は、**レコードセット**が閉じられたときにスコープ外になることに注意してください。  
  
|ADO プロパティ名|OLE DB プロパティ名|  
|-----------------------|--------------------------|  
|IAccessor|DBPROP_IACCESSOR|  
|IChapteredRowset||  
|IColumnsInfo|DBPROP_ICOLUMNSINFO|  
|IColumnsRowset|DBPROP_ICOLUMNSROWSET|  
|IConnectionPointContainer|DBPROP_ICONNECTIONPOINTCONTAINER|  
|IConvertType||  
|ILockBytes|DBPROP_ILOCKBYTES|  
|IRowset|DBPROP_IROWSET|  
|IDBAsynchStatus|DBPROP_IDBASYNCHSTATUS|  
|IParentRowset||  
|IRowsetChange|DBPROP_IROWSETCHANGE|  
|IRowsetExactScroll||  
|IRowsetFind|DBPROP_IROWSETFIND|  
|IRowsetIdentity|DBPROP_IROWSETIDENTITY|  
|IRowsetInfo|DBPROP_IROWSETINFO|  
|IRowsetLocate|DBPROP_IROWSETLOCATE|  
|IRowsetRefresh|DBPROP_IROWSETREFRESH|  
|IRowsetResynch||  
|IRowsetScroll|DBPROP_IROWSETSCROLL|  
|IRowsetUpdate|DBPROP_IROWSETUPDATE|  
|IRowsetView|DBPROP_IROWSETVIEW|  
|IRowsetIndex|DBPROP_IROWSETINDEX|  
|ISequentialStream|DBPROP_ISEQUENTIALSTREAM|  
|IStorage|DBPROP_ISTORAGE|  
|IStream|DBPROP_ISTREAM|  
|ISupportErrorInfo|DBPROP_ISUPPORTERRORINFO|  
|アクセス順序|DBPROP_ACCESSORDER|  
|追加専用の行セット|DBPROP_APPENDONLY|  
|非同期の行セットの処理|DBPROP_ROWSET_ASYNCH|  
|自動再計算|DBPROP_ADC_AUTORECALC|  
|バックグラウンドフェッチサイズ|DBPROP_ASYNCHFETCHSIZE|  
|バックグラウンド スレッド優先順位|DBPROP_ASYNCHTHREADPRIORITY|  
|バッチ サイズ|DBPROP_ADC_BATCHSIZE|  
|ブロッキングストレージオブジェクト|DBPROP_BLOCKINGSTORAGEOBJECTS|  
|ブックマークの種類|DBPROP_BOOKMARKTYPE|  
|Bookmarkable|DBPROP_IROWSETLOCATE|  
|ブックマークの順序付け|DBPROP_ORDEREDBOOKMARKS|  
|子行のキャッシュ|DBPROP_ADC_CACHECHILDROWS|  
|遅延列をキャッシュする|DBPROP_CACHEDEFERRED|  
|挿入された行の変更|DBPROP_CHANGEINSERTEDROWS|  
|列の特権|DBPROP_COLUMNRESTRICT|  
|列セットの通知|DBPROP_NOTIFYCOLUMNSET|  
|書き込み可能列|DBPROP_MAYWRITECOLUMN|  
|コマンドのタイムアウト|DBPROP_COMMANDTIMEOUT|  
|カーソルエンジンのバージョン|DBPROP_ADC_CEVER|  
|列の遅延|DBPROP_DEFERRED|  
|ストレージオブジェクトの更新の遅延|DBPROP_DELAYSTORAGEOBJECTS|  
|後方フェッチ|DBPROP_CANFETCHBACKWARDS|  
|フィルター操作|DBPROP_FILTERCOMPAREOPS|  
|検索操作|DBPROP_FINDCOMPAREOPS|  
|非表示の列 (カウント)|DBPROP_HIDDENCOLUMNS|  
|行の保持|DBPROP_CANHOLDROWS|  
|Immobile 行|DBPROP_IMMOBILEROWS|  
|初期フェッチサイズ|DBPROP_ASYNCHPREFETCHSIZE|  
|リテラルブックマーク|DBPROP_LITERALBOOKMARKS|  
|リテラル行の Id|DBPROP_LITERALIDENTITY|  
|変更の状態を維持する|DBPROP_ADC_MAINTAINCHANGESTATUS|  
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
|Private1||  
|クイック再起動|DBPROP_QUICKRESTART|  
|再入イベント|DBPROP_REENTRANTEVENTS|  
|削除された行の削除|DBPROP_REMOVEDELETED|  
|複数の変更を報告する|DBPROP_REPORTMULTIPLECHANGES|  
|名前のリシェイプ|DBPROP_ADC_RESHAPENAME|  
|再同期コマンド|DBPROP_ADC_CUSTOMRESYNCH|  
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
|サーバーカーソル|DBPROP_SERVERCURSOR|  
|削除されたブックマークをスキップ|DBPROP_BOOKMARKSKIPPED|  
|厳密な行の Id|DBPROP_STRONGIDENTITY|  
|一意のカタログ|DBPROP_ADC_UNIQUECATALOG|  
|一意の行|DBPROP_UNIQUEROWS|  
|一意のスキーマ|DBPROP_ADC_UNIQUESCHEMA|  
|Unique Table|DBPROP_ADC_UNIQUETABLE|  
|更新|DBPROP_UPDATABILITY|  
|更新条件|DBPROP_ADC_UPDATECRITERIA|  
|再同期の更新|DBPROP_ADC_UPDATERESYNC|  
|ブックマークを使用する|DBPROP_BOOKMARKS|