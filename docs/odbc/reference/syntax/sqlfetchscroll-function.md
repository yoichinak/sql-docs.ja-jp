---
description: SQLFetchScroll 関数
title: SQLFetchScroll 関数 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFetchScroll
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLFetchScroll
helpviewer_keywords:
- SQLFetchScroll function [ODBC]
ms.assetid: c0243667-428c-4dda-ae91-3c307616a1ac
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e3c725e11c889765c18c2ff14625b6bde4705051
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476087"
---
# <a name="sqlfetchscroll-function"></a>SQLFetchScroll 関数
**互換性**  
 導入されたバージョン: ODBC 3.0 標準準拠: ISO 92  
  
 **まとめ**  
 **Sqlfetchscroll** は、指定されたデータの行セットを結果セットからフェッチし、すべてのバインドされた列のデータを返します。 行セットは、絶対位置または相対位置またはブックマークによって指定できます。  
  
 ODBC 2.x ドライバーを使用する場合、ドライバーマネージャーはこの関数を **SQLExtendedFetch**にマップします。 詳細については、「 [アプリケーションの旧バージョンとの互換性のための置換関数のマッピング](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLFetchScroll(  
      SQLHSTMT      StatementHandle,  
      SQLSMALLINT   FetchOrientation,  
      SQLLEN        FetchOffset);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル。  
  
 *FetchOrientation*  
 代入  
  
 フェッチの種類:  
  
 SQL_FETCH_NEXT  
  
 SQL_FETCH_PRIOR  
  
 SQL_FETCH_FIRST  
  
 SQL_FETCH_LAST  
  
 SQL_FETCH_ABSOLUTE  
  
 SQL_FETCH_RELATIVE  
  
 SQL_FETCH_BOOKMARK  
  
 詳細については、「コメント」セクションの「カーソルの配置」を参照してください。  
  
 *FetchOffset*  
 代入  
  
 フェッチする行の番号。 この引数の解釈は、 *Fetchorientation* 引数の値によって異なります。 詳細については、「コメント」セクションの「カーソルの配置」を参照してください。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **Sqlfetchscroll**が SQL_ERROR または SQL_SUCCESS_WITH_INFO のいずれかを返す場合、関連付けられた SQLSTATE 値を取得するには、handletype を SQL_HANDLE_STMT、StatementHandle のハンドルを指定して**SQLGetDiagRec**を呼び出します。 次の表に、 **Sqlfetchscroll** によって一般的に返される SQLSTATE 値の一覧を示し、この関数のコンテキストでそれぞれについて説明します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。 1つの列でエラーが発生した場合は、エラーが発生した列を特定するために、SQL_DIAG_COLUMN_NUMBER の DiagIdentifier を使用して **SQLGetDiagField** を呼び出すことができます。および **SQLGetDiagField** は、その列を含む行を判断するために、SQL_DIAG_ROW_NUMBER の DiagIdentifier を使用して呼び出すことができます。  
  
 SQL_SUCCESS_WITH_INFO または SQL_ERROR を返すことができるすべての SQLSTATEs (01xxx SQLSTATEs を除く) では、複数行操作のすべての行ではなく、1つ以上の行でエラーが発生した場合に SQL_SUCCESS_WITH_INFO が返され、単一行操作でエラーが発生した場合は SQL_ERROR が返されます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データ、右側が切り捨てられました|列に対して返された文字列またはバイナリデータにより、空白以外の文字または NULL 以外のバイナリデータが切り捨てられました。 文字列値の場合は、右側が切り捨てられました。|  
|01S01|行にエラーがあります|1つ以上の行をフェッチ中にエラーが発生しました。<br /><br /> (Odbc*2.x アプリケーションが* odbc 2.x ドライバーで動作しているときにこの SQLSTATE が返された場合は、無視してかまい*ません)* 。|  
|01S06|結果セットが最初の行セットを返した前にフェッチしようとしました|要求された行セットは、FetchOrientation が SQL_FETCH_PRIOR、現在の位置が最初の行を超えており、現在の行の数が行セットのサイズ以下である場合に、結果セットの先頭に重なっています。<br /><br /> 要求された行セットは、FetchOrientation が SQL_FETCH_PRIOR、現在の位置が結果セットの末尾を超えており、行セットのサイズが結果セットのサイズを超えている場合に、結果セットの先頭に重なっています。<br /><br /> 要求された行セットは、FetchOrientation が SQL_FETCH_RELATIVE、Fetchorientation が負で、Fetchorientation の絶対値が行セットのサイズ以下である場合に、結果セットの先頭に重なっています。<br /><br /> 要求された行セットは、FetchOrientation が SQL_FETCH_ABSOLUTE、Fetchorientation が負の値、および Fetchorientation の絶対値が、結果セットのサイズよりも大きく、行セットのサイズ以下である場合に、結果セットの先頭に重なっています。<br /><br /> (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01S07|小数部の切り捨て|列に対して返されたデータが切り捨てられました。 数値データ型の場合、数値の小数部は切り捨てられました。 時間、タイムスタンプ、および期間のデータ型については、時刻の部分が切り捨てられました。<br /><br /> (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|07006|制限されたデータ型の属性違反|結果セットの列のデータ値を、 **SQLBindCol**の*TargetType*によって指定されたデータ型に変換できませんでした。<br /><br /> 列0は SQL_C_BOOKMARK のデータ型にバインドされており、SQL_ATTR_USE_BOOKMARKS statement 属性が SQL_UB_VARIABLE に設定されました。<br /><br /> 列0は SQL_C_VARBOOKMARK のデータ型にバインドされており、SQL_ATTR_USE_BOOKMARKS statement 属性は SQL_UB_VARIABLE に設定されていませんでした。|  
|07009|無効な記述子のインデックス|ドライバーは、 **SQLExtendedFetch**をサポートしていない ODBC*2.x ドライバーで*、列のバインドに指定された列番号が0でした。<br /><br /> 列0がバインドされ、SQL_ATTR_USE_BOOKMARKS statement 属性が SQL_UB_OFF に設定されました。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続されていたデータソースとの間の通信リンクが失敗しました。|  
|22001|文字列データ、右側が切り捨てられました|列に対して返された可変長のブックマークが切り捨てられました。|  
|22002|インジケーター変数が必要ですが、指定されていません|**SQLBindCol**によって設定された*StrLen_or_IndPtr* (または**SQLSetDescField**または**SQLSetDescRec**によって設定された SQL_DESC_INDICATOR_PTR) が null ポインターである列に null データがフェッチされました。|  
|22003|数値が有効範囲にありません|1つ以上のバインドされた列に対して数値または文字列として数値または文字列として数値を返すと、切り捨てられる数値の一部 (小数部分ではなく) が発生する可能性があります。<br /><br /> 詳細については、「[付録 D: データ型](../../../odbc/reference/appendixes/appendix-d-data-types.md)」の「 [SQL から C データ型へのデータの変換](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)」を参照してください。|  
|22007|無効な datetime 形式|結果セットの文字列が日付、時刻、またはタイムスタンプ C 構造体にバインドされました。列の値は、それぞれ無効な日付、時刻、またはタイムスタンプです。|  
|22012|0による除算|算術式からの値が返されました。この結果、0による除算が行われました。|  
|22015|間隔フィールドオーバーフロー|数値または期間の SQL 型から範囲 C 型への割り当てにより、先頭のフィールドの有効桁数が失われました。<br /><br /> データを interval C 型にフェッチする場合、interval C 型の SQL 型の値は表現されませんでした。|  
|22018|キャストの指定に無効な文字値があります|結果セットの文字列が文字 C バッファーにバインドされました。この列には、バッファーの文字セットに表現がなかった文字が含まれていました。<br /><br /> C 型は、正確な数値、概数、datetime、または interval データ型でした。列の SQL 型は文字データ型でした。列の値が、バインドされた C 型の有効なリテラルではありませんでした。|  
|24000|カーソル状態が無効|*StatementHandle*は実行状態でしたが、結果セットが*StatementHandle*に関連付けられていませんでした。|  
|40001|シリアル化エラー|フェッチが実行されたトランザクションは、デッドロックを防ぐために終了されました。|  
|40003|ステートメントの完了が不明です|この関数の実行中に関連付けられた接続に失敗しました。トランザクションの状態を確認できません。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * \* Messagetext*バッファーの**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|*StatementHandle*に対して非同期処理が有効になりました。 関数が呼び出され、実行が完了する前に、 **SQLCancel** または **Sqlcancelhandle** が *StatementHandle*で呼び出されました。 次に、 *StatementHandle*で関数が再度呼び出されました。<br /><br /> 関数が呼び出され、実行が完了する前に、マルチスレッドアプリケーションの別のスレッドの*StatementHandle*で**SQLCancel**または**sqlcancelhandle**が呼び出されました。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、 **Sqlfetchscroll** 関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または **Sqlmoreresults** が *StatementHandle* に対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。<br /><br /> (DM) 指定された *StatementHandle* は実行状態ではありませんでした。 最初に **SQLExecDirect**、 **sqlexecute** 、または catalog 関数を呼び出さずに関数が呼び出されました。<br /><br /> (DM) 非同期的に実行されている関数 (この1つではない) が *StatementHandle* に対して呼び出され、この関数が呼び出されたときにまだ実行されています。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **Sqlbulkoperations**、 **SQLSetPos** が *StatementHandle* に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。<br /><br /> (DM) **SQLExtendedFetch**が呼び出された後、SQL_CLOSE**オプションが呼び出された前に**、 *StatementHandle*に対して**sqlfetch**が呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY090|文字列またはバッファーの長さが無効です|SQL_ATTR_USE_BOOKMARK statement 属性が SQL_UB_VARIABLE に設定されました。列0は、長さがこの結果セットのブックマークの最大長と等しくないバッファーにバインドされています。 (この長さは IRD の [SQL_DESC_OCTET_LENGTH] フィールドで使用でき、 **SQLDescribeCol**、 **sqlcolattribute**、または **SQLGetDescField**を呼び出すことによって取得できます)。|  
|HY106|フェッチの型が範囲を超えています|DM) 引数 FetchOrientation に指定された値が無効でした。<br /><br /> (DM) 引数 FetchOrientation が SQL_FETCH_BOOKMARK、SQL_ATTR_USE_BOOKMARKS statement 属性が SQL_UB_OFF に設定されました。<br /><br /> SQL_ATTR_CURSOR_TYPE statement 属性の値が SQL_CURSOR_FORWARD_ONLY ましたが、引数 FetchOrientation の値が SQL_FETCH_NEXT いませんでした。<br /><br /> SQL_ATTR_CURSOR_SCROLLABLE statement 属性の値が SQL_NONSCROLLABLE ましたが、引数 FetchOrientation の値が SQL_FETCH_NEXT いませんでした。|  
|HY107|行の値が有効範囲にありません|SQL_ATTR_CURSOR_TYPE statement 属性で指定された値が SQL_CURSOR_KEYSET_DRIVEN ましたが、SQL_ATTR_KEYSET_SIZE statement 属性で指定された値が0より大きく、SQL_ATTR_ROW_ARRAY_SIZE statement 属性で指定された値を下回っています。|  
|HY111|ブックマークの値が無効です|引数 FetchOrientation が SQL_FETCH_BOOKMARK、SQL_ATTR_FETCH_BOOKMARK_PTR statement 属性の値が指すブックマークが無効であるか、null ポインターでした。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYC00|省略可能な機能は実装されていません|ドライバーまたはデータソースが、 **SQLBindCol**の*TargetType*と対応する列の SQL データ型の組み合わせによって指定された変換をサポートしていません。|  
|HYT00|タイムアウトに達しました|データソースが要求された結果セットを返す前に、クエリのタイムアウト期間が経過しました。 タイムアウト期間は、SQLSetStmtAttr、SQL_ATTR_QUERY_TIMEOUT によって設定されます。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle* に関連付けられているドライバーでは、関数はサポートされていません。|  
|IM017|非同期通知モードでは、ポーリングは無効になっています|通知モデルが使用されるたびに、ポーリングは無効になります。|  
|IM018|**Sqlcompleteasync** は、このハンドルで前の非同期操作を完了するために呼び出されていません。|ハンドルに対する前の関数呼び出しが SQL_STILL_EXECUTING を返し、通知モードが有効になっている場合は、処理を完了するために、ハンドルに対して **Sqlcompleteasync** を呼び出す必要があります。|  
  
## <a name="comments"></a>コメント  
 **Sqlfetchscroll** は、結果セットから指定された行セットを返します。 行セットは、絶対位置または相対位置またはブックマークによって指定できます。 **Sqlfetchscroll** は、結果セットが存在する場合にのみ呼び出すことができます。つまり、結果セットを作成し、その結果セットにカーソルを移動する前に、呼び出しが終了します。 列がバインドされている場合は、それらの列のデータが返されます。 フェッチされた行の数を返す行の状態の配列またはバッファーへのポインターをアプリケーションが指定した場合、 **Sqlfetchscroll** はこの情報も返します。 **Sqlfetchscroll**の呼び出しと**sqlfetch**の呼び出しを混在させることはできますが、 **SQLExtendedFetch**の呼び出しと混在させることはできません。  
  
 詳細については、「 [ブロックカーソルの使用](../../../odbc/reference/develop-app/using-block-cursors.md) 」および「スクロール可能な [カーソルの使用](../../../odbc/reference/develop-app/using-scrollable-cursors.md)」を参照してください。  
  
## <a name="positioning-the-cursor"></a>カーソルの位置を指定する  
 結果セットが作成されると、カーソルが結果セットの先頭の前に配置されます。 **Sqlfetchscroll** は、次の表に示すように、 *Fetchorientation* および *fetchoffset* 引数の値に基づいてブロックカーソルを位置付けます。 次のセクションでは、新しい行セットの開始を決定するための正確なルールを示します。  
  
|FetchOrientation|説明|  
|----------------------|-------------|  
|SQL_FETCH_NEXT|次の行セットを返します。 これは、 **Sqlfetch**を呼び出すことと同じです。<br /><br /> **Sqlfetchscroll** は、 *fetchoffset*の値を無視します。|  
|SQL_FETCH_PRIOR|前の行セットを返します。<br /><br /> **Sqlfetchscroll** は、 *fetchoffset*の値を無視します。|  
|SQL_FETCH_RELATIVE|現在の行セットの先頭から行セット *Fetchoffset* を返します。|  
|SQL_FETCH_ABSOLUTE|行 *フェッチオフセット*で始まる行セットを返します。|  
|SQL_FETCH_FIRST|結果セットの最初の行セットを返します。<br /><br /> **Sqlfetchscroll** は、 *fetchoffset*の値を無視します。|  
|SQL_FETCH_LAST|結果セットの最後の完全な行セットを返します。<br /><br /> **Sqlfetchscroll** は、 *fetchoffset*の値を無視します。|  
|SQL_FETCH_BOOKMARK|SQL_ATTR_FETCH_BOOKMARK_PTR statement 属性によって指定されたブックマークから行セット FetchOffset 行を返します。|  
  
 すべてのフェッチの向きをサポートするためにドライバーは必要ありません。アプリケーションでは、SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1、または SQL_STATIC_CURSOR_ATTRIBUTES1 の情報の種類を使用して **SQLGetInfo** を呼び出します (カーソルの種類によって異なります)。ドライバーでサポートされているフェッチの方向を決定します。 アプリケーションは、これらの情報の種類の SQL_CA1_NEXT、SQL_CA1_RELATIVE、SQL_CA1_ABSOLUTE、および WQL_CA1_BOOKMARK ビットマスクを確認する必要があります。 さらに、カーソルが順方向専用で、FetchOrientation が SQL_FETCH_NEXT ない場合、 **Sqlfetchscroll** は SQLSTATE HY106 (範囲外のフェッチ型) を返します。  
  
 SQL_ATTR_ROW_ARRAY_SIZE statement 属性は、行セット内の行の数を指定します。 **Sqlfetchscroll**によってフェッチされる行セットが結果セットの末尾と重複する場合、 **sqlfetchscroll**は部分的な行セットを返します。 つまり、S + R-1 が L よりも大きい場合 (S はフェッチされる行セットの開始行、R は行セットのサイズ、L は結果セットの最後の行)、行セットの最初の L-S + 1 行だけが有効です。 残りの行は空であり、SQL_ROW_NOROW の状態になっています。  
  
 **Sqlfetchscroll**が返された後、現在の行が行セットの最初の行になります。  
  
## <a name="cursor-positioning-rules"></a>カーソルの配置ルール  
 次のセクションでは、FetchOrientation の各値の正確な規則について説明します。 これらの規則では、次の表記を使用します。  
  
|表記|説明|  
|--------------|-------------|  
|*開始前*|ブロックカーソルは、結果セットの先頭の前に配置されます。 新しい行セットの最初の行が結果セットの先頭より前にある場合、 **Sqlfetchscroll** は SQL_NO_DATA を返します。|  
|*終了後*|ブロックカーソルは、結果セットの末尾の後に配置されます。 新しい行セットの最初の行が結果セットの末尾より後にある場合、 **Sqlfetchscroll** は SQL_NO_DATA を返します。|  
|*CurrRowsetStart*|現在の行セットの最初の行の番号。|  
|*LastResultRow*|結果セットの最後の行の番号。|  
|*RowsetSize*|行セットのサイズ。|  
|*FetchOffset*|*Fetchoffset*引数の値。|  
|*BookmarkRow*|SQL_ATTR_FETCH_BOOKMARK_PTR statement 属性によって指定されたブックマークに対応する行。|  
  
## <a name="sql_fetch_next"></a>SQL_FETCH_NEXT  
 次の規則が適用されます。  
  
|条件|新しい行セットの最初の行|  
|---------------|-----------------------------|  
|*開始前*|1|  
|*CurrRowsetStart + RowsetSize*[1] * \< = lastresultrow*|*CurrRowsetStart + RowsetSize*[1]|  
|*CurrRowsetStart + RowsetSize*[1]*> lastresultrow*|*終了後*|  
|*終了後*|*終了後*|  
  
 [1] 前回の呼び出し以降に行セットのサイズが変更されている場合は、前の呼び出しで使用された行セットのサイズになります。  
  
## <a name="sql_fetch_prior"></a>SQL_FETCH_PRIOR  
 次の規則が適用されます。  
  
|条件|新しい行セットの最初の行|  
|---------------|-----------------------------|  
|*開始前*|*開始前*|  
|*CurrRowsetStart = 1*|*開始前*|  
|*1 < CurrRowsetStart <= RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*CurrRowsetStart > RowsetSize* <sup>[2]</sup>|*CurrRowsetStart-RowsetSize* <sup>[2]</sup>|  
|*END および LastResultRow < RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*END および LastResultRow >= RowsetSize* <sup>[2]</sup>|*Lastresultrow-RowsetSize + 1* <sup>[2]</sup>|  
  
 [1]   **Sqlfetchscroll** は SQLSTATE 01S06 (最初の行セットを返す前にフェッチしようとします) および SQL_SUCCESS_WITH_INFO を返します。  
  
 [2] 以前に行をフェッチした後に行セットのサイズが変更された場合、これは新しい行セットサイズになります。  
  
## <a name="sql_fetch_relative"></a>SQL_FETCH_RELATIVE  
 次の規則が適用されます。  
  
|条件|新しい行セットの最初の行|  
|---------------|-----------------------------|  
|*(Start と FetchOffset > 0)または (end と FetchOffset < 0)*|*--*<sup>[1]</sup>|  
|*BeforeStart と FetchOffset <= 0*|*開始前*|  
|*CurrRowsetStart = 1、FetchOffset < 0*|*開始前*|  
|*CurrRowsetStart > 1 および CurrRowsetStart + fetchoffset < 1 &#124; fetchoffset &#124; > RowsetSize* <sup>[3]</sup>|*開始前*|  
|*CurrRowsetStart > 1 および CurrRowsetStart + fetchoffset < 1 および &#124; fetchoffset &#124; <= RowsetSize* <sup>[3]</sup>|*1* <sup>[2]</sup>|  
|*1 <= CurrRowsetStart + FetchOffset \< = lastresultrow*|*CurrRowsetStart + FetchOffset*|  
|*CurrRowsetStart + FetchOffset > LastResultRow*|*終了後*|  
|*終了と FetchOffset >= 0*|*終了後*|  
  
 [1]   ***Sqlfetchscroll*** は、fetchorientation を SQL_FETCH_ABSOLUTE に設定して呼び出された場合と同じ行セットを返します。 詳細については、「SQL_FETCH_ABSOLUTE」セクションを参照してください。  
  
 [2]   **Sqlfetchscroll** は SQLSTATE 01S06 (最初の行セットを返す前にフェッチを試行) と SQL_SUCCESS_WITH_INFO を返します。  
  
 [3] 以前に行をフェッチした後に行セットのサイズが変更された場合、これは新しい行セットサイズになります。  
  
## <a name="sql_fetch_absolute"></a>SQL_FETCH_ABSOLUTE  
 次の規則が適用されます。  
  
|条件|新しい行セットの最初の行|  
|---------------|-----------------------------|  
|*FetchOffset < 0 および &#124; FetchOffset &#124; <= LastResultRow*|*LastResultRow + FetchOffset + 1*|  
|*Fetchoffset < 0 および &#124; fetchoffset &#124; > LastResultRow および &#124; fetchoffset &#124; > RowsetSize* <sup>[2]</sup>|*開始前*|  
|*Fetchoffset < 0 および &#124; fetchoffset &#124; > LastResultRow および &#124; fetchoffset &#124; <= RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*FetchOffset = 0*|*開始前*|  
|*1 <= FetchOffset \< = lastresultrow*|*FetchOffset*|  
|*FetchOffset > LastResultRow*|*終了後*|  
  
 [1]   **Sqlfetchscroll** は SQLSTATE 01S06 (最初の行セットを返す前にフェッチしようとします) および SQL_SUCCESS_WITH_INFO を返します。  
  
 [2] 以前に行をフェッチした後に行セットのサイズが変更された場合、これは新しい行セットサイズになります。  
  
 動的カーソルの行位置が不明であるため、動的カーソルに対して実行される絶対フェッチでは、必要な結果を得ることができません。 このような操作は、最初に fetch を実行し、次に fetch を相対的に実行することと同じです。これはアトミック操作ではなく、静的カーソルに対する絶対フェッチです。  
  
## <a name="sql_fetch_first"></a>SQL_FETCH_FIRST  
 次の規則が適用されます。  
  
|条件|新しい行セットの最初の行|  
|---------------|-----------------------------|  
|*[任意]*|*1*|  
  
## <a name="sql_fetch_last"></a>SQL_FETCH_LAST  
 次の規則が適用されます。  
  
|条件|新しい行セットの最初の行|  
|---------------|-----------------------------|  
|*RowsetSize* <sup>[1]</sup> <= lastresultrow|*Lastresultrow-RowsetSize + 1* <sup>[1]</sup>|  
|*RowsetSize* <sup>[1]</sup> > lastresultrow|*1*|  
  
 [1] 以前に行をフェッチした後に行セットのサイズが変更された場合、これは新しい行セットサイズになります。  
  
## <a name="sql_fetch_bookmark"></a>SQL_FETCH_BOOKMARK  
 次の規則が適用されます。  
  
|条件|新しい行セットの最初の行|  
|---------------|-----------------------------|  
|*BookmarkRow + FetchOffset < 1*|*開始前*|  
|*1 <= BookmarkRow + FetchOffset \< = lastresultrow*|*BookmarkRow + FetchOffset*|  
|*BookmarkRow + FetchOffset > LastResultRow*|*終了後*|  
  
 ブックマークの詳細については、「 [ブックマーク (ODBC)](../../../odbc/reference/develop-app/bookmarks-odbc.md)」を参照してください。  
  
## <a name="effect-of-deleted-added-and-error-rows-on-cursor-movement"></a>カーソルの移動時の削除、追加、およびエラー行の影響  
 静的カーソルとキーセットドリブンカーソルは、結果セットに追加された行を検出し、結果セットから削除された行を削除することがあります。 SQL_STATIC_CURSOR_ATTRIBUTES2 オプションと SQL_KEYSET_CURSOR_ATTRIBUTES2 オプションを指定して **SQLGetInfo** を呼び出し、SQL_CA2_SENSITIVITY_ADDITIONS、SQL_CA2_SENSITIVITY_DELETIONS、および SQL_CA2_SENSITIVITY_UPDATES ビットマスクを確認すると、特定のドライバーによって実装されているカーソルがこれを実行するかどうかがアプリケーションによって判断されます。 削除された行を検出して削除するドライバーの場合、次の段落でこの動作の影響について説明します。 削除された行を検出できても削除できないドライバーの場合、削除はカーソルの動きに影響を与えず、次の段落は適用されません。  
  
 カーソルが結果セットに追加された行を検出した場合、または結果セットから削除された行を削除した場合、データをフェッチするときにのみこれらの変更が検出されたように見えます。 これには、FetchOrientation を SQL_FETCH_RELATIVE に設定し、FetchOffset を0に設定して同じ行セットを再フェッチする **Sqlfetchscroll** が呼び出されますが、foption を SQL_REFRESH に設定して SQLSetPos が呼び出された場合のケースは含まれません。 後者の場合、行セットバッファー内のデータは更新されますが、refetched は更新されず、削除された行は結果セットから削除されません。 このため、現在の行セットから行が削除されたり、現在の行セットに挿入されたりしても、カーソルは行セットバッファーを変更しません。 代わりに、削除された行が以前に含まれていた行セットをフェッチするか、挿入された行が含まれるようになったときに、変更が検出されます。  
  
 次に例を示します。  
  
```cpp  
// Fetch the next rowset.  
SQLFetchScroll(hstmt, SQL_FETCH_NEXT, 0);  
// Delete third row of the rowset. Does not modify the rowset buffers.  
SQLSetPos(hstmt, 3, SQL_DELETE, SQL_LOCK_NO_CHANGE);  
// The third row has a status of SQL_ROW_DELETED after this call.  
SQLSetPos(hstmt, 3, SQL_REFRESH, SQL_LOCK_NO_CHANGE);  
// Refetch the same rowset. The third row is removed, replaced by what  
// was previously the fourth row.  
SQLFetchScroll(hstmt, SQL_FETCH_RELATIVE, 0);  
```  
  
 **Sqlfetchscroll**が、現在の行セットを基準とした相対位置を持つ新しい行セットを返す場合、つまり、fetchorientation が SQL_FETCH_NEXT、SQL_FETCH_PRIOR、または SQL_FETCH_RELATIVE である場合、新しい行セットの開始位置を計算するときに現在の行セットに対する変更は含まれません。 ただし、現在の行セットの外部にある変更を検出できる場合は、その変更が含まれます。 さらに、 **Sqlfetchscroll** は、現在の行セットから独立した位置を持つ新しい行セットを返します。つまり、fetchorientation が SQL_FETCH_FIRST、SQL_FETCH_LAST、SQL_FETCH_ABSOLUTE、または SQL_FETCH_BOOKMARK-現在の行セット内にある場合でも、検出できるすべての変更が含まれます。  
  
 新しく追加された行が現在の行セットの内部または外部にあるかどうかを判断する場合、部分的な行セットは最後の有効な行で終了したと見なされます。つまり、行の状態が SQL_ROW_NOROW されていない最後の行です。 たとえば、カーソルが新しく追加された行を検出できる場合、現在の行セットが部分的な行セットであり、アプリケーションによって新しい行が追加され、カーソルによってこれらの行が結果セットの末尾に追加されるとします。 アプリケーションが FetchOrientation を SQL_FETCH_NEXT に設定して **Sqlfetchscroll** を呼び出すと、 **sqlfetchscroll** は、新しく追加された最初の行で始まる行セットを返します。  
  
 たとえば、現在の行セットが 21 ~ 30 行で構成され、行セットのサイズが10である場合、カーソルが結果セットから削除された行を削除し、カーソルが結果セットに追加された行を検出したとします。 次の表は、さまざまな状況で **Sqlfetchscroll** が返す行を示しています。  
  
|Change|フェッチの種類|FetchOffset|新しい行セット [1]|  
|------------|----------------|-----------------|---------------------|  
|行21の削除|NEXT|0|31 ~ 40|  
|行31の削除|NEXT|0|32 ~ 41|  
|21行と22行の間に行を挿入する|NEXT|0|31 ~ 40|  
|30 ~ 31 行の行を挿入|NEXT|0|挿入された行、31 ~ 39|  
|行21の削除|PRIOR|0|11 ~ 20|  
|行20の削除|PRIOR|0|10 ~ 19|  
|21行と22行の間に行を挿入する|PRIOR|0|11 ~ 20|  
|20 ~ 21 行の行を挿入|PRIOR|0|12 ~ 20、挿入された行|  
|行21の削除|RELATIVE|0|22 ~ 31<sup>[2]</sup>|  
|行21の削除|RELATIVE|1|22 ~ 31|  
|21行と22行の間に行を挿入する|RELATIVE|0|21、挿入された行、22 ~ 29|  
|21行と22行の間に行を挿入する|RELATIVE|1|22 ~ 31|  
|行21の削除|ABSOLUTE|21|22 ~ 31<sup>[2]</sup>|  
|行22の削除|ABSOLUTE|21|21、23 ~ 31|  
|21行と22行の間に行を挿入する|ABSOLUTE|22|挿入された行、22 ~ 29|  
  
 [1] この列は、行が挿入または削除される前に行番号を使用します。  
  
 [2] この場合、カーソルは行21で始まる行を返します。 行21は削除されているので、最初に返される行は行22です。  
  
 エラー行 (つまり、状態が SQL_ROW_ERROR の行) は、カーソルの移動には影響しません。 たとえば、現在の行セットが行11で始まり、行11の状態が SQL_ROW_ERROR である場合、FetchOrientation を SQL_FETCH_RELATIVE に設定して **Sqlfetchscroll** を呼び出し、fetchoffset を5に設定すると、行11の状態が SQL_SUCCESS 場合と同様に、行16で始まる行セットが返されます。  
  
## <a name="returning-data-in-bound-columns"></a>バインドされた列のデータを返す  
 **Sqlfetchscroll** は、 **sqlfetch**と同じように、バインドされた列のデータを返します。 詳細については、「 [Sqlfetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)」の「バインドされた列にデータを返す」を参照してください。  
  
 列がバインドされていない場合、 **Sqlfetchscroll** はデータを返しませんが、ブロックカーソルを指定された位置に移動します。 **SQLGetData**を使用してブロックカーソルのバインドされていない列からデータを取得できるかどうかは、ドライバーによって異なります。 この機能は、 **SQLGetInfo** の呼び出しが SQL_GETDATA_EXTENSIONS 情報型の SQL_GD_BLOCK ビットを返す場合にサポートされます。  
  
## <a name="buffer-addresses"></a>バッファーアドレス  
 **Sqlfetchscroll** では、同じ数式を使用して、データのアドレスと長さ/インジケーターバッファーを **sqlfetch**として指定します。 詳細については、 [SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)の「Buffer Addresses」を参照してください。  
  
## <a name="row-status-array"></a>行の状態の配列  
 **Sqlfetchscroll** は、sqlfetch と同じ方法で、行の状態配列の値を設定します。 詳細については、「 [Sqlfetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)」の「行の状態の配列」を参照してください。  
  
## <a name="rows-fetched-buffer"></a>フェッチされる行のバッファー  
 **Sqlfetchscroll** は、 **sqlfetch**と同じ方法でフェッチされた行のフェッチされた行数を返します。 詳細については、「 [Sqlfetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)」の「行フェッチバッファー」を参照してください。  
  
## <a name="error-handling"></a>エラー処理  
 アプリケーションが ODBC 3. x ドライバーで **Sqlfetchscroll** を呼び出すと、ドライバーマネージャーはドライバーで **sqlfetchscroll** を呼び出します。 アプリケーションが ODBC 2.x ドライバーで **Sqlfetchscroll** を呼び出すと、ドライバーマネージャーはドライバーで SQLExtendedFetch を呼び出します。 **Sqlfetchscroll**と SQLExtendedFetch は少し異なる方法でエラーを処理するため、odbc 2.X および odbc 3.x ドライバーで**sqlfetchscroll**を呼び出すと、わずかに異なるエラー動作が表示されます。  
  
 **Sqlfetchscroll** は、 **sqlfetch**と同じ方法でエラーと警告を返します。詳細については、「 **Sqlfetch**でのエラー処理」を参照してください。 **SQLExtendedFetch** は、 **sqlfetch**と同じ方法でエラーを返します。ただし、次の例外があります。  
  
 行セット内の特定の行に適用される警告が発生すると、SQLExtendedFetch は行の状態配列内の対応するエントリを SQL_ROW_SUCCESS_WITH_INFO ではなく SQL_ROW_SUCCESS に設定します。  
  
 行セット内のすべての行でエラーが発生した場合、SQLExtendedFetch は SQL_ERROR ではなく SQL_SUCCESS_WITH_INFO を返します。  
  
 個々の行に適用される状態レコードの各グループでは、SQLExtendedFetch によって返される最初のステータスレコードに SQLSTATE 01S01 が含まれている必要があります (行にエラーがあります)。 **Sqlfetchscroll** は、この SQLSTATE を返しません。 SQLExtendedFetch が追加の SQLSTATEs を返すことができない場合でも、この SQLSTATE を返す必要があります。  
  
## <a name="sqlfetchscroll-and-optimistic-concurrency"></a>SQLFetchScroll とオプティミスティック同時実行制御  
 カーソルでオプティミスティック同時実行制御が使用されている場合、つまり、SQL_ATTR_CONCURRENCY statement 属性の値が SQL_CONCUR_VALUES または SQL_CONCUR_ROWVER- **Sqlfetchscroll** は、行が変更されたかどうかを検出するためにデータソースによって使用されるオプティミスティック同時実行制御値を更新します。 これは、 **Sqlfetchscroll** が現在の行セットの refetches 時を含め、新しい行セットをフェッチするたびに発生します。 (FetchOrientation を SQL_FETCH_RELATIVE に設定し、Fetchorientation を0に設定して呼び出されます)。  
  
## <a name="sqlfetchscroll-and-odbc-2x-drivers"></a>SQLFetchScroll および ODBC 2.x ドライバー  
 アプリケーションが ODBC 2.x ドライバーで **Sqlfetchscroll** を呼び出すと、ドライバーマネージャーはこの呼び出しを **SQLExtendedFetch**にマップします。 **SQLExtendedFetch**の引数には、次の値を渡します。  
  
|SQLExtendedFetch 引数|値|  
|-------------------------------|-----------|  
|StatementHandle|**Sqlfetchscroll**で StatementHandle。|  
|FetchOrientation|**Sqlfetchscroll**での fetchorientation。|  
|FetchOffset|FetchOrientation が SQL_FETCH_BOOKMARK ない場合は、 **Sqlfetchscroll** の fetchorientation 引数の値が使用されます。<br /><br /> FetchOrientation が SQL_FETCH_BOOKMARK 場合、SQL_ATTR_FETCH_BOOKMARK_PTR statement 属性で指定されたアドレスに格納されている値が使用されます。|  
|RowCountPtr|SQL_ATTR_ROWS_FETCHED_PTR statement 属性によって指定されたアドレス。|  
|RowStatusArray|SQL_ATTR_ROW_STATUS_PTR statement 属性によって指定されたアドレス。|  
  
 詳細については、「付録 G: 旧バージョンとの互換性のためのドライバーガイドライン」の「 [ブロックカーソル、スクロール可能なカーソル、および旧バージョンとの互換性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) 」を参照してください。  
  
## <a name="descriptors-and-sqlfetchscroll"></a>記述子と SQLFetchScroll  
 **Sqlfetchscroll** は、 **sqlfetch**と同じ方法で記述子と対話します。 詳細については、「 [Sqlfetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)」の「記述子と SQLFetchScroll」セクションを参照してください。  
  
## <a name="code-example"></a>コード例  
 [列方向のバインド](../../../odbc/reference/develop-app/column-wise-binding.md)、[行方向のバインド](../../../odbc/reference/develop-app/row-wise-binding.md)、位置指定の[Update および Delete ステートメント](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)、および[SQLSetPos を使用](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)した行セットの行の更新を参照してください。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|結果セット内の列へのバッファーのバインド|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|一括挿入、更新、または削除操作の実行|[SQLBulkOperations 関数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|ステートメント処理の取り消し|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|結果セットの列に関する情報を返す|[SQLDescribeCol 関数](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|SQL ステートメントの実行|[SQLExecDirect 関数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|準備された SQL ステートメントの実行|[SQLExecute 関数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|1つの行またはデータのブロックを順方向専用にフェッチする|[SQLFetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|ステートメントでカーソルを閉じる|[SQLFreeStmt 関数](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|結果セットの列数を返す|[SQLNumResultCols 関数](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|カーソルの配置、行セット内のデータの更新、または結果セット内のデータの更新または削除|[SQLSetPos 関数](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|ステートメント属性の設定|[SQLSetStmtAttr 関数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
