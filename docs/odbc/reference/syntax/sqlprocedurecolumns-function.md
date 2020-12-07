---
description: SQLProcedureColumns 関数
title: SQLProcedureColumns 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLProcedureColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLProcedureColumns
helpviewer_keywords:
- SQLProcedureColumns function [ODBC]
ms.assetid: 4ca37b28-a6df-465b-8988-d422d37fc025
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6a818eb4f01d22a8dfda7a7fa5958d7914c8c126
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487160"
---
# <a name="sqlprocedurecolumns-function"></a>SQLProcedureColumns 関数
**互換性**  
 導入されたバージョン: ODBC 1.0 標準準拠: ODBC  
  
 **まとめ**  
 **SQLProcedureColumns** は、入力パラメーターと出力パラメーターの一覧、および指定されたプロシージャの結果セットを構成する列を返します。 ドライバーは、指定されたステートメントの結果セットとして情報を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLProcedureColumns(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     ProcName,  
     SQLSMALLINT   NameLength3,  
     SQLCHAR *     ColumnName,  
     SQLSMALLINT   NameLength4);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル。  
  
 *CatalogName*  
 代入プロシージャカタログ名。 ドライバーがいくつかの手順のカタログをサポートしていても、他のプロシージャに対してはサポートされていない場合 (ドライバーが異なる Dbms からデータを取得する場合など)、空の文字列 ("") は、カタログを持たないプロシージャを表します。 *CatalogName* に文字列検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *CatalogName* は識別子として扱われ、大文字小文字は区別されません。 SQL_FALSE の場合、 *CatalogName* は通常の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。 詳細については、「 [カタログ関数の引数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)」を参照してください。  
  
 *NameLength1*  
 代入**CatalogName*の文字数。  
  
 *SchemaName*  
 代入プロシージャスキーマ名の文字列検索パターン。 ドライバーがいくつかのプロシージャのスキーマをサポートしているが、他のプロシージャのスキーマをサポートしていない場合 (ドライバーがさまざまな Dbms からデータを取得する場合など)、空の文字列 ("") はスキーマを持たないプロシージャを表します。  
  
 SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *SchemaName* は識別子として扱われ、大文字小文字は区別されません。 SQL_FALSE の場合、 *SchemaName* はパターン値の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。  
  
 *NameLength2*  
 代入**SchemaName*の文字数。  
  
 *ProcName*  
 代入プロシージャ名の文字列検索パターン。  
  
 SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *ProcName* は識別子として扱われ、大文字小文字は区別されません。 SQL_FALSE の場合、 *ProcName* はパターン値の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。  
  
 *NameLength3*  
 代入**ProcName*の文字数。  
  
 *[ColumnName]*  
 代入列名の文字列検索パターン。  
  
 SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *ColumnName* は識別子として扱われ、その大文字と小文字は区別されません。 SQL_FALSE の場合、 *ColumnName* はパターン値の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。  
  
 *NameLength4*  
 代入**ColumnName*の文字数。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **SQLProcedureColumns**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合、関連付けられた SQLSTATE 値を取得するには、 *Handletype* SQL_HANDLE_STMT と*StatementHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出します。 次の表に、 **SQLProcedureColumns** によって一般的に返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続されていたデータソースとの間の通信リンクが失敗しました。|  
