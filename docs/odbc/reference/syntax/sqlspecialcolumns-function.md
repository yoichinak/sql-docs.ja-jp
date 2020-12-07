---
description: SQLSpecialColumns 関数
title: Sql特殊列関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSpecialColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSpecialColumns
helpviewer_keywords:
- SQLSpecialColumns function [ODBC]
ms.assetid: bb2d9f21-bda0-4e50-a8be-f710db660034
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca29bf8bbef30296ad1aef17bda6890b23da8fb4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476068"
---
# <a name="sqlspecialcolumns-function"></a>SQLSpecialColumns 関数
**互換性**  
 導入されたバージョン: ODBC 1.0 標準準拠: グループを開く  
  
 **まとめ**  
 **Sqlの列** は、指定されたテーブル内の列に関する次の情報を取得します。  
  
-   テーブル内の行を一意に識別する、最適な列のセット。  
  
-   行の任意の値がトランザクションによって更新されたときに自動的に更新される列。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLSpecialColumns(  
     SQLHSTMT      StatementHandle,  
     SQLSMALLINT   IdentifierType,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     TableName,  
     SQLSMALLINT   NameLength3,  
     SQLSMALLINT   Scope,  
     SQLSMALLINT   Nullable);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル。  
  
 *IdentifierType*  
 代入返される列の型。 次のいずれかの値を指定する必要があります。  
  
 SQL_BEST_ROWID: 1 つまたは複数の列から値を取得することによって、指定されたテーブル内の任意の行を一意に識別できる、最適な列または列のセットを返します。 列には、この目的のために特別に設計された疑似列 (Oracle ROWID や Ingres TID など)、またはテーブルの一意インデックスの1つまたは複数の列を指定できます。  
  
 SQL_ROWVER: 任意のトランザクションで (SQLBase ROWID または Sybase TIMESTAMP と同様に) 更新された場合に、データソースによって自動的に更新される、指定されたテーブル内の列がある場合は、その列を返します。  
  
 *CatalogName*  
 代入テーブルのカタログ名。 ドライバーが一部のテーブルのカタログをサポートしていても、他のテーブルではサポートされていない場合 (ドライバーが異なる Dbms からデータを取得する場合など)、空の文字列 ("") は、カタログを持たないテーブルを表します。 *CatalogName* に文字列検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *CatalogName* は識別子として扱われ、大文字小文字は区別されません。 SQL_FALSE の場合、 *CatalogName* は通常の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。 詳細については、「 [カタログ関数の引数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)」を参照してください。  
  
 *NameLength1*  
 代入**CatalogName*の文字数。  
  
 *SchemaName*  
 代入テーブルのスキーマ名。 ドライバーがいくつかのテーブルのスキーマをサポートしていても、他のテーブルのスキーマをサポートしていない場合 (ドライバーが異なる Dbms からデータを取得する場合など)、空の文字列 ("") はスキーマを持たないテーブルを表します。 *SchemaName* に文字列検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *SchemaName* は識別子として扱われ、大文字小文字は区別されません。 SQL_FALSE の場合、 *SchemaName* は通常の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。  
  
 *NameLength2*  
 代入**SchemaName*の文字数。  
  
 *TableName*  
 代入テーブル名。 この引数を null ポインターにすることはできません。 *TableName* に文字列検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *TableName* は識別子として扱われ、その大文字と小文字は区別されません。 SQL_FALSE の場合、 *TableName* は通常の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。  
  
 *NameLength3*  
 代入**TableName*の長さ (文字数)。  
  
 *スコープ*  
 代入Rowid の最低限必要なスコープ。 返された rowid の範囲がより大きくなる可能性があります。 次のいずれかである必要があります。  
  
 SQL_SCOPE_CURROW: rowid は、その行に位置している場合にのみ有効であることが保証されます。 後で rowid を使用して再選択すると、行が別のトランザクションによって更新または削除された場合に、行が返されない可能性があります。  
  
 SQL_SCOPE_TRANSACTION: rowid は、現在のトランザクションの期間中は有効であることが保証されます。  
  
 SQL_SCOPE_SESSION: rowid は、(トランザクションの境界を越えて) セッションが継続している間は有効であることが保証されます。  
  
 *NULL 値の使用*  
 代入NULL 値を持つことができる特殊な列を返すかどうかを決定します。 次のいずれかである必要があります。  
  
 SQL_NO_NULLS: NULL 値を持つことができる特殊な列を除外します。 一部のドライバーでは SQL_NO_NULLS がサポートされていません。 SQL_NO_NULLS が指定されている場合、これらのドライバーは空の結果セットを返します。 この場合はアプリケーションを準備し、必要な場合にのみ SQL_NO_NULLS 要求します。  
  
 SQL_NULLABLE: NULL 値を持つことができる場合でも、特殊な列を返します。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **SqlSQLGetDiagRec**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合、関連付けられた SQLSTATE 値を取得するには、 *Handletype* SQL_HANDLE_STMT と*StatementHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出します。 次の表は、通常 **Sqlの列** によって返される SQLSTATE 値の一覧です。この関数のコンテキストでは、それぞれについて説明しています。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続されていたデータソースとの間の通信リンクが失敗しました。|  
