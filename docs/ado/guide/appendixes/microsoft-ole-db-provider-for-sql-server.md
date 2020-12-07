---
description: Microsoft OLE DB Provider for SQL Server の概要
title: Microsoft OLE DB Provider for SQL Server |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB provider for SQL Server
- OLE DB provider for SQL Server [ADO]
- SQLOLEDB [ADO]
ms.assetid: 99bc40c4-9181-4ca1-a06f-9a1a914a0b7b
author: rothja
ms.author: jroth
ms.openlocfilehash: 0a307a0de76ce1e74e3e1773a414fce93957572b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991003"
---
# <a name="microsoft-ole-db-provider-for-sql-server-overview"></a>Microsoft OLE DB Provider for SQL Server の概要
Microsoft OLE DB Provider for SQL Server (SQLOLEDB) を使用すると、ADO は Microsoft SQL Server にアクセスできます。

> [!IMPORTANT]
> Microsoft OLE DB Provider for SQL Server (SQLOLEDB) は非推奨とされます。新しい開発作業には使用しないことをお勧めします。 代わりに、新しい [Microsoft OLE DB Driver for SQL Server](../../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL) を使用します。これは、最新のサーバー機能で更新されます。

## <a name="connection-string-parameters"></a>接続文字列パラメーター
 このプロバイダーに接続するには、 *provider* 引数を [ConnectionString](../../reference/ado-api/connectionstring-property-ado.md) プロパティに設定します。

```vb
SQLOLEDB
```

 この値は、 [プロバイダー](../../reference/ado-api/provider-property-ado.md) プロパティを使用して設定または読み取ることもできます。

## <a name="typical-connection-string"></a>一般的な接続文字列
 このプロバイダーの一般的な接続文字列は次のとおりです。

```vb
"Provider=SQLOLEDB;Data Source=serverName;"
Initial Catalog=databaseName;
User ID=MyUserID;Password=MyPassword;"
```

 文字列は、次のキーワードで構成されています。

|キーワード|説明|
|-------------|-----------------|
|**プロバイダー**|SQL Server の OLE DB プロバイダーを指定します。|
|**データソース** または **サーバー**|サーバーの名前を指定します。|
|**初期カタログ** または **データベース**|サーバー上のデータベースの名前を指定します。|
|**ユーザー ID** または **uid**|SQL Server 認証用のユーザー名を指定します。|
|**Password** または **pwd**|SQL Server 認証用のユーザーパスワードを指定します。|

> [!NOTE]
>  Windows 認証をサポートするデータソースプロバイダーに接続する場合は、接続文字列にユーザー ID とパスワードの情報ではなく、 **Trusted_Connection = yes** または **INTEGRATED Security = SSPI** を指定する必要があります。

## <a name="provider-specific-connection-parameters"></a>プロバイダー固有の接続パラメーター
 プロバイダーは、ADO によって定義されているものに加えて、いくつかのプロバイダー固有の接続パラメーターをサポートしています。 ADO の接続プロパティと同様に、これらのプロバイダー固有のプロパティは、[接続](../../reference/ado-api/connection-object-ado.md)の[properties](../../reference/ado-api/properties-collection-ado.md)コレクションを使用して設定することも、 **ConnectionString**の一部として設定することもできます。

|パラメーター|説明|
|---------------|-----------------|
|Trusted_Connection|ユーザー認証モードを示します。 これは、 **[はい]** または [ **いいえ**] に設定できます。 既定値は **No**です。 このプロパティが **[はい]** に設定されている場合、SQLOLEDB は MICROSOFT Windows NT 認証モードを使用して、 **Location** プロパティ値および [Datasource](../../reference/ado-api/datasource-property-ado.md) プロパティ値で指定された SQL Server データベースへのユーザーアクセスを承認します。 このプロパティが [ **いいえ**] に設定されている場合、SQLOLEDB は混合モードを使用して、SQL Server データベースへのユーザーアクセスを承認します。 SQL Server のログインとパスワードは、 **ユーザー Id** と **パスワード** のプロパティで指定します。|
|[現在の言語]|SQL Server 言語名を示します。 システム メッセージの選択や書式設定に使われる言語を示します。 この言語は SQL Server にインストールする必要があります。そうしないと、接続を開くことができません。|
|[ネットワーク アドレス]|**Location**プロパティによって指定された SQL Server のネットワークアドレスを示します。|
|Network Library|SQL Server との通信に使用されるネットワークライブラリ (DLL) の名前を示します。 この名前には、パスやファイル拡張子 (.dll) は含めません。 既定値は SQL Server クライアント構成によって提供されます。|
|準備のためにプロシージャを使用する|コマンドが準備されたときに ( **準備** されたプロパティによって) SQL Server が一時ストアドプロシージャを作成するかどうかを決定します。|
|自動翻訳|OEM/ANSI 文字を変換するかどうかを示します。 このプロパティは、 **True** または **False**に設定できます。 既定値は **True** です。 このプロパティが **True**に設定されている場合、SQLOLEDB は、SQL Server に対してマルチバイト文字の文字列を取得または送信するときに、OEM/ANSI 文字の変換を実行します。 このプロパティが **False**に設定されている場合、SQLOLEDB は、マルチバイト文字の文字列データに対して OEM/ANSI 文字変換を実行しません。|
|Packet Size|ネットワークパケットサイズ (バイト単位) を示します。 パケットサイズのプロパティ値は、512 ~ 32767 の範囲で指定する必要があります。 既定の SQLOLEDB ネットワークパケットサイズは4096です。|
|アプリケーション名|クライアントアプリケーション名を示します。|
|[ワークステーション ID]|ワークステーションを識別する文字列。|

