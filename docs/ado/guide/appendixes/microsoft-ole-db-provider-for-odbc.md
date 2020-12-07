---
description: Microsoft OLE DB Provider for ODBC の概要
title: Microsoft OLE DB Provider for ODBC |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB provider for ODBC [ADO]
- providers [ADO], OLE DB provider for ODBC
ms.assetid: 2dc0372d-e74d-4d0f-9c8c-04e5a168c148
author: rothja
ms.author: jroth
ms.openlocfilehash: 1bce53fd000baace86d32542d9b9cc843ee68296
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991023"
---
# <a name="microsoft-ole-db-provider-for-odbc-overview"></a>Microsoft OLE DB Provider for ODBC の概要
ADO または RDS プログラマーにとって理想的な世界は、ADO がデータソースを直接呼び出すことができるように、すべてのデータソースが OLE DB インターフェイスを公開することです。 OLE DB インターフェイスを実装しているデータベースベンダーはますます増えていますが、一部のデータソースはまだこのように公開されていません。 ただし、現在使用されている DBMS システムのほとんどは、ODBC を使用してアクセスできます。

 ODBC ドライバーは、現在使用されているすべての主要な DBMS (Microsoft SQL Server、Microsoft Access (Microsoft Jet データベースエンジン)、Microsoft FoxPro など) に加えて、Oracle などの Microsoft 以外のデータベース製品にも使用できます。

 ただし、Microsoft ODBC プロバイダーを使用すると、ADO は任意の ODBC データソースに接続できます。 プロバイダーは、フリースレッドで、Unicode が有効になっています。

 プロバイダーはトランザクションをサポートしていますが、DBMS エンジンによって提供されるトランザクションサポートの種類も異なります。 たとえば、Microsoft Access では、最大5レベルまで入れ子になったトランザクションをサポートしています。

 これは ADO の既定のプロバイダーであり、プロバイダーに依存するすべての ADO プロパティとメソッドがサポートされています。

## <a name="connection-string-parameters"></a>接続文字列パラメーター
 このプロバイダーに接続するには、 [ConnectionString](../../reference/ado-api/connectionstring-property-ado.md)プロパティの**provider =** 引数をに設定します。

```
MSDASQL
```

 [プロバイダー](../../reference/ado-api/provider-property-ado.md)プロパティを読み取ると、この文字列も返されます。

## <a name="typical-connection-string"></a>一般的な接続文字列
 このプロバイダーの一般的な接続文字列は次のとおりです。

```
"Provider=MSDASQL;DSN=dsnName;UID=MyUserID;PWD=MyPassword;"
```

 文字列は、次のキーワードで構成されています。

|キーワード|説明|
|-------------|-----------------|
|**プロバイダー**|ODBC の OLE DB プロバイダーを指定します。|
|**DSN**|データソース名を指定します。|
|**UID**|ユーザー名を指定します。|
|**PWD**|ユーザーのパスワードを指定します。|
|**URL**|Web フォルダーに発行されたファイルまたはディレクトリの URL を指定します。|

 これは ADO の既定のプロバイダーであるため、接続文字列から **provider =** パラメーターを省略した場合、ado はこのプロバイダーへの接続を確立しようとします。

> [!NOTE]
>  Windows 認証をサポートするデータソースプロバイダーに接続する場合は、接続文字列にユーザー ID とパスワードの情報ではなく、 **Trusted_Connection = yes** または **INTEGRATED Security = SSPI** を指定する必要があります。

 プロバイダーは、ADO によって定義されているものに加えて、特定の接続パラメーターをサポートしていません。 ただし、プロバイダーは ADO 以外の接続パラメーターを ODBC ドライバーマネージャーに渡します。

 このため、 **プロバイダー** パラメーターを省略できるため、同じデータソースの ODBC 接続文字列と同じ ADO 接続文字列を作成できます。 ODBC 接続文字列を作成する場合と同じパラメーター名 (**DRIVER =**、 **DATABASE =**、 **DSN =** など)、値、構文を使用します。 定義済みのデータソース名 (DSN) または FileDSN を使用して、または使用せずに接続できます。

