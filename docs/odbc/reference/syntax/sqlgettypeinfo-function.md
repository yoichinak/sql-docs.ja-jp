---
description: SQLGetTypeInfo 関数
title: SQLGetTypeInfo 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetTypeInfo
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetTypeInfo
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC]
ms.assetid: bdedb044-8924-4ca4-85f3-8b37578e0257
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 47ff65a1c7912aef196c79b9b26c8286fb05fef2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421196"
---
# <a name="sqlgettypeinfo-function"></a>SQLGetTypeInfo 関数
**互換性**  
 導入されたバージョン: ODBC 1.0 標準準拠: ISO 92  
  
 **まとめ**  
 **SQLGetTypeInfo** は、データソースでサポートされているデータ型に関する情報を返します。 ドライバーは、SQL 結果セットの形式で情報を返します。 データ型は、データ定義言語 (DDL) ステートメントで使用することを目的としています。  
  
> [!IMPORTANT]  
>  アプリケーションでは、 **ALTER TABLE**および**CREATE TABLE**ステートメントの**SQLGetTypeInfo**結果セットの TYPE_NAME 列に返される型名を使用する必要があります。 **SQLGetTypeInfo** は、DATA_TYPE 列に同じ値を持つ複数の行を返す場合があります。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLGetTypeInfo(  
     SQLHSTMT      StatementHandle,  
     SQLSMALLINT   DataType);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入結果セットのステートメントハンドル。  
  
 *DataType*  
 代入SQL データ型。 これは、「付録 D: データ型」の「 [Sql データ型](../../../odbc/reference/appendixes/sql-data-types.md) 」またはドライバー固有の sql データ型のいずれかの値である必要があります。 SQL_ALL_TYPES は、すべてのデータ型に関する情報を返すことを指定します。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **SQLGetTypeInfo**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合、関連付けられた SQLSTATE 値を取得するには、 *Handletype* SQL_HANDLE_STMT と*StatementHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出します。 次の表に、 **SQLGetTypeInfo** によって一般的に返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01S02|オプションの値が変更されました|実装の動作条件により、指定されたステートメント属性は無効でした。そのため、類似した値が一時的に置き換えられました。 ( **SQLGetStmtAttr** を呼び出して、一時的に置き換えられる値を決定します。)代替値は、カーソルが閉じられるまで *StatementHandle* に対して有効です。 変更できるステートメント属性は、SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE、SQL_ATTR_KEYSET_SIZE、SQL_ATTR_MAX_LENGTH、SQL_ATTR_MAX_ROWS、SQL_ATTR_QUERY_TIMEOUT、および SQL_ATTR_SIMULATE_CURSOR です。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続されていたデータソースとの間の通信リンクが失敗しました。|  
