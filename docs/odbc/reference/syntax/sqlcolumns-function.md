---
description: SQLColumns 関数
title: SQLColumns 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLColumns
helpviewer_keywords:
- SQLColumns function [ODBC]
ms.assetid: 4a3618b7-d2b8-43c6-a1fd-7a4e6fa8c7d0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d5fc96b275badf5eab68f78e863648c3a73eaab6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448775"
---
# <a name="sqlcolumns-function"></a>SQLColumns 関数
**互換性**  
 導入されたバージョン: ODBC 1.0 標準準拠: グループを開く  
  
 **まとめ**  
 **Sqlcolumns** は、指定されたテーブル内の列名の一覧を返します。 ドライバーは、指定された *StatementHandle*の結果セットとしてこの情報を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLColumns(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      TableName,  
     SQLSMALLINT    NameLength3,  
     SQLCHAR *      ColumnName,  
     SQLSMALLINT    NameLength4);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル。  
  
 *CatalogName*  
 代入カタログ名。 ドライバーが一部のテーブルのカタログをサポートしていても、他のテーブルではサポートされていない場合 (ドライバーがさまざまな Dbms からデータを取得する場合など)、空の文字列 ("") は、カタログを持たないテーブルを示します。 *CatalogName* に文字列検索パターンを含めることはできません。  
  
> [!NOTE]  
>  SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *CatalogName* は識別子として扱われ、大文字小文字は区別されません。 SQL_FALSE の場合、 *CatalogName* は通常の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。 詳細については、「 [カタログ関数の引数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)」を参照してください。  
  
 *NameLength1*  
 代入**CatalogName*の文字数。  
  
 *SchemaName*  
 代入スキーマ名の文字列検索パターン。 ドライバーがいくつかのテーブルのスキーマをサポートしていても、他のテーブルのスキーマをサポートしていない場合 (ドライバーが異なる Dbms からデータを取得する場合など)、空の文字列 ("") はスキーマを持たないテーブルを示します。  
  
> [!NOTE]  
>  SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *SchemaName* は識別子として扱われ、大文字小文字は区別されません。 SQL_FALSE の場合、 *SchemaName* はパターン値の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。  
  
 *NameLength2*  
 代入**SchemaName*の文字数。  
  
 *TableName*  
 代入テーブル名の文字列検索パターン。  
  
> [!NOTE]  
>  SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *TableName* は識別子として扱われ、その大文字と小文字は区別されません。 SQL_FALSE の場合、 *TableName* はパターン値の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。  
  
 *NameLength3*  
 代入**TableName*の長さ (文字数)。  
  
 *[ColumnName]*  
 代入列名の文字列検索パターン。  
  
> [!NOTE]  
>  SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *ColumnName* は識別子として扱われ、その大文字と小文字は区別されません。 SQL_FALSE の場合、 *ColumnName* はパターン値の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。  
  
 *NameLength4*  
 代入**ColumnName*の文字数。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **Sqlcolumns**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合、関連付けられた SQLSTATE 値を取得するには、 *Handletype* SQL_HANDLE_STMT と*StatementHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出します。 次の表に、 **Sqlcolumns** によって通常返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続されていたデータソースとの間の通信リンクが失敗しました。|  