|24000|カーソル状態が無効|*StatementHandle*でカーソルが開かれました。 **sqlfetch**または**sqlfetchscroll**が呼び出されました。 このエラーは、sqlfetch または**Sqlfetchscroll**が SQL_NO_DATA 返されず、 **Sqlfetch**または**sqlfetchscroll**が SQL_NO_DATA を返した場合にドライバーによって返され**た場合に**、ドライバーマネージャーによって返されます。<br /><br /> *StatementHandle*でカーソルが開いていましたが、 **sqlfetch**または**sqlfetchscroll**が呼び出されていません。|  
|40001|シリアル化エラー|リソースが別のトランザクションでデッドロックしているため、トランザクションがロールバックされました。|  
|40003|ステートメントの完了が不明です|この関数の実行中に関連付けられた接続に失敗しました。トランザクションの状態を確認できません。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * \* Messagetext*バッファーの**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|*StatementHandle*に対して非同期処理が有効になりました。 関数が呼び出され、実行が完了する前に、 **SQLCancel** または **Sqlcancelhandle** が *StatementHandle*で呼び出されました。 次に、 *StatementHandle*で関数が再度呼び出されました。<br /><br /> 関数が呼び出され、実行が完了する前に、マルチスレッドアプリケーションの別のスレッドの*StatementHandle*で**SQLCancel**または**sqlcancelhandle**が呼び出されました。|  
|HY009|Null ポインターの使い方が正しくありません|*TableName*引数が null ポインターでした。<br /><br /> SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されました。 *CatalogName* 引数は null ポインターで、SQL_CATALOG_NAME *InfoType* はカタログ名がサポートされていることを返します。<br /><br /> (DM) SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定され、 *SchemaName* 引数が null ポインターでした。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 **Sqlの列**が呼び出されたときに、この関数はまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または **Sqlmoreresults** が *StatementHandle* に対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。<br /><br /> (DM) 非同期的に実行されている関数 (この1つではない) が *StatementHandle* に対して呼び出され、この関数が呼び出されたときにまだ実行されています。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **Sqlbulkoperations**、 **SQLSetPos** が *StatementHandle* に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY090|文字列またはバッファーの長さが無効です|(DM) 長さの引数の1つの値が0未満ですが SQL_NTS と等しくありません。<br /><br /> 長さの引数の1つの値が、対応する名前の最大長の値を超えました。 各名前の最大長は、SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN、または SQL_MAX_TABLE_NAME_LEN の*InfoType*値を指定して**SQLGetInfo**を呼び出すことによって取得できます。|  
|HY097|列の型が有効範囲にありません|(DM) 無効な *Identifiertype* 値が指定されました。|  
|HY098|スコープの型が有効範囲にありません|(DM) 無効な *スコープ* 値が指定されました。|  
|HY099|Null 許容型が有効範囲にありません|(DM) 無効な *Null 許容* 値が指定されました。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYC00|省略可能な機能は実装されていません|カタログが指定されましたが、ドライバーまたはデータソースがカタログをサポートしていません。<br /><br /> スキーマが指定されましたが、ドライバーまたはデータソースがスキーマをサポートしていません。<br /><br /> SQL_ATTR_CONCURRENCY および SQL_ATTR_CURSOR_TYPE statement 属性の現在の設定の組み合わせは、ドライバーまたはデータソースではサポートされていませんでした。<br /><br /> SQL_ATTR_USE_BOOKMARKS statement 属性が SQL_UB_VARIABLE に設定されており、SQL_ATTR_CURSOR_TYPE statement 属性が、ドライバーがブックマークをサポートしていないカーソルの種類に設定されました。|  
|HYT00|タイムアウトに達しました|データソースが要求された結果セットを返す前に、クエリのタイムアウト期間が経過しました。 タイムアウト期間は、 **SQLSetStmtAttr**、SQL_ATTR_QUERY_TIMEOUT によって設定されます。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle* に関連付けられているドライバーでは、関数はサポートされていません。|  
|IM017|非同期通知モードでは、ポーリングは無効になっています|通知モデルが使用されるたびに、ポーリングは無効になります。|  
|IM018|**Sqlcompleteasync** は、このハンドルで前の非同期操作を完了するために呼び出されていません。|ハンドルに対する前の関数呼び出しが SQL_STILL_EXECUTING を返し、通知モードが有効になっている場合は、処理を完了するために、ハンドルに対して **Sqlcompleteasync** を呼び出す必要があります。|  
  