## <a name="syntax-with-a-dsn-or-filedsn"></a>DSN または FileDSN を使用した構文:

```
"[Provider=MSDASQL;] { DSN=name | FileDSN=filename } ;
[DATABASE=database;] UID=user; PWD=password"
```

## <a name="syntax-without-a-dsn-dsn-less-connection"></a>DSN のない構文 (DSN レス接続):

```
"[Provider=MSDASQL;] DRIVER=driver; SERVER=server;
DATABASE=database; UID=MyUserID; PWD=MyPassword"
```

## <a name="remarks"></a>解説
 **DSN**または**FileDSN**を使用する場合は、Windows のコントロールパネルで ODBC データソースアドミニストレーターを使用して定義する必要があります。 Microsoft Windows 2000 では、ODBC 管理者は [管理ツール] の下にあります。 以前のバージョンの Windows では、ODBC 管理者アイコンには、 **32 ビット odbc** または **odbc**のみという名前が付けられていました。

 **DSN**を設定する代わりに、ODBC ドライバー (**driver =**) を指定することもできます。たとえば、"SQL Server;" のようにサーバー名 (**server =**) を指定できます。データベース名 (**データベース =**) を指定します。

 また、ODBC 固有のパラメーターのユーザーアカウント名 (**UID =**) と、ユーザーアカウントのパスワード (**PWD =**) を指定することも、ADO によって定義された標準の *ユーザー* パラメーターと *パスワード* パラメーターを指定することもできます。

 **Dsn**定義には既にデータベースが指定されていますが、 **dsn**に加えて、別のデータベースに接続するための*データベース*パラメーター*を指定する*こともできます。 **DSN**を使用する場合は *、* 常に*database*パラメーターを含めることをお勧めします。 これにより、 **DSN** 定義を最後に確認した後に、別のユーザーが既定のデータベースパラメーターを変更した場合に、正しいデータベースに接続できるようになります。

## <a name="provider-specific-connection-properties"></a>プロバイダー固有の接続プロパティ
 ODBC の OLE DB プロバイダーは、 **Connection**オブジェクトの[properties](../../reference/ado-api/properties-collection-ado.md)コレクションにいくつかのプロパティを追加します。 次の表は、これらのプロパティをかっこで囲んで、対応する OLE DB プロパティ名を示しています。

