---
description: SQLSetDescField 関数
title: SQLSetDescField 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetDescField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetDescField
helpviewer_keywords:
- SQLSetDescField function [ODBC]
ms.assetid: 8c544388-fe9d-4f94-a0ac-fa0b9c9c88a5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2c21d3a21e863d62a3cc8d685e81c6e3265c1551
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421136"
---
# <a name="sqlsetdescfield-function"></a>SQLSetDescField 関数

**互換性**  
 導入されたバージョン: ODBC 3.0 標準準拠: ISO 92  
  
 **まとめ**  
 **SQLSetDescField** は、記述子レコードの1つのフィールドの値を設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
SQLRETURN SQLSetDescField(  
     SQLHDESC      DescriptorHandle,  
     SQLSMALLINT   RecNumber,  
     SQLSMALLINT   FieldIdentifier,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    BufferLength);  
```  
  
## <a name="arguments"></a>引数  
 *DescriptorHandle*  
 代入記述子ハンドル。  
  
 *RecNumber*  
 代入アプリケーションが設定を行うフィールドを含む記述子レコードを示します。 記述子レコードは0から番号が付けられ、レコード番号0はブックマークレコードになります。 *Recnumber*引数は、ヘッダーフィールドでは無視されます。  
  
 *FieldIdentifier*  
 代入値が設定される記述子のフィールドを示します。 詳細については、「コメント」セクションの「*FieldIdentifier* 引数」を参照してください。  
  
 *ValuePtr*  
 代入記述子情報を格納しているバッファーへのポインター、または整数値。 データ型は、 *FieldIdentifier*の値によって異なります。 *Valueptr*が整数値の場合、 *FieldIdentifier*引数の値に応じて、8バイト (sqllen)、4バイト (SQLINTEGER)、または2バイト (sqlsmallint) と見なすことができます。  
  
 *BufferLength*  
 代入 *FieldIdentifier* が ODBC で定義されたフィールドであり、 *valueptr* が文字列またはバイナリバッファーを指している場合、この引数は **valueptr*の長さである必要があります。 文字列データの場合、この引数には文字列のバイト数を含める必要があります。  
  
 *FieldIdentifier*が ODBC で定義されたフィールドであり、 *valueptr*が整数の場合、 *bufferlength*は無視されます。  
  
 *FieldIdentifier*がドライバーによって定義されたフィールドである場合、アプリケーションは、 *bufferlength*引数を設定することによって、ドライバーマネージャーに対してフィールドの性質を示します。 *Bufferlength* には次の値を指定できます。  
  
-   *Valueptr*が文字列へのポインターである場合、 *bufferlength*は文字列または SQL_NTS の長さになります。  
  
-   *Valueptr*がバイナリバッファーへのポインターである場合、アプリケーションは、SQL_LEN_BINARY_ATTR (*長さ*) マクロの結果を*bufferlength*に配置します。 これにより、 *Bufferlength*に負の値が挿入されます。  
  
-   *Valueptr*が文字列またはバイナリ文字列以外の値へのポインターである場合、 *bufferlength*には SQL_IS_POINTER 値を指定する必要があります。  
  
-   *Valueptr*に固定長の値が含まれている場合、 *bufferlength*は、必要に応じて SQL_IS_INTEGER、SQL_IS_UINTEGER、SQL_IS_SMALLINT、SQL_IS_USMALLINT のいずれかになります。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **SQLSetDescField**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合、関連付けられた SQLSTATE 値を取得するには、 *handletype*が SQL_HANDLE_DESC で、*記述子ハンドル*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出します。 次の表に、 **SQLSetDescField** によって一般的に返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01S02|オプションの値が変更されました|ドライバーは、 * \* valueptr*に指定された値 ( *valueptr*がポインターの場合) または*valueptr*の値 ( *valueptr*が整数値の場合) をサポートしていなかったか、または valueptr が実装の動作条件により無効だったため、ドライバーは同様の値に置き換えられました。 * \* * (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|07009|無効な記述子のインデックス|*FieldIdentifier*引数がレコードフィールドで、 *recnumber*引数が0で、*記述子 handle*引数が IPD ハンドルを参照しています。<br /><br /> *Recnumber*引数が0未満で、*記述子ハンドル*引数が、APD またはが参照されています。<br /><br /> *Recnumber*引数が、データソースがサポートできる列またはパラメーターの最大数を超えています。また、*記述子ハンドル*引数が APD またはを参照しています。<br /><br /> (DM) *FieldIdentifier*引数が SQL_DESC_COUNT、 * \* valueptr*引数が0未満でした。<br /><br /> *Recnumber*引数が0で、*記述子ハンドル*引数が暗黙的に割り当てられた APD を参照しています。 (明示的に割り当てられたアプリケーション記述子が APD であるか、または実行時まで適用されるかが不明であるため、明示的に割り当てられたアプリケーション記述子では、このエラーは発生しません)。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続されていたデータソースとの間の通信リンクが失敗しました。|  
|22001|文字列データ、右側が切り捨てられました|*FieldIdentifier*引数が SQL_DESC_NAME ましたが、 *bufferlength*引数の値が SQL_MAX_IDENTIFIER_LEN を超えています。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * \* Messagetext*バッファーの**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY010|関数のシーケンスエラー|(DM) *記述子ハンドル* は *StatementHandle* に関連付けられていました。このハンドルは非同期に実行される関数 (この関数ではありません) が呼び出され、この関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **sqlbulkoperations**、または**SQLSetPos**が、*記述子ハンドル*が関連付けられて SQL_NEED_DATA 返された*StatementHandle*に対して呼び出されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。<br /><br /> (DM) 実行中の非同期関数が、 *記述子ハンドル*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、 **SQLSetDescField** 関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または **sqlmoreresults** が、 *記述子ハンドル* に関連付けられたステートメントハンドルの1つに対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY016|実装行記述子を変更できません|*記述子ハンドル*引数が IRD に関連付けられましたが、 *FieldIdentifier*引数が SQL_DESC_ARRAY_STATUS_PTR でも SQL_DESC_ROWS_PROCESSED_PTR でもありませんでした。|  
|HY021|不整合な記述子情報|SQL_DESC_TYPE フィールドと SQL_DESC_DATETIME_INTERVAL_CODE フィールドは、有効な ODBC SQL 型または有効なドライバー固有の SQL 型 (IPDs の場合) または有効な ODBC C 型 (APDs または ARDs の場合) を形成しません。<br /><br /> 整合性チェック中にチェックされた記述子情報が一致しませんでした。 ( **SQLSetDescRec**の「整合性チェック」を参照してください)。|  
|HY090|文字列またはバッファーの長さが無効です|(DM) * \* valueptr*は文字列であり、 *bufferlength*は0未満ですが SQL_NTS と等しくありませんでした。<br /><br /> (DM) ドライバーは ODBC*2.x ドライバーでし* たが、記述子は、その *columnnumber* 引数が0に設定されており、引数 *bufferlength* に指定された値が4ではありませんでした。|  
|HY091|無効な記述子フィールド識別子|*FieldIdentifier*引数に指定された値が ODBC 定義のフィールドではなく、実装定義の値ではありませんでした。<br /><br /> *FieldIdentifier*引数が、*記述子ハンドル*引数に対して無効でした。<br /><br /> *FieldIdentifier*引数は、読み取り専用の ODBC 定義フィールドでした。|  
|HY092|属性またはオプションの識別子が無効です|* \* Valueptr*の値は、 *FieldIdentifier*引数に対して無効です。<br /><br /> *FieldIdentifier*引数が SQL_DESC_UNNAMED、 *valueptr*が SQL_NAMED でした。|  
|HY105|パラメーターの型が無効です|(DM) SQL_DESC_PARAMETER_TYPE フィールドに指定された値が無効でした。 (詳細については、 **SQLBindParameter**の「*inputoutputtype*引数」セクションを参照してください)。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [ODBC 3.8 の新機能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)」を参照してください。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *記述子ハンドル* に関連付けられているドライバーでは、関数はサポートされていません。|  
  
## <a name="comments"></a>コメント  
 アプリケーションでは、 **SQLSetDescField** を呼び出して、任意の記述子フィールドを一度に1つずつ設定できます。 **SQLSetDescField**を呼び出すと、1つの記述子に1つのフィールドが設定されます。 フィールドを設定できる場合は、この関数を呼び出して任意の記述子の型の任意のフィールドを設定できます。 (このセクションの後半の表を参照してください)。  
  
> [!NOTE]  
>  **SQLSetDescField**の呼び出しが失敗した場合、 *recnumber*引数によって識別される記述子レコードの内容は未定義になります。  
  
 関数の1回の呼び出しで複数の記述子フィールドを設定するために、他の関数を呼び出すことができます。 **SQLSetDescRec**関数は、列またはパラメーター (SQL_DESC_TYPE、SQL_DESC_DATETIME_INTERVAL_CODE、SQL_DESC_OCTET_LENGTH、SQL_DESC_PRECISION、SQL_DESC_SCALE、SQL_DESC_DATA_PTR、SQL_DESC_OCTET_LENGTH_PTR、および SQL_DESC_INDICATOR_PTR フィールド) にバインドされたデータ型およびバッファーに影響を与えるさまざまなフィールドを設定します。 **SQLBindCol** または **SQLBindParameter** を使用すると、列またはパラメーターのバインドを完全に指定できます。 これらの関数は、1つの関数呼び出しを使用して、特定の記述子フィールドのグループを設定します。  
  
 **SQLSetDescField** は、バインドポインター (SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、または SQL_DESC_OCTET_LENGTH_PTR) にオフセットを追加することによって、バインドバッファーを変更するために呼び出すことができます。 これにより、 **SQLBindCol** または **SQLBindParameter**を呼び出さずにバインドバッファーが変更されます。これにより、アプリケーションは、他のフィールド (SQL_DESC_DATA_TYPE など) を変更せずに SQL_DESC_DATA_PTR を変更できます。  
  
 アプリケーションが **SQLSetDescField** を呼び出して、SQL_DESC_COUNT または遅延フィールド SQL_DESC_DATA_PTR、SQL_DESC_OCTET_LENGTH_PTR、または SQL_DESC_INDICATOR_PTR 以外のフィールドを設定すると、レコードはバインド解除されます。  
  
 記述子ヘッダーフィールドは、適切な*FieldIdentifier*を使用して**SQLSetDescField**を呼び出すことによって設定されます。 多くのヘッダーフィールドはステートメント属性でもあるため、 **SQLSetStmtAttr**を呼び出すことによって設定することもできます。 これにより、アプリケーションは最初に記述子ハンドルを取得せずに記述子フィールドを設定できます。 ヘッダーフィールドを設定するために **SQLSetDescField** が呼び出された場合、 *recnumber* 引数は無視されます。  
  
 0の *値* は、ブックマークフィールドを設定するために使用されます。  
  
> [!NOTE]  
>  **SQLSetDescField**を呼び出してブックマークフィールドを設定する前に、ステートメント属性 SQL_ATTR_USE_BOOKMARKS を常に設定する必要があります。 必須ではありませんが、強くお勧めします。  
  
## <a name="sequence-of-setting-descriptor-fields"></a>設定記述子フィールドのシーケンス  
 **SQLSetDescField**を呼び出して記述子フィールドを設定する場合、アプリケーションは特定のシーケンスに従う必要があります。  
  
1.  アプリケーションでは、最初に SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE、または SQL_DESC_DATETIME_INTERVAL_CODE フィールドを設定する必要があります。  
  
2.  これらのフィールドのいずれかが設定されると、アプリケーションはデータ型の属性を設定でき、ドライバーはデータ型の属性フィールドにデータ型の適切な既定値を設定します。 自動的に型属性フィールドの既定を使用すると、アプリケーションでデータ型を指定した後、常に記述子を使用できるようになります。 アプリケーションでデータ型の属性が明示的に設定されている場合、既定の属性はオーバーライドされます。  
  
3.  手順 1. で一覧表示されたフィールドの1つが設定され、データ型の属性が設定された後、アプリケーションで SQL_DESC_DATA_PTR を設定できます。 これにより、記述子フィールドの整合性チェックが求められます。 SQL_DESC_DATA_PTR フィールドを設定した後にアプリケーションがデータ型または属性を変更した場合、ドライバーは SQL_DESC_DATA_PTR を null ポインターに設定し、レコードのバインドを解除します。 これにより、記述子レコードが使用できるようになる前に、アプリケーションが適切な手順を順番どおりに完了するように強制されます。  
  
## <a name="initialization-of-descriptor-fields"></a>記述子フィールドの初期化  
 記述子が割り当てられている場合は、記述子のフィールドを既定値に初期化するか、既定値を使用せずに初期化するか、記述子の型に対して未定義にすることができます。 次の表は、記述子の型ごとに各フィールドを初期化することを示しています。 "D" はフィールドが既定値で初期化されることを示し、"ND" はフィールドが既定値なしで初期化されることを示します。 数値が表示されている場合、フィールドの既定値はその数値です。 また、テーブルは、フィールドが読み取り/書き込み可能 (R/W) であるか、読み取り専用 (R) であるかを示します。  
  
 IRD のフィールドに既定値が設定されているのは、ステートメントハンドルまたは記述子が割り当てられているときではなく、ステートメントの準備または実行が完了し、IRD が設定された後だけです。 IRD が設定されるまで、IRD のフィールドにアクセスしようとすると、エラーが返されます。  
  
 一部の記述子フィールドは、記述子の種類 (ARDs と IRDs、および APDs および IPDs) の1つ以上 (ただし、すべてではない) に対して定義されています。 フィールドが記述子の型に対して定義されていない場合、その記述子を使用する関数では必要ありません。  
  
 **SQLGetDescField**によってアクセスできるフィールドは、必ずしも**SQLSetDescField**によって設定されるとは限りません。 **SQLSetDescField**で設定できるフィールドを次の表に示します。  
  
 ヘッダーフィールドの初期化については、次の表で説明します。  
  
|ヘッダーフィールド名|種類|R/W|Default|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_ALLOC_TYPE|SQLSMALLINT|APD: R IRD: R IPD: R|SQL_DESC_ALLOC_AUTO: 暗黙的または SQL_DESC_ALLOC_USER (明示的の場合)<br /><br /> APD: 暗黙的または SQL_DESC_ALLOC_USER を明示的に SQL_DESC_ALLOC_AUTO<br /><br /> IRD: SQL_DESC_ALLOC_AUTO<br /><br /> IPD: SQL_DESC_ALLOC_AUTO|  
|SQL_DESC_ARRAY_SIZE|SQLULEN 向け|APD: r/w IRD: 未使用の IPD: 未使用|APD: [1]: [1] IRD: 未使用の IPD: 使用されていません|  
|SQL_DESC_ARRAY_STATUS_PTR|SQLUS悪意のある *|APD: R/W IRD: R/W IPD: R/W|標準: Null ptr APD: null ptr IRD: null ptr IPD: null ptr|  
|SQL_DESC_BIND_OFFSET_PTR|SQLLEN|APD: r/w IRD: 未使用の IPD: 未使用|標準: Null ptr APD: Null ptr IRD: 未使用 IPD: 使用されていません|  
|SQL_DESC_BIND_TYPE|SQLINTEGER|APD: r/w IRD: 未使用の IPD: 未使用|_: SQL_BIND_BY_COLUMN<br /><br /> APD: SQL_BIND_BY_COLUMN<br /><br /> IRD: 使用されていません<br /><br /> IPD: 使用されていません|  
|SQL_DESC_COUNT|SQLSMALLINT|APD: R/W IRD: R IPD: R/W|APD: 0 IRD: D IPD: 0|  
|SQL_DESC_ROWS_PROCESSED_PTR|SQLULEN 向け|APD: 未使用の IRD: R/W IPD: R/W|APD: 未使用の IRD: Null ptr IPD: Null ptr|  
  
 [1] これらのフィールドは、ドライバーによって IPD が自動的に設定される場合にのみ定義されます。 定義されていない場合は未定義です。 アプリケーションでこれらのフィールドを設定しようとすると、SQLSTATE HY091 (無効な記述子フィールド識別子) が返されます。  
  
 レコードフィールドの初期化は、次の表に示すようになります。  
  
|レコードフィールド名|種類|R/W|Default|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|APD: 未使用の IRD: R IPD: 使用しない|APD: 未使用の IRD: D IPD: 未使用|  
|SQL_DESC_BASE_COLUMN_NAME|SQLCHAR|APD: 未使用の IRD: R IPD: 使用しない|APD: 未使用の IRD: D IPD: 未使用|  
|SQL_DESC_BASE_TABLE_NAME|SQLCHAR|APD: 未使用の IRD: R IPD: 使用しない|APD: 未使用の IRD: D IPD: 未使用|  
|SQL_DESC_CASE_SENSITIVE|SQLINTEGER|APD: 未使用の IRD: R IPD: R|APD: 未使用の IRD: D IPD: D [1]|  
|SQL_DESC_CATALOG_NAME|SQLCHAR|APD: 未使用の IRD: R IPD: 使用しない|APD: 未使用の IRD: D IPD: 未使用|  
|SQL_DESC_CONCISE_TYPE|SQLSMALLINT|APD: R/W IRD: R IPD: R/W|SQL_C_ 既定の APD: SQL_C_ 既定の IRD: D IPD: ND|  
|SQL_DESC_DATA_PTR|へ SQLPOINTER|APD: r/w IRD: 未使用の IPD: 未使用|標準: Null ptr APD: Null ptr IRD: 未使用 IPD: 使用されていません [2]|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQLSMALLINT|APD: R/W IRD: R IPD: R/W|APD: ND IRD: D IPD: ND|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|SQLINTEGER|APD: R/W IRD: R IPD: R/W|APD: ND IRD: D IPD: ND|  
|SQL_DESC_DISPLAY_SIZE|SQLLEN|APD: 未使用の IRD: R IPD: 使用しない|APD: 未使用の IRD: D IPD: 未使用|  
|SQL_DESC_FIXED_PREC_SCALE|SQLSMALLINT|APD: 未使用の IRD: R IPD: R|APD: 未使用の IRD: D IPD: D [1]|  
|SQL_DESC_INDICATOR_PTR|SQLLEN|APD: r/w IRD: 未使用の IPD: 未使用|標準: Null ptr APD: Null ptr IRD: 未使用 IPD: 使用されていません|  
|SQL_DESC_LABEL|SQLCHAR|APD: 未使用の IRD: R IPD: 使用しない|APD: 未使用の IRD: D IPD: 未使用|  
|SQL_DESC_LENGTH|SQLULEN 向け|APD: R/W IRD: R IPD: R/W|APD: ND IRD: D IPD: ND|  
|SQL_DESC_LITERAL_PREFIX|SQLCHAR|APD: 未使用の IRD: R IPD: 使用しない|APD: 未使用の IRD: D IPD: 未使用|  
|SQL_DESC_LITERAL_SUFFIX|SQLCHAR|APD: 未使用の IRD: R IPD: 使用しない|APD: 未使用の IRD: D IPD: 未使用|  
|SQL_DESC_LOCAL_TYPE_NAME|SQLCHAR|APD: 未使用の IRD: R IPD: R|APD: 未使用の IRD: D IPD: D [1]|  
|SQL_DESC_NAME|SQLCHAR|APD: 未使用の IRD: R IPD: r/W|APD: ND IRD: D IPD: ND|  
|SQL_DESC_NULLABLE|SQLSMALLINT|APD: 未使用の IRD: R IPD: R|APD: ND IRD: D IPD: ND|  
|SQL_DESC_NUM_PREC_RADIX|SQLINTEGER|APD: R/W IRD: R IPD: R/W|APD: ND IRD: D IPD: ND|  
|SQL_DESC_OCTET_LENGTH|SQLLEN|APD: R/W IRD: R IPD: R/W|APD: ND IRD: D IPD: ND|  
|SQL_DESC_OCTET_LENGTH_PTR|SQLLEN|APD: r/w IRD: 未使用の IPD: 未使用|標準: Null ptr APD: Null ptr IRD: 未使用 IPD: 使用されていません|  
|SQL_DESC_PARAMETER_TYPE|SQLSMALLINT|APD: 未使用の IRD: 未使用の IPD: R/W|APD: 未使用の IRD: 未使用の IPD: D = SQL_PARAM_INPUT|  
|SQL_DESC_PRECISION|SQLSMALLINT|APD: R/W IRD: R IPD: R/W|APD: ND IRD: D IPD: ND|  
|SQL_DESC_ROWVER|SQLSMALLINT|標準: 未使用<br /><br /> APD: 使用されていません<br /><br /> IRD: R<br /><br /> IPD: R|標準: 未使用<br /><br /> APD: 使用されていません<br /><br /> IRD: ND<br /><br /> IPD: ND|  
|SQL_DESC_SCALE|SQLSMALLINT|APD: R/W IRD: R IPD: R/W|APD: ND IRD: D IPD: ND|  
|SQL_DESC_SCHEMA_NAME|SQLCHAR|APD: 未使用の IRD: R IPD: 使用しない|APD: 未使用の IRD: D IPD: 未使用|  
|SQL_DESC_SEARCHABLE|SQLSMALLINT|APD: 未使用の IRD: R IPD: 使用しない|APD: 未使用の IRD: D IPD: 未使用|  
|SQL_DESC_TABLE_NAME|SQLCHAR|APD: 未使用の IRD: R IPD: 使用しない|APD: 未使用の IRD: D IPD: 未使用|  
|SQL_DESC_TYPE|SQLSMALLINT|APD: R/W IRD: R IPD: R/W|APD: SQL_C_DEFAULT IRD: D IPD: ND SQL_C_DEFAULT|  
|SQL_DESC_TYPE_NAME|SQLCHAR|APD: 未使用の IRD: R IPD: R|APD: 未使用の IRD: D IPD: D [1]|  
|SQL_DESC_UNNAMED|SQLSMALLINT|APD: 未使用の IRD: R IPD: r/W|APD: ND IRD: D IPD: ND|  
|SQL_DESC_UNSIGNED|SQLSMALLINT|APD: 未使用の IRD: R IPD: R|APD: 未使用の IRD: D IPD: D [1]|  
|SQL_DESC_UPDATABLE|SQLSMALLINT|APD: 未使用の IRD: R IPD: 使用しない|APD: 未使用の IRD: D IPD: 未使用|  
  
 [1] これらのフィールドは、ドライバーによって IPD が自動的に設定される場合にのみ定義されます。 定義されていない場合は未定義です。 アプリケーションでこれらのフィールドを設定しようとすると、SQLSTATE HY091 (無効な記述子フィールド識別子) が返されます。  
  
 [2] IPD の SQL_DESC_DATA_PTR フィールドは、整合性チェックを強制するように設定できます。 後続の **SQLGetDescField** または **Sqlgetdescrec**の呼び出しでは、ドライバーは SQL_DESC_DATA_PTR がに設定されている値を返す必要はありません。  
  
## <a name="fieldidentifier-argument"></a>FieldIdentifier 引数  
 *FieldIdentifier*引数は、設定される記述子フィールドを示します。 記述子には、次のセクション「ヘッダーフィールド」で説明されているヘッダーフィールドと0個以上の*記述子レコード*で構成される記述子*ヘッダー*が含まれています。これについては、「ヘッダーフィールド」セクションに記載されているレコードフィールドを参照してください。  
  
## <a name="header-fields"></a>ヘッダーフィールド  
 各記述子には、次のフィールドで構成されるヘッダーがあります。  
  
 **SQL_DESC_ALLOC_TYPE [すべて]**  
 この読み取り専用の SQLSMALLINT ヘッダーフィールドは、記述子がドライバーによって自動的に割り当てられたか、またはアプリケーションによって明示的に割り当てられたかを指定します。 このフィールドはアプリケーションで取得できますが、変更はできません。 記述子がドライバーによって自動的に割り当てられた場合、このフィールドはドライバーによって SQL_DESC_ALLOC_AUTO するように設定されます。 記述子がアプリケーションによって明示的に割り当てられている場合、ドライバーによって SQL_DESC_ALLOC_USER するように設定されます。  
  
 **SQL_DESC_ARRAY_SIZE [アプリケーション記述子]**  
 ARDs では、この SQLULEN ヘッダーフィールドは、行セット内の行の数を指定します。 Sqlfetch または**Sqlfetchscroll**への呼び出しによって**SQLFetch**返される行の数、または**Sqlbulkoperations**または**SQLSetPos**の呼び出しによって操作される行数です。  
  
 APDs では、この SQLULEN ヘッダーフィールドは、各パラメーターの値の数を指定します。  
  
 このフィールドの既定値は1です。 SQL_DESC_ARRAY_SIZE が1より大きい場合は、APD またはの配列を SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、および SQL_DESC_OCTET_LENGTH_PTR します。 各配列のカーディナリティは、このフィールドの値と同じです。  
  
 このフィールドは、SQL_ATTR_ROW_ARRAY_SIZE 属性を指定して **SQLSetStmtAttr** を呼び出すことによって設定することもできます。 APD のこのフィールドは、SQL_ATTR_PARAMSET_SIZE 属性を指定して **SQLSetStmtAttr** を呼び出すことによって設定することもできます。  
  
 **SQL_DESC_ARRAY_STATUS_PTR [すべて]**  
 各記述子の種類に対して、この SQLUS悪意のある * ヘッダーフィールドは、SQLUS悪意のある値の配列を指します。 これらの配列には次の名前が付けられます。 row status array (IRD)、parameter status array (IPD)、row operation array ()、および parameter operation array (APD)。  
  
 IRD では、このヘッダーフィールドは、 **Sqlbulkoperations**、 **sqlfetch**、 **sqlbulkoperations**、または **SQLSetPos**の呼び出し後の状態値を含む行ステータス配列を指します。 配列には、行セット内の行と同じ数の要素があります。 アプリケーションで Sqlusマルウェアの配列を割り当て、このフィールドを配列を指すように設定する必要があります。 既定では、このフィールドは null ポインターに設定されます。 ドライバーは、SQL_DESC_ARRAY_STATUS_PTR フィールドが null ポインターに設定されていない限り、配列に値を設定します。この場合、状態値は生成されず、配列には設定されません。  
  
> [!CAUTION]  
>  IRD の SQL_DESC_ARRAY_STATUS_PTR フィールドが指す行ステータス配列の要素をアプリケーションで設定した場合、ドライバーの動作は未定義です。  
  
 配列には、 **Sqlbulkoperations**、 **sqlfetch**、 **sqlbulkoperations**、または **SQLSetPos**の呼び出しが最初に設定されます。 呼び出しで SQL_SUCCESS または SQL_SUCCESS_WITH_INFO が返されなかった場合、このフィールドが指す配列の内容は未定義になります。 配列内の要素には、次の値を含めることができます。  
  
-   SQL_ROW_SUCCESS: 行は正常にフェッチされましたが、最後にフェッチされてから変更されていません。  
  
-   SQL_ROW_SUCCESS_WITH_INFO: 行は正常にフェッチされましたが、最後にフェッチされてから変更されていません。 ただし、行に関する警告が返されました。  
  
-   SQL_ROW_ERROR: 行のフェッチ中にエラーが発生しました。  
  
-   SQL_ROW_UPDATED: 行は正常にフェッチされ、最後にフェッチされてから更新されました。 行が再度フェッチされると、その状態は SQL_ROW_SUCCESS になります。  
  
-   SQL_ROW_DELETED: 行は最後にフェッチされてから削除されています。  
  
-   SQL_ROW_ADDED: 行は **Sqlbulkoperations**によって挿入されました。 行が再度フェッチされると、その状態は SQL_ROW_SUCCESS になります。  
  
-   SQL_ROW_NOROW: 行セットは結果セットの末尾に重なっていますが、行の状態配列のこの要素にこれする行は返されませんでした。  
  
 IRD のこのフィールドは、SQL_ATTR_ROW_STATUS_PTR 属性を指定して **SQLSetStmtAttr** を呼び出すことによって設定することもできます。  
  
 IRD の SQL_DESC_ARRAY_STATUS_PTR フィールドは、SQL_SUCCESS または SQL_SUCCESS_WITH_INFO が返された後にのみ有効です。 リターンコードがこれらのいずれでもない場合、SQL_DESC_ROWS_PROCESSED_PTR が指す位置は定義されていません。  
  
 IPD では、このヘッダーフィールドは、 **Sqlexecute** または **SQLExecDirect**の呼び出し後のパラメーター値の各セットの状態情報を含むパラメーター状態配列を指します。 **Sqlexecute**または**SQLExecDirect**の呼び出しで SQL_SUCCESS または SQL_SUCCESS_WITH_INFO が返されなかった場合、このフィールドが指す配列の内容は未定義になります。 アプリケーションで Sqlusマルウェアの配列を割り当て、このフィールドを配列を指すように設定する必要があります。 ドライバーは、SQL_DESC_ARRAY_STATUS_PTR フィールドが null ポインターに設定されていない限り、配列に値を設定します。この場合、状態値は生成されず、配列には設定されません。 配列内の要素には、次の値を含めることができます。  
  
-   SQL_PARAM_SUCCESS: このパラメーターのセットに対して SQL ステートメントが正常に実行されました。  
  
-   SQL_PARAM_SUCCESS_WITH_INFO: このパラメーターのセットに対して SQL ステートメントが正常に実行されました。ただし、警告情報は診断データ構造で使用できます。  
  
-   SQL_PARAM_ERROR: この一連のパラメーターを処理中にエラーが発生しました。 診断データ構造では、追加のエラー情報を利用できます。  
  
-   SQL_PARAM_UNUSED: このパラメーターセットは使用されていませんでした。以前のパラメーターセットによって、処理を中止したエラーが発生したか、または APD の SQL_DESC_ARRAY_STATUS_PTR フィールドで指定された配列内のパラメーターのセットに SQL_PARAM_IGNORE が設定されていることが原因である可能性があります。  
  
-   SQL_PARAM_DIAG_UNAVAILABLE: 診断情報が使用できません。 この例として、ドライバーがパラメーターの配列をモノリシック単位として扱う場合に、このレベルのエラー情報は生成されません。  
  
 IPD のこのフィールドは、SQL_ATTR_PARAM_STATUS_PTR 属性を指定して **SQLSetStmtAttr** を呼び出すことによって設定することもできます。  
  
 このヘッダーフィールドは、この行が **SQLSetPos** 操作で無視されるかどうかを示すために、アプリケーションによって設定できる値の行操作配列を指しています。 配列内の要素には、次の値を含めることができます。  
  
-   SQL_ROW_PROCEED: 行は **SQLSetPos**を使用して bulk 操作に含まれています。 (この設定では、行に対して操作が実行されることは保証されません。 行の SQL_ROW_ERROR 状態が IRD 行の状態配列にある場合、ドライバーは行で操作を実行できない可能性があります)。  
  
-   SQL_ROW_IGNORE: 行は **SQLSetPos**を使用して一括操作から除外されます。  
  
 配列の要素が設定されていない場合は、すべての行が一括操作に含まれます。 SQL_DESC_ARRAY_STATUS_PTR フィールドの値が null ポインターの場合、すべての行が一括操作に含まれます。この解釈は、ポインターが有効な配列を指し、配列のすべての要素が SQL_ROW_PROCEED されている場合と同じです。 配列内の要素が SQL_ROW_IGNORE に設定されている場合、無視された行の行状態配列の値は変更されません。  
  
 このフィールドは、SQL_ATTR_ROW_OPERATION_PTR 属性を指定して **SQLSetStmtAttr** を呼び出すことによって設定することもできます。  
  
 APD では、このヘッダーフィールドは、 **Sqlexecute** または **SQLExecDirect** が呼び出されたときにこの一連のパラメーターを無視するかどうかを示すために、アプリケーションによって設定できる値のパラメーター操作配列を指します。 配列内の要素には、次の値を含めることができます。  
  
-   SQL_PARAM_PROCEED: パラメーターのセットは、 **Sqlexecute** または **SQLExecDirect** の呼び出しに含まれています。  
  
-   SQL_PARAM_IGNORE: パラメーターのセットは、 **Sqlexecute** または **SQLExecDirect** 呼び出しから除外されます。  
  
 配列の要素が設定されていない場合は、配列内のすべてのパラメーターセットが **Sqlexecute** または **SQLExecDirect** の呼び出しで使用されます。 APD の [SQL_DESC_ARRAY_STATUS_PTR] フィールドの値が null ポインターの場合は、すべてのパラメーターのセットが使用されます。この解釈は、ポインターが有効な配列を指し、配列のすべての要素が SQL_PARAM_PROCEED されている場合と同じです。  
  
 APD のこのフィールドは、SQL_ATTR_PARAM_OPERATION_PTR 属性を指定して **SQLSetStmtAttr** を呼び出すことによって設定することもできます。  
  
 **SQL_DESC_BIND_OFFSET_PTR [アプリケーション記述子]**  
 この SQLLEN * ヘッダーフィールドは、バインドオフセットを指します。 既定では、null ポインターに設定されています。 このフィールドが null ポインターではない場合、ドライバーはポインターを逆参照し、フェッチ時に null 以外の値を持つ各遅延フィールド (SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、および SQL_DESC_OCTET_LENGTH_PTR) に逆参照値を追加し、バインド時に新しいポインター値を使用します。  
  
 バインドオフセットは、常に、SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、および SQL_DESC_OCTET_LENGTH_PTR の各フィールドの値に直接追加されます。 オフセットが別の値に変更された場合でも、新しい値は各記述子フィールドの値に直接追加されます。 新しいオフセットは、フィールド値に前のオフセットと共に追加されることはありません。  
  
 このフィールドは *遅延フィールド*です。設定時には使用されませんが、データバッファーのアドレスを決定する必要がある場合は、後でドライバーによって使用されます。  
  
 このフィールドは、SQL_ATTR_ROW_BIND_OFFSET_PTR 属性を指定して **SQLSetStmtAttr** を呼び出すことによって設定することもできます。 このフィールドは、SQL_ATTR_PARAM_BIND_OFFSET_PTR 属性を指定して **SQLSetStmtAttr** を呼び出すことによって設定することもできます。  
  
 詳細については、 [Sqlfetchscroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) と [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)での行方向のバインドの説明を参照してください。  
  
 **SQL_DESC_BIND_TYPE [アプリケーション記述子]**  
 この SQLUINTEGER header フィールドは、列またはパラメーターのバインドに使用されるバインドの向きを設定します。  
  
 ARDs では、このフィールドは、関連付けられているステートメントハンドルで **Sqlfetchscroll** または **sqlfetch** が呼び出されたときのバインドの方向を指定します。  
  
 列に対して列方向のバインドを選択する場合、このフィールドは SQL_BIND_BY_COLUMN (既定) に設定されます。  
  
 このフィールドは、SQL_ATTR_ROW_BIND_TYPE*属性*を指定して**SQLSetStmtAttr**を呼び出すことによって設定することもできます。  
  
 APDs では、このフィールドは動的パラメーターに使用されるバインドの方向を指定します。  
  
 パラメーターの列方向のバインドを選択するには、このフィールドを SQL_BIND_BY_COLUMN (既定) に設定します。  
  
 APD のこのフィールドは、SQL_ATTR_PARAM_BIND_TYPE*属性*を指定して**SQLSetStmtAttr**を呼び出すことによって設定することもできます。  
  
 **SQL_DESC_COUNT [すべて]**  
 この SQLSMALLINT ヘッダーフィールドは、データを格納する最大番号のレコードの1から始まるインデックスを指定します。 ドライバーは、記述子のデータ構造を設定するときに、SQL_DESC_COUNT フィールドを設定して、重要なレコード数を表示する必要もあります。 アプリケーションがこのデータ構造のインスタンスを割り当てる場合、領域を確保するためのレコード数を指定する必要はありません。 アプリケーションがレコードの内容を指定すると、ドライバーは必要な操作を行い、記述子ハンドルが適切なサイズのデータ構造を参照するようにします。  
  
 SQL_DESC_COUNT は、バインドされているすべてのデータ列 (フィールドが APD にある場合) またはバインドされているすべてのパラメーター (フィールドが内にある場合) のカウントではなく、最も番号が大きいレコードの数です。 最も番号が大きい列またはパラメーターがバインド解除されている場合、SQL_DESC_COUNT は、次に大きい番号の列またはパラメーターの番号に変更されます。 列またはパラメーターの番号が最も大きい列数よりも小さい場合、 **SQLBindCol**は、 *targetvalueptr*引数が null ポインターに設定された状態で、または*parametervalueptr*引数が null ポインターに設定された**SQLBindParameter**を呼び出すことによって SQL_DESC_COUNT、変更されません。 追加の列またはパラメーターが、データを含む最も番号の大きいレコードよりも大きい数値にバインドされている場合、ドライバーは [SQL_DESC_COUNT] フィールドの値を自動的に増やします。 SQL_UNBIND オプションを指定して **SQLFreeStmt** を呼び出すことによってすべての列のバインドが解除された場合 SQL_DESC_COUNT、IRD とのフィールドは0に設定されます。 SQL_RESET_PARAMS オプションを指定して **SQLFreeStmt** を呼び出すと、APD と IPD の SQL_DESC_COUNT フィールドが0に設定されます。  
  
 SQL_DESC_COUNT の値は、 **SQLSetDescField**を呼び出すことによって、アプリケーションによって明示的に設定できます。 SQL_DESC_COUNT の値が明示的に減少した場合、SQL_DESC_COUNT の新しい値よりも大きい数値を持つすべてのレコードが実質的に削除されます。 SQL_DESC_COUNT の値が明示的に0に設定されていて、フィールドがである場合、バインドされたブックマーク列を除くすべてのデータバッファーが解放されます。  
  
 このフィールドのレコード数には、バインドされたブックマーク列は含まれません。 ブックマーク列をバインド解除する唯一の方法は、SQL_DESC_DATA_PTR フィールドを null ポインターに設定することです。  
  
 **SQL_DESC_ROWS_PROCESSED_PTR [実装記述子]**  
 IRD では、この SQLULEN \* header フィールドは、 **sqlfetch** または **sqlulen**の呼び出しの後にフェッチされた行の数を含むバッファー、または **sqlulen** または **SQLSetPos**の呼び出しによって実行される一括操作の影響を受ける行の数 (エラー行を含む) を指します。  
  
 IPD では、この SQLUINTEGER * ヘッダーフィールドは、エラーセットを含む、処理されたパラメーターのセットの数を格納しているバッファーを指します。 Null ポインターの場合、数値は返されません。  
  
 SQL_DESC_ROWS_PROCESSED_PTR は、 **Sqlfetch** または **SQLFETCHSCROLL** (IRD フィールドの場合) または **Sqlfetch**、 **SQLExecDirect**、 **sqlparamdata** (IPD フィールドの場合) の呼び出し後に、SQL_SUCCESS または SQL_SUCCESS_WITH_INFO が返された後にのみ有効です。 このフィールドが指すバッファーに入力する呼び出しが SQL_SUCCESS または SQL_SUCCESS_WITH_INFO を返さない場合、SQL_NO_DATA を返さない限り、バッファーの内容は未定義になります。この場合、バッファー内の値は0に設定されます。  
  
 このフィールドは、SQL_ATTR_ROWS_FETCHED_PTR 属性を指定して **SQLSetStmtAttr** を呼び出すことによって設定することもできます。 APD のこのフィールドは、SQL_ATTR_PARAMS_PROCESSED_PTR 属性を指定して **SQLSetStmtAttr** を呼び出すことによって設定することもできます。  
  
 このフィールドが指すバッファーは、アプリケーションによって割り当てられます。 これは、ドライバーによって設定される遅延出力バッファーです。 既定では、null ポインターに設定されています。  
  
## <a name="record-fields"></a>レコードフィールド  
 各記述子には、記述子の種類に応じて、列データまたは動的パラメーターのいずれかを定義するフィールドで構成される1つ以上のレコードが含まれます。 各レコードは、1つの列またはパラメーターの完全な定義です。  
  
 **SQL_DESC_AUTO_UNIQUE_VALUE [IRDs]**  
 この読み取り専用の SQLINTEGER レコードフィールドには、列が自動インクリメント列の場合は SQL_TRUE が、列が自動インクリメント列でない場合は SQL_FALSE が含まれます。 このフィールドは読み取り専用ですが、基になる自動インクリメント列は必ずしも読み取り専用ではありません。  
  
 **SQL_DESC_BASE_COLUMN_NAME [IRDs]**  
 この読み取り専用の SQLCHAR * レコードフィールドには、結果セット列の基本列名が含まれています。 ベース列名が存在しない場合 (式である列の場合のように)、この変数には空の文字列が含まれます。  
  
 **SQL_DESC_BASE_TABLE_NAME [IRDs]**  
 この読み取り専用の SQLCHAR * レコードフィールドには、結果セット列のベーステーブル名が含まれています。 ベーステーブルの名前を定義できない場合、または適用できない場合、この変数には空の文字列が含まれます。  
  
 **SQL_DESC_CASE_SENSITIVE [実装記述子]**  
 この読み取り専用の SQLINTEGER レコードフィールドには、照合順序と比較のために列またはパラメーターが大文字と小文字を区別するように処理される場合は SQL_TRUE が含まれます。照合順序と比較で列が大文字と小文字を区別して扱われない場合、または列が非文字の列である場合は SQL_FALSE ます。  
  
 **SQL_DESC_CATALOG_NAME [IRDs]**  
 この読み取り専用の SQLCHAR * レコードフィールドには、列を含むベーステーブルのカタログが含まれています。 列が式である場合、または列がビューの一部である場合、戻り値はドライバーに依存します。 データソースでカタログがサポートされていない場合、またはカタログを特定できない場合、この変数には空の文字列が含まれます。  
  
 **SQL_DESC_CONCISE_TYPE [すべて]**  
 この SQLSMALLINT ヘッダーフィールドは、datetime データ型および interval データ型を含む、すべてのデータ型の簡潔なデータ型を指定します。  
  
 SQL_DESC_CONCISE_TYPE、SQL_DESC_TYPE、および SQL_DESC_DATETIME_INTERVAL_CODE の各フィールドの値は相互に依存しています。 いずれかのフィールドが設定されるたびに、もう一方も設定する必要があります。 SQL_DESC_CONCISE_TYPE は、 **SQLBindCol** 、 **SQLBindParameter**、または **SQLSetDescField**への呼び出しによって設定できます。 SQL_DESC_TYPE は、 **SQLSetDescField** または **SQLSetDescRec**の呼び出しによって設定できます。  
  
 SQL_DESC_CONCISE_TYPE が interval データ型または datetime データ型以外の簡潔なデータ型に設定されている場合、SQL_DESC_TYPE フィールドは同じ値に設定され、SQL_DESC_DATETIME_INTERVAL_CODE フィールドは0に設定されます。  
  
 SQL_DESC_CONCISE_TYPE が簡潔な datetime または interval データ型に設定されている場合、SQL_DESC_TYPE フィールドは対応する詳細な種類 (SQL_DATETIME または SQL_INTERVAL) に設定され、SQL_DESC_DATETIME_INTERVAL_CODE フィールドは適切なサブコードに設定されます。  
  
 **SQL_DESC_DATA_PTR [アプリケーション記述子と IPDs]**  
 この SQLPOINTER レコードフィールドは、パラメーター値 (APDs の場合) または列の値 (ARDs の場合) が含まれる変数を指します。 このフィールドは *遅延フィールド*です。 設定時には使用されませんが、後でデータを取得するためにドライバーによって使用されます。  
  
 **SQLBindCol**への呼び出しで*targetvalueptr*引数が null ポインターである場合、または**SQLSetDescField**または**SQLSetDescRec**への呼び出しによって null ポインターに設定されている場合 SQL_DESC_DATA_PTR は、SQL_DESC_DATA_PTR フィールドで指定された列がバインド解除されます。 SQL_DESC_DATA_PTR フィールドが null ポインターに設定されている場合、他のフィールドは影響を受けません。  
  
 このフィールドが指すバッファーをいっぱいにする **Sqlfetch** または **sqlfetchscroll** の呼び出しで SQL_SUCCESS または SQL_SUCCESS_WITH_INFO が返されなかった場合、バッファーの内容は未定義になります。  
  
 APD、、または IPD の SQL_DESC_DATA_PTR フィールドが設定されている場合、ドライバーは、SQL_DESC_TYPE フィールドの値に有効な ODBC C データ型またはドライバー固有のデータ型のいずれかが含まれていること、およびデータ型に影響する他のすべてのフィールドが一致していることを確認します。 IPD の [SQL_DESC_DATA_PTR] フィールドを使用するのは、整合性チェックを要求することだけです。 具体的には、アプリケーションで IPD の SQL_DESC_DATA_PTR フィールドを設定した後、このフィールドで **SQLGetDescField** を呼び出すと、必ずしも設定された値が返されるとは限りません。 詳細については、「 [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)」の「整合性チェック」を参照してください。  
  
 **SQL_DESC_DATETIME_INTERVAL_CODE [すべて]**  
 この SQLSMALLINT レコードフィールドには、SQL_DESC_TYPE フィールドが SQL_DATETIME または SQL_INTERVAL ときの、特定の datetime データ型または interval データ型のサブコードが含まれています。 これは、SQL データ型と C データ型の両方に当てはまります。 このコードは、"TYPE" または "C_TYPE" (datetime 型の場合)、または "INTERVAL" または "C_INTERVAL" (interval 型の場合) に置き換えられた "code" を使用して、データ型名で構成されます。  
  
 アプリケーション記述子の SQL_DESC_TYPE および SQL_DESC_CONCISE_TYPE が SQL_C_DEFAULT に設定されており、記述子がステートメントハンドルに関連付けられていない場合、SQL_DESC_DATETIME_INTERVAL_CODE の内容は未定義になります。  
  
 このフィールドは、次の表に示す datetime データ型に対して設定できます。  
  
|Datetime 型|DATETIME_INTERVAL_CODE|  
|--------------------|------------------------------|  
|SQL_TYPE_DATE/SQL_C_TYPE_DATE|SQL_CODE_DATE|  
|SQL_TYPE_TIME/SQL_C_TYPE_TIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP/SQL_C_TYPE_TIMESTAMP|SQL_CODE_TIMESTAMP|  
  
 このフィールドは、次の表に示す interval データ型に対して設定できます。  
  
|[間隔の種類]|DATETIME_INTERVAL_CODE|  
|-------------------|------------------------------|  
|SQL_INTERVAL_DAY/SQL_C_INTERVAL_DAY|SQL_CODE_DAY|  
|SQL_INTERVAL_DAY_TO_HOUR/SQL_C_INTERVAL_DAY_TO_HOUR|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE/SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_CODE_DAY_TO_MINUTE|  
|SQL_INTERVAL_DAY_TO_SECOND/SQL_C_INTERVAL_DAY_TO_SECOND|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR/SQL_C_INTERVAL_HOUR|SQL_CODE_HOUR|  
|SQL_INTERVAL_HOUR_TO_MINUTE/SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND/SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE/SQL_C_INTERVAL_MINUTE|SQL_CODE_MINUTE|  
|SQL_INTERVAL_MINUTE_TO_SECOND/SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_CODE_MINUTE_TO_SECOND|  
|SQL_INTERVAL_MONTH/SQL_C_INTERVAL_MONTH|SQL_CODE_MONTH|  
|SQL_INTERVAL_SECOND/SQL_C_INTERVAL_SECOND|SQL_CODE_SECOND|  
|SQL_INTERVAL_YEAR/SQL_C_INTERVAL_YEAR|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH/SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_CODE_YEAR_TO_MONTH|  
  
 データ間隔およびこのフィールドの詳細については、「 [データ型の識別子と記述子](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)」を参照してください。  
  
 **SQL_DESC_DATETIME_INTERVAL_PRECISION [すべて]**  
 この SQLINTEGER レコードフィールドには、SQL_DESC_TYPE フィールドが SQL_INTERVAL 場合の間隔を表す有効桁数が含まれます。 SQL_DESC_DATETIME_INTERVAL_CODE フィールドが interval データ型に設定されている場合、このフィールドは既定の間隔の有効桁数に設定されます。  
  
 **SQL_DESC_DISPLAY_SIZE [IRDs]**  
 この読み取り専用の SQLINTEGER レコードフィールドには、列のデータを表示するために必要な最大文字数が含まれています。  
  
 **SQL_DESC_FIXED_PREC_SCALE [実装記述子]**  
 この読み取り専用の SQLSMALLINT レコードフィールドは、列が正確な数値列であり、固定の有効桁数と0以外の小数点以下桁数を持つ場合は SQL_TRUE に設定されます。また、列が固定有効桁数と小数点以下桁数が固定されている正確な数値列でない場合は SQL_FALSE に設定されます。  
  
 **SQL_DESC_INDICATOR_PTR [アプリケーション記述子]**  
 ARDs では、この SQLLEN * レコードフィールドはインジケーター変数を指しています。 この変数には、列の値が NULL の場合に SQL_NULL_DATA が含まれます。 APDs では、インジケーター変数を SQL_NULL_DATA に設定して NULL 動的引数を指定します。 それ以外の場合、変数は0になります (SQL_DESC_INDICATOR_PTR と SQL_DESC_OCTET_LENGTH_PTR の値が同じポインターである場合を除く)。  
  
 の SQL_DESC_INDICATOR_PTR フィールドが null ポインターの場合、ドライバーは、列が NULL かどうかに関する情報を返すことはできません。 列が NULL で SQL_DESC_INDICATOR_PTR が null ポインターである場合は、 **Sqlfetch** または **sqlfetchscroll**の呼び出し後にドライバーがバッファーを設定しようとすると、SQLSTATE 22002 (必要に応じて指定されていないインジケーター変数) が返されます。 **Sqlfetch**または**sqlfetchscroll**への呼び出しで SQL_SUCCESS または SQL_SUCCESS_WITH_INFO が返されなかった場合、バッファーの内容は未定義になります。  
  
 SQL_DESC_INDICATOR_PTR フィールドは、SQL_DESC_OCTET_LENGTH_PTR が指すフィールドが設定されているかどうかを判断します。 列のデータ値が NULL の場合、ドライバーは、インジケーター変数を SQL_NULL_DATA に設定します。 SQL_DESC_OCTET_LENGTH_PTR によってポイントされているフィールドは設定されません。 フェッチ中に NULL 値が検出されなかった場合、SQL_DESC_INDICATOR_PTR が指すバッファーは0に設定され、SQL_DESC_OCTET_LENGTH_PTR が指すバッファーはデータの長さに設定されます。  
  
 APD の SQL_DESC_INDICATOR_PTR フィールドが null ポインターの場合、アプリケーションはこの記述子レコードを使用して NULL 引数を指定することはできません。  
  
 このフィールドは *遅延フィールド*です。このフィールドは、設定時には使用されませんが、後でドライバーによって使用されます (ARDs の場合)。または、null 値を許容するかどうかを指定します (apds の場合)。  
  
 **SQL_DESC_LABEL [IRDs]**  
 この読み取り専用の SQLCHAR * レコードフィールドには、列のラベルまたはタイトルが含まれています。 列にラベルがない場合、この変数には列名が格納されます。 列に名前が付けられていない場合、ラベルが付いていない場合、この変数には空の文字列が含まれます。  
  
 **SQL_DESC_LENGTH [すべて]**  
 この SQLULEN レコードフィールドは、文字の文字列の最大長または実際の長さ (バイト単位) か、バイナリデータ型です。 固定長データ型の場合は最大長、可変長データ型の場合は実際の長さです。 この値は、文字列を終了する null 終了文字を常に除外します。 型が SQL_TYPE_DATE、SQL_TYPE_TIME、SQL_TYPE_TIMESTAMP、または SQL interval データ型のいずれかである値の場合、このフィールドには datetime または interval 値の文字列形式の文字数が含まれます。  
  
 このフィールドの値は、ODBC 2.x で定義*されて*いる "length" の値とは異なる場合があります。 詳細については、「 [付録 D: データ型](../../../odbc/reference/appendixes/appendix-d-data-types.md)」を参照してください。  
  
 **SQL_DESC_LITERAL_PREFIX [IRDs]**  
 この読み取り専用の SQLCHAR * レコードフィールドには、ドライバーがこのデータ型のリテラルのプレフィックスとして認識する文字または文字が含まれています。 この変数には、リテラルプレフィックスが適用されないデータ型の空の文字列が含まれています。  
  
 **SQL_DESC_LITERAL_SUFFIX [IRDs]**  
 この読み取り専用の SQLCHAR * レコードフィールドには、ドライバーがこのデータ型のリテラルのサフィックスとして認識する文字または文字が含まれています。 この変数には、リテラルサフィックスが適用されないデータ型の空の文字列が含まれています。  
  
 **SQL_DESC_LOCAL_TYPE_NAME [実装記述子]**  
 この読み取り専用の SQLCHAR * レコードフィールドには、データ型の標準名とは異なる可能性がある、ローカライズされた (ネイティブ言語) 名が含まれています。 ローカライズされた名前がない場合は、空の文字列が返されます。 このフィールドは、表示のみを目的としています。  
  
 **SQL_DESC_NAME [実装記述子]**  
 行記述子のこの SQLCHAR * レコードフィールドには、列の別名 (該当する場合) が含まれています。 列の別名が適用されない場合は、列名が返されます。 どちらの場合も、ドライバーは SQL_DESC_NAME フィールドを設定するときに、SQL_DESC_UNNAMED フィールドを SQL_NAMED に設定します。 列名または列の別名がない場合、ドライバーは SQL_DESC_NAME フィールドに空の文字列を返し、SQL_DESC_UNNAMED フィールドを SQL_UNNAMED に設定します。  
  
 アプリケーションでは、IPD の SQL_DESC_NAME フィールドをパラメーター名または別名に設定して、ストアドプロシージャパラメーターを名前で指定できます。 (詳細については、「 [名前によるパラメーターのバインド (名前付きパラメーター)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)」を参照してください)。IRD の SQL_DESC_NAME フィールドは読み取り専用フィールドです。アプリケーションが設定を試みた場合、SQLSTATE HY091 (無効な記述子フィールド識別子) が返されます。  
  
 IPDs では、ドライバーが名前付きパラメーターをサポートしていない場合、このフィールドは定義されません。 ドライバーが名前付きパラメーターをサポートしていて、パラメーターを記述できる場合は、このフィールドにパラメーター名が返されます。  
  
 **SQL_DESC_NULLABLE [実装記述子]**  
 IRDs では、この読み取り専用の SQLSMALLINT レコードフィールドは、列が null 値を持つことができる場合は SQL_NULLABLE、列に null 値がない場合は SQL_NO_NULLS、null 値を許容するかどうかが不明な場合は SQL_NULLABLE_UNKNOWN ます。 このフィールドは、ベース列ではなく、結果セットの列に関連します。  
  
 IPDs では、動的パラメーターは常に null 値が許容されるため、アプリケーションでは設定できないため、このフィールドは常に SQL_NULLABLE に設定されます。  
  
 **SQL_DESC_NUM_PREC_RADIX [すべて]**  
 SQL_DESC_PRECISION フィールドにはビット数が含まれているため、SQL_DESC_TYPE フィールドのデータ型が概数データ型の場合、このフィールドの値は2になります。 SQL_DESC_PRECISION フィールドには小数点以下の桁数が含まれているため、SQL_DESC_TYPE フィールドのデータ型が正確な数値データ型である場合、このフィールドの値は10になります。 数値以外のすべてのデータ型では、このフィールドは0に設定されます。  
  
 **SQL_DESC_OCTET_LENGTH [すべて]**  
 この SQLLEN レコードフィールドには、文字列またはバイナリデータ型の長さ (バイト単位) が含まれています。 固定長の文字型またはバイナリ型の場合、実際のバイト数です。 可変長の文字型またはバイナリ型の場合は、バイト単位の最大長です。 この値は、実装記述子の null 終端文字のスペースを常に除外し、アプリケーション記述子の null 終端文字のスペースを常に含みます。 アプリケーションデータの場合、このフィールドにはバッファーのサイズが格納されます。 APDs の場合、このフィールドは出力パラメーターまたは入出力パラメーターに対してのみ定義されます。  
  
 **SQL_DESC_OCTET_LENGTH_PTR [アプリケーション記述子]**  
 この SQLLEN * レコードフィールドは、動的引数 (パラメーター記述子の場合) またはバインドされた列の値 (行記述子の場合) の合計長をバイト単位で格納する変数を指します。  
  
 APD の場合、この値は文字列とバイナリを除くすべての引数に対して無視されます。このフィールドが SQL_NTS を指している場合、動的引数は null で終わる必要があります。 バインドされたパラメーターが実行時データパラメーターであることを示すために、アプリケーションは、APD の適切なレコードのこのフィールドを、実行時に SQL_LEN_DATA_AT_EXEC マクロの値 SQL_DATA_AT_EXEC または結果を含む変数に設定します。 このようなフィールドが複数ある場合、SQL_DESC_DATA_PTR は、要求されているパラメーターをアプリケーションが判断できるように、パラメーターを一意に識別する値に設定できます。  
  
 の OCTET_LENGTH_PTR フィールドが null ポインターの場合、ドライバーは列の長さの情報を返しません。 APD の SQL_DESC_OCTET_LENGTH_PTR フィールドが null ポインターの場合、ドライバーは、文字列とバイナリ値が null で終わることを前提としています。 (バイナリ値は null で終わることはできませんが、切り捨てを避けるために長さを指定する必要があります)。  
  
 このフィールドが指すバッファーをいっぱいにする **Sqlfetch** または **sqlfetchscroll** の呼び出しで SQL_SUCCESS または SQL_SUCCESS_WITH_INFO が返されなかった場合、バッファーの内容は未定義になります。 このフィールドは *遅延フィールド*です。 この値は、設定時には使用されませんが、後でドライバーによって使用され、データのオクテット長を決定または示すことができます。  
  
 **SQL_DESC_PARAMETER_TYPE [IPDs]**  
 この SQLSMALLINT レコードフィールドは、入力パラメーターに対して SQL_PARAM_INPUT に設定されます。入力パラメーターまたは出力パラメーターの場合は SQL_PARAM_INPUT_OUTPUT、出力パラメーターの場合は SQL_PARAM_OUTPUT、入出力ストリームパラメーターの場合は SQL_PARAM_INPUT_OUTPUT_STREAM、出力ストリームパラメーターの場合は SQL_PARAM_OUTPUT_STREAM です。 既定では SQL_PARAM_INPUT に設定されています。  
  
 IPD の場合、IPD がドライバーによって自動的に設定されない場合、フィールドは既定で SQL_PARAM_INPUT に設定されます (SQL_ATTR_ENABLE_AUTO_IPD statement 属性は SQL_FALSE)。 アプリケーションでは、入力パラメーターではないパラメーターの IPD にこのフィールドを設定する必要があります。  
  
 **SQL_DESC_PRECISION [すべて]**  
 この SQLSMALLINT レコードフィールドには、正確な数値型の数字の数、概数型の仮数部のビット数 (binary precision)、または SQL_TYPE_TIME、SQL_TYPE_TIMESTAMP、または SQL_INTERVAL_SECOND データ型の秒の小数部の桁数が含まれています。 このフィールドは、他のすべてのデータ型には定義されていません。  
  
 このフィールドの値は、ODBC 2.x で定義*されて*いる "有効桁数" の値とは異なる場合があります。 詳細については、「 [付録 D: データ型](../../../odbc/reference/appendixes/appendix-d-data-types.md)」を参照してください。  
  
 **SQL_DESC_ROWVER [実装記述子]**  
 この SQLSMALLINTrecord フィールドは、行が更新されたときに、DBMS によって列が自動的に変更されるかどうかを示します (たとえば、SQL Server の "timestamp" 型の列)。 このレコードフィールドの値は、列が行のバージョン管理列である場合は SQL_TRUE に、それ以外の場合は SQL_FALSE に設定されます。 この列属性は、列が自動的に更新されるかどうかを判断するために、IdentifierType SQL_ROWVER を指定して **Sqlの列** を呼び出す場合と似ています。  
  
 **SQL_DESC_SCALE [すべて]**  
 この SQLSMALLINT レコードフィールドには、decimal データ型と numeric データ型に対して定義された小数点以下桁数が含まれています。 フィールドは、他のすべてのデータ型に対して定義されていません。  
  
 このフィールドの値は、ODBC 2.x で定義*されて*いる "scale" の値とは異なる場合があります。 詳細については、「 [付録 D: データ型](../../../odbc/reference/appendixes/appendix-d-data-types.md)」を参照してください。  
  
 **SQL_DESC_SCHEMA_NAME [IRDs]**  
 この読み取り専用の SQLCHAR * レコードフィールドには、列を含むベーステーブルのスキーマ名が格納されます。 列が式である場合、または列がビューの一部である場合、戻り値はドライバーに依存します。 データソースでスキーマがサポートされていない場合、またはスキーマ名を特定できない場合、この変数には空の文字列が含まれます。  
  
 **SQL_DESC_SEARCHABLE [IRDs]**  
 この読み取り専用の SQLSMALLINT レコードフィールドは、次のいずれかの値に設定されます。  
  
-   **WHERE**句で列を使用できない場合は SQL_PRED_NONE します。 (これは、ODBC 2.x の SQL_UNSEARCHABLE 値と*同じです)。*  
  
-   **WHERE**句で列を使用できるが、 **LIKE**述語でのみ使用できる場合は SQL_PRED_CHAR します。 (これは、ODBC 2.x の SQL_LIKE_ONLY 値と*同じです)。*  
  
-   **WHERE**句で列を使用できるかどうかを SQL_PRED_BASIC します。ただし、の**よう**にすべての比較演算子を使用できます。 (これは、ODBC 2.x の SQL_EXCEPT_LIKE 値と*同じです)。*  
  
-   任意の比較演算子を持つ **where** 句で列を使用できるかどうかを SQL_PRED_SEARCHABLE します。  
  
 **SQL_DESC_TABLE_NAME [IRDs]**  
 この読み取り専用の SQLCHAR * レコードフィールドには、この列を含むベーステーブルの名前が含まれています。 列が式である場合、または列がビューの一部である場合、戻り値はドライバーに依存します。  
  
 **SQL_DESC_TYPE [すべて]**  
 この SQLSMALLINT レコードフィールドは、datetime データ型および interval データ型を除くすべてのデータ型について、簡潔な SQL データ型または C データ型を指定します。 Datetime および interval データ型の場合、このフィールドには、SQL_DATETIME または SQL_INTERVAL の詳細データ型を指定します。  
  
 このフィールドに SQL_DATETIME または SQL_INTERVAL が含まれている場合は、SQL_DESC_DATETIME_INTERVAL_CODE フィールドに簡潔な型の適切なサブコードが含まれている必要があります。 Datetime データ型の場合、SQL_DESC_TYPE には SQL_DATETIME が含まれ、SQL_DESC_DATETIME_INTERVAL_CODE フィールドには特定の datetime データ型のサブコードが含まれます。 Interval データ型の場合、SQL_DESC_TYPE には SQL_INTERVAL が含まれ、SQL_DESC_DATETIME_INTERVAL_CODE フィールドには特定の interval データ型のサブコードが含まれます。  
  
 SQL_DESC_TYPE フィールドと SQL_DESC_CONCISE_TYPE フィールドの値は相互に依存しています。 いずれかのフィールドが設定されるたびに、もう一方も設定する必要があります。 SQL_DESC_TYPE は、 **SQLSetDescField** または **SQLSetDescRec**の呼び出しによって設定できます。 SQL_DESC_CONCISE_TYPE は、 **SQLBindCol** 、 **SQLBindParameter**、または **SQLSetDescField**への呼び出しによって設定できます。  
  
 SQL_DESC_TYPE が interval データ型または datetime データ型以外の簡潔なデータ型に設定されている場合、SQL_DESC_CONCISE_TYPE フィールドは同じ値に設定され、SQL_DESC_DATETIME_INTERVAL_CODE フィールドは0に設定されます。  
  
 SQL_DESC_TYPE が verbose datetime または interval データ型 (SQL_DATETIME または SQL_INTERVAL) に設定されていて、SQL_DESC_DATETIME_INTERVAL_CODE フィールドが適切なサブコードに設定されている場合、[SQL_DESC_CONCISE の種類] フィールドは、対応する簡潔な型に設定されます。 SQL_DESC_TYPE を簡潔な datetime 型または interval 型のいずれかに設定しようとすると、SQLSTATE HY021 (矛盾した記述子情報) が返されます。  
  
 **SQLBindCol**、 **SQLBindParameter**、または**SQLSetDescField**の呼び出しによって SQL_DESC_TYPE フィールドが設定されている場合、次の表に示すように、次のフィールドは既定値に設定されます。 同じレコードの残りのフィールドの値は未定義です。  
  
|SQL_DESC_TYPE の値|その他のフィールドは暗黙的に設定します|  
|------------------------------|---------------------------------|  
|SQL_CHAR、SQL_VARCHAR、SQL_C_CHAR、SQL_C_VARCHAR|SQL_DESC_LENGTH が1に設定されています。 SQL_DESC_PRECISION が0に設定されています。|  
|SQL_DATETIME|SQL_DESC_DATETIME_INTERVAL_CODE が SQL_CODE_DATE または SQL_CODE_TIME に設定されている場合、SQL_DESC_PRECISION は0に設定されます。 SQL_DESC_TIMESTAMP に設定されている場合、SQL_DESC_PRECISION は6に設定されます。|  
|SQL_DECIMAL、SQL_NUMERIC、SQL_C_NUMERIC|SQL_DESC_SCALE が0に設定されています。 SQL_DESC_PRECISION は、それぞれのデータ型に対して実装で定義された有効桁数に設定されます。<br /><br /> SQL_C_NUMERIC 値を手動でバインドする方法については、「 [SQL To C: Numeric](../../../odbc/reference/appendixes/sql-to-c-numeric.md) 」を参照してください。|  
|SQL_FLOAT、SQL_C_FLOAT|SQL_DESC_PRECISION は、SQL_FLOAT の実装で定義された既定の有効桁数に設定されます。|  
|SQL_INTERVAL|SQL_DESC_DATETIME_INTERVAL_CODE が INTERVAL データ型に設定されている場合、SQL_DESC_DATETIME_INTERVAL_PRECISION は 2 (既定の間隔の有効桁数) に設定されます。 間隔に秒の部分がある場合、SQL_DESC_PRECISION は 6 (既定の間隔 (秒) の有効桁数) に設定されます。|  
  
 アプリケーションが**SQLSetDescRec**を呼び出すのではなく、記述子のフィールドを設定するために**SQLSetDescField**を呼び出す場合、アプリケーションは最初にデータ型を宣言する必要があります。 この場合、前の表に示されている他のフィールドが暗黙的に設定されます。 暗黙的に設定された値のいずれかが受け入れられない場合、アプリケーションは **SQLSetDescField** または **SQLSetDescRec** を呼び出して、許容できない値を明示的に設定できます。  
  
 **SQL_DESC_TYPE_NAME [実装記述子]**  
 この読み取り専用の SQLCHAR * レコードフィールドには、データソースに依存する型の名前 (たとえば、"CHAR"、"VARCHAR" など) が含まれています。 データ型名が不明な場合、この変数には空の文字列が含まれます。  
  
 **SQL_DESC_UNNAMED [実装記述子]**  
 行記述子のこの SQLSMALLINT レコードフィールドは、ドライバーが SQL_DESC_NAME フィールドを設定するときに SQL_NAMED または SQL_UNNAMED のいずれかに設定されます。 SQL_DESC_NAME フィールドに列の別名が含まれている場合、または列の別名が適用されていない場合は、ドライバーによって SQL_DESC_UNNAMED フィールドが SQL_NAMED に設定されます。 アプリケーションで IPD の SQL_DESC_NAME フィールドをパラメーター名またはエイリアスに設定すると、ドライバーは IPD の SQL_DESC_UNNAMED フィールドを SQL_NAMED に設定します。 列名または列の別名がない場合、ドライバーは SQL_DESC_UNNAMED フィールドを SQL_UNNAMED に設定します。  
  
 アプリケーションでは、IPD の SQL_DESC_UNNAMED フィールドを SQL_UNNAMED に設定できます。 アプリケーションが IPD の SQL_DESC_UNNAMED フィールドを SQL_NAMED に設定しようとすると、SQLSTATE HY091 (無効な記述子フィールド識別子) が返されます。 IRD の SQL_DESC_UNNAMED フィールドは読み取り専用です。アプリケーションが設定を試みた場合、SQLSTATE HY091 (無効な記述子フィールド識別子) が返されます。  
  
 **SQL_DESC_UNSIGNED [実装記述子]**  
 この読み取り専用の SQLSMALLINT レコードフィールドは、列の型が符号なしまたは非数値の場合は SQL_TRUE に、列の型が署名されている場合は SQL_FALSE に設定されます。  
  
 **SQL_DESC_UPDATABLE [IRDs]**  
 この読み取り専用の SQLSMALLINT レコードフィールドは、次のいずれかの値に設定されます。  
  
-   結果セット列が読み取り専用の場合は SQL_ATTR_READ_ONLY します。  
  
-   結果セット列が読み取り/書き込み可能かどうかを SQL_ATTR_WRITE します。  
  
-   結果セット列が更新可能かどうかが不明な場合は、SQL_ATTR_READWRITE_UNKNOWN します。  
  
 SQL_DESC_UPDATABLE は、ベーステーブルの列ではなく、結果セットの列の更新可能性について説明します。 この結果セット列の基になるベーステーブルの列の更新可能性は、このフィールドの値と異なる場合があります。 列を更新できるかどうかは、データ型、ユーザー権限、および結果セット自体の定義に基づいて決まります。 列が更新可能かどうかが不明な場合は、SQL_ATTR_READWRITE_UNKNOWN が返されます。  
  
## <a name="consistency-checks"></a>整合性チェック  
 アプリケーションが APD または IPD の SQL_DESC_DATA_PTR フィールドに値を渡すたびに、ドライバーによって整合性チェックが自動的に実行されます。 いずれかのフィールドが他のフィールドと矛盾している場合、 **SQLSetDescField** は SQLSTATE HY021 (矛盾した記述子情報) を返します。 詳細については、 [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)の「整合性チェック」を参照してください。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|列のバインド|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|パラメーターのバインド|[SQLBindParameter 関数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|記述子フィールドを取得する|[SQLGetDescField 関数](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|複数の記述子フィールドの取得|[SQLGetDescRec 関数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|複数の記述子フィールドの設定|[SQLSetDescRec 関数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC ヘッダーファイル](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)
