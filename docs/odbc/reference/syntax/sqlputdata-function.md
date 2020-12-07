---
description: SQLPutData 関数
title: SQLPutData 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLPutData
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPutData
helpviewer_keywords:
- SQLPutData function [ODBC]
ms.assetid: 9a60f004-1477-4c54-a20c-7378e1116713
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8adda30141a99c1a575d8cc66511f1606e77dcf5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487135"
---
# <a name="sqlputdata-function"></a>SQLPutData 関数
**互換性**  
 導入されたバージョン: ODBC 1.0 標準準拠: ISO 92  
  
 **まとめ**  
 **Sqlputdata** を使用すると、ステートメントの実行時に、アプリケーションからドライバーにパラメーターまたは列のデータを送信できます。 この関数を使用すると、文字、バイナリ、またはデータソース固有のデータ型 (たとえば、SQL_LONGVARBINARY または SQL_LONGVARCHAR 型のパラメーター) を使用して、部分的に文字またはバイナリデータ値を列に送信できます。 **Sqlputdata** は、基になるドライバーが unicode データをサポートしていない場合でも、unicode C データ型へのバインドをサポートします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLPutData(  
      SQLHSTMT     StatementHandle,  
      SQLPOINTER   DataPtr,  
      SQLLEN       StrLen_or_Ind);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル。  
  
 *DataPtr*  
 代入パラメーターまたは列の実際のデータを格納しているバッファーへのポインター。 データは、 **SQLBindParameter**の*ValueType*引数で指定された C データ型 (パラメーターデータの場合) または**SQLBindCol**の*TargetType*引数 (列データの場合) である必要があります。  
  
 *StrLen_or_Ind*  
 代入\* *DataPtr*の長さ。 **Sqlputdata**の呼び出しで送信されるデータの量を指定します。 データの量は、指定されたパラメーターまたは列の呼び出しごとに変化する可能性があります。 *StrLen_or_Ind* は、次のいずれかの条件を満たしている場合を除き、無視されます。  
  
-   *StrLen_or_Ind* は、SQL_NTS、SQL_NULL_DATA、または SQL_DEFAULT_PARAM です。  
  
-   **SQLBindParameter**または**SQLBindCol**で指定された C データ型は、SQL_C_CHAR または SQL_C_BINARY です。  
  
-   C データ型は SQL_C_DEFAULT で、指定された SQL データ型の既定の C データ型は SQL_C_CHAR または SQL_C_BINARY です。  
  
 他のすべての種類の C データでは、 *StrLen_or_Ind*が SQL_NULL_DATA または SQL_DEFAULT_PARAM でない場合、ドライバーは \* *DataPtr*バッファーのサイズが*ValueType*または*TargetType*で指定された C データ型のサイズであると想定し、データ値全体を送信します。 詳細については、「付録 D: データ型」の「 [C から SQL データ型へのデータの変換」を](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) 参照してください。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **Sqlputdata**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合、関連付けられた SQLSTATE 値を取得するには、 *Handletype* SQL_HANDLE_STMT と*StatementHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出します。 次の表に、 **Sqlputdata** によって一般的に返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データ、右側が切り捨てられました|出力パラメーターに対して返された文字列またはバイナリデータにより、空白以外の文字または NULL 以外のバイナリデータが切り捨てられました。 文字列値の場合は、右側が切り捨てられました。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|07006|制限されたデータ型の属性違反|バインドされたパラメーターの**SQLBindParameter**の*ValueType*引数によって識別されるデータ値を、 **SQLBindParameter**の*ParameterType*引数で識別されるデータ型に変換できませんでした。|  