|プロパティ名|説明|
|-------------------|-----------------|
|アクセス可能なプロシージャ (KAGPROP_ACCESSIBLEPROCEDURES)|ユーザーがストアドプロシージャにアクセスできるかどうかを示します。|
|アクセス可能なテーブル (KAGPROP_ACCESSIBLETABLES)|ユーザーがデータベーステーブルに対して SELECT ステートメントを実行する権限を持っているかどうかを示します。|
|アクティブなステートメント (KAGPROP_ACTIVESTATEMENTS)|ODBC ドライバーが接続でサポートできるハンドルの数を示します。|
|ドライバー名 (KAGPROP_DRIVERNAME)|ODBC ドライバーのファイル名を示します。|
|ドライバー ODBC バージョン (KAGPROP_DRIVERODBCVER)|このドライバーがサポートする ODBC のバージョンを示します。|
|ファイルの使用法 (KAGPROP_FILEUSAGE)|ドライバーがデータソース内のファイルを処理する方法を示します。テーブルまたはカタログとして。|
|Like Escape 句 (KAGPROP_LIKEESCAPECLAUSE)|ドライバーが、パーセント文字 (%) のエスケープ文字の定義と使用をサポートしているかどうかを示します。また、WHERE 句の LIKE 述語で文字 (_) に下線を引くことができます。|
|Group By の最大列数 (KAGPROP_MAXCOLUMNSINGROUPBY)|SELECT ステートメントの GROUP BY 句に表示できる列の最大数を示します。|
|インデックスの最大列数 (KAGPROP_MAXCOLUMNSININDEX)|インデックスに含めることができる列の最大数を示します。|
|Order By の Max 列数 (KAGPROP_MAXCOLUMNSINORDERBY)|SELECT ステートメントの ORDER BY 句に表示できる列の最大数を示します。|
|Select の最大列数 (KAGPROP_MAXCOLUMNSINSELECT)|SELECT ステートメントの SELECT 部分に表示できる列の最大数を示します。|
|テーブルの最大列数 (KAGPROP_MAXCOLUMNSINTABLE)|テーブルで許容される列の最大数を示します。|
|数値関数 (KAGPROP_NUMERICFUNCTIONS)|ODBC ドライバーでサポートされている数値関数を示します。 このビットマスクで使用される関数名と関連する値の一覧については、ODBC のドキュメントの「 [付録 E: スカラー関数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)」を参照してください。|
|外部結合機能 (KAGPROP_OJCAPABILITY)|プロバイダーによってサポートされる外部結合の種類を示します。|
|外部結合 (KAGPROP_OUTERJOINS)|プロバイダーが外部結合をサポートするかどうかを示します。|
|特殊文字 (KAGPROP_SPECIALCHARACTERS)|ODBC ドライバーに対して特別な意味を持つ文字を示します。|
|ストアドプロシージャ (KAGPROP_PROCEDURES)|ストアドプロシージャをこの ODBC ドライバーで使用できるかどうかを示します。|
|文字列関数 (KAGPROP_STRINGFUNCTIONS)|ODBC ドライバーでサポートされている文字列関数を示します。 このビットマスクで使用される関数名と関連する値の一覧については、ODBC のドキュメントの「 [付録 E: スカラー関数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)」を参照してください。|
|システム関数 (KAGPROP_SYSTEMFUNCTIONS)|ODBC ドライバーでサポートされているシステム関数を示します。 このビットマスクで使用される関数名と関連する値の一覧については、ODBC のドキュメントの「 [付録 E: スカラー関数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)」を参照してください。|
|時刻/日付関数 (KAGPROP_TIMEDATEFUNCTIONS)|ODBC ドライバーでサポートされている時刻と日付の関数を示します。 このビットマスクで使用される関数名と関連する値の一覧については、ODBC のドキュメントの「 [付録 E: スカラー関数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)」を参照してください。|
|SQL 文法のサポート (KAGPROP_ODBCSQLCONFORMANCE)|ODBC ドライバーがサポートする SQL 文法を示します。|

## <a name="provider-specific-recordset-and-command-properties"></a>プロバイダー固有のレコードセットとコマンドのプロパティ
 OLE DB provider for ODBC では、**レコードセット**オブジェクトと**コマンド**オブジェクトの**properties**コレクションにいくつかのプロパティが追加されます。 次の表は、これらのプロパティをかっこで囲んで、対応する OLE DB プロパティ名を示しています。