|24000|カーソル状態が無効|*StatementHandle*でカーソルが開かれました。 **sqlfetch**または**sqlfetchscroll**が呼び出されました。 このエラーは、 **Sqlfetch** または **sqlfetchscroll** が SQL_NO_DATA 返されなかった場合にドライバーマネージャーによって返されます。また、 **Sqlfetch** または **sqlfetchscroll** が SQL_NO_DATA を返した場合は、ドライバーによって返されます。<br /><br /> *StatementHandle*で結果セットが開かれましたが、 **sqlfetch**または**sqlfetchscroll**は呼び出されませんでした。|  
|40001|シリアル化エラー|リソースが別のトランザクションでデッドロックしているため、トランザクションがロールバックされました。|  
|40003|ステートメントの完了が不明です|この関数の実行中に関連付けられた接続が失敗したため、トランザクションの状態を確認できません。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * \* Messagetext*バッファーの**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY004|SQL データ型が無効です|引数のデータ型に指定 *された* 値は、有効な ODBC SQL データ型識別子でも、ドライバーでサポートされているドライバー固有のデータ型識別子でもありませんでした。|  
|HY008|操作が取り消されました|非同期処理が *StatementHandle*に対して有効にされた後、関数が呼び出され、実行が完了する前に、 **SQLCancel** または **sqlcancelhandle** が *StatementHandle*で呼び出されました。 次に、 *StatementHandle*で関数が再度呼び出されました。<br /><br /> 関数が呼び出され、実行が完了する前に、マルチスレッドアプリケーションの別のスレッドの*StatementHandle*で**SQLCancel**または**sqlcancelhandle**が呼び出されました。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、 **SQLGetTypeInfo** 関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または **Sqlmoreresults** が *StatementHandle* に対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。<br /><br /> (DM) 非同期的に実行されている関数 (この1つではない) が *StatementHandle* に対して呼び出され、この関数が呼び出されたときにまだ実行されています。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **Sqlbulkoperations**、 **SQLSetPos** が *StatementHandle* に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYC00|省略可能な機能は実装されていません|SQL_ATTR_CONCURRENCY および SQL_ATTR_CURSOR_TYPE statement 属性の現在の設定の組み合わせは、ドライバーまたはデータソースではサポートされていませんでした。<br /><br /> SQL_ATTR_USE_BOOKMARKS statement 属性が SQL_UB_VARIABLE に設定されており、SQL_ATTR_CURSOR_TYPE statement 属性が、ドライバーがブックマークをサポートしていないカーソルの種類に設定されました。|  
|HYT00|タイムアウトに達しました|データソースから結果セットが返される前に、クエリのタイムアウト期間が経過しました。 タイムアウト期間は、 **SQLSetStmtAttr**、SQL_ATTR_QUERY_TIMEOUT によって設定されます。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle* に対応するドライバーでは、関数はサポートされていません。|  
|IM017|非同期通知モードでは、ポーリングは無効になっています|通知モデルが使用されるたびに、ポーリングは無効になります。|  
|IM018|**Sqlcompleteasync** は、このハンドルで前の非同期操作を完了するために呼び出されていません。|ハンドルに対する前の関数呼び出しが SQL_STILL_EXECUTING を返し、通知モードが有効になっている場合は、処理を完了するために、ハンドルに対して **Sqlcompleteasync** を呼び出す必要があります。|  
  
## <a name="comments"></a>コメント  
 **SQLGetTypeInfo** は、結果を DATA_TYPE 順に並べ替え、データ型が対応する ODBC SQL データ型にどの程度近いかを、標準の結果セットとして返します。 データソースによって定義されるデータ型は、ユーザー定義データ型よりも優先されます。 その結果、並べ替え順序は必ずしも一貫しているとは限りませんが、最初に DATA_TYPE として一般化し、次に昇順で TYPE_NAME することができます。 たとえば、データソースが定義されている整数データ型とカウンターデータ型で、COUNTER は自動インクリメントされ、ユーザー定義データ型 WHOLENUM も定義されているとします。 WHOLENUM は ODBC SQL データ型 SQL_INTEGER に厳密にマップされますが、データソースでサポートされている場合でも自動インクリメントデータ型は ODBC SQL データ型には厳密にマップされないため、これらは order INTEGER、WHOLENUM、および COUNTER で返されます。 この情報の使用方法については、「 [DDL ステートメント](../../../odbc/reference/develop-app/ddl-statements.md)」を参照してください。  
  
 *DataType*引数で、ドライバーでサポートされている ODBC のバージョンに対して有効なデータ型が指定されているが、ドライバーでサポートされていない場合、空の結果セットが返されます。  
  
> [!NOTE]  
>  一般的な使用、引数、および ODBC カタログ関数の返されるデータの詳細については、「 [カタログ関数](../../../odbc/reference/develop-app/catalog-functions.md)」を参照してください。  
  
 ODBC 3 では、次の列の名前が変更されています。*x*。 アプリケーションは列番号でバインドされるため、列名の変更は旧バージョンとの互換性に影響しません。  
  
|ODBC 2.0 列|ODBC 3.*x* 列|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|MONEY|FIXED_PREC_SCALE|  
|AUTO_INCREMENT|AUTO_UNIQUE_VALUE|  
  
 **SQLGetTypeInfo**によって ODBC 3 に返される結果セットには、次の列が追加されています。*x*:  
  
-   SQL_DATA_TYPE  
  
-   INTERVAL_PRECISION  
  
-   SQL_DATETIME_SUB  
  