## <a name="command-object-usage"></a>コマンドオブジェクトの使用法
 SQLOLEDB は、混在の ODBC、ANSI、および SQL Server 固有の Transact-sql を有効な構文として受け入れます。 たとえば、次の SQL ステートメントでは、ODBC SQL のエスケープ シーケンスを使用して、LCASE 文字列関数を指定しています。

```sql
SELECT customerid={fn LCASE(CustomerID)} FROM Customers

```

 LCASE 関数は、大文字をすべて小文字に変換した文字列を返します。 ANSI SQL 文字列関数 LOWER は同じ操作を実行するため、次の SQL ステートメントは、前に示した ODBC ステートメントと同等の ANSI です。

```sql
SELECT customerid=LOWER(CustomerID) FROM Customers

```

 SQLOLEDB は、コマンドのテキストとして指定されている場合に、いずれかの形式のステートメントを正常に処理します。

## <a name="stored-procedures"></a>ストアド プロシージャ
 SQLOLEDB コマンドを使用して SQL Server ストアドプロシージャを実行する場合は、コマンドテキストで ODBC プロシージャ呼び出しのエスケープシーケンスを使用します。 SQLOLEDB は、SQL Server のリモートプロシージャコールメカニズムを使用して、コマンド処理を最適化します。 たとえば、次の ODBC SQL ステートメントは、Transact-sql 形式で推奨されるコマンドテキストです。

## <a name="odbc-sql"></a>ODBC SQL

```vb
{call SalesByCategory('Produce', '1995')}

```

## <a name="transact-sql"></a>Transact-SQL

```sql
EXECUTE SalesByCategory 'Produce', '1995'

```

## <a name="sql-server-features"></a>SQL Server 機能
 SQL Server を使用すると、ADO は **コマンド** 入力に xml を使用し、 **レコードセット** オブジェクトではなく xml ストリーム形式で結果を取得できます。 詳細については、「 [コマンド入力用のストリームの使用](../data/command-streams.md) 」および「 [結果セットのストリームへの取得](../data/retrieving-resultsets-into-streams.md)」を参照してください。

### <a name="accessing-sql_variant-data-using-mdac-27-mdac-28-or-windows-dac-60"></a>MDAC 2.7、MDAC 2.8、または Windows DAC 6.0 を使用した sql_variant データへのアクセス
 Microsoft SQL Server には **sql_variant**と呼ばれるデータ型があります。 OLE DB の **DBTYPE_VARIANT**と同様に、 **sql_variant** データ型には複数の異なる型のデータを格納できます。 ただし、 **DBTYPE_VARIANT** と **sql_variant**にはいくつかの重要な違いがあります。 また、ADO は、 **sql_variant** 値として格納されるデータを、他のデータ型を処理する方法とは異なる方法で処理します。 次の一覧では、 **sql_variant**型の列に格納されている SQL Server データにアクセスする際に考慮する必要がある問題について説明します。

-   MDAC 2.7、MDAC 2.8、および Windows Data Access Components (Windows DAC) 6.0 では、SQL Server の OLE DB Provider は **sql_variant** の種類をサポートしています。 OLE DB Provider for ODBC は使用できません。