|24000|カーソル状態が無効|*StatementHandle*でカーソルが開かれました。 **sqlfetch**または**sqlfetchscroll**が呼び出されました。 このエラーは、 **Sqlfetch** または **sqlfetchscroll** が SQL_NO_DATA 返されなかった場合にドライバーマネージャーによって返されます。また、 **Sqlfetch** または **sqlfetchscroll** が SQL_NO_DATA を返した場合は、ドライバーによって返されます。<br /><br /> *StatementHandle*でカーソルが開いていましたが、 **sqlfetch**または**sqlfetchscroll**が呼び出されていません。|  
|40001|シリアル化エラー|リソースが別のトランザクションでデッドロックしているため、トランザクションがロールバックされました。|  
|40003|ステートメントの完了が不明です|この関数の実行中に関連付けられた接続に失敗しました。トランザクションの状態を確認できません。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * \* Messagetext*バッファーの**SQLError**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|*StatementHandle*に対して非同期処理が有効になりました。 関数が呼び出され、実行が完了する前に、 **SQLCancel** または **Sqlcancelhandle** が *StatementHandle*で呼び出されました。 次に、 *StatementHandle*で関数が再度呼び出されました。<br /><br /> 関数が呼び出され、実行が完了する前に、マルチスレッドアプリケーションの別のスレッドの*StatementHandle*で**SQLCancel**または**sqlcancelhandle**が呼び出されました。|  
|HY009|Null ポインターの使い方が正しくありません|SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されました。 *CatalogName* 引数は null ポインターで、SQL_CATALOG_NAME *InfoType* はカタログ名がサポートされていることを返します。<br /><br /> (DM) SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定され、 *SchemaName*、 *ProcName*、または *ColumnName* 引数が null ポインターでした。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この aynschronous 関数は、SQLProcedureColumns 関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または **Sqlmoreresults** が *StatementHandle* に対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。<br /><br /> (DM) 非同期的に実行されている関数 (この1つではない) が *StatementHandle* に対して呼び出され、この関数が呼び出されたときにまだ実行されています。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **Sqlbulkoperations**、 **SQLSetPos** が *StatementHandle* に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。|  
|HY090|文字列またはバッファーの長さが無効です|(DM) 名前の長さの引数のいずれかの値が0未満ですが SQL_NTS と等しくありません。<br /><br /> 名前の長さの引数のいずれかの値が、対応するカタログ、スキーマ、プロシージャ、または列名の最大長の値を超えています。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYC00|省略可能な機能は実装されていません|プロシージャカタログが指定されましたが、ドライバーまたはデータソースがカタログをサポートしていません。<br /><br /> プロシージャスキーマが指定されましたが、ドライバーまたはデータソースがスキーマをサポートしていません。<br /><br /> プロシージャスキーマ、プロシージャ名、または列名に文字列検索パターンが指定されています。データソースは、これらの引数の1つ以上の検索パターンをサポートしていません。<br /><br /> SQL_ATTR_CONCURRENCY および SQL_ATTR_CURSOR_TYPE statement 属性の現在の設定の組み合わせは、ドライバーまたはデータソースではサポートされていませんでした。<br /><br /> SQL_ATTR_USE_BOOKMARKS statement 属性が SQL_UB_VARIABLE に設定されており、SQL_ATTR_CURSOR_TYPE statement 属性が、ドライバーがブックマークをサポートしていないカーソルの種類に設定されました。|  
|HYT00|タイムアウトに達しました|データソースが結果セットを返す前にタイムアウト期間が経過しました。 タイムアウト期間は、 **SQLSetStmtAttr**、SQL_ATTR_QUERY_TIMEOUT によって設定されます。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle* に関連付けられているドライバーでは、関数はサポートされていません。|  
|IM017|非同期通知モードでは、ポーリングは無効になっています|通知モデルが使用されるたびに、ポーリングは無効になります。|  
|IM018|**Sqlcompleteasync** は、このハンドルで前の非同期操作を完了するために呼び出されていません。|ハンドルに対する前の関数呼び出しが SQL_STILL_EXECUTING を返し、通知モードが有効になっている場合は、処理を完了するために、ハンドルに対して **Sqlcompleteasync** を呼び出す必要があります。|  
  
## <a name="comments"></a>コメント  
 通常、この関数は、プロシージャパラメーターに関する情報と、プロシージャによって返される結果セットを構成する列 (存在する場合) を取得するために、ステートメントの実行前に使用されます。 詳細については、「[プロシージャ](../../../odbc/reference/develop-app/procedures-odbc.md)」を参照してください。  
  