-   NUM_PREC_RADIX  
  
 次の表に、結果セット内の列の一覧を示します。 ドライバーでは、列 19 (INTERVAL_PRECISION) 以外の列を定義できます。 アプリケーションでは、明示的な序数位置を指定するのではなく、結果セットの末尾からカウントすることで、ドライバー固有の列にアクセスする必要があります。 詳細については、「 [カタログ関数によって返されるデータ](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)」を参照してください。  
  
> [!NOTE]  
>  **SQLGetTypeInfo** では、すべてのデータ型が返されるとは限りません。 たとえば、ドライバーがユーザー定義データ型を返さない場合があります。 アプリケーションでは、 **SQLGetTypeInfo**によって返されるかどうかにかかわらず、任意の有効なデータ型を使用できます。 **SQLGetTypeInfo**によって返されるデータ型は、データソースでサポートされています。 これらは、データ定義言語 (DDL) ステートメントで使用するためのものです。 ドライバーは、 **SQLGetTypeInfo**によって返される型以外のデータ型を使用して、結果セットのデータを返すことができます。 カタログ関数の結果セットを作成するときに、ドライバーがデータソースでサポートされていないデータ型を使用している可能性があります。  
  
|列名|列<br /><br /> number|データ型|コメント|  
|-----------------|-----------------------|---------------|--------------|  
|TYPE_NAME (ODBC 2.0)|1|Varchar not NULL|データソースに依存するデータ型の名前。たとえば、「CHAR ()」、「VARCHAR ()」、「MONEY」、「LONG VARBINARY」、または「CHAR () FOR BIT DATA」とします。 アプリケーションでは、 **CREATE TABLE** および **ALTER TABLE** ステートメントでこの名前を使用する必要があります。|  
|DATA_TYPE (ODBC 2.0)|2|Smallint (NULL 以外)|SQL データ型。 ODBC SQL データ型またはドライバー固有の SQL データ型を指定できます。 Datetime または interval データ型の場合、この列は簡潔なデータ型 (SQL_TYPE_TIME や SQL_INTERVAL_YEAR_TO_MONTH など) を返します。 有効な ODBC SQL データ型の一覧については、「付録 D: データ型」の「 [Sql データ](../../../odbc/reference/appendixes/sql-data-types.md) 型」を参照してください。 ドライバー固有の SQL データ型の詳細については、ドライバーのドキュメントを参照してください。|  
|COLUMN_SIZE (ODBC 2.0)|3|Integer|サーバーがこのデータ型に対してサポートする最大列サイズ。 数値データの場合、これは最大有効桁数です。 文字列データの場合は、文字数で指定します。 Datetime データ型の場合、これは文字列形式の文字数 (秒の小数部の最大有効桁数を想定) です。 列サイズが適用されないデータ型に対しては NULL が返されます。 Interval データ型の場合、これは間隔のリテラルの文字表現に含まれる文字数です。これは、間隔の先頭の有効桁数によって定義されます。「付録 D: データ型」の「 [Interval データ型の長さ](../../../odbc/reference/appendixes/interval-data-type-length.md) 」を参照してください。<br /><br /> 列のサイズの詳細については、「付録 D: データ型」の「 [列のサイズ、10進数、転送オクテットの長さ、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 」を参照してください。|  
|LITERAL_PREFIX (ODBC 2.0)|4|Varchar|リテラルのプレフィックスとして使用される文字または文字。たとえば、文字データ型には単一引用符 (')、バイナリデータ型には0x を使用します。リテラルプレフィックスが適用されないデータ型に対しては NULL が返されます。|  
|LITERAL_SUFFIX (ODBC 2.0)|5|Varchar|リテラルを終了するために使用される文字。たとえば、文字データ型には単一引用符 (') を使用します。リテラルサフィックスが適用されないデータ型に対しては NULL が返されます。|  
|CREATE_PARAMS (ODBC 2.0)|6|Varchar|TYPE_NAME フィールドで返される名前を使用するときに、アプリケーションがかっこで囲んで指定できる各パラメーターに対応する、コンマで区切られたキーワードの一覧。 リスト内のキーワードには、長さ、有効桁数、または小数点以下のいずれかを指定できます。 構文の使用に必要な順序で表示されます。 たとえば、DECIMAL の CREATE_PARAMS は "precision, scale" です。VARCHAR の CREATE_PARAMS は "length" と等しくなります。 データ型の定義にパラメーターがない場合は、NULL が返されます。たとえば、INTEGER のようになります。<br /><br /> ドライバーは、使用されている国/地域の言語で CREATE_PARAMS テキストを提供します。|  
|NULLABLE (ODBC 2.0)|7|Smallint (NULL 以外)|データ型が NULL 値を許容するかどうかを示します。<br /><br /> データ型が NULL 値を許容しない場合は SQL_NO_NULLS。<br /><br /> データ型が NULL 値を許容するかどうかを SQL_NULLABLE します。<br /><br /> 列が NULL 値を許容するかどうかが不明な場合に SQL_NULLABLE_UNKNOWN します。|  
|CASE_SENSITIVE (ODBC 2.0)|8|Smallint (NULL 以外)|照合順序と比較で文字データ型が大文字と小文字を区別するかどうか。<br /><br /> データ型が文字データ型で、大文字と小文字を区別する場合は SQL_TRUE。<br /><br /> データ型が文字データ型でない場合、または大文字と小文字を区別しない場合は SQL_FALSE。|  
|検索可能 (ODBC 2.0)|9|Smallint (NULL 以外)|**WHERE**句でのデータ型の使用方法:<br /><br /> **WHERE**句で列を使用できない場合は SQL_PRED_NONE します。 (これは、ODBC 2 の SQL_UNSEARCHABLE 値と同じです。*x*)<br /><br /> **WHERE**句で列を使用できるかどうかを SQL_PRED_CHAR します。ただし、 **LIKE**述語でのみ使用できます。 (これは、ODBC 2 の SQL_LIKE_ONLY 値と同じです。*x*)<br /><br /> **WHERE**句で列を使用できるかどうかを指定します。ただし、 **LIKE** (比較、定量化された比較、 **BETWEEN**、 **DISTINCT**、 **in**、 **MATCH**、 **UNIQUE**) 以外のすべての比較演算子を使用できます。 SQL_PRED_BASIC (これは、ODBC 2 の SQL_ALL_EXCEPT_LIKE 値と同じです。*x*)<br /><br /> 任意の比較演算子を持つ **where** 句で列を使用できるかどうかを SQL_SEARCHABLE します。|  
|UNSIGNED_ATTRIBUTE (ODBC 2.0)|10|Smallint|データ型が符号なしであるかどうか。<br /><br /> データ型が符号なしである場合は SQL_TRUE します。<br /><br /> データ型が署名されている場合は SQL_FALSE します。<br /><br /> 属性がデータ型に適用されない場合、またはデータ型が数値でない場合は、NULL が返されます。|  
|FIXED_PREC_SCALE (ODBC 2.0)|11|Smallint (NULL 以外)|データ型に、money データ型などの定義済みの有効桁数と小数点以下桁数 (データソース固有) があるかどうか。<br /><br /> 定義済みの有効桁数と小数点以下桁数が設定されている場合は SQL_TRUE します。<br /><br /> 定義済みの有効桁数と小数点以下桁数が定義されていない場合は SQL_FALSE します。|  
|AUTO_UNIQUE_VALUE (ODBC 2.0)|12|Smallint|データ型が自動増分であるかどうか。<br /><br /> データ型が自動増分の場合に SQL_TRUE します。<br /><br /> データ型が自動増分でない場合は SQL_FALSE します。<br /><br /> 属性がデータ型に適用されない場合、またはデータ型が数値でない場合は、NULL が返されます。<br /><br /> アプリケーションでは、この属性を持つ列に値を挿入できますが、通常、列の値を更新することはできません。<br /><br /> 自動インクリメント列に挿入が行われると、挿入時に一意の値が列に挿入されます。 インクリメントは定義されていませんが、データソース固有です。 アプリケーションでは、自動インクリメント列が特定のポイントで開始されるか、特定の値によってインクリメントされることを想定しないでください。|  
|LOCAL_TYPE_NAME (ODBC 2.0)|13|Varchar|データソースに依存するデータ型のローカライズされたバージョン。 ローカライズされた名前がそのデータ ソースによってサポートされない場合は NULL が返されます。 この名前は、ダイアログボックスなどの表示のみを目的としています。|  
|MINIMUM_SCALE (ODBC 2.0)|14|Smallint|データソースのデータ型の最小小数点以下桁数です。 データ型の小数点以下桁数が固定されている場合は、MINIMUM_SCALE 列および MAXIMUM_SCALE 列の両方にこの値が入ります。 たとえば、SQL_TYPE_TIMESTAMP 列には、秒の小数部に固定された小数点以下桁数があります。 小数点以下桁数が適用されない場合は NULL が返されます。 詳細については、「付録 D: データ型」の「 [列のサイズ、10進数、転送オクテットの長さ、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 」を参照してください。|  
|MAXIMUM_SCALE (ODBC 2.0)|15|Smallint|データソースのデータ型の最大小数点以下桁数です。 小数点以下桁数が適用されない場合は NULL が返されます。 最大小数点以下桁数がデータソースで個別に定義されていないが、最大有効桁数と同じになるように定義されている場合、この列には COLUMN_SIZE 列と同じ値が格納されます。 詳細については、「付録 D: データ型」の「 [列のサイズ、10進数、転送オクテットの長さ、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 」を参照してください。|  
|SQL_DATA_TYPE (ODBC 3.0)|16|NULL でない Smallint|記述子の SQL_DESC_TYPE フィールドに表示される SQL データ型の値。 この列は DATA_TYPE 列と同じですが、interval データ型と datetime データ型は除きます。<br /><br /> Interval データ型および datetime データ型の場合、結果セットの SQL_DATA_TYPE フィールドは SQL_INTERVAL または SQL_DATETIME を返し、SQL_DATETIME_SUB フィールドは特定の interval データ型または datetime データ型のサブコードを返します。 (「 [付録 D: データ型](../../../odbc/reference/appendixes/appendix-d-data-types.md)」を参照してください)。|  
|SQL_DATETIME_SUB (ODBC 3.0)|17|Smallint|SQL_DATA_TYPE の値が SQL_DATETIME または SQL_INTERVAL の場合、この列には DATETIME/INTERVAL サブコードが格納されます。 Datetime および interval 以外のデータ型の場合、このフィールドは NULL になります。<br /><br /> Interval データ型または datetime データ型の場合、結果セットの SQL_DATA_TYPE フィールドは SQL_INTERVAL または SQL_DATETIME を返し、SQL_DATETIME_SUB フィールドは特定の interval データ型または datetime データ型のサブコードを返します。 (「 [付録 D: データ型](../../../odbc/reference/appendixes/appendix-d-data-types.md)」を参照してください)。|  
|NUM_PREC_RADIX (ODBC 3.0)|18|Integer|データ型が概数型の場合、この列には値2が含まれ、COLUMN_SIZE によってビット数が指定されていることを示します。 真数型の場合、この列には値10が格納され、COLUMN_SIZE が小数点以下桁数を指定することを示します。 その他の場合、この列は NULL になります。|  
|INTERVAL_PRECISION (ODBC 3.0)|19|Smallint|データ型が interval データ型の場合、この列には、間隔の先頭の有効桁数の値が格納されます。 (「付録 D: データ型」の「 [Interval データ型の有効桁数](../../../odbc/reference/appendixes/interval-data-type-precision.md) 」を参照してください)。それ以外の場合、この列は NULL になります。|  
  
 属性情報は、データ型または結果セット内の特定の列に適用できます。 **SQLGetTypeInfo** は、データ型に関連付けられている属性に関する情報を返します。 **Sqlcolattribute** は、結果セット内の列に関連付けられている属性に関する情報を返します。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|結果セット内の列へのバッファーのバインド|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|ステートメント処理の取り消し|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|結果セットの列に関する情報を返す|[SQLColAttribute 関数](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|データのブロックのフェッチまたは結果セットのスクロール|[SQLFetchScroll 関数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|1つの行またはデータのブロックを順方向専用にフェッチする|[SQLFetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|ドライバーまたはデータソースに関する情報を返す|[SQLGetInfo 関数](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
