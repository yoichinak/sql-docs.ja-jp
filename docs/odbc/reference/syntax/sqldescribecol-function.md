---
description: SQLDescribeCol 関数
title: SQLDescribeCol 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDescribeCol
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDescribeCol
helpviewer_keywords:
- SQLDescribeCol function [ODBC]
ms.assetid: eddef353-83f3-4a3c-8f24-f9ed888890a4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4007d5edbd400e65ea92d8c5dcab947a53779ec4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491327"
---
# <a name="sqldescribecol-function"></a>SQLDescribeCol 関数
**互換性**  
 導入されたバージョン: ODBC 1.0 標準準拠: ISO 92  
  
 **まとめ**  
 結果セットの1つの列に対して、 **SQLDescribeCol**は結果記述子-列名、型、列サイズ、10進数、および null 値の許容属性を返します。 この情報は、IRD のフィールドにも記載されています。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLDescribeCol(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   ColumnNumber,  
      SQLCHAR *      ColumnName,  
      SQLSMALLINT    BufferLength,  
      SQLSMALLINT *  NameLengthPtr,  
      SQLSMALLINT *  DataTypePtr,  
      SQLULEN *      ColumnSizePtr,  
      SQLSMALLINT *  DecimalDigitsPtr,  
      SQLSMALLINT *  NullablePtr);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル。  
  
 *ColumnNumber*  
 代入列の順序の昇順で並べ替えられた結果データの列数。1から始まります。 *Columnnumber*引数を0に設定して、ブックマーク列を記述することもできます。  
  
 *[ColumnName]*  
 Output列名を返す null で終わるバッファーへのポインター。 この値は、IRD の SQL_DESC_NAME フィールドから読み取られます。 列に名前が付いていない場合、または列名を特定できない場合、ドライバーは空の文字列を返します。  
  
 *Columnname*が NULL の場合でも、 *NameLengthPtr*は、 *columnname*が指すバッファーで返すことができる文字の合計数 (文字データの null 終端文字を除く) を返します。  
  
 *BufferLength*  
 代入**ColumnName* バッファーの長さ (文字数)。  
  
 *NameLengthPtr*  
 OutputColumnName で返すことができる合計文字数 (null 終了を除く) を返すバッファーへのポインター \* *ColumnName*。 返すことのできる文字数が*Bufferlength*以上の場合、ColumnName の列名は \* *ColumnName* *bufferlength*に切り捨てられ、null 終了文字の長さを引いたものになります。  
  
 *DataTypePtr*  
 Output列の SQL データ型を返すバッファーへのポインター。 この値は、IRD の SQL_DESC_CONCISE_TYPE フィールドから読み取られます。 これは、 [Sql データ型](../../../odbc/reference/appendixes/sql-data-types.md)の値、またはドライバー固有の sql データ型のいずれかになります。 データ型を特定できない場合、ドライバーは SQL_UNKNOWN_TYPE を返します。  
  
 ODBC 3 の場合。*x*、SQL_TYPE_DATE、SQL_TYPE_TIME、または SQL_TYPE_TIMESTAMP が、ODBC 2 では、日付、時刻、またはタイムスタンプデータの* \* DataTypePtr*で返されます。*x*、SQL_DATE、SQL_TIME、または SQL_TIMESTAMP が返されます。 ODBC 2 では、ドライバーマネージャーが必要なマッピングを実行します。*x* アプリケーションは ODBC 3 を使用して動作しています。*x* ドライバーまたは ODBC 3 の場合。*x* アプリケーションは ODBC 2 で動作しています。*x* ドライバー。  
  
 *Columnnumber*が 0 (ブックマーク列) の場合、 * \* DataTypePtr*では可変長のブックマークに対して SQL_BINARY が返されます。 (SQL_INTEGER は、ブックマークが ODBC 3 で使用されている場合に返されます。*x* アプリケーションが ODBC 2 で動作する。*x* ドライバーまたは ODBC 2。*x* アプリケーションが ODBC 3 を使用して動作している。*x* ドライバー。)  
  
 これらのデータ型の詳細については、「付録 D: データ型」の「 [SQL データ型](../../../odbc/reference/appendixes/sql-data-types.md) 」を参照してください。 ドライバー固有の SQL データ型の詳細については、ドライバーのドキュメントを参照してください。  
  
 *ColumnSizePtr*  
 Outputデータソース上の列のサイズ (文字数) を返すバッファーへのポインター。 列のサイズを特定できない場合、ドライバーは0を返します。 列のサイズの詳細については、「付録 D: データ型」の「 [列のサイズ、10進数、転送オクテットの長さ、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 」を参照してください。  
  
 *DecimalDigitsPtr*  
 Outputデータソース上の列の小数点以下桁数を返すバッファーへのポインター。 小数点以下桁数を特定できない場合、または適用できない場合、ドライバーは0を返します。 10進数の詳細については、「付録 D: データ型」の「 [列のサイズ、10進数字、転送オクテットの長さ、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 」を参照してください。  
  
 *NullablePtr*  
 Output列で NULL 値が許容されるかどうかを示す値を返すバッファーへのポインター。 この値は、IRD の SQL_DESC_NULLABLE フィールドから読み取られます。 値は、次のいずれかになります。  
  
 SQL_NO_NULLS: この列では NULL 値が許可されていません。  
  
 SQL_NULLABLE: この列では NULL 値が許可されます。  
  
 SQL_NULLABLE_UNKNOWN: ドライバーは、列で NULL 値が許可されているかどうかを判断できません。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **SQLDescribeCol**が SQL_ERROR または SQL_SUCCESS_WITH_INFO のいずれかを返す場合、関連付けられた SQLSTATE 値を取得するには、 *Handletype* SQL_HANDLE_STMT と*StatementHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出します。 次の表に、 **SQLDescribeCol** によって一般的に返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データ、右側が切り捨てられました|バッファー \* *ColumnName*が列名全体を返すのに十分な大きさではないため、列名が切り捨てられました。 切り捨てられた列名の長さは **NameLengthPtr*で返されます。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|07005|準備されたステートメントが*カーソル指定*ではありません|*StatementHandle*に関連付けられたステートメントは、結果セットを返しませんでした。 説明する列がありませんでした。|  
|07009|無効な記述子のインデックス|(DM) 引数 *Columnnumber* に指定された値が0で、SQL_ATTR_USE_BOOKMARKS statement オプションが SQL_UB_OFF でした。<br /><br /> 引数 *Columnnumber* に指定された値が、結果セット内の列数を超えています。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続されていたデータソースとの間の通信リンクが失敗しました。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * \* Messagetext*バッファーの**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|*StatementHandle*に対して非同期処理が有効になりました。 関数が呼び出され、実行が完了する前に、 **SQLCancel** または **Sqlcancelhandle** が *StatementHandle*で呼び出されました。 次に、 *StatementHandle*で関数が再度呼び出されました。<br /><br /> 関数が呼び出され、実行が完了する前に、マルチスレッドアプリケーションの別のスレッドの*StatementHandle*で**SQLCancel**または**sqlcancelhandle**が呼び出されました。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、 **SQLDescribeCol** が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または **Sqlmoreresults** が *StatementHandle* に対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。<br /><br /> (DM) 非同期的に実行されている関数 (この1つではない) が *StatementHandle* に対して呼び出され、この関数が呼び出されたときにまだ実行されています。<br /><br /> (DM) 関数は、ステートメントハンドルで **SQLPrepare**、 **sqlexecute**、または catalog 関数を呼び出す前に呼び出されました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **Sqlbulkoperations**、 **SQLSetPos** が *StatementHandle* に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY090|文字列またはバッファーの長さが無効です|(DM) 引数 *Bufferlength* に指定された値が0未満でした。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle* に関連付けられているドライバーでは、関数はサポートされていません。|  
|IM017|非同期通知モードでは、ポーリングは無効になっています|通知モデルが使用されるたびに、ポーリングは無効になります。|  
|IM018|**Sqlcompleteasync** は、このハンドルで前の非同期操作を完了するために呼び出されていません。|ハンドルに対する前の関数呼び出しが SQL_STILL_EXECUTING を返し、通知モードが有効になっている場合は、処理を完了するために、ハンドルに対して **Sqlcompleteasync** を呼び出す必要があります。|  
  
 **SQLDescribeCol**は、ステートメントハンドルに関連付けられている SQL ステートメントがデータソースによって評価されたかどうかに応じて、 **SQLPrepare**または**sqlexecute** **によっ**て返されるすべての**SQLSTATE を返す**ことができます。  
  
 パフォーマンス上の理由から、アプリケーションでは、ステートメントを実行する前に **SQLDescribeCol** を呼び出さないでください。  
  
## <a name="comments"></a>コメント  
 通常、アプリケーションは**SQLPrepare**の呼び出しの後、関連付けられた**sqlexecute**の呼び出しの前または後に**SQLDescribeCol**を呼び出します。 アプリケーションでは、 **SQLExecDirect**の呼び出し後に**SQLDescribeCol**を呼び出すこともできます。 詳細については、「 [結果セットのメタデータ](../../../odbc/reference/develop-app/result-set-metadata.md)」を参照してください。  
  
 **SQLDescribeCol** は、 **SELECT** ステートメントによって生成される列の名前、型、および長さを取得します。 列が式の場合、**ColumnName* は空の文字列またはドライバーで定義された名前のいずれかになります。  
  
> [!NOTE]  
>  Open Group および SQL Access Group 呼び出しレベルのインターフェイスの仕様で **SQLDescribeCol**のオプションが指定されていない場合でも、ODBC では拡張として SQL_NULLABLE_UNKNOWN がサポートされます。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|結果セット内の列へのバッファーのバインド|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|ステートメント処理の取り消し|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|結果セットの列に関する情報を返す|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|複数行のデータのフェッチ|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|結果セットの列数を返す|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|実行するステートメントの準備|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