|24000|カーソル状態が無効|*StatementHandle*でカーソルが開かれました。 **sqlfetch**または**sqlfetchscroll**が呼び出されました。 このエラーは、 **Sqlfetch** または **sqlfetchscroll** が SQL_NO_DATA 返されなかった場合にドライバーマネージャーによって返されます。また、 **Sqlfetch** または **sqlfetchscroll** が SQL_NO_DATA を返した場合は、ドライバーによって返されます。<br /><br /> *StatementHandle*でカーソルが開いていましたが、 **sqlfetch**または**sqlfetchscroll**が呼び出されていません。|  
|40001|シリアル化エラー|別のトランザクションでリソースのデッドロックが発生したため、トランザクションがロールバックされました。|  
|40003|ステートメントの完了が不明です|この関数の実行中に関連付けられた接続に失敗しました。トランザクションの状態を確認できません。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * \* Messagetext*バッファーの**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|*StatementHandle*に対して非同期処理が有効になりました。 関数が呼び出され、実行が完了する前に、 **SQLCancel** または **Sqlcancelhandle** が *StatementHandle*で呼び出されました。 次に、 *StatementHandle*で関数が再度呼び出されました。<br /><br /> 関数が呼び出され、実行が完了する前に、マルチスレッドアプリケーションの別のスレッドの*StatementHandle*で**SQLCancel**または**sqlcancelhandle**が呼び出されました。|  
|HY009|Null ポインターの使い方が正しくありません|SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されました。 *CatalogName* 引数は null ポインターで、SQL_CATALOG_NAME *InfoType* はカタログ名がサポートされていることを返します。<br /><br /> (DM) SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定され、 *SchemaName*、 *TableName*、または *ColumnName* 引数が null ポインターでした。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、 **Sqlcolumns** 関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または **Sqlmoreresults** が *StatementHandle* に対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。<br /><br /> (DM) 非同期的に実行されている関数 (この1つではない) が *StatementHandle* に対して呼び出され、この関数が呼び出されたときにまだ実行されています。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **Sqlbulkoperations**、 **SQLSetPos** が *StatementHandle* に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY090|文字列またはバッファーの長さが無効です|(DM) 名前の長さの引数のいずれかの値が0未満ですが SQL_NTS と等しくありません。|  
|||名前の長さの引数のいずれかの値が、対応するカタログまたは名前の最大長の値を超えています。 各カタログまたは名前の最大長は、 *InfoType*値を指定して**SQLGetInfo**を呼び出すことによって取得できます。 (「コメント」を参照してください)。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYC00|省略可能な機能は実装されていません|カタログ名が指定されていますが、ドライバーまたはデータソースがカタログをサポートしていません。<br /><br /> スキーマ名が指定されましたが、ドライバーまたはデータソースがスキーマをサポートしていません。<br /><br /> スキーマ名、テーブル名、または列名に文字列検索パターンが指定されています。データソースは、これらの引数の1つ以上の検索パターンをサポートしていません。<br /><br /> SQL_ATTR_CONCURRENCY および SQL_ATTR_CURSOR_TYPE statement 属性の現在の設定の組み合わせは、ドライバーまたはデータソースではサポートされていませんでした。<br /><br /> SQL_ATTR_USE_BOOKMARKS statement 属性が SQL_UB_VARIABLE に設定されており、SQL_ATTR_CURSOR_TYPE statement 属性が、ドライバーがブックマークをサポートしていないカーソルの種類に設定されました。|  
|HYT00|タイムアウトに達しました|データソースから結果セットが返される前に、クエリのタイムアウト期間が経過しました。 タイムアウト期間は、 **SQLSetStmtAttr**、SQL_ATTR_QUERY_TIMEOUT によって設定されます。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle* に関連付けられているドライバーでは、関数はサポートされていません。|  
|IM017|非同期通知モードでは、ポーリングは無効になっています|通知モデルが使用されるたびに、ポーリングは無効になります。|  
|IM018|**Sqlcompleteasync** は、このハンドルで前の非同期操作を完了するために呼び出されていません。|ハンドルに対する前の関数呼び出しが SQL_STILL_EXECUTING を返し、通知モードが有効になっている場合は、処理を完了するために、ハンドルに対して **Sqlcompleteasync** を呼び出す必要があります。|  
  
## <a name="comments"></a>コメント  
 通常、この関数は、ステートメントを実行する前に、データソースのカタログからテーブルの列に関する情報を取得するために使用されます。 **Sqlcolumns** は、 **sqlcolumns**によって返されるすべての種類のアイテムのデータを取得するために使用できます。 ベーステーブルに加えて、ビュー、シノニム、システムテーブルなどが含まれている場合もあります。 これに対し、 **Sqlcolattribute** および **SQLDescribeCol** 関数は、結果セット内の列を記述し、 **sqlnumresultcols** 関数は結果セット内の列の数を返します。 詳細については、「 [カタログデータの使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)」を参照してください。  
  
> [!NOTE]  
>  一般的な使用、引数、および ODBC カタログ関数の返されるデータの詳細については、「 [カタログ関数](../../../odbc/reference/develop-app/catalog-functions.md)」を参照してください。  
  
 **Sqlcolumns** は、TABLE_CAT、TABLE_SCHEM、TABLE_NAME、および ORDINAL_POSITION 順に並べ替えられた結果を標準の結果セットとして返します。  
  
> [!NOTE]  
>  アプリケーションが ODBC 2 で動作する場合。*x* ドライバー、ORDINAL_POSITION の列が結果セットに返されません。 結果として、ODBC 2 を使用する場合。*x* ドライバー。 **sqlcolumns** によって返される列リスト内の列の順序は、アプリケーションがそのテーブル内のすべての列に対して select ステートメントを実行したときに返される列の順序と必ずしも同じであるとは限りません。  
  