-   **Sql_variant**型が**DBTYPE_VARIANT**のデータ型と正確に一致しません。  **Sql_variant**型は、 **GUID**、 **ANSI** (UNICODE 以外) 文字列、 **BIGINT**など **、DBTYPE_VARIANT**でサポートされていないいくつかの新しいサブタイプをサポートしています。 上記以外のサブタイプを使用すると、正しく動作します。

-   **Sql_variant** Subtype の**数値**が**DBTYPE_DECIMAL**のサイズと一致しません。

-   複数のデータ型の強制型変換では、一致しない型が生成されます。 たとえば、 **sql_variant** を **GUID** のサブタイプで **DBTYPE_VARIANT** にすると、 **safearray**(バイト) のサブタイプになります。 この型を **sql_variant** に変換すると、 **配列**の新しいサブタイプ (バイト) になります。

-   **Sql_variant**データを含む**レコードセット**フィールドは、 **sql_variant**に特定のサブタイプが含まれている場合にのみ、リモート処理 (マーシャリング) できます。 サポートされていない次のサブタイプを使用してデータをリモートまたは永続化しようとすると、Microsoft 永続化プロバイダー (MSPersist) からの実行時エラー (サポートされていない変換) ( **VT_VARIANT**、 **VT_RECORD**、 **VT_ILLEGAL**、 **VT_UNKNOWN**、 **VT_BSTR**、および VT_DISPATCH) が発生 **します。**

-   MDAC 2.7、MDAC 2.8、および Windows DAC 6.0 の SQL Server の OLE DB プロバイダーには、"**ネイティブバリアントを許可**する" という動的プロパティがあります。これは、名前が示すように、開発者が**DBTYPE_VARIANT**ではなくネイティブ形式で**sql_variant**にアクセスできるようにします。 このプロパティが設定されていて、 **レコードセット** がクライアントカーソルエンジン (**adUseClient**) で開かれている場合、 **レコードセット** の呼び出しは失敗します。 このプロパティが設定されていて、 **レコードセット** がサーバーカーソル (**aduseserver**) で開かれている場合、 **レコードセット** の呼び出しは成功しますが、 **sql_variant** 型の列にアクセスするとエラーが発生します。

-   MDAC 2.5 を使用するクライアントアプリケーションでは、Microsoft SQL Server に対するクエリで **sql_variant** データを使用できます。 ただし、 **sql_variant** データの値は文字列として扱われます。 このようなクライアントアプリケーションは、MDAC 2.7、MDAC 2.8、または Windows DAC 6.0 にアップグレードする必要があります。

## <a name="recordset-behavior"></a>レコードセットの動作
 SQLOLEDB は SQL Server カーソルを使用して、多くのコマンドによって生成される複数の結果をサポートすることはできません。 コンシューマーが SQL Server カーソルサポートを必要とするレコードセットを要求した場合、使用されたコマンドテキストが結果として複数のレコードセットを生成すると、エラーが発生します。

 スクロール可能な SQLOLEDB レコードセットは SQL Server カーソルによってサポートされています。 SQL Server では、データベースの他のユーザーによって行われた変更によって影響を受けるカーソルに制限が課されます。 具体的には、一部のカーソル内の行を並べ替えることはできません。また、SQL ORDER BY 句を含むコマンドを使用してレコードセットを作成しようとすると失敗することがあります。

## <a name="dynamic-properties"></a>動的プロパティ
 Microsoft OLE DB Provider for SQL Server では、開かれていない[接続](../../reference/ado-api/connection-object-ado.md)、[レコードセット](../../reference/ado-api/recordset-object-ado.md)、および[コマンド](../../reference/ado-api/command-object-ado.md)オブジェクトの**properties**コレクションに動的なプロパティがいくつか挿入されます。

 次の表は、各動的プロパティの ADO と OLE DB 名のクロスインデックスです。 OLE DB プログラマーリファレンスでは、ADO プロパティ名を "Description" という用語で参照しています。 これらのプロパティの詳細については、OLE DB プログラマーリファレンスを参照してください。 インデックスで OLE DB プロパティ名を検索するか、「 [付録 C: OLE DB のプロパティ](/previous-versions/windows/desktop/ms723130(v=vs.85))」を参照してください。

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
|インデックスの最大サイズ|DBPROP_MAXINDEXSIZE|
|行の最大サイズ|DBPROP_MAXROWSIZE|
|行の最大サイズに BLOB が含まれる|DBPROP_MAXROWSIZEINCLUDESBLOB|
|SELECT 内の最大テーブル数|DBPROP_MAXTABLESINSELECT|
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
 次のプロパティが、**レコードセット**オブジェクトの**properties**コレクションに追加されます。