> [!NOTE]  
>  **SQLProcedureColumns** は、プロシージャで使用されているすべての列を返すとは限りません。 たとえば、ドライバーが返すのは、プロシージャによって使用されるパラメーターに関する情報だけで、生成される結果セットの列ではありません。  
  
 *SchemaName*、 *ProcName*、および*ColumnName*引数では、検索パターンを使用できます。 有効な検索パターンの詳細については、「 [Pattern 値の引数](../../../odbc/reference/develop-app/pattern-value-arguments.md)」を参照してください。  
  
> [!NOTE]  
>  一般的な使用、引数、および ODBC カタログ関数の返されるデータの詳細については、「 [カタログ関数](../../../odbc/reference/develop-app/catalog-functions.md)」を参照してください。  
  
 **SQLProcedureColumns** は、結果を PROCEDURE_CAT、PROCEDURE_SCHEM、PROCEDURE_NAME、および COLUMN_TYPE 順に並べ替えて、標準の結果セットとして返します。 各プロシージャに対して列名が返される順序は、戻り値の名前、プロシージャ呼び出し内の各パラメーターの名前 (呼び出し順)、およびプロシージャによって返される結果セット内の各列の名前 (列の順序) です。  
  
 アプリケーションでは、ドライバー固有の列を結果セットの末尾に対して相対的にバインドする必要があります。 詳細については、「 [カタログ関数によって返されるデータ](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)」を参照してください。  
  
 PROCEDURE_CAT、PROCEDURE_SCHEM、PROCEDURE_NAME、および COLUMN_NAME 列の実際の長さを確認するには、アプリケーションで、SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN、SQL_MAX_PROCEDURE_NAME_LEN、および SQL_MAX_COLUMN_NAME_LEN の各オプションを指定して **SQLGetInfo** を呼び出すことができます。  
  
 ODBC 3 では、次の列の名前が変更されています。*x*。 アプリケーションは列番号でバインドされるため、列名の変更は旧バージョンとの互換性に影響しません。  
  
|ODBC 2.0 列|ODBC 3.*x* 列|  
|---------------------|-----------------------|  
|PROCEDURE_QUALIFIER|PROCEDURE_CAT|  
|手順 _OWNER|PROCEDURE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 **SQLProcedureColumns**によって ODBC 3 に返される結果セットには、次の列が追加されています。*x*:  
  
-   COLUMN_DEF  
  
-   DATETIME_CODE  
  
-   CHAR_OCTET_LENGTH  
  
-   ORDINAL_POSITION  
  
-   IS_NULLABLE  
  
 次の表に、結果セット内の列の一覧を示します。 ドライバーでは、列 19 (IS_NULLABLE) 以外の列を定義できます。 アプリケーションでは、明示的な序数位置を指定するのではなく、結果セットの末尾からカウントすることで、ドライバー固有の列にアクセスする必要があります。 詳細については、「 [カタログ関数によって返されるデータ](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)」を参照してください。  
  