|プロパティ名|説明|
|-------------------|-----------------|
|クエリベースの更新/削除/挿入 (KAGPROP_QUERYBASEDUPDATES)|SQL クエリを使用して、更新、削除、および挿入を実行できるかどうかを示します。|
|ODBC 同時実行の種類 (KAGPROP_CONCURRENCY)|2人のユーザーがデータソースから同じデータに同時にアクセスしようとした場合に発生する可能性のある問題を軽減するために使用される方法を示します。|
|順方向専用カーソルの BLOB アクセシビリティ (KAGPROP_BLOBSONFOCURSOR)|順方向専用カーソルを使用しているときに、BLOB **フィールド** にアクセスできるかどうかを示します。|
|QBU WHERE 句 (KAGPROP_INCLUDENONEXACT) に SQL_FLOAT、SQL_DOUBLE、および SQL_REAL を含める|SQL_FLOAT、SQL_DOUBLE、および SQL_REAL 値を QBU WHERE 句に含めることができるかどうかを示します。|
|挿入後の最後の行の位置 (KAGPROP_POSITIONONNEWROW)|新しいレコードがテーブルに挿入された後、テーブルの最後の行が現在の行になることを示します。|
|IRowsetChangeExtInfo (KAGPROP_IROWSETCHANGEEXTINFO)|**IRowsetChange**インターフェイスが拡張情報サポートを提供するかどうかを示します。|
|ODBC カーソルの種類 (KAGPROP_CURSOR)|**レコードセット**によって使用されるカーソルの種類を示します。|
|マーシャリング可能な行セットを生成する (KAGPROP_MARSHALLABLE)|ODBC ドライバーがマーシャリング可能なレコードセットを生成することを示します。|

## <a name="command-text"></a>コマンド テキスト
 [Command](../../reference/ado-api/command-object-ado.md)オブジェクトの使用方法は、データソースと、それが受け入れるクエリまたはコマンドステートメントの種類によって大きく異なります。

 ODBC には、ストアドプロシージャを呼び出すための特定の構文が用意されています。 **Command**オブジェクトの[commandtext](../../reference/ado-api/commandtext-property-ado.md)プロパティでは、 [Connection](../../reference/ado-api/connection-object-ado.md)オブジェクトの**Execute**メソッドの*commandtext*引数、または[Recordset](../../reference/ado-api/recordset-object-ado.md)オブジェクトの**Open**メソッドに対する*Source*引数は、次の構文で文字列を渡します。

```
"{ [ ? = ] call procedure [ ( ? [, ? [ , ... ]] ) ] }"
```

 各 **?** [Parameters](../../reference/ado-api/parameters-collection-ado.md)コレクション内のオブジェクトを参照します。 **まず、** 次の **パラメーター**(0) を参照し **ますか?** **パラメーター**(1) などを参照します。

 パラメーター参照は省略可能で、ストアドプロシージャの構造によって異なります。 パラメーターを定義しないストアドプロシージャを呼び出す場合、文字列は次のようになります。

```
"{ call procedure }"
```

 2つのクエリパラメーターがある場合、文字列は次のようになります。

```
"{ call procedure ( ?, ? ) }"
```

 ストアドプロシージャが値を返す場合、戻り値は別のパラメーターとして扱われます。 クエリパラメーターがなく、戻り値がある場合、文字列は次のようになります。

```
"{ ? = call procedure }"
```

 最後に、戻り値と2つのクエリパラメーターがある場合、文字列は次のようになります。

```
"{ ? = call procedure ( ?, ? ) }"
```

## <a name="recordset-behavior"></a>レコードセットの動作
 次の表は、このプロバイダーで開かれた **レコードセット** オブジェクトで使用できる標準の ADO メソッドとプロパティを示しています。

 プロバイダー構成の**レコードセット**の動作の詳細については、[サポート](../../reference/ado-api/supports-method.md)メソッドを実行し、**レコードセット**の**properties**コレクションを列挙して、プロバイダー固有の動的プロパティが存在するかどうかを判断します。

 標準の ADO **レコードセット** プロパティの可用性:

|プロパティ|ForwardOnly|動的|Keyset|静的|
|--------------|-----------------|-------------|------------|------------|
|[AbsolutePage](../../reference/ado-api/absolutepage-property-ado.md)|利用不可|利用不可|読み取り/書き込み|読み取り/書き込み|
|[AbsolutePosition](../../reference/ado-api/absoluteposition-property-ado.md)|利用不可|利用不可|読み取り/書き込み|読み取り/書き込み|
|[ActiveConnection](../../reference/ado-api/activeconnection-property-ado.md)|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|
|[BOF](../../reference/ado-api/bof-eof-properties-ado.md)|読み取り専用|読み取り専用|読み取り専用|読み取り専用|
|[ブックマーク](../../reference/ado-api/bookmark-property-ado.md)|利用不可|利用不可|読み取り/書き込み|読み取り/書き込み|
|[CacheSize](../../reference/ado-api/cachesize-property-ado.md)|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|
|[CursorLocation](../../reference/ado-api/cursorlocation-property-ado.md)|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|
|[CursorType](../../reference/ado-api/cursortype-property-ado.md)|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|
|[EditMode](../../reference/ado-api/editmode-property.md)|読み取り専用|読み取り専用|読み取り専用|読み取り専用|
|[Assert](../../reference/ado-api/filter-property.md)|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|
|[LockType](../../reference/ado-api/locktype-property-ado.md)|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|
|[MarshalOptions](../../reference/ado-api/marshaloptions-property-ado.md)|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|
|[数](../../reference/ado-api/maxrecords-property-ado.md)|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|
|[PageCount](../../reference/ado-api/pagecount-property-ado.md)|読み取り/書き込み|利用不可|読み取り専用|読み取り専用|
|[PageSize](../../reference/ado-api/pagesize-property-ado.md)|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|
|[RecordCount](../../reference/ado-api/recordcount-property-ado.md)|読み取り/書き込み|利用不可|読み取り専用|読み取り専用|
|[ソース](../../reference/ado-api/source-property-ado-recordset.md)|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|読み取り/書き込み|
|[State](../../reference/ado-api/state-property-ado.md)|読み取り専用|読み取り専用|読み取り専用|読み取り専用|
|[状態](../../reference/ado-api/status-property-ado-recordset.md)|読み取り専用|読み取り専用|読み取り専用|読み取り専用|

 [AbsolutePosition](../../reference/ado-api/absoluteposition-property-ado.md)プロパティと[AbsolutePage](../../reference/ado-api/absolutepage-property-ado.md)プロパティは、MICROSOFT OLE DB Provider for ODBC のバージョン1.0 で ADO が使用されている場合は書き込み専用です。

 標準の ADO **レコードセット** メソッドの可用性:

|方法|ForwardOnly|動的|Keyset|静的|
|------------|-----------------|-------------|------------|------------|
|[AddNew](../../reference/ado-api/addnew-method-ado.md)|はい|はい|はい|はい|
|[キャンセル](../../reference/ado-api/cancel-method-ado.md)|はい|はい|はい|はい|
|[CancelBatch](../../reference/ado-api/cancelbatch-method-ado.md)|はい|はい|はい|はい|
|[CancelUpdate](../../reference/ado-api/cancelupdate-method-ado.md)|はい|はい|はい|はい|
|[複製](../../reference/ado-api/clone-method-ado.md)|いいえ|いいえ|はい|はい|
|[閉じる](../../reference/ado-api/close-method-ado.md)|はい|はい|はい|はい|
|[削除](../../reference/ado-api/delete-method-ado-recordset.md)|はい|はい|はい|はい|
|[GetRows](../../reference/ado-api/getrows-method-ado.md)|はい|はい|はい|はい|
|[移動](../../reference/ado-api/move-method-ado.md)|はい|はい|はい|はい|
|[MoveFirst](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|はい|はい|はい|はい|
|[MoveLast](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|いいえ|はい|はい|はい|
|[MoveNext](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|はい|はい|はい|はい|
|[MovePrevious](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|いいえ|はい|はい|はい|
|[NextRecordset](../../reference/ado-api/nextrecordset-method-ado.md)*|はい|はい|はい|はい|
|[[ファイル]](../../reference/ado-api/open-method-ado-recordset.md)|はい|はい|はい|はい|
|[Requery](../../reference/ado-api/requery-method.md)|はい|はい|はい|はい|
|[再同期](../../reference/ado-api/resync-method.md)|いいえ|いいえ|はい|はい|
|[サポート](../../reference/ado-api/supports-method.md)|はい|はい|はい|はい|
|[アップデート](../../reference/ado-api/update-method.md)|はい|はい|はい|はい|
|[UpdateBatch](../../reference/ado-api/updatebatch-method.md)|はい|はい|はい|はい|

 * Microsoft Access データベースではサポートされていません。

## <a name="dynamic-properties"></a>動的プロパティ
 Microsoft OLE DB Provider for ODBC では、開かれていない[接続](../../reference/ado-api/connection-object-ado.md)、[レコードセット](../../reference/ado-api/recordset-object-ado.md)、および[コマンド](../../reference/ado-api/command-object-ado.md)オブジェクトの**properties**コレクションに動的なプロパティがいくつか挿入されます。

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
|Password|DBPROP_AUTH_PASSWORD|
|Ref アクセサーで渡す|DBPROP_BYREFACCESSORS|
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
 **レコードセット**オブジェクトの**properties**コレクションには、次のプロパティが追加されます。

|ADO プロパティ名|OLE DB プロパティ名|
|-----------------------|--------------------------|
|アクセス順序|DBPROP_ACCESSORDER|
|ブロッキングストレージオブジェクト|DBPROP_BLOCKINGSTORAGEOBJECTS|
|ブックマークの種類|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|挿入された行の変更|DBPROP_CHANGEINSERTEDROWS|
|列の特権|DBPROP_COLUMNRESTRICT|
|列セットの通知|DBPROP_NOTIFYCOLUMNSET|
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
|IRowsetResynch||
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
|一意の行|DBPROP_UNIQUEROWS|
|更新|DBPROP_UPDATABILITY|
|ブックマークを使用する|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>コマンドの動的プロパティ
 次のプロパティが、 **Command** オブジェクトの **properties** コレクションに追加されます。

|ADO プロパティ名|OLE DB プロパティ名|
|-----------------------|--------------------------|
|アクセス順序|DBPROP_ACCESSORDER|
|ブロッキングストレージオブジェクト|DBPROP_BLOCKINGSTORAGEOBJECTS|
|ブックマークの種類|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|挿入された行の変更|DBPROP_CHANGEINSERTEDROWS|
|列の特権|DBPROP_COLUMNRESTRICT|
|列セットの通知|DBPROP_NOTIFYCOLUMNSET|
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
|IRowsetResynch||
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
|削除されたブックマークをスキップ|DBPROP_BOOKMARKSKIP|
|厳密な行の Id|DBPROP_STRONGIDENTITY|
|更新|DBPROP_UPDATABILITY|
|ブックマークを使用する|DBPROP_BOOKMARKS|

 Microsoft OLE DB Provider for ODBC に関する特定の実装と機能に関する詳細については、MSDN の「データアクセスおよびストレージデベロッパーセンター [OLE DB](/previous-versions/windows/desktop/ms713643(v=vs.85)) 」 Web サイトを参照してください。

## <a name="see-also"></a>参照
 [Command Object (ado)](../../reference/ado-api/command-object-ado.md) [CommandText property](../../reference/ado-api/commandtext-property-ado.md) (ado) [Connection Object](../../reference/ado-api/connection-object-ado.md) (ado) [ConnectionString プロパティ (](../../reference/ado-api/connectionstring-property-ado.md) ado) [EXECUTE メソッド (ado コマンド)](../../reference/ado-api/execute-method-ado-command.md) [Open メソッド (ado Recordset)](../../reference/ado-api/open-method-ado-recordset.md) [Parameters collection](../../reference/ado-api/parameters-collection-ado.md) ( [ado)](../../reference/ado-api/provider-property-ado.md) Properties コレクション (ado) [Properties](../../reference/ado-api/properties-collection-ado.md) collection (ado) [recordset オブジェクト (](../../reference/ado-api/recordset-object-ado.md) ado) [Supports メソッド](../../reference/ado-api/supports-method.md)