|ADO プロパティ名|OLE DB プロパティ名|
|-----------------------|--------------------------|
|アクセス順序|DBPROP_ACCESSORDER|
|ブロッキングストレージオブジェクト|DBPROP_BLOCKINGSTORAGEOBJECTS|
|ブックマークの種類|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|挿入された行の変更|DBPROP_CHANGEINSERTEDROWS|
|列の特権|DBPROP_COLUMNRESTRICT|
|列セットの通知|DBPROP_NOTIFYCOLUMNSET|
|コマンドのタイムアウト|DBPROP_COMMANDTIMEOUT|
|列の遅延|DBPROP_DEFERRED|
|ストレージオブジェクトの更新の遅延|DBPROP_DELAYSTORAGEOBJECTS|
|後方フェッチ|DBPROP_CANFETCHBACKWARDS|
|行の保持|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|Immobile 行|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsestLocate|
|IRowsetResynch||
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|リテラルブックマーク|DBPROP_LITERALBOOKMARKS|
|リテラル行の Id|DBPROP_LITERALIDENTITY|
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
|行セットのフェッチ位置の変更通知|DBPROP_NOTIFYROWSETFETCHPOSISIONCHANGE|
|行セットのリリース通知|DBPROP_NOTIFYROWSETRELEASE|
|後方にスクロール|DBPROP_CANSCROLLBACKWARDS|
|サーバーカーソル|DBPROP_SERVERCURSOR|
|削除されたブックマークをスキップ|DBPROP_BOOKMARKSKIPPED|
|厳密な行の Id|DBPROP_STRONGITDENTITY|
|一意の行|DBPROP_UNIQUEROWS|
|更新|DBPROP_UPDATABILITY|
|ブックマークを使用する|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>コマンドの動的プロパティ
 次のプロパティは、 **Command**オブジェクトの**properties**コレクションに追加されます。

|ADO プロパティ名|OLE DB プロパティ名|
|-----------------------|--------------------------|
|アクセス順序|DBPROP_ACCESSORDER|
|基本パス|SSPROP_STREAM_BASEPATH|
|ブロッキングストレージオブジェクト|DBPROP_BLOCKINGSTORAGEOBJECTS|
|ブックマークの種類|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|挿入された行の変更|DBPROP_CHANGEINSERTEDROWS|
|列の特権|DBPROP_COLUMNRESTRICT|
|列セットの通知|DBPROP_NOTIFYCOLUMNSET|
|コンテンツの種類|SSPROP_STREAM_CONTENTTYPE|
|カーソルの自動フェッチ|SSPROP_CURSORAUTOFETCH|
|列の遅延|DBPROP_DEFERRED|
|準備コマンドの遅延送信|SSPROP_DEFERPREPARE|
|ストレージオブジェクトの更新の遅延|DBPROP_DELAYSTORAGEOBJECTS|
|後方フェッチ|DBPROP_CANFETCHBACKWARDS|
|行の保持|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|Immobile 行|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsetLocate|
|IRowsetResynch|DBPROP_IRowsetResynch|
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
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
|"出力エンコード" プロパティ|DBPROP_OUTPUTENCODING|
|出力ストリームのプロパティ|DBPROP_OUTPUTSTREAM|
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
|サーバーカーソル|DBPROP_SERVERCURSOR|
|挿入時のサーバーデータ|DBPROP_SERVERDATAONINSERT|
|削除されたブックマークをスキップ|DBPROP_BOOKMARKSKIP|
|厳密な行の Id|DBPROP_STRONGIDENTITY|
|更新|DBPROP_UPDATABILITY|
|ブックマークを使用する|DBPROP_BOOKMARKS|
|XML ルート|SSPROP_STREAM_XMLROOT|
|XSL (XSL)|SSPROP_STREAM_XSL|

 Microsoft SQL Server OLE DB プロバイダーの具体的な実装の詳細と機能については、 [SQL Server プロバイダー](/previous-versions/windows/desktop/ms720897(v=vs.85))に関する説明を参照してください。

## <a name="see-also"></a>参照
 [ConnectionString プロパティ (ado)](../../reference/ado-api/connectionstring-property-ado.md) [プロバイダープロパティ (ado](../../reference/ado-api/provider-property-ado.md) ) [レコードセットオブジェクト (ado)](../../reference/ado-api/recordset-object-ado.md)