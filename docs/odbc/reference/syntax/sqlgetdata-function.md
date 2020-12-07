---
description: SQLGetData 関数
title: SQLGetData 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetData
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetData
helpviewer_keywords:
- SQLGetData function [ODBC]
ms.assetid: e3c1356a-5db7-4186-85fd-8b74633317e8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a659e1bb5ad7765dbfcbcb01dbc16744de7cfc20
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461080"
---
# <a name="sqlgetdata-function"></a>SQLGetData 関数
**互換性**  
 導入されたバージョン: ODBC 1.0 標準準拠: ISO 92  
  
 **まとめ**  
 **SQLGetData** は、結果セット内の単一の列のデータを取得します。または、 **sqlparamdata** が SQL_PARAM_DATA_AVAILABLE を返す後に1つのパラメーターを取得します。 複数回呼び出すことで、可変長データを部分的に取得できます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLGetData(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   Col_or_Param_Num,  
      SQLSMALLINT    TargetType,  
      SQLPOINTER     TargetValuePtr,  
      SQLLEN         BufferLength,  
      SQLLEN *       StrLen_or_IndPtr);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル。  
  
 *Col_or_Param_Num*  
 代入列データを取得するために、データを返す列の番号です。 結果セットの列には、1から始まる昇順の列の順序が付けられます。 ブックマーク列は列番号0です。これは、ブックマークが有効になっている場合にのみ指定できます。  
  
 パラメーターデータを取得する場合、これはパラメーターの序数であり、1から開始されます。  
  
 *TargetType*  
 代入**Targetvalueptr* バッファーの C データ型の型識別子。 有効な C データ型と型識別子の一覧については、「付録 D: データ型」の「 [c データ型](../../../odbc/reference/appendixes/c-data-types.md) 」を参照してください。  
  
 *TargetType*が SQL_ARD_TYPE 場合、ドライバーは、の SQL_DESC_CONCISE_TYPE フィールドで指定された型識別子を使用します。 *TargetType*が SQL_APD_TYPE 場合、 **SQLGetData**は**SQLBindParameter**で指定されたのと同じ C データ型を使用します。 それ以外の場合、 **SQLGetData** で指定した c データ型は、 **SQLBindParameter**で指定された c データ型よりも優先されます。 SQL_C_DEFAULT の場合、ドライバーはソースの SQL データ型に基づいて、既定の C データ型を選択します。  
  
 拡張 C データ型を指定することもできます。 詳細については、「 [ODBC の C データ型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)」を参照してください。  
  
 *TargetValuePtr*  
 Outputデータを返すバッファーへのポインター。  
  
 *Targetvalueptr* を NULL にすることはできません。  
  
 *BufferLength*  
 代入**Targetvalueptr* バッファーの長さ (バイト単位)。  
  
 ドライバーは*Bufferlength*を使用し \* て、文字やバイナリデータなどの可変長データを返すときに*targetvalueptr*バッファーの末尾を越えた書き込みを回避します。 ドライバーは、 \* *targetvalueptr*に文字データを返すときに、null 終端文字をカウントすることに注意してください。 *したがって、 *Targetvalueptr*には null 終端文字用の領域が含まれている必要があります。それ以外の場合は、ドライバーによってデータが切り捨てられます。  
  
 ドライバーが整数や日付構造などの固定長データを返す場合、ドライバーは *Bufferlength* を無視し、バッファーがデータを保持するのに十分な大きさであると想定します。 このため、アプリケーションで固定長データ用に十分な大きさのバッファーを割り当てることが重要です。そうしないと、ドライバーはバッファーの末尾を越えて書き込みを行います。  
  
 *Bufferlength が 0*未満の場合、 **SQLGETDATA**は SQLSTATE HY090 (無効な文字列またはバッファー長) を返しますが、 *bufferlength*が0のときは返されません。  
  
 *StrLen_or_IndPtr*  
 Output長さまたはインジケーターの値を返すバッファーへのポインター。 Null ポインターの場合は、長さまたはインジケーターの値は返されません。 これは、フェッチされるデータが NULL の場合にエラーを返します。  
  
 **SQLGetData** は、長さ/インジケーターバッファー内の次の値を返すことができます。  
  
