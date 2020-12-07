---
description: SQLExtendedFetch 関数
title: SQLExtendedFetch 関数 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLExtendedFetch
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLExtendedFetch
helpviewer_keywords:
- SQLExtendedFetch function [ODBC]
ms.assetid: 940b5cf7-581c-4ede-8533-c67d5e9ef488
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ac19d017baf4a3f0e873be64cd2eb812ca1b05e0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476112"
---
# <a name="sqlextendedfetch-function"></a>SQLExtendedFetch 関数
**互換性**  
 導入されたバージョン: ODBC 1.0 標準準拠: 非推奨  
  
 **まとめ**  
 **SQLExtendedFetch** は、指定されたデータの行セットを結果セットからフェッチし、すべてのバインドされた列のデータを返します。 行セットは、絶対位置または相対位置またはブックマークによって指定できます。  
  
> [!NOTE]
>  ODBC 3.x で*は、* **SQLExtendedFetch** は **sqlfetchscroll**に置き換えられました。 ODBC 3 *. x* アプリケーションでは **SQLExtendedFetch**を呼び出さないでください。代わりに、 **Sqlfetchscroll**を呼び出す必要があります。 ODBC*2.x ドライバーを*使用する場合、ドライバーマネージャーは**Sqlfetchscroll**を**SQLExtendedFetch**にマップします。 ODBC 3.x*ドライバーは*、それを呼び出す odbc*2.x アプリケーションを*操作する場合、 **SQLExtendedFetch**をサポートする必要があります。 詳細については、「付録 G: 旧バージョンとの互換性のためのドライバーガイドライン」の「コメント」、 [ブロックカーソル、スクロール可能なカーソル、および旧バージョンとの互換性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) に関する説明を参照してください。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLExtendedFetch(  
      SQLHSTMT         StatementHandle,  
      SQLUSMALLINT     FetchOrientation,  
      SQLLEN           FetchOffset,  
      SQLULEN *        RowCountPtr,  
      SQLUSMALLINT *   RowStatusArray);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル。  
  
 *FetchOrientation*  
 代入フェッチの種類。 これは、 **Sqlfetchscroll**の*fetchorientation*と同じです。  
  
 *FetchOffset*  
 代入フェッチする行の番号。 これは、 **Sqlfetchscroll**の*fetchoffset*と同じですが、1つの例外があります。 *Fetchorientation*が SQL_FETCH_BOOKMARK 場合、 *fetchorientation*は、ブックマークからのオフセットではなく、固定長のブックマークです。 言い換えると、 **SQLExtendedFetch** は、SQL_ATTR_FETCH_BOOKMARK_PTR statement 属性ではなく、この引数からブックマークを取得します。 可変長のブックマークはサポートされておらず、ブックマークからのオフセット (0 以外) での行セットのフェッチはサポートされていません。  
  
 *RowCountPtr*  
 Output実際にフェッチされた行の数を返すバッファーへのポインター。 このバッファーは、SQL_ATTR_ROWS_FETCHED_PTR statement 属性によって指定されたバッファーと同じ方法で使用されます。 このバッファーは、 **SQLExtendedFetch**によってのみ使用されます。 **Sqlfetch**または**sqlfetchscroll**では使用されません。  
  
 *RowStatusArray*  
 Output各行の状態を返す配列へのポインター。 この配列は、SQL_ATTR_ROW_STATUS_PTR statement 属性によって指定された配列と同じ方法で使用されます。  
  
 ただし、この配列のアドレスは、IRD の SQL_DESC_STATUS_ARRAY_PTR フィールドに格納されていません。 さらに、この配列は、 **SQLExtendedFetch**によって、または**SQLExtendedFetch**の後に呼び出されたときに SQL_ADD または**SQLSetPos**操作を伴う**sqlbulkoperations**によってのみ使用されます。 *Operation* **Sqlfetch**または**sqlfetchscroll**では使用されません。 **Sqlfetch**または**sqlfetchscroll**の後に呼び出された場合、 **sqlbulkoperations**または**SQLSetPos**では使用されません。 また、fetch 関数が呼び出される前に、SQL_ADD*操作*を伴う**sqlbulkoperations**が呼び出された場合にも使用されません。 つまり、ステートメントの状態 S7 でのみ使用されます。 ステートメントの状態 S5 または S6 では使用されません。 詳細については、「付録 B: ODBC 状態遷移テーブル」の「 [ステートメントの遷移](../../../odbc/reference/appendixes/statement-transitions.md) 」を参照してください。  
  
 アプリケーションでは、 *Rowstatusarray*引数に有効なポインターを指定する必要があります。それ以外の場合、 **SQLExtendedFetch**の動作と、カーソルが**SQLExtendedFetch**によって配置された後の**Sqlbulkoperations**または**SQLSetPos**の動作は未定義になります。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **SQLExtendedFetch**が SQL_ERROR または SQL_SUCCESS_WITH_INFO のいずれかを返す場合は、 **SQLError**を呼び出すことによって、関連付けられた SQLSTATE 値を取得できます。 次の表に、 **SQLExtendedFetch** によって一般的に返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。 1つの列でエラーが発生した場合は、エラーが発生した列を特定するために、SQL_DIAG_COLUMN_NUMBER の*DiagIdentifier*を使用して**SQLGetDiagField**を呼び出すことができます。および**SQLGetDiagField**は、その列を含む行を判断するために、SQL_DIAG_ROW_NUMBER の*DiagIdentifier*を使用して呼び出すことができます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データ、右側が切り捨てられました|列に対して返された文字列またはバイナリデータにより、空白以外の文字または NULL 以外のバイナリデータが切り捨てられました。 文字列値の場合は、右側が切り捨てられました。 数値の場合は、数値の小数部が切り捨てられています。  (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01S01|行にエラーがあります|1つ以上の行をフェッチ中にエラーが発生しました。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01S06|結果セットが最初の行セットを返した前にフェッチしようとしました|要求された行セットは、現在の位置が最初の行を超えた場合に、結果セットの先頭に重なっています。また、 *Fetchorientation* が SQL_PRIOR であるか、 *fetchorientation* が、負の値が現在の SQL_ROWSET_SIZE 以下である負の *fetchorientation* で SQL_RELATIVE でした。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01S07|小数部の切り捨て|列に対して返されたデータが切り捨てられました。 数値データ型の場合、数値の小数部は切り捨てられました。 時間、タイムスタンプ、および期間のデータ型については、時刻の部分が切り捨てられました。<br /><br /> (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|07006|制限されたデータ型の属性違反|**SQLBindCol**の*TargetType*によって指定された C データ型にデータ値を変換できませんでした。|  
|07009|無効な記述子のインデックス|列0は **SQLBindCol**にバインドされており、SQL_ATTR_USE_BOOKMARKS statement 属性が SQL_UB_OFF に設定されています。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続されていたデータソースとの間の通信リンクが失敗しました。|  
|22002|インジケーター変数が必要ですが、指定されていません|**SQLBindCol**によって設定された*StrLen_or_IndPtr*が null ポインターである列に null データがフェッチされました。<br /><br /> (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|22003|数値が有効範囲にありません|1つ以上の列に対して数値または文字列として数値または文字列として数値を返すと、切り捨てられる数値の一部 (小数部分ではなく) が発生する可能性があります。<br /><br /> (関数は SQL_SUCCESS_WITH_INFO を返します)。<br /><br /> 詳細については、「付録 D: データ型」の「 [間隔と数値データ型のガイドライン](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md) 」を参照してください。|  
|22007|無効な datetime 形式|結果セットの文字列が日付、時刻、またはタイムスタンプ C 構造体にバインドされました。列の値は、それぞれ無効な日付、時刻、またはタイムスタンプです。<br /><br /> (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|22012|0による除算|算術式からの値が返されました。この結果、0による除算が行われました。<br /><br /> (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|22015|間隔フィールドオーバーフロー|数値または期間の SQL 型から範囲 C 型への割り当てにより、先頭のフィールドの有効桁数が失われました。<br /><br /> データを interval C 型にフェッチする場合、interval C 型の SQL 型の値は表現されませんでした。<br /><br /> (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|22018|キャストの指定に無効な文字値があります|C 型は、正確な数値、概数、datetime、または interval データ型でした。列の SQL 型は文字データ型でした。列の値が、バインドされた C 型の有効なリテラルではありませんでした。<br /><br /> (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|24000|カーソル状態が無効|*StatementHandle*は実行状態でしたが、結果セットが*StatementHandle*に関連付けられていませんでした。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * \* Messagetext*バッファーの**SQLError**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|*StatementHandle*に対して非同期処理が有効になりました。 関数が呼び出され、実行が完了する前に、 **SQLCancel** または **Sqlcancelhandle** が *StatementHandle*で呼び出された後、 *StatementHandle*で関数が再度呼び出されました。<br /><br /> 関数が呼び出され、実行が完了する前に、マルチスレッドアプリケーションの別のスレッドの*StatementHandle*で**SQLCancel**または**sqlcancelhandle**が呼び出されました。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、 **SQLExtendedFetch** 関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または **Sqlmoreresults** が *StatementHandle* に対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。<br /><br /> (DM) 指定された *StatementHandle* は実行状態ではありませんでした。 最初に **SQLExecDirect**、 **sqlexecute**、またはカタログ関数を呼び出さずに関数が呼び出されました。<br /><br /> (DM) 非同期的に実行されている関数 (この1つではない) が *StatementHandle* に対して呼び出され、この関数が呼び出されたときにまだ実行されています。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **Sqlbulkoperations**、 **SQLSetPos** が *StatementHandle* に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。<br /><br /> (DM) **SQLExtendedFetch**は、 **sqlfetch**または**sqlfetchscroll**が呼び出された後、および SQL_CLOSE オプションを使用して**SQLFreeStmt**が呼び出される前に、 *StatementHandle*に対して呼び出されました。<br /><br /> (DM) **Sqlbulkoperations**が、 **sqlfetch**、 **Sqlbulkoperations**、または**SQLExtendedFetch**が呼び出される前にステートメントに対して呼び出された後、 **SQLFreeStmt**が SQL_CLOSE 呼び出される前に**SQLExtendedFetch**が呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY106|フェッチの型が範囲を超えています|(DM) 引数 *Fetchorientation* に指定された値が無効でした。 (「コメント」を参照してください)。<br /><br /> 引数 *Fetchorientation* が SQL_FETCH_BOOKMARK、SQL_ATTR_USE_BOOKMARKS statement 属性が SQL_UB_OFF に設定されました。<br /><br /> SQL_CURSOR_TYPE statement オプションの値が SQL_CURSOR_FORWARD_ONLY ましたが、引数 *Fetchorientation* の値が SQL_FETCH_NEXT いませんでした。<br /><br /> 引数 *Fetchorientation* が SQL_FETCH_RESUME でした。|  
|HY107|行の値が有効範囲にありません|SQL_CURSOR_TYPE statement オプションで指定された値が SQL_CURSOR_KEYSET_DRIVEN ましたが、SQL_KEYSET_SIZE statement 属性で指定された値は、0より大きく、SQL_ROWSET_SIZE statement 属性で指定された値よりも小さくなっています。|  
|HY111|ブックマークの値が無効です|引数 *Fetchorientation* が SQL_FETCH_BOOKMARK、 *fetchorientation* 引数で指定されたブックマークが有効ではありませんでした。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYC00|省略可能な機能は実装されていません|ドライバーまたはデータソースは、指定されたフェッチの種類をサポートしていません。<br /><br /> ドライバーまたはデータソースが、 **SQLBindCol**の*TargetType*と対応する列の SQL データ型の組み合わせによって指定された変換をサポートしていません。 このエラーは、列の SQL データ型がドライバー固有の SQL データ型にマップされている場合にのみ適用されます。|  
|HYT00|タイムアウトに達しました|データソースから結果セットが返される前に、クエリのタイムアウト期間が経過しました。 タイムアウト期間は、 **SQLSetStmtOption**、SQL_QUERY_TIMEOUT によって設定されます。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle* に関連付けられているドライバーでは、関数はサポートされていません。|  
  
## <a name="comments"></a>コメント  
 **SQLExtendedFetch**の動作は、 **sqlfetchscroll**と同じですが、次のような例外があります。  
  
-   **SQLExtendedFetch** と **sqlfetchscroll** では、異なるメソッドを使用して、フェッチされた行の数を返します。 **SQLExtendedFetch**は、 * \* rowcountptr*; でフェッチされた行の数を返します。**Sqlfetchscroll**は、SQL_ATTR_ROWS_FETCHED_PTR が指すバッファーに直接フェッチされた行の数を返します。 詳細については、 *Rowcountptr* 引数を参照してください。  
  
-   **SQLExtendedFetch** と **sqlfetchscroll** は、異なる配列の各行の状態を返します。 詳細については、 *Rowstatusarray* 引数を参照してください。  
  
-   **SQLExtendedFetch** と **sqlfetchscroll** では、 *fetchorientation* が SQL_FETCH_BOOKMARK ときにブックマークを取得するために別の方法を使用します。 **SQLExtendedFetch** は、可変長のブックマークをサポートしていないか、ブックマークから0以外のオフセットで行セットをフェッチしていません。 詳細については、 *Fetchoffset* 引数を参照してください。  
  
-   **SQLExtendedFetch** と **sqlfetchscroll** では、異なる行セットサイズが使用されます。 **SQLExtendedFetch** は SQL_ROWSET_SIZE statement 属性の値を使用し、 **sqlfetchscroll** は SQL_ATTR_ROW_ARRAY_SIZE statement 属性の値を使用します。  
  
-   **SQLExtendedFetch** には、 **sqlfetchscroll**とは少し異なるエラー処理セマンティクスがあります。 詳細については、「 [Sqlfetchscroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)」の「コメント」セクションの「エラー処理」を参照してください。  
  
-   **SQLExtendedFetch** では、バインドオフセット (SQL_ATTR_ROW_BIND_OFFSET_PTR statement 属性) はサポートされていません。  
  
-   **SQLExtendedFetch**への呼び出しを**Sqlfetch**または**sqlfetchscroll**の呼び出しと混在させることはできません。また、fetch 関数が呼び出される前に**sqlbulkoperation**を呼び出すと、カーソルを閉じて再度開くまで、 **SQLExtendedFetch**を呼び出すことはできません。 つまり、 **SQLExtendedFetch** は、ステートメント状態 S7 でのみ呼び出すことができます。 詳細については、「付録 B: ODBC 状態遷移テーブル」の「 [ステートメントの遷移](../../../odbc/reference/appendixes/statement-transitions.md) 」を参照してください。  
  
 ODBC*2.x ドライバーを*使用しているときにアプリケーションが**sqlfetchscroll**を呼び出すと、ドライバーマネージャーはこの呼び出しを**SQLExtendedFetch**にマップします。 詳細については、 [「sqlfetchscroll」の「](../../../odbc/reference/syntax/sqlfetchscroll-function.md)sqlfetchscroll および ODBC*2.x ドライバー」* を参照してください。  
  
 ODBC 2.x で*は、複数*の行をフェッチするために **SQLExtendedFetch** が呼び出され、1つの行をフェッチするために **sqlfetch** が呼び出されました。 一方、ODBC 3.x で*は、* **sqlfetch** を呼び出して複数の行をフェッチすることができます。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|結果セット内の列へのバッファーのバインド|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|一括挿入、更新、または削除操作の実行|[SQLBulkOperations 関数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|ステートメント処理の取り消し|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|結果セットの列に関する情報を返す|[SQLDescribeCol 関数](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|SQL ステートメントの実行|[SQLExecDirect 関数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|準備された SQL ステートメントの実行|[SQLExecute 関数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|結果セットの列数を返す|[SQLNumResultCols 関数](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|カーソルの配置、行セット内のデータの更新、または結果セット内のデータの更新または削除|[SQLSetPos 関数](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|ステートメント属性の設定|[SQLSetStmtAttr 関数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