> [!NOTE]  
>  **Sqlcolumns** は、すべての列を返すとは限りません。 たとえば、ドライバーが Oracle ROWID などの擬似列に関する情報を返さない場合があります。 アプリケーションでは、 **Sqlcolumns**によって返されるかどうかにかかわらず、任意の有効な列を使用できます。  
>   
>  Sqlstatistics によって返される**SQLStatistics**列には、 **sqlstatistics**によって返されないものがあります。 たとえば、 **Sqlcolumns** は、式またはフィルターに対して作成されたインデックスの列を返しません (例: SALARY + 福利厚生または DEPT = 0012)。  
  
 VARCHAR 型の列の長さはテーブルには表示されません。実際の長さは、データソースによって異なります。 TABLE_CAT、TABLE_SCHEM、TABLE_NAME、および COLUMN_NAME 列の実際の長さを確認するには、アプリケーションで、SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN、SQL_MAX_TABLE_NAME_LEN、および SQL_MAX_COLUMN_NAME_LEN の各オプションを指定して **SQLGetInfo** を呼び出すことができます。  
  
 ODBC 3 では、次の列の名前が変更されています。*x*。 アプリケーションは列番号でバインドされるため、列名の変更は旧バージョンとの互換性に影響しません。  
  
|ODBC 2.0 列|ODBC 3.*x* 列|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 **Sqlcolumns** for ODBC 3 によって返される結果セットには、次の列が追加されています。*x*:  

:::row:::
    :::column:::
        CHAR_OCTET_LENGTH  
        COLUMN_DEF  
    :::column-end:::
    :::column:::
        IS_NULLABLE  
        ORDINAL_POSITION  
    :::column-end:::
    :::column:::
        SQL_DATA_TYPE  
        SQL_DATETIME_SUB  
    :::column-end:::
:::row-end:::

 次の表に、結果セット内の列の一覧を示します。 列 18 (IS_NULLABLE) を超える追加の列は、ドライバーで定義できます。 アプリケーションでは、明示的な序数位置を指定するのではなく、結果セットの末尾からカウントすることで、ドライバー固有の列にアクセスする必要があります。 詳細については、「 [カタログ関数によって返されるデータ](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)」を参照してください。  
  