-   返すことができるデータの長さ  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 詳細については、このトピックの「 [長さ/インジケーター値の使用](../../../odbc/reference/develop-app/using-length-and-indicator-values.md) 」および「コメント」を参照してください。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **SQLGetData**が SQL_ERROR または SQL_SUCCESS_WITH_INFO のいずれかを返す場合、関連付けられた SQLSTATE 値を取得するには、 *Handletype* SQL_HANDLE_STMT と*StatementHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出します。 次の表に、 **SQLGetData** によって一般的に返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データ、右側が切り捨てられました|指定された列 *Col_or_Param_Num*の一部のデータは、関数の1回の呼び出しで取得できませんでした。 **SQLGetData**の現在の呼び出しの前に、指定した列に残っているデータの SQL_NO_TOTAL または長さが StrLen_or_IndPtr に返され \* *StrLen_or_IndPtr*ます。 (関数は SQL_SUCCESS_WITH_INFO を返します)。<br /><br /> 1つの列に対して複数の **SQLGetData** 呼び出しを使用する方法の詳細については、「コメント」を参照してください。|  
|01S07|小数部の切り捨て|1つ以上の列に対して返されたデータが切り捨てられました。 数値データ型の場合、数値の小数部は切り捨てられました。 時間、タイムスタンプ、および期間のデータ型については、時刻の部分が切り捨てられました。<br /><br /> (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|07006|制限されたデータ型の属性違反|結果セット内の列のデータ値を、引数 *TargetType*によって指定された C データ型に変換することはできません。|  
|07009|無効な記述子のインデックス|引数 *Col_or_Param_Num* に指定された値が0で、SQL_ATTR_USE_BOOKMARKS statement 属性が SQL_UB_OFF に設定されました。<br /><br /> 引数 *Col_or_Param_Num* に指定された値が、結果セット内の列数を超えています。<br /><br /> *Col_or_Param_Num*値が、使用可能なパラメーターの序数と等しくありませんでした。<br /><br /> (DM) 指定された列がバインドされました。 この説明は、 **SQLGetInfo**の SQL_GETDATA_EXTENSIONS オプションの SQL_GD_BOUND ビットマスクを返すドライバーには適用されません。<br /><br /> (DM) 指定された列の数が、バインドされた列の最大数以下でした。 この説明は、 **SQLGetInfo**の SQL_GETDATA_EXTENSIONS オプションの SQL_GD_ANY_COLUMN ビットマスクを返すドライバーには適用されません。<br /><br /> (DM) アプリケーションは、現在の行に対して既に **SQLGetData** を呼び出しています。現在の呼び出しで指定された列の数が、前の呼び出しで指定された列の数より少なくなっています。また、このドライバーは、 **SQLGetInfo**の SQL_GETDATA_EXTENSIONS オプションの SQL_GD_ANY_ORDER ビットマスクを返しません。<br /><br /> (DM) *TargetType* 引数が SQL_ARD_TYPE、の *Col_or_Param_Num* 記述子レコードが整合性チェックに失敗しました。<br /><br /> (DM) *TargetType* 引数が SQL_ARD_TYPE ましたが、の SQL_DESC_COUNT フィールドの値が *Col_or_Param_Num* 引数より小さくなっています。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続されていたデータソースとの間の通信リンクが失敗しました。|  
|22002|インジケーター変数が必要ですが、指定されていません|*StrLen_or_IndPtr* が null ポインターであり、null データが取得されました。|  
|22003|数値が有効範囲にありません|数値または文字列として、列の数値または文字列として数値を返すと、切り捨てられる数値の一部 (小数部分ではなく) が発生します。<br /><br /> 詳細については、「 [付録 D: データ型](../../../odbc/reference/appendixes/appendix-d-data-types.md)」を参照してください。|  
|22007|無効な datetime 形式|結果セットの文字列が C の日付、時刻、またはタイムスタンプの構造体にバインドされましたが、列の値がそれぞれ無効な日付、時刻、またはタイムスタンプになっていました。 詳細については、「 [付録 D: データ型](../../../odbc/reference/appendixes/appendix-d-data-types.md)」を参照してください。|  
|22012|0による除算|0による除算が発生した算術式の値が返されました。|  
|22015|間隔フィールドオーバーフロー|数値または期間の SQL 型から範囲 C 型への割り当てにより、先頭のフィールドの有効桁数が失われました。<br /><br /> データを interval C 型に返す場合、interval C 型の SQL 型の値は表現されませんでした。|  
|22018|キャストの指定に無効な文字値があります|結果セットの文字列が文字 C バッファーに返され、列にはバッファーの文字セット内に表現がなかった文字が含まれていました。<br /><br /> C 型は、正確な数値、概数、datetime、または interval データ型でした。列の SQL 型は文字データ型でした。列の値が、バインドされた C 型の有効なリテラルではありませんでした。|  
|24000|カーソル状態が無効|(DM) 関数が呼び出されました。最初に **sqlfetch** または **sqlfetchscroll** を呼び出して、必要なデータ行にカーソルを置きます。<br /><br /> (DM) *StatementHandle* は実行状態でしたが、結果セットが *StatementHandle*に関連付けられていませんでした。<br /><br /> *StatementHandle*でカーソルが開かれましたが、 **sqlfetch**または**sqlfetchscroll**が呼び出されましたが、カーソルが結果セットの先頭より前、または結果セットの末尾の後に配置されました。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 *Messagetext*バッファーの**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY003|プログラムの種類が有効範囲にありません|(DM) 引数 *TargetType* は、有効なデータ型、SQL_C_DEFAULT、SQL_ARD_TYPE (列データを取得する場合)、または SQL_APD_TYPE (パラメーターデータを取得する場合) ではありませんでした。<br /><br /> (DM) *Col_or_Param_Num* 引数が0でしたが、引数 *TargetType* が固定長のブックマークまたは可変長のブックマークの SQL_C_VARBOOKMARK に SQL_C_BOOKMARK ませんでした。|  
|HY008|操作が取り消されました|*StatementHandle*に対して非同期処理が有効になりました。 関数が呼び出され、実行が完了する前に、 **SQLCancel** または **Sqlcancelhandle** が *StatementHandle*で呼び出された後、 *StatementHandle*で関数が再度呼び出されました。<br /><br /> 関数が呼び出され、実行が完了する前に、マルチスレッドアプリケーションの別のスレッドの*StatementHandle*に対して**SQLCancel**または**sqlcancelhandle**が呼び出されました。その後、 *StatementHandle*で関数が再度呼び出されました。|  
|HY009|Null ポインターの使い方が正しくありません|(DM) 引数 *Targetvalueptr* は null ポインターでした。|  
|HY010|関数のシーケンスエラー|(DM) 指定された *StatementHandle* は実行状態ではありませんでした。 最初に **SQLExecDirect**、 **sqlexecute** 、または catalog 関数を呼び出さずに関数が呼び出されました。<br /><br /> (DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、 **SQLGetData** 関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) 非同期的に実行されている関数 (この1つではない) が *StatementHandle* に対して呼び出され、この関数が呼び出されたときにまだ実行されています。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **Sqlbulkoperations**、 **SQLSetPos** が *StatementHandle* に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。<br /><br /> (DM) *StatementHandle* は実行状態でしたが、結果セットが *StatementHandle*に関連付けられていませんでした。<br /><br /> **SQLExeceute**、 **SQLExecDirect**、または**sqlmoreresults**の呼び出しによって SQL_PARAM_DATA_AVAILABLE が返されましたが、 **sqlparamdata**ではなく**SQLGetData**が呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY090|文字列またはバッファーの長さが無効です|(DM) 引数 *Bufferlength* に指定された値が0未満でした。<br /><br /> 引数*Bufferlength*に指定された値が4未満で、 *Col_or_Param_Num*引数が0に設定され、ドライバーが ODBC 2.x*ドライバーでした。*|  
|HY109|カーソル位置が無効です|カーソルが、削除されたかフェッチできなかった行に ( **SQLSetPos**、 **sqlfetch**、 **Sqlfetchscroll**、または **sqlbulkscroll**によって) 配置されました。<br /><br /> カーソルは順方向専用カーソルで、行セットのサイズが1を超えています。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYC00|省略可能な機能は実装されていません|ドライバーまたはデータソースは、 **Sqlfetchscroll**で複数の行を含む**SQLGetData**の使用をサポートしていません。 この説明は、 **SQLGetInfo**の SQL_GETDATA_EXTENSIONS オプションの SQL_GD_BLOCK ビットマスクを返すドライバーには適用されません。<br /><br /> ドライバーまたはデータソースが、 *TargetType* 引数と対応する列の SQL データ型の組み合わせによって指定された変換をサポートしていません。 このエラーは、列の SQL データ型がドライバー固有の SQL データ型にマップされている場合にのみ適用されます。<br /><br /> ドライバーは ODBC 2.x*のみをサポートし、引数* *TargetType* は次のいずれかでした。<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> また、「付録 D: データ型」の [c データ型](../../../odbc/reference/appendixes/c-data-types.md) に示されているすべての interval c データ型についても説明します。<br /><br /> ドライバーがサポートしているのは3.50 より前のバージョンの ODBC のみで、引数 *TargetType* は SQL_C_GUID。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle* に対応するドライバーでは、関数はサポートされていません。|  
|IM017|非同期通知モードでは、ポーリングは無効になっています|通知モデルが使用されるたびに、ポーリングは無効になります。|  
|IM018|**Sqlcompleteasync** は、このハンドルで前の非同期操作を完了するために呼び出されていません。|ハンドルに対する前の関数呼び出しが SQL_STILL_EXECUTING を返し、通知モードが有効になっている場合は、処理を完了するために、ハンドルに対して **Sqlcompleteasync** を呼び出す必要があります。|  
  
## <a name="comments"></a>コメント  
 **SQLGetData** は、指定された列のデータを返します。 **SQLGetData** は、 **sqlfetch**、 **Sqlfetchscroll**、または **SQLExtendedFetch**によって結果セットから1つ以上の行がフェッチされた後にのみ呼び出すことができます。 可変長データが大きすぎて **SQLGetData** の1回の呼び出しで返されない場合 (アプリケーションの制限のため)、 **SQLGetData** はそれらを部分的に取得できます。 行の一部の列をバインドし、他の列に対して **SQLGetData** を呼び出すこともできますが、これにはいくつかの制限があります。 詳細については、「 [長い形式のデータの取得](../../../odbc/reference/develop-app/getting-long-data.md)」を参照してください。  
  
 ストリーミング出力パラメーターでの **SQLGetData** の使用の詳細については、「 [SQLGetData を使用した出力パラメーターの取得](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)」を参照してください。  
  
## <a name="using-sqlgetdata"></a>SQLGetData の使用  
 ドライバーが **SQLGetData**の拡張機能をサポートしていない場合、関数は、最後にバインドされた列よりも大きい数値を持つ非バインド列に対してのみデータを返すことができます。 さらに、データ行の中で、 **SQLGetData**の各呼び出しの*Col_or_Param_Num*引数の値は、前の呼び出しの*Col_or_Param_Num*の値以上である必要があります。つまり、列番号の昇順でデータを取得する必要があります。 最後に、拡張機能がサポートされていない場合は、行セットのサイズが1より大きい場合に **SQLGetData** を呼び出すことはできません。  
  
 ドライバーは、これらの制限を緩和できます。 アプリケーションは、ドライバーが緩和されする制限を判断するために、次のいずれかの SQL_GETDATA_EXTENSIONS オプションを使用して **SQLGetInfo** を呼び出します。  
  
-   SQL_GD_OUTPUT_PARAMS = **SQLGetData** を呼び出して、出力パラメーターの値を返すことができます。 詳細については、「 [SQLGetData を使用した出力パラメーターの取得](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)」を参照してください。  
  
-   SQL_GD_ANY_COLUMN。 このオプションが返された場合は、バインドされていない列に対して **SQLGetData** を呼び出すことができます (最後にバインドされた列の前を含む)。  
  
-   SQL_GD_ANY_ORDER。 このオプションが返された場合、バインドされていない列に対しては、任意の順序で **SQLGetData** を呼び出すことができます。  
  
-   SQL_GD_BLOCK。 このオプションが SQL_GETDATA_EXTENSIONS InfoType の **SQLGetInfo** によって返された場合、ドライバーは、行セットのサイズが1より大きい場合に **SQLGetData** への呼び出しをサポートします。また、SQLGetData を呼び出す前に、アプリケーションは、SQL_POSITION オプションを使用して **SQLSetPos** を呼び出して、正しい行にカーソルを置くことができ **ます。**  
  
-   SQL_GD_BOUND。 このオプションが返された場合は、バインドされた列および非バインド列に対して **SQLGetData** を呼び出すことができます。  
  
 これらの制限には、2つの例外があり、それらを緩和するためのドライバーの機能があります。 まず、行セットのサイズが1より大きい場合は、順方向専用カーソルに対して **SQLGetData** を呼び出さないでください。 2つ目の方法として、ドライバーがブックマークをサポートしている場合は、最後にバインドされた列の前にアプリケーションが**SQLGetData**を呼び出すことができない場合でも、列0に対して**SQLGetData**を呼び出すことを常にサポートする必要があります。 (アプリケーションが ODBC 2 を使用している*場合。 x*ドライバーは、 **sqlfetch**の呼び出しの**後に、** **SQLGetData**が0に等しい*Col_or_Param_Num*で呼び出された場合にブックマークを返し*ます。これ*は、 **sqlfetch**が SQL_FETCH_NEXT の*fetchorientation*によってマップされ、0の*Col_or_Param_Num*を持つ**SQLGetData**が*odbc 3. x ドライバー*マネージャーによって、 *foption* for SQL_GET_BOOKMARK で**SQLGetStmtOption**にマップされるためです。  
  
 カーソルが行に配置されていないため、SQLGetData オプションを指定 SQL_ADD して**Sqlbulkoperations**を呼び出すことによって挿入された行のブックマークを取得するために**SQLGetData**を使用することはできません。 アプリケーションでは、列0をバインドすることによって、そのような行のブックマークを取得できます。この場合、SQL_ADD で **Sqlbulkoperations** が呼び出されます。この場合、 **sqlbulkoperations** はバインドされたバッファー内のブックマークを返します。 その後、SQL_FETCH_BOOKMARK を指定して**Sqlfetchscroll**を呼び出して、その行のカーソルを再配置できます。  
  
 *TargetType*引数が interval データ型の場合、既定の間隔の有効桁数 (2) と既定の間隔の秒の有効桁数 (6) が、それぞれのの SQL_DESC_DATETIME_INTERVAL_PRECISION および SQL_DESC_PRECISION の各フィールドに設定されています。 *TargetType*引数が SQL_C_NUMERIC データ型である場合は、既定の有効桁数 (ドライバー定義) と既定の小数点以下桁数 (0) が使用されます。この値は、通常のの SQL_DESC_PRECISION と SQL_DESC_SCALE のフィールドで設定されます。 既定の有効桁数または小数点以下桁数が適切でない場合、アプリケーションは、 **SQLSetDescField** または **SQLSetDescRec**の呼び出しによって適切な記述子フィールドを明示的に設定する必要があります。 SQL_DESC_CONCISE_TYPE フィールドを SQL_C_NUMERIC に設定し、 *TargetType*引数を SQL_ARD_TYPE として**SQLGetData**を呼び出すことができます。これにより、記述子フィールドの有効桁数と小数点以下桁数の値が使用されます。  
  
> [!NOTE]
>  ODBC 2.x では、*アプリケーションは* *TargetType*を SQL_C_DATE、SQL_C_TIME、または SQL_C_TIMESTAMP に設定して、 \* *targetvalueptr*が日付、時刻、またはタイムスタンプの構造体であることを示します。 ODBC 3.x では、アプリケーションは*TargetType*を SQL_C_TYPE_DATE、SQL_C_TYPE_TIME、または SQL_C_TYPE_TIMESTAMP に設定*します。* ドライバーマネージャーは、アプリケーションとドライバーのバージョンに基づいて、必要に応じて適切なマッピングを行います。  
  
## <a name="retrieving-variable-length-data-in-parts"></a>部分的な可変長データの取得  
 **SQLGetData** を使用して、可変長データを含む列からデータを取得することができます。つまり、列の SQL データ型の識別子が SQL_CHAR、SQL_VARCHAR、SQL_LONGVARCHAR、SQL_WCHAR、SQL_WVARCHAR、SQL_WLONGVARCHAR、SQL_BINARY、SQL_VARBINARY、SQL_LONGVARBINARY、または可変長型のドライバー固有の識別子になります。  
  
 アプリケーションは、パーツの列からデータを取得するために、同じ列に対して複数回 **SQLGetData** を連続して呼び出します。 各呼び出しで、 **SQLGetData** はデータの次の部分を返します。 部分を再アセンブルするアプリケーションは、文字データの中間部分から null 終端文字を削除することに注意してください。 返されるデータが多いか、終端文字に十分なバッファーが割り当てられていない場合、 **SQLGetData** は SQL_SUCCESS_WITH_INFO と SQLSTATE 01004 (データが切り捨てられました) を返します。 データの最後の部分が返されると、 **SQLGetData** は SQL_SUCCESS を返します。 データを列から取得するための最後の有効な呼び出しでは、SQL_NO_TOTAL も0も返されません。これは、アプリケーションがアプリケーションバッファー内のどの程度のデータが有効であるかを知る方法がないためです。 この後に **SQLGetData** が呼び出されると、SQL_NO_DATA が返されます。 詳細については、次の「SQLGetData を使用したデータの取得」を参照してください。  
  
 可変長のブックマークは、 **SQLGetData**によって部分的に返すことができます。 他のデータと同様に、 **SQLGetData** を呼び出して可変長ブックマークを部分的に返すと、SQLSTATE 01004 (文字列データ、右側が切り詰められています) が返され、返されるデータが増えると SQL_SUCCESS_WITH_INFO されます。 これは、 **Sqlfetch** または **sqlfetchscroll**を呼び出すことによって可変長のブックマークが切り捨てられる場合とは異なり、SQL_ERROR と SQLSTATE 22001 (文字列データ、右の切り捨て) が返されます。  
  
 **SQLGetData** を使用して、固定長データを部分的に返すことはできません。 固定長データを含む列の行で **SQLGetData** が複数回呼び出された場合は、最初のすべての呼び出しに対して SQL_NO_DATA が返されます。  
  
## <a name="retrieving-streamed-output-parameters"></a>ストリーム出力パラメーターの取得  
 ドライバーでストリーム出力パラメーターがサポートされている場合、アプリケーションは小さなバッファーを使用して **SQLGetData** を何度も呼び出して、大きなパラメーター値を取得できます。 ストリーミング出力パラメーターの詳細については、「 [SQLGetData を使用した出力パラメーターの取得](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)」を参照してください。  
  
## <a name="retrieving-data-with-sqlgetdata"></a>SQLGetData を使用したデータの取得  
 **SQLGetData**は、指定された列のデータを返すために、次の一連の手順を実行します。  
  
1.  列のすべてのデータが既に返されている場合は SQL_NO_DATA を返します。  
  
2.  \*データが NULL の場合は、 *StrLen_or_IndPtr*を SQL_NULL_DATA に設定します。 データが NULL で *StrLen_or_IndPtr* が null ポインターの場合、 **SQLGetData** は SQLSTATE 22002 を返します (インジケーター変数が必要ですが、指定されていません)。  
  
     列のデータが NULL でない場合、 **SQLGetData** は手順3に進みます。  
  
3.  SQL_ATTR_MAX_LENGTH statement 属性が0以外の値に設定されている場合、列に文字データまたはバイナリデータが含まれていて、 **SQLGetData** が以前に列に対して呼び出されていない場合、データは SQL_ATTR_MAX_LENGTH バイトに切り捨てられます。  
  
    > [!NOTE]  
    >  SQL_ATTR_MAX_LENGTH statement 属性は、ネットワークトラフィックを減らすことを目的としています。 通常、データソースによって実装されます。これにより、データはネットワーク経由で返される前に切り捨てられます。 ドライバーとデータソースは、それをサポートするためには必要ありません。 したがって、データが特定のサイズに切り捨てられることを保証するために、アプリケーションでは、そのサイズのバッファーを割り当て、 *Bufferlength* 引数でサイズを指定する必要があります。  
  
4.  データを *TargetType*で指定された型に変換します。 データには、そのデータ型の既定の有効桁数と小数点以下桁数が指定されます。 *TargetType*が SQL_ARD_TYPE 場合は、の SQL_DESC_CONCISE_TYPE フィールドのデータ型が使用されます。 *TargetType*が SQL_ARD_TYPE 場合、データには、SQL_DESC_CONCISE_TYPE フィールドのデータ型に応じて、の SQL_DESC_DATETIME_INTERVAL_PRECISION、SQL_DESC_PRECISION、および SQL_DESC_SCALE の各フィールドに有効桁数と小数点以下桁数が設定されます。 既定の有効桁数または小数点以下桁数が適切でない場合、アプリケーションは、 **SQLSetDescField** または **SQLSetDescRec**の呼び出しによって適切な記述子フィールドを明示的に設定する必要があります。  
  
5.  データが文字やバイナリなどの可変長データ型に変換された場合、 **SQLGetData** はデータ長が *bufferlength*を超えているかどうかをチェックします。 文字データの長さ (null 終端文字を含む) が *Bufferlength*を超える場合、 **SQLGetData** は、null 終端文字の長さを下回る *bufferlength* にデータを切り捨てます。 その後、データを null で終了します。 バイナリデータの長さがデータバッファーの長さを超える場合、 **SQLGetData** はそれを *bufferlength* バイトに切り捨てます。  
  
     指定されたデータバッファーが小さすぎて null 終了文字を保持できない場合、 **SQLGetData** は SQL_SUCCESS_WITH_INFO と SQLSTATE 01004 を返します。  
  
     **SQLGetData** では、固定長データ型に変換されたデータは切り捨てられません。常に、**Targetvalueptr* の長さがデータ型のサイズであることを前提としています。  
  
6.  変換された (場合によっては切り捨てられた) データを \* *targetvalueptr*に配置します。 **SQLGetData**は、行外のデータを返すことができないことに注意してください。  
  
7.  データの長さを StrLen_or_IndPtr に配置し \* *StrLen_or_IndPtr*ます。 *StrLen_or_IndPtr*が null ポインターの場合、 **SQLGetData**は長さを返しません。  
  
    -   文字またはバイナリデータの場合、これは変換後のデータの長さと *Bufferlength*による切り捨ての前になります。 変換後にドライバーがデータの長さを決定できない場合は、長いデータの場合と同様に、SQL_SUCCESS_WITH_INFO を返し、長さを SQL_NO_TOTAL に設定します。 ( **SQLGetData**への最後の呼び出しでは、0または SQL_NO_TOTAL ではなく、常にデータの長さが返される必要があります)。SQL_ATTR_MAX_LENGTH statement 属性によりデータが切り詰められた場合、実際の長さではなく、この属性の値が StrLen_or_IndPtr に配置され \* *StrLen_or_IndPtr*ます。 この属性は変換前にサーバー上のデータを切り捨てるように設計されているため、ドライバーは実際の長さを調べることができません。 同じ列に対して **SQLGetData** が連続して複数回呼び出された場合、これは現在の呼び出しの開始時に使用できるデータの長さになります。つまり、後続の各呼び出しで長さが減少します。  
  
    -   他のすべてのデータ型については、変換後のデータの長さです。つまり、データが変換された型のサイズです。  
  
8.  変換中に有意性を損なうことなくデータが切り捨てられた場合 (たとえば、実数1.234 が整数1に変換されたときに切り捨てられた場合)、または *Bufferlength* が小さすぎる (たとえば、文字列 "abcdef" が4バイトバッファーに配置されている) 場合、 **SQLGetData** は SQLSTATE 01004 (データの切り捨て) と SQL_SUCCESS_WITH_INFO を返します SQL_ATTR_MAX_LENGTH statement 属性が原因で、データが有意性を失わずに切り捨てられた場合、 **SQLGetData** は SQL_SUCCESS を返し、SQLSTATE 01004 (データが切り捨てられたデータ) を返しません。  
  
 バインドされたデータバッファーの内容 (バインドされた列で **SQLGetData** が呼び出された場合)。 **SQLGetData** が SQL_SUCCESS または SQL_SUCCESS_WITH_INFO を返さない場合は、長さ/インジケーターバッファーが未定義になります。  
  
 **SQLGetData**を連続して呼び出すと、要求された最後の列からデータが取得されます。前のオフセットが無効になります。 たとえば、次のようなシーケンスが実行されたとします。  
  
```cpp  
SQLGetData(icol=n), SQLGetData(icol=m), SQLGetData(icol=n)  
```  
  
 SQLGetData (icol = n) への2回目の呼び出しでは、n 列の先頭からデータを取得します。 以前に列の **SQLGetData** を呼び出すことによるデータのオフセットは、有効ではなくなりました。  
  
## <a name="descriptors-and-sqlgetdata"></a>記述子と SQLGetData  
 **SQLGetData** は、どの記述子フィールドとも直接は対話しません。  
  
 *TargetType*が SQL_ARD_TYPE 場合は、の SQL_DESC_CONCISE_TYPE フィールドのデータ型が使用されます。 *TargetType*が SQL_ARD_TYPE または SQL_C_DEFAULT の場合は、SQL_DESC_SCALE フィールドのデータ型に応じて、の SQL_DESC_DATETIME_INTERVAL_PRECISION、SQL_DESC_PRECISION、および SQL_DESC_CONCISE_TYPE の各フィールドの有効桁数と小数点以下桁数がデータに与えられます。  
  
## <a name="code-example"></a>コード例  
 次の例では、アプリケーションが SELECT ステートメントを実行 **し** て、名前、ID、および電話番号で並べ替えられた顧客 id、名前、および電話番号の結果セットを返します。 データの各行に対して **Sqlfetch** を呼び出して、カーソルを次の行に配置します。 **SQLGetData**を呼び出して、フェッチされたデータを取得します。データのバッファーと返されるバイト数は、 **SQLGetData**の呼び出しで指定されます。 最後に、各従業員の名前、ID、および電話番号を出力します。  
  
```cpp  
#define NAME_LEN 50  
#define PHONE_LEN 50  
  
SQLCHAR      szName[NAME_LEN], szPhone[PHONE_LEN];  
SQLINTEGER   sCustID, cbName, cbAge, cbBirthday;  
SQLRETURN    retcode;  
SQLHSTMT     hstmt;  
  
retcode = SQLExecDirect(hstmt,  
   "SELECT CUSTID, NAME, PHONE FROM CUSTOMERS ORDER BY 2, 1, 3",  
   SQL_NTS);  
  
if (retcode == SQL_SUCCESS) {  
   while (TRUE) {  
      retcode = SQLFetch(hstmt);  
      if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO) {  
         show_error();  
      }  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO){  
  
         /* Get data for columns 1, 2, and 3 */  
  
         SQLGetData(hstmt, 1, SQL_C_ULONG, &sCustID, 0, &cbCustID);  
         SQLGetData(hstmt, 2, SQL_C_CHAR, szName, NAME_LEN, &cbName);  
         SQLGetData(hstmt, 3, SQL_C_CHAR, szPhone, PHONE_LEN,  
            &cbPhone);  
  
         /* Print the row of data */  
  
         fprintf(out, "%-5d %-*s %*s", sCustID, NAME_LEN-1, szName,   
            PHONE_LEN-1, szPhone);  
      } else {  
         break;  
      }  
   }  
}  
```  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|結果セットの列にストレージを割り当てる|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|ブロックカーソル位置に関係のない一括操作の実行|[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|ステートメント処理の取り消し|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|SQL ステートメントの実行|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|準備された SQL ステートメントの実行|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|データのブロックのフェッチまたは結果セットのスクロール|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|1行のデータまたはデータのブロックを順方向専用にフェッチする|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|実行時にパラメーターデータを送信する|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|カーソルの配置、行セット内のデータの更新、または行セット内のデータの更新または削除|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダーファイル](../../../odbc/reference/install/odbc-header-files.md)   
 [SQLGetData を使用した出力パラメーターの取得](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