## <a name="comments"></a>コメント  
 *Identifiertype*引数を SQL_BEST_ROWID すると、テーブル内の各行を一意に識別する1つまたは複数の列が**sql特殊列**から返されます。 これらの列は、常に *選択リスト* または **WHERE** 句で使用できます。 テーブルの列に関するさまざまな情報を返すために使用される**Sqlcolumns**は、各行を一意に識別する列、または行のいずれかの値がトランザクションによって更新されたときに自動的に更新される列を返すとは限りません。 たとえば、 **Sqlcolumns** は、Oracle 擬似列 ROWID を返さない場合があります。 このため、これらの列を返すために **sqlの列** が使用されています。 詳細については、「 [カタログデータの使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)」を参照してください。  
  
> [!NOTE]  
>  一般的な使用、引数、および ODBC カタログ関数の返されるデータの詳細については、「 [カタログ関数](../../../odbc/reference/develop-app/catalog-functions.md)」を参照してください。  
  
 テーブル内の各行を一意に識別する列がない場合、 **Sqlの列** は行のない行セットを返します。その後、ステートメントで **sqlfetch** または **sqlfetchscroll** を呼び出すと SQL_NO_DATA が返されます。  
  
 *Identifiertype*、 *Scope*、または*Nullable*の各引数で、データソースでサポートされていない特性が指定されている場合、 **sqlspecialcolumns**は空の結果セットを返します。  
  
 SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *CatalogName*、 *SchemaName*、および *TableName* の各引数は識別子として扱われるので、特定の状況で null ポインターに設定することはできません。 (詳細については、「 [カタログ関数の引数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)」を参照してください)。  
  
 **Sqlて列** を指定すると、結果が標準の結果セットとして、スコープ別に並べ替えられて返されます。  
  
 ODBC *3. x*では、次の列の名前が変更されました。 アプリケーションは列番号でバインドされるため、列名の変更は旧バージョンとの互換性に影響しません。  
  
|ODBC 2.0 列|ODBC *3. x* 列|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
  
 COLUMN_NAME の列の実際の長さを判断するために、アプリケーションは SQL_MAX_COLUMN_NAME_LEN オプションを使用して **SQLGetInfo** を呼び出すことができます。  
  
 次の表に、結果セット内の列の一覧を示します。 列 8 (PSEUDO_COLUMN) 以外の列は、ドライバーで定義できます。 アプリケーションでは、明示的な序数位置を指定するのではなく、結果セットの末尾からカウントすることで、ドライバー固有の列にアクセスする必要があります。 詳細については、「 [カタログ関数によって返されるデータ](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)」を参照してください。  
  