|07S01|既定のパラメーターの使い方が正しくありません|**SQLBindParameter**で設定されたパラメーター値が SQL_DEFAULT_PARAM ましたが、対応するパラメーターに既定値がありませんでした。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続されていたデータソースとの間の通信リンクが失敗しました。|  
|22001|文字列データ、右切り捨て|文字またはバイナリ値が列に割り当てられた結果、空白文字 (文字) または null 以外 (バイナリ) の文字またはバイトが切り捨てられました。<br /><br /> **SQLGetInfo**の SQL_NEED_LONG_DATA_LEN 情報の種類は "Y" であり、長いパラメーター (データ型は SQL_LONGVARCHAR、SQL_LONGVARBINARY、または長いデータソース固有のデータ型) に対して、 **SQLBindParameter**の*StrLen_or_IndPtr*引数で指定されたデータよりも多くのデータが送信されました。<br /><br /> **SQLGetInfo**の SQL_NEED_LONG_DATA_LEN 情報の種類は "Y" で、long 型の列 (データ型は SQL_LONGVARCHAR、SQL_LONGVARBINARY、または長いデータソース固有のデータ型) に対して、 **sqlbulkoperations**で追加または更新されたか、 **SQLSetPos**で更新されたデータ行の列に対応する長さバッファーに指定されたデータ型です。|  
|22003|数値が有効範囲にありません|バインドされた数値パラメーターまたは列に対して送信されたデータにより、関連付けられたテーブル列に割り当てられたときに、数値の一部 (小数部分ではなく) が切り捨てられます。<br /><br /> 1つ以上の入力/出力パラメーターまたは出力パラメーターに対して数値または文字列として数値または文字列として数値を返すと、切り捨てられる数値の一部 (小数部分ではなく) が発生する可能性があります。|  
|22007|無効な datetime 形式|日付、時刻、またはタイムスタンプの構造にバインドされたパラメーターまたは列に対して送信されるデータは、それぞれ無効な日付、時刻、またはタイムスタンプになりました。<br /><br /> 入力/出力パラメーターまたは出力パラメーターが日付、時刻、またはタイムスタンプ C 構造体にバインドされました。返されたパラメーターの値は、それぞれ無効な日付、時刻、またはタイムスタンプです。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|22008|Datetime フィールドオーバーフロー|入力/出力パラメーターまたは出力パラメーターに対して計算された datetime 式で、無効だった日付、時刻、またはタイムスタンプの C 構造体が返されました。|  
|22012|0による除算|入力/出力パラメーターまたは出力パラメーターに対して計算された算術式により、0除算が発生しました。|  
|22015|間隔フィールドオーバーフロー|完全な数値または間隔の列またはパラメーターに対して送信されたデータが interval SQL データ型に対して返されたため、有効桁数が失われました。<br /><br /> 複数のフィールドを含む interval 列またはパラメーターのデータが送信されましたが、数値データ型に変換されましたが、数値データ型には表現がありませんでした。<br /><br /> 列またはパラメーターのデータに送信されたデータは、interval SQL 型に割り当てられていますが、interval SQL 型では C 型の値が表現されていませんでした。<br /><br /> 数値または間隔が C の正確な列またはパラメーターに対して送信されたデータの範囲 C 型に対して、有効桁数の損失が発生しました。<br /><br /> 列またはパラメーターのデータに送信されたデータは、期間 C の構造体に割り当てられており、interval データ構造体にデータは表示されませんでした。|  
|22018|キャストの指定に無効な文字値があります|C 型は、正確な数値、概数、datetime、または interval データ型でした。列の SQL 型は文字データ型でした。また、列またはパラメーターの値が、バインドされた C 型の有効なリテラルではありませんでした。<br /><br /> SQL 型は、正確な数値、概数、datetime、または interval データ型でした。C 型が SQL_C_CHAR でした。また、列またはパラメーターの値が、バインドされた SQL 型の有効なリテラルではありませんでした。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * \* Messagetext*バッファーの**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|*StatementHandle*に対して非同期処理が有効になりました。 関数が呼び出され、実行が完了する前に、 **SQLCancel** または **Sqlcancelhandle** が *StatementHandle*で呼び出されました。 次に、 *StatementHandle*で関数が再度呼び出されました。<br /><br /> 関数が呼び出され、実行が完了する前に、マルチスレッドアプリケーションの別のスレッドの*StatementHandle*で**SQLCancel**または**sqlcancelhandle**が呼び出されました。|  
|HY009|Null ポインターの使い方が正しくありません|(DM) 引数 *DataPtr* が null ポインターであり、 *StrLen_or_Ind* 引数が0、SQL_DEFAULT_PARAM、または SQL_NULL_DATA ではありませんでした。|  
|HY010|関数のシーケンスエラー|(DM) 前の関数呼び出しは **Sqlputdata** または **sqlputdata**への呼び出しではありませんでした。<br /><br /> (DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、SQLPutData 関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または **Sqlmoreresults** が *StatementHandle* に対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。<br /><br /> (DM) 非同期的に実行されている関数 (この1つではない) が *StatementHandle* に対して呼び出され、この関数が呼び出されたときにまだ実行されています。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY019|文字以外のデータおよびバイナリ以外のデータが部分的に送信される|**Sqlputdata** がパラメーターまたは列に対して複数回呼び出されました。このデータは、文字、バイナリ、またはデータソース固有のデータ型の列に文字 c データを送信するために使用されていないか、またはバイナリ c データを文字、バイナリ、またはデータソース固有のデータ型の列に送信していません|  
|HY020|Null 値を連結しようとしました|SQL_NEED_DATA を返した呼び出しと、これらの呼び出しのいずれかで**Sqlputdata**が2回以上呼び出されました。 *StrLen_or_Ind*引数は SQL_NULL_DATA または SQL_DEFAULT_PARAM に含まれていました。|  
|HY090|文字列またはバッファーの長さが無効です|引数 *DataPtr* が null ポインターではなく、引数 *StrLen_or_Ind* が0未満ですが、SQL_NTS または SQL_NULL_DATA と等しくありません。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle* に関連付けられているドライバーでは、関数はサポートされていません。|  
|IM017|非同期通知モードでは、ポーリングは無効になっています|通知モデルが使用されるたびに、ポーリングは無効になります。|  
|IM018|**Sqlcompleteasync** は、このハンドルで前の非同期操作を完了するために呼び出されていません。|ハンドルに対する前の関数呼び出しが SQL_STILL_EXECUTING を返し、通知モードが有効になっている場合は、処理を完了するために、ハンドルに対して **Sqlcompleteasync** を呼び出す必要があります。|  
  
 SQL ステートメントでパラメーターのデータを送信しているときに **Sqlputdata** が呼び出された場合、ステートメントを実行するために呼び出された関数 (**sqlexecute** または **SQLExecDirect**) から返されるすべての SQLSTATE を返すことができます。 **Sqlbulkoperations**で更新または追加された列または**sqlsetpos**で更新されている列のデータの送信中に呼び出された場合は、 **Sqlbulkoperations**または**sqlsetpos**で返すことができる SQLSTATE を返すことができます。  
  
## <a name="comments"></a>コメント  
 **Sqlputdata** を呼び出すと、 **Sqlexecute** または **SQLExecDirect**の呼び出しで使用されるパラメーターデータ、または **sqlputdata** への呼び出しによって行が更新または追加されたとき、または **SQLSetPos**の呼び出しによって更新されたときに使用される列データを、実行時データに渡すことができます。  
  
 アプリケーションが **Sqlparamdata** を呼び出して送信するデータを決定すると、ドライバーは、送信するパラメーターデータまたは列のデータがどこにあるかを判断するためにアプリケーションで使用できるインジケーターを返します。 また、SQL_NEED_DATA も返されます。これは、データを送信するために **Sqlputdata** を呼び出す必要があることをアプリケーションに示すインジケーターです。 **Sqlputdata**の*DataPtr*引数には、パラメーターまたは列の実際のデータを格納しているバッファーへのポインターが渡されます。  
  
 ドライバーが **Sqlputdata**の SQL_SUCCESS を返すと、アプリケーションは **sqlputdata** を再度呼び出します。 **Sqlparamdata** は、より多くのデータを送信する必要がある場合に SQL_NEED_DATA を返します。この場合、アプリケーションは **sqlparamdata** を再度呼び出します。 実行時データのすべてのデータが送信された場合は、SQL_SUCCESS を返します。 次に、アプリケーションは **Sqlparamdata** を再度呼び出します。 ドライバーが SQL_NEED_DATA と* \* valueptrptr*内の別のインジケーターを返した場合、別のパラメーターまたは列のデータが必要であり、 **sqlputdata**が再度呼び出されます。 ドライバーが SQL_SUCCESS を返す場合は、実行時データのすべてのデータが送信され、SQL ステートメントを実行するか、 **Sqlbulkoperations** または **SQLSetPos** の呼び出しを処理できます。  
  
 ステートメントの実行時に実行時データパラメーターのデータを渡す方法の詳細については、「 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) 」の「パラメーター値の引き渡し」と「 [長い形式のデータの送信](../../../odbc/reference/develop-app/sending-long-data.md)」を参照してください。 実行時データ列のデータを更新または追加する方法の詳細については、「 [sqlsetpos](../../../odbc/reference/syntax/sqlsetpos-function.md)での Sqlsetpos の使用」、「 [sqlbulkoperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)」の「ブックマークを使用した一括更新の実行」、および「Long Data」と「SQLSetPos」および「 [sqlbulkoperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)」を参照してください。  
  