|列名|列<br /><br /> number|データ型|コメント|  
|-----------------|-----------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|カタログ名。データソースに適用されない場合は NULL です。 ドライバーが一部のテーブルのカタログをサポートしていても、他のテーブルではサポートされていない場合 (ドライバーが異なる Dbms からデータを取得する場合など)、カタログを持たないテーブルに対して空の文字列 ("") が返されます。|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|スキーマ名;データソースに適用されない場合は NULL です。 ドライバーがいくつかのテーブルのスキーマをサポートしていても、他のテーブルではサポートされていない場合 (ドライバーが異なる Dbms からデータを取得する場合など) は、スキーマがないテーブルに対して空の文字列 ("") を返します。|  
|TABLE_NAME (ODBC 1.0)|3|Varchar not NULL|テーブル名。|  
|COLUMN_NAME (ODBC 1.0)|4|Varchar not NULL|列名。 ドライバーは、名前のない列に対して空の文字列を返します。|  
|DATA_TYPE (ODBC 1.0)|5|Smallint (NULL 以外)|SQL データ型。 ODBC SQL データ型またはドライバー固有の SQL データ型を指定できます。 Datetime データ型および interval データ型の場合、この列には、SQL_DATETIME や SQL_INTERVAL などの簡潔ではないデータ型ではなく、SQL_TYPE_DATE や SQL_INTERVAL_YEAR_TO_MONTH などの簡潔なデータ型が返されます。 有効な ODBC SQL データ型の一覧については、「付録 D: データ型」の「 [Sql データ](../../../odbc/reference/appendixes/sql-data-types.md) 型」を参照してください。 ドライバー固有の SQL データ型の詳細については、ドライバーのドキュメントを参照してください。<br /><br /> ODBC 3 で返されるデータ型。*x* および ODBC 2。*x* アプリケーションは異なる場合があります。 詳細については、「 [旧バージョンとの互換性と標準の準拠](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)」を参照してください。|  
|TYPE_NAME (ODBC 1.0)|6|Varchar not NULL|データソースに依存するデータ型の名前。たとえば、"CHAR"、"VARCHAR"、"MONEY"、"LONG VARBINAR"、または "CHAR () FOR BIT DATA" などです。|  
|COLUMN_SIZE (ODBC 1.0)|7|Integer|DATA_TYPE が SQL_CHAR または SQL_VARCHAR の場合、この列には列の最大文字数が格納されます。 Datetime データ型の場合、これは、値を文字に変換したときに値を表示するために必要な文字の合計数です。 数値データ型の場合は、NUM_PREC_RADIX 列に従って、列に許可されている合計桁数または合計ビット数を示します。 Interval データ型の場合は、間隔のリテラルの文字表現に含まれる文字数です (「付録 D: データ型」の「 [Interval データ型の長さ](../../../odbc/reference/appendixes/interval-data-type-length.md) 」を参照してください)。 詳細については、「付録 D: データ型」の「 [列のサイズ、10進数、転送オクテットの長さ、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 」を参照してください。|  
|BUFFER_LENGTH (ODBC 1.0)|8|Integer|SQL_C_DEFAULT が指定されている場合に、SQLGetData、SQLFetch、または SQLFetchScroll 操作で転送されるデータのバイト単位の長さ。 数値データの場合、このサイズは、データソースに格納されているデータのサイズとは異なる場合があります。 この値は、文字データの COLUMN_SIZE 列とは異なる場合があります。 長さの詳細については、「付録 D: データ型」の「 [列のサイズ、10進数、転送オクテットの長さ、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 」を参照してください。|  
|DECIMAL_DIGITS (ODBC 1.0)|9|Smallint|小数点の右側の有効桁数の合計。 SQL_TYPE_TIME と SQL_TYPE_TIMESTAMP の場合、この列には秒の小数部の桁数が含まれます。 その他のデータ型の場合は、データソースの列の小数点以下の桁数になります。 時間部分を含む interval データ型の場合、この列には小数点の右側の桁数 (秒の小数部) が格納されます。 時間部分を含まない interval データ型の場合、この列は0になります。 10進数の詳細については、「付録 D: データ型」の「 [列のサイズ、10進数字、転送オクテットの長さ、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 」を参照してください。 DECIMAL_DIGITS が適用されないデータ型に対しては NULL が返されます。|  
|NUM_PREC_RADIX (ODBC 1.0)|10|Smallint|数値データ型の場合は、10または2のいずれかになります。 10の場合、COLUMN_SIZE と DECIMAL_DIGITS の値によって、列に許可される小数点以下桁数が指定されます。 たとえば、DECIMAL (12, 5) 列は、10、COLUMN_SIZE 12、および DECIMAL_DIGITS 5 の NUM_PREC_RADIX を返します。FLOAT 型の列は、10、COLUMN_SIZE 15、および NULL の DECIMAL_DIGITS の NUM_PREC_RADIX を返す場合があります。<br /><br /> 2の場合、COLUMN_SIZE と DECIMAL_DIGITS の値によって、列で許可されるビット数が与えられます。 たとえば、FLOAT 型の列は、基数が2、COLUMN_SIZE が53、DECIMAL_DIGITS が NULL の場合に返されます。<br /><br /> NUM_PREC_RADIX が適用されないデータ型に対しては NULL が返されます。|  
|NULLABLE (ODBC 1.0)|11|Smallint (NULL 以外)|列に NULL 値を含めることができなかった場合に SQL_NO_NULLS します。<br /><br /> 列が NULL 値を許容するかどうかを SQL_NULLABLE します。<br /><br /> 列が NULL 値を許容するかどうかが不明な場合に SQL_NULLABLE_UNKNOWN します。<br /><br /> この列に返される値は、IS_NULLABLE 列に返される値とは異なります。 NULL 値を許容する列は、列が null を許容できることを意味しますが、Null 値を許容しない列であることを示すことはできません。 IS_NULLABLE 列は、列が Null 値を許容できないことを示していますが、列が Null 値を許容するという確実性を示すことはできません。|  
|解説 (ODBC 1.0)|12|Varchar|列の説明。|  
|COLUMN_DEF (ODBC 3.0)|13|Varchar|列の既定値です。 この列の値は、引用符で囲まれている場合は、文字列として解釈される必要があります。<br /><br /> NULL が既定値として指定されている場合、この列は NULL で、引用符で囲まれていません。 既定値を切り捨てずに表すことができない場合、この列には単一引用符を囲まずに切り捨てられたが含まれます。 既定値が指定されていない場合、この列は NULL になります。<br /><br /> COLUMN_DEF の値は、切り捨てられた値が含まれている場合を除き、新しい列定義を生成するときに使用できます。|  
|SQL_DATA_TYPE (ODBC 3.0)|14|Smallint (NULL 以外)|IRD の [SQL_DESC_TYPE レコード] フィールドに表示される SQL データ型。 ODBC SQL データ型またはドライバー固有の SQL データ型を指定できます。 この列は、datetime および interval データ型を除き、DATA_TYPE 列と同じです。 この列は、DATETIME データ型および INTERVAL データ型の簡潔なデータ型 (SQL_TYPE_DATE や SQL_INTERVAL_YEAR_TO_MONTH など) ではなく、簡潔なデータ型 (SQL_DATETIME や SQL_INTERVAL など) を返します。 この列が SQL_DATETIME または SQL_INTERVAL を返す場合、SQL_DATETIME_SUB 列から特定のデータ型を特定できます。 有効な ODBC SQL データ型の一覧については、「付録 D: データ型」の「 [Sql データ](../../../odbc/reference/appendixes/sql-data-types.md) 型」を参照してください。 ドライバー固有の SQL データ型の詳細については、ドライバーのドキュメントを参照してください。<br /><br /> ODBC 3 で返されるデータ型。*x* および ODBC 2。*x* アプリケーションは異なる場合があります。 詳細については、「 [旧バージョンとの互換性と標準の準拠](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)」を参照してください。|  
|SQL_DATETIME_SUB (ODBC 3.0)|15|Smallint|Datetime および interval データ型のサブタイプコード。 その他のデータ型の場合、この列は NULL を返します。 Datetime および interval サブコードの詳細については、 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)の「SQL_DESC_DATETIME_INTERVAL_CODE」を参照してください。|  
|CHAR_OCTET_LENGTH (ODBC 3.0)|16|Integer|文字またはバイナリデータ型の列の最大長 (バイト単位)。 他のすべてのデータ型については、この列は NULL を返します。|  
|ORDINAL_POSITION (ODBC 3.0)|17|Integer (NULL 以外)|テーブル内の列の序数位置です。 テーブルの最初の列は number 1 です。|  
|IS_NULLABLE (ODBC 3.0)|18|Varchar|列に Null が含まれていない場合は "NO" になります。<br /><br /> 列に Null を含めることができる場合は "YES" になります。<br /><br /> Null 値許容属性が不明の場合、この列は長さ0の文字列を返します。<br /><br /> ISO ルールの後に、null 値の許容属性が決定されます。 ISO SQL に準拠している DBMS では、空の文字列を返すことはできません。<br /><br /> この列に返される値は、NULL 許容列に対して返される値とは異なります。 (NULL 許容列の説明を参照してください)。|  
  
## <a name="code-example"></a>コード例  
 次の例では、アプリケーションが **Sqlcolumns**によって返される結果セットのバッファーを宣言します。 このメソッドは、 **Sqlcolumns** を呼び出して、EMPLOYEE テーブル内の各列を記述する結果セットを返します。 次に、 **SQLBindCol** を呼び出して、結果セットの列をバッファーにバインドします。 最後に、アプリケーションは **Sqlfetch** を使用してデータの各行をフェッチし、処理します。  
  
```cpp  
// SQLColumns_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqlext.h>  
#define STR_LEN 128 + 1  
#define REM_LEN 254 + 1  
  
// Declare buffers for result set data  
SQLCHAR szSchema[STR_LEN];  
SQLCHAR szCatalog[STR_LEN];  
SQLCHAR szColumnName[STR_LEN];  
SQLCHAR szTableName[STR_LEN];  
SQLCHAR szTypeName[STR_LEN];  
SQLCHAR szRemarks[REM_LEN];  
SQLCHAR szColumnDefault[STR_LEN];  
SQLCHAR szIsNullable[STR_LEN];  
  
SQLINTEGER ColumnSize;  
SQLINTEGER BufferLength;  
SQLINTEGER CharOctetLength;  
SQLINTEGER OrdinalPosition;  
  
SQLSMALLINT DataType;  
SQLSMALLINT DecimalDigits;  
SQLSMALLINT NumPrecRadix;  
SQLSMALLINT Nullable;  
SQLSMALLINT SQLDataType;  
SQLSMALLINT DatetimeSubtypeCode;  
  
SQLHSTMT hstmt = NULL;  
  
// Declare buffers for bytes available to return  
SQLINTEGER cbCatalog;  
SQLINTEGER cbSchema;  
SQLINTEGER cbTableName;  
SQLINTEGER cbColumnName;  
SQLINTEGER cbDataType;  
SQLINTEGER cbTypeName;  
SQLINTEGER cbColumnSize;  
SQLLEN cbBufferLength;  
SQLINTEGER cbDecimalDigits;  
SQLINTEGER cbNumPrecRadix;  
SQLINTEGER cbNullable;  
SQLINTEGER cbRemarks;  
SQLINTEGER cbColumnDefault;  
SQLINTEGER cbSQLDataType;  
SQLINTEGER cbDatetimeSubtypeCode;  
SQLINTEGER cbCharOctetLength;  
SQLINTEGER cbOrdinalPosition;  
SQLINTEGER cbIsNullable;  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt = 0;  
   SQLRETURN retcode;  
  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
   retcode = SQLColumns(hstmt, NULL, 0, NULL, 0, (SQLCHAR*)"CUSTOMERS", SQL_NTS, NULL, 0);  
  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      // Bind columns in result set to buffers  
      SQLBindCol(hstmt, 1, SQL_C_CHAR, szCatalog, STR_LEN,&cbCatalog);  
      SQLBindCol(hstmt, 2, SQL_C_CHAR, szSchema, STR_LEN, &cbSchema);  
      SQLBindCol(hstmt, 3, SQL_C_CHAR, szTableName, STR_LEN,&cbTableName);  
      SQLBindCol(hstmt, 4, SQL_C_CHAR, szColumnName, STR_LEN, &cbColumnName);  
      SQLBindCol(hstmt, 5, SQL_C_SSHORT, &DataType, 0, &cbDataType);  
      SQLBindCol(hstmt, 6, SQL_C_CHAR, szTypeName, STR_LEN, &cbTypeName);  
      SQLBindCol(hstmt, 7, SQL_C_SLONG, &ColumnSize, 0, &cbColumnSize);  
      SQLBindCol(hstmt, 8, SQL_C_SLONG, &BufferLength, 0, &cbBufferLength);  
      SQLBindCol(hstmt, 9, SQL_C_SSHORT, &DecimalDigits, 0, &cbDecimalDigits);  
      SQLBindCol(hstmt, 10, SQL_C_SSHORT, &NumPrecRadix, 0, &cbNumPrecRadix);  
      SQLBindCol(hstmt, 11, SQL_C_SSHORT, &Nullable, 0, &cbNullable);  
      SQLBindCol(hstmt, 12, SQL_C_CHAR, szRemarks, REM_LEN, &cbRemarks);  
      SQLBindCol(hstmt, 13, SQL_C_CHAR, szColumnDefault, STR_LEN, &cbColumnDefault);  
      SQLBindCol(hstmt, 14, SQL_C_SSHORT, &SQLDataType, 0, &cbSQLDataType);  
      SQLBindCol(hstmt, 15, SQL_C_SSHORT, &DatetimeSubtypeCode, 0, &cbDatetimeSubtypeCode);  
      SQLBindCol(hstmt, 16, SQL_C_SLONG, &CharOctetLength, 0, &cbCharOctetLength);  
      SQLBindCol(hstmt, 17, SQL_C_SLONG, &OrdinalPosition, 0, &cbOrdinalPosition);  
      SQLBindCol(hstmt, 18, SQL_C_CHAR, szIsNullable, STR_LEN, &cbIsNullable);  
  
      while (SQL_SUCCESS == retcode) {  
         retcode = SQLFetch(hstmt);  
         /*  
         if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO)  
            0;   // show_error();  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
            0;   // Process fetched data  
         else  
            break;  
        */  
      }  
   }  
}  
```  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|結果セット内の列へのバッファーのバインド|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|ステートメント処理の取り消し|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|1つまたは複数の列に対する権限を返す|[SQLColumnPrivileges 関数](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|データのブロックのフェッチまたは結果セットのスクロール|[SQLFetchScroll 関数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|複数行のデータのフェッチ|[SQLFetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|行を一意に識別する列、またはトランザクションによって自動的に更新される列を返す|[SQLSpecialColumns 関数](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|  
|テーブルの統計とインデックスの取得|[SQLStatistics 関数](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|データソース内のテーブルの一覧を取得する|[SQLTables 関数](../../../odbc/reference/syntax/sqltables-function.md)|  
|テーブルまたはテーブルの権限を取得する|[SQLTablePrivileges 関数](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