|列名|列番号|データ型|コメント|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT (ODBC 2.0)|1|Varchar|プロシージャカタログ名;データソースに適用されない場合は NULL です。 ドライバーがいくつかのプロシージャのカタログをサポートしていても、他のプロシージャに対してはサポートされていない場合 (ドライバーが異なる Dbms からデータを取得する場合など)、カタログを持たないプロシージャに対して空の文字列 ("") が返されます。|  
|PROCEDURE_SCHEM (ODBC 2.0)|2|Varchar|プロシージャスキーマ名;データソースに適用されない場合は NULL です。 ドライバーがいくつかのプロシージャのスキーマをサポートしていて、他のプロシージャに対してはサポートされていない場合 (ドライバーが異なる Dbms からデータを取得する場合など)、スキーマを持たないプロシージャに対して空の文字列 ("") が返されます。|  
|PROCEDURE_NAME (ODBC 2.0)|3|Varchar not NULL|プロシージャ名。 名前のないプロシージャに対して空の文字列が返されます。|  
|COLUMN_NAME (ODBC 2.0)|4|Varchar not NULL|プロシージャ列の名前。 ドライバーは、名前のないプロシージャ列に対して空の文字列を返します。|  
|COLUMN_TYPE (ODBC 2.0)|5|Smallint (NULL 以外)|プロシージャ列をパラメーターまたは結果セット列として定義します。<br /><br /> SQL_PARAM_TYPE_UNKNOWN: プロシージャ列は、型が不明なパラメーターです。 (ODBC 1.0)<br /><br /> SQL_PARAM_INPUT: プロシージャ列は入力パラメーターです。 (ODBC 1.0)<br /><br /> SQL_PARAM_INPUT_OUTPUT: プロシージャ列は入力/出力パラメーターです。 (ODBC 1.0)<br /><br /> SQL_PARAM_OUTPUT: プロシージャ列は出力パラメーターです。 (ODBC 2.0)<br /><br /> SQL_RETURN_VALUE: プロシージャ列は、プロシージャの戻り値です。 (ODBC 2.0)<br /><br /> SQL_RESULT_COL: プロシージャ列は結果セット列です。 (ODBC 1.0)|  
|DATA_TYPE (ODBC 2.0)|6|Smallint (NULL 以外)|SQL データ型。 ODBC SQL データ型またはドライバー固有の SQL データ型を指定できます。 Datetime および interval データ型の場合、この列には、簡潔なデータ型 (たとえば、SQL_TYPE_TIME や SQL_INTERVAL_YEAR_TO_MONTH) が返されます。 有効な ODBC SQL データ型の一覧については、「付録 D: データ型」の「 [Sql データ](../../../odbc/reference/appendixes/sql-data-types.md) 型」を参照してください。 ドライバー固有の SQL データ型の詳細については、ドライバーのドキュメントを参照してください。|  
|TYPE_NAME (ODBC 2.0)|7|Varchar not NULL|データソースに依存するデータ型の名前。たとえば、"CHAR"、"VARCHAR"、"MONEY"、"LONG VARBINARY"、"CHAR () FOR BIT DATA" などです。|  
|COLUMN_SIZE (ODBC 2.0)|8|Integer|データソースのプロシージャ列の列サイズ。 列サイズが適用されないデータ型に対しては NULL が返されます。 精度の詳細については、「付録 D: データ型」の「 [列のサイズ、10進数、転送オクテットの長さ、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 」を参照してください。|  
|BUFFER_LENGTH (ODBC 2.0)|9|Integer|SQL_C_DEFAULT が指定されている場合に、 **SQLGetData** または **sqlfetch** 操作で転送されるデータのバイト単位の長さ。 数値データの場合、このサイズは、データソースに格納されているデータのサイズとは異なる場合があります。 詳細については、「付録 D: データ型」の「 [列のサイズ、10進数、転送オクテットの長さ、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)」を参照してください。|  
|DECIMAL_DIGITS (ODBC 2.0)|10|Smallint|データソースのプロシージャ列の小数点以下桁数です。 10進数が適用されないデータ型に対しては NULL が返されます。 10進数の詳細については、「付録 D: データ型」の「 [列のサイズ、10進数字、転送オクテットの長さ、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)」を参照してください。|  
|NUM_PREC_RADIX (ODBC 2.0)|11|Smallint|数値データ型の場合は、10または2のいずれかになります。<br /><br /> 10の場合、COLUMN_SIZE と DECIMAL_DIGITS の値によって、列に許可される小数点以下桁数が指定されます。 たとえば、DECIMAL (12, 5) 列は、10、COLUMN_SIZE 12、および DECIMAL_DIGITS 5 の NUM_PREC_RADIX を返します。FLOAT 型の列は、10、COLUMN_SIZE 15、および NULL の DECIMAL_DIGITS の NUM_PREC_RADIX を返す場合があります。<br /><br /> 2の場合、COLUMN_SIZE および DECIMAL_DIGITS の値によって、列で許可されるビット数が指定されます。 たとえば、FLOAT 型の列は、NUM_PREC_RADIX 2、COLUMN_SIZE 53、および NULL の DECIMAL_DIGITS を返す可能性があります。<br /><br /> NUM_PREC_RADIX が適用されないデータ型に対しては NULL が返されます。|  
|NULLABLE (ODBC 2.0)|12|Smallint (NULL 以外)|プロシージャ列が NULL 値を許容するかどうかを示します。<br /><br /> SQL_NO_NULLS: プロシージャ列に NULL 値を使用することはできません。<br /><br /> SQL_NULLABLE: プロシージャ列は NULL 値を許容します。<br /><br /> SQL_NULLABLE_UNKNOWN: プロシージャ列が NULL 値を許容するかどうかは不明です。|  
|解説 (ODBC 2.0)|13|Varchar|プロシージャ列の説明です。|  
|COLUMN_DEF (ODBC 3.0)|14|Varchar|列の既定値です。<br /><br /> NULL が既定値として指定されている場合、この列は NULL で、引用符で囲まれていません。 既定値を切り捨てずに表すことができない場合、この列には、単一引用符を含まない、切り捨てられたが含まれます。 既定値が指定されていない場合、この列は NULL になります。<br /><br /> COLUMN_DEF の値は、切り捨てられた値が含まれている場合を除き、新しい列定義を生成するときに使用できます。|  
|SQL_DATA_TYPE (ODBC 3.0)|15|Smallint (NULL 以外)|記述子の SQL_DESC_TYPE フィールドに表示される SQL データ型の値。 この列は、datetime および interval データ型を除き、DATA_TYPE 列と同じです。<br /><br /> Datetime データ型および interval データ型の場合、結果セットの SQL_DATA_TYPE フィールドは SQL_INTERVAL または SQL_DATETIME を返し、SQL_DATETIME_SUB フィールドは特定の interval データ型または datetime データ型のサブコードを返します。 (「 [付録 D: データ型](../../../odbc/reference/appendixes/appendix-d-data-types.md)」を参照してください)。|  
|SQL_DATETIME_SUB (ODBC 3.0)|16|Smallint|Datetime および interval データ型のサブタイプコード。 その他のデータ型の場合、この列は NULL を返します。|  
|CHAR_OCTET_LENGTH (ODBC 3.0)|17|Integer|文字またはバイナリデータ型の列の最大長 (バイト単位)。 他のすべてのデータ型については、この列は NULL を返します。|  
|ORDINAL_POSITION (ODBC 3.0)|18|Integer (NULL 以外)|入力パラメーターと出力パラメーターの場合は、プロシージャ定義内のパラメーターの位置を表す序数です (パラメーターの順序を上げるには、1から開始します)。 戻り値 (存在する場合) の場合は、0が返されます。 結果セットの列の場合は、結果セット内の列の序数位置。結果セットの最初の列は番号1です。 複数の結果セットがある場合は、ドライバー固有の方法で列の序数位置が返されます。|  
|IS_NULLABLE (ODBC 3.0)|19|Varchar|列に Null が含まれていない場合は "NO" になります。<br /><br /> 列に Null を含めることができる場合は "YES" になります。<br /><br /> Null 値許容属性が不明の場合、この列は長さ0の文字列を返します。<br /><br /> ISO ルールの後に、null 値の許容属性が決定されます。 ISO SQL に準拠している DBMS では、空の文字列を返すことはできません。<br /><br /> この列に返される値は、NULLABLE 列に返される値とは異なります。 (NULL 許容列の説明を参照してください)。|  
  
## <a name="code-example"></a>コード例  
 「 [プロシージャ呼び出し](../../../odbc/reference/develop-app/procedure-calls.md)」を参照してください。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|結果セット内の列へのバッファーのバインド|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|ステートメント処理の取り消し|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|1つの行またはデータのブロックを順方向専用にフェッチする|[SQLFetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|データのブロックのフェッチまたは結果セットのスクロール|[SQLFetchScroll 関数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|データソース内のプロシージャの一覧を返す|[SQLProcedures 関数](../../../odbc/reference/syntax/sqlprocedures-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