> [!NOTE]  
>  アプリケーションでは、文字、バイナリ、またはデータソース固有のデータ型の列に文字 C データを送信する場合、または文字、バイナリ、またはデータソース固有のデータ型を持つ列にバイナリ C データを送信する場合にのみ、 **Sqlputdata** を使用してデータを部分的に送信できます。 **Sqlputdata**がその他の条件の下で複数回呼び出された場合、SQL_ERROR と SQLSTATE HY019 (非文字およびバイナリ以外のデータが部分的に送信されます) が返されます。  
  
## <a name="example"></a>例  
 次の例では、Test というデータソース名を前提としています。 関連付けられたデータベースには、次のように作成できるテーブルが必要です。  
  
```sql  
CREATE TABLE emp4 (NAME char(30), AGE int, BIRTHDAY datetime, Memo1 text)  
```  
  
```cpp  
// SQLPutData.cpp  
// compile with: odbc32.lib user32.lib  
#include <stdio.h>  
#include <windows.h>  
#include <sqlext.h>  
#include <odbcss.h>  
  
#define TEXTSIZE  12000  
#define MAXBUFLEN 256  
  
SQLHENV henv = SQL_NULL_HENV;  
SQLHDBC hdbc1 = SQL_NULL_HDBC;       
SQLHSTMT hstmt1 = SQL_NULL_HSTMT;  
  
void Cleanup() {  
   if (hstmt1 != SQL_NULL_HSTMT)  
      SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
  
   if (hdbc1 != SQL_NULL_HDBC) {  
      SQLDisconnect(hdbc1);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   }  
  
   if (henv != SQL_NULL_HENV)  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
  
int main() {  
   RETCODE retcode;  
  
   // SQLBindParameter variables.  
   SQLLEN cbTextSize, lbytes;  
  
   // SQLParamData variable.  
   PTR pParmID;  
  
   // SQLPutData variables.  
   UCHAR  Data[] =   
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyz";  
  
   SDWORD cbBatch = (SDWORD)sizeof(Data) - 1;  
  
   // Allocate the ODBC environment and save handle.  
   retcode = SQLAllocHandle (SQL_HANDLE_ENV, NULL, &henv);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(Env) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Notify ODBC that this is an ODBC 3.0 app.  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetEnvAttr(ODBC version) Failed\n\n");  
      Cleanup();  
      return(9);      
   }  
  
   // Allocate ODBC connection handle and connect.  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Sample uses Integrated Security, create SQL Server DSN using Windows NT authentication.   
   retcode = SQLConnect(hdbc1, (UCHAR*)"Test", SQL_NTS, (UCHAR*)"",SQL_NTS, (UCHAR*)"", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Allocate statement handle.  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLAllocHandle(hstmt1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Set parameters based on total data to send.  
   lbytes = (SDWORD)TEXTSIZE;  
   cbTextSize = SQL_LEN_DATA_AT_EXEC(lbytes);  
  
   // Bind the parameter marker.  
   retcode = SQLBindParameter (hstmt1,           // hstmt  
                               1,                // ipar  
                               SQL_PARAM_INPUT,  // fParamType  
                               SQL_C_CHAR,       // fCType  
                               SQL_LONGVARCHAR,  // FSqlType  
                               lbytes,           // cbColDef  
                               0,                // ibScale  
                               (VOID *)1,        // rgbValue  
                               0,                // cbValueMax  
                               &cbTextSize);     // pcbValue  
  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLBindParameter Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Execute the command.  
   retcode =   
      SQLExecDirect(hstmt1, (UCHAR*)"INSERT INTO emp4 VALUES('Paul Borm', 46,'1950-11-12 00:00:00', ?)", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_NEED_DATA) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLExecDirect Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Check to see if NEED_DATA; if yes, use SQLPutData.  
   retcode = SQLParamData(hstmt1, &pParmID);  
   if (retcode == SQL_NEED_DATA) {  
      while (lbytes > cbBatch) {  
         SQLPutData(hstmt1, Data, cbBatch);  
         lbytes -= cbBatch;  
      }  
      // Put final batch.  
      retcode = SQLPutData(hstmt1, Data, lbytes);   
   }  
  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLParamData Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Make final SQLParamData call.  
   retcode = SQLParamData(hstmt1, &pParmID);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("Final SQLParamData Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Clean up.  
   SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|バッファーをパラメーターにバインドする|[SQLBindParameter 関数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|ステートメント処理の取り消し|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|SQL ステートメントの実行|[SQLExecDirect 関数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|準備された SQL ステートメントの実行|[SQLExecute 関数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|データを送信する次のパラメーターを返す|[SQLParamData 関数](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