|列名|列番号|データ型|コメント|  
|-----------------|-------------------|---------------|--------------|  
|スコープ (ODBC 1.0)|1|Smallint|Rowid の実際のスコープ。 次のいずれかの値が含まれます。<br /><br /> SQL_SCOPE_CURROW SQL_SCOPE_TRANSACTION SQL_SCOPE_SESSION<br /><br /> *Identifiertype*が SQL_ROWVER 場合、NULL が返されます。 各値の説明については、このセクションで前述した「構文」の *スコープ* の説明を参照してください。|  
|COLUMN_NAME (ODBC 1.0)|2|Varchar not NULL|列名。 ドライバーは、名前のない列に対して空の文字列を返します。|  
|DATA_TYPE (ODBC 1.0)|3|Smallint (NULL 以外)|SQL データ型。 ODBC SQL データ型またはドライバー固有の SQL データ型を指定できます。 有効な ODBC SQL データ型の一覧については、「 [Sql データ型](../../../odbc/reference/appendixes/sql-data-types.md)」を参照してください。 ドライバー固有の SQL データ型の詳細については、ドライバーのドキュメントを参照してください。|  
|TYPE_NAME (ODBC 1.0)|4|Varchar not NULL|データソースに依存するデータ型の名前。たとえば、"CHAR"、"VARCHAR"、"MONEY"、"LONG VARBINARY"、"CHAR () FOR BIT DATA" などです。|  
|COLUMN_SIZE (ODBC 1.0)|5|Integer|データソース上の列のサイズ。 列のサイズの詳細については、「 [列のサイズ、10進数、転送オクテットの長さ、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)」を参照してください。|  
|BUFFER_LENGTH (ODBC 1.0)|6|Integer|SQL_C_DEFAULT が指定されている場合に、 **SQLGetData** または **sqlfetch** 操作で転送されるデータのバイト単位の長さ。 数値データの場合、このサイズは、データソースに格納されているデータのサイズとは異なる場合があります。 この値は、文字またはバイナリデータの COLUMN_SIZE 列と同じです。 詳細については、「 [列のサイズ、10進数、転送オクテットの長さ、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)」を参照してください。|  
|DECIMAL_DIGITS (ODBC 1.0)|7|Smallint|データソース上の列の小数点以下の桁数。 10進数が適用されないデータ型に対しては NULL が返されます。 10進数の詳細については、「 [列のサイズ、10進数、転送オクテットの長さ、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)」を参照してください。|  
|PSEUDO_COLUMN (ODBC 2.0)|8|Smallint|列が、Oracle ROWID などの疑似列であるかどうかを示します。<br /><br /> SQL_PC_UNKNOWN SQL_PC_NOT_PSEUDO SQL_PC_PSEUDO **メモ:**  相互運用性を最大にするには、 **SQLGetInfo**によって返される識別子引用符文字で擬似列を引用符で囲む必要があります。|  
  
 アプリケーションで SQL_BEST_ROWID の値を取得すると、アプリケーションはこれらの値を使用して、定義されたスコープ内でその行を再選択できます。 **SELECT**ステートメントは、行も1行も返されないことが保証されています。  
  
 アプリケーションで rowid 列または列に基づいて行が選択され、その行が見つからない場合、アプリケーションでは、行が削除されたか、rowid 列が変更されたと見なすことができます。 逆の場合は、rowid が変更されていない場合でも、行の他の列が変更されている可能性があります。  
  
 列型 SQL_BEST_ROWID に対して返される列は、一連の行から最新のデータを取得するために、結果セット内を前後にスクロールする必要があるアプリケーションに役立ちます。 Rowid の列は、その行に位置している間は変更されないことが保証されています。  
  
 カーソルが行に配置されていない場合でも、rowid の列が有効なままになることがあります。アプリケーションでは、結果セット内のスコープ列をチェックすることによって、このことを判断できます。  
  
 列型 SQL_ROWVER に対して返される列は、rowid を使用して行を再度実行したときに、特定の行の列が更新されたかどうかを確認する機能を必要とするアプリケーションに役立ちます。 たとえば、rowid を使用して行を再度実行した後、アプリケーションは、SQL_ROWVER の列の以前の値を、フェッチしたものと比較することができます。 SQL_ROWVER 列の値が前の値と異なる場合、アプリケーションは、表示上のデータが変更されたことをユーザーに警告できます。  
  
## <a name="code-example"></a>コード例  
 同様の関数のコード例については、「 [Sqlcolumns](../../../odbc/reference/syntax/sqlcolumns-function.md)」を参照してください。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|結果セット内の列へのバッファーのバインド|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|ステートメント処理の取り消し|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|テーブル内の列を返す|[SQLColumns 関数](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|1つの行またはデータのブロックを順方向専用にフェッチする|[SQLFetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|データのブロックのフェッチまたは結果セットのスクロール|[SQLFetchScroll 関数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|主キーの列を返す|[SQLPrimaryKeys 関数](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
