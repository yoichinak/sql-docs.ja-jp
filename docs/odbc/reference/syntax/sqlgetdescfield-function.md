---
description: SQLGetDescField 関数
title: SQLGetDescField 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDescField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDescField
helpviewer_keywords:
- SQLGetDescField function [ODBC]
ms.assetid: f09ff660-1e4a-4370-be85-90d4da0487d3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31618ca5283ae6875cb4243cc88e643452cef4d1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461068"
---
# <a name="sqlgetdescfield-function"></a>SQLGetDescField 関数
**互換性**  
 導入されたバージョン: ODBC 3.0 標準準拠: ISO 92  
  
 **まとめ**  
 **SQLGetDescField** は、記述子レコードの1つのフィールドの現在の設定または値を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLGetDescField(  
     SQLHDESC        DescriptorHandle,  
     SQLSMALLINT     RecNumber,  
     SQLSMALLINT     FieldIdentifier,  
     SQLPOINTER      ValuePtr,  
     SQLINTEGER      BufferLength,  
     SQLINTEGER *    StringLengthPtr);  
```  
  
## <a name="arguments"></a>引数  
 *DescriptorHandle*  
 代入記述子ハンドル。  
  
 *RecNumber*  
 代入アプリケーションが情報をシークする記述子レコードを示します。 記述子レコードは0から番号が付けられ、レコード番号0はブックマークレコードになります。 *FieldIdentifier*引数がヘッダーフィールドを示す場合、 *recnumber*は無視されます。 *Recnumber*が SQL_DESC_COUNT 以下で、行に列またはパラメーターのデータが含まれていない場合、 **SQLGetDescField**を呼び出すと、フィールドの既定値が返されます。 (詳細については、 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)の「記述子フィールドの初期化」を参照してください)。  
  
 *FieldIdentifier*  
 代入値が返される記述子のフィールドを示します。 詳細については、 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)の「*FieldIdentifier*引数」セクションを参照してください。  
  
 *ValuePtr*  
 Output記述子情報を返すバッファーへのポインター。 データ型は、 *FieldIdentifier*の値によって異なります。  
  
 *Valueptr*が整数型の場合、アプリケーションは SQLULEN のバッファーを使用し、この関数を呼び出す前に値を0に初期化する必要があります。一部のドライバーでは、バッファーの下位の32ビットまたは16ビットのみが書き込まれ、上位ビットは変更されないためです。  
  
 *Valueptr*が NULL の場合でも、 *stringlength Ptr*は、 *valueptr*が指すバッファー内で返されるバイトの合計数 (文字データの NULL 終端文字を除く) を返します。  
  
 *BufferLength*  
 代入*FieldIdentifier*が ODBC で定義されたフィールドであり、 *valueptr*が文字列またはバイナリバッファーを指している場合、この引数は \* *valueptr*の長さである必要があります。 *FieldIdentifier*が ODBC で定義されたフィールドであり、 \* *valueptr*が整数の場合、 *bufferlength*は無視されます。 * \* Valueptr*の値が Unicode データ型の場合 ( **SQLGetDescFieldW**を呼び出す場合)、 *bufferlength*引数は偶数である必要があります。  
  
 *FieldIdentifier*がドライバーによって定義されたフィールドである場合、アプリケーションは、 *bufferlength*引数を設定することによって、ドライバーマネージャーに対してフィールドの性質を示します。 *Bufferlength* には次の値を指定できます。  
  
-   * \* Valueptr*が文字列へのポインターである場合、 *bufferlength*は文字列または SQL_NTS の長さになります。  
  
-   * \* Valueptr*がバイナリバッファーへのポインターである場合、アプリケーションは、SQL_LEN_BINARY_ATTR (*長さ*) マクロの結果を*bufferlength*に配置します。 これにより、 *Bufferlength*に負の値が挿入されます。  
  
-   * \* Valueptr*が文字列またはバイナリ文字列以外の値へのポインターである場合、 *bufferlength*には SQL_IS_POINTER 値を指定する必要があります。  
  
-   * \* Valueptr*に固定長データ型が含まれている場合、 *bufferlength*は、必要に応じて SQL_IS_INTEGER、SQL_IS_UINTEGER、SQL_IS_SMALLINT、SQL_IS_USMALLINT のいずれかになります。  
  
 *Stringlength Ptr*  
 Output**Valueptr*で返すことができるバイト数の合計 (null 終端文字に必要なバイト数を除く) を返すバッファーへのポインター。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_NO_DATA、または SQL_INVALID_HANDLE。  
  
 *Recnumber*が現在の記述子レコードの数より大きい場合、SQL_NO_DATA が返されます。  
  
 SQL_NO_DATA が返されるのは、 *記述子ハンドル* が IRD ハンドルで、ステートメントが prepared または実行状態であるが、開いているカーソルが関連付けられていない場合です。  
  
## <a name="diagnostics"></a>診断  
 **SQLGetDescField**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合、関連付けられた SQLSTATE 値を取得するには、 *Handletype* SQL_HANDLE_STMT と*StatementHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出します。 次の表に、 **SQLGetDescField** によって一般的に返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データ、右側が切り捨てられました|バッファー \* *valueptr*は、記述子フィールド全体を返すのに十分な大きさではなかったため、フィールドは切り捨てられました。 切り詰められていない記述子フィールドの長さは、**Stringlength ptr*で返されます。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|07009|無効な記述子のインデックス|(DM) *Recnumber* 引数が0、SQL_ATTR_USE_BOOKMARK statement 属性が SQL_UB_OFF、および *記述子 HANDLE* 引数が IRD ハンドルでした。 (このエラーは、記述子がステートメントハンドルに関連付けられている場合にのみ、明示的に割り当てられた記述子に対して返されます)。<br /><br /> *FieldIdentifier*引数がレコードフィールドで、 *recnumber*引数が0で、*記述子ハンドル*引数が IPD ハンドルでした。<br /><br /> *Recnumber*引数が0未満でした。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続されていたデータソースとの間の通信リンクが失敗しました。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * \* Messagetext*バッファーの**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY007|関連付けられたステートメントは準備されていません|*記述子ハンドル* が IRD として *StatementHandle* に関連付けられましたが、関連付けられているステートメントハンドルは準備されていないか、実行されていません。|  
|HY010|関数のシーケンスエラー|(DM) *記述子ハンドル* が、この関数が呼び出されたときに非同期的に実行されている関数 (この関数ではない) が呼び出された *StatementHandle* に関連付けられました。<br /><br /> (DM)*記述子ハンドル*は、 **sqlexecute**、 **SQLExecDirect**、 **sqlbulkoperations**、または**SQLSetPos**が呼び出され SQL_NEED_DATA 返された*StatementHandle*に関連付けられました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。<br /><br /> (DM) 実行中の非同期関数が、 *記述子ハンドル*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、 **SQLGetDescField** 関数が呼び出されたときにまだ実行されていました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY021|不整合な記述子情報|SQL_DESC_TYPE フィールドと SQL_DESC_DATETIME_INTERVAL_CODE フィールドは、有効な ODBC SQL 型、有効なドライバー固有の SQL 型 (IPDs の場合)、または有効な ODBC C 型 (APDs または ARDs の場合) を形成しません。|  
|HY090|文字列またはバッファーの長さが無効です|(DM) * \* valueptr*が文字列であり、 *bufferlength*が0未満でした。|  
|HY091|無効な記述子フィールド識別子|*FieldIdentifier* は ODBC で定義されたフィールドではなく、実装定義の値ではありませんでした。<br /><br /> *FieldIdentifier* は、 *記述子ハンドル*に対して定義されていません。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *記述子ハンドル* に関連付けられているドライバーでは、関数はサポートされていません。|  
  
## <a name="comments"></a>コメント  
 アプリケーションは、 **SQLGetDescField** を呼び出して、記述子レコードの1つのフィールドの値を返すことができます。 **SQLGetDescField**を呼び出すと、ヘッダーフィールド、レコードフィールド、ブックマークフィールドなど、任意の記述子の種類の任意のフィールドの設定を返すことができます。 アプリケーションでは、 **SQLGetDescField**を繰り返し呼び出すことによって、同じまたは別の記述子内の複数のフィールドの設定を任意の順序で取得できます。 **SQLGetDescField** を呼び出して、ドライバー定義の記述子フィールドを返すこともできます。  
  
 パフォーマンス上の理由から、アプリケーションでは、ステートメントを実行する前に、IRD の **SQLGetDescField** を呼び出さないでください。  
  
 列またはパラメーターのデータの名前、データ型、および格納方法を記述する複数のフィールドの設定も、 **Sqlgetdescrec**の1回の呼び出しで取得できます。 **SQLGetStmtAttr** を呼び出すと、ステートメント属性でもある記述子ヘッダー内の1つのフィールドの設定を返すことができます。 **Sqlcolattribute**、 **SQLDescribeCol**、および **SQLDescribeParam** は、レコードまたはブックマークフィールドを返します。  
  
 アプリケーションが **SQLGetDescField** を呼び出して、特定の記述子の種類に対して定義されていないフィールドの値を取得する場合、関数は SQL_SUCCESS を返しますが、フィールドに返される値は定義されていません。 たとえば、APD または **SQLGetDescField** の SQL_DESC_NAME または SQL_DESC_NULLABLE フィールドに対してを呼び出すと、SQL_SUCCESS が返されますが、フィールドの値は未定義になります。  
  
 アプリケーションが **SQLGetDescField** を呼び出して、特定の記述子の種類に対して定義されているフィールドの値を取得するときに、既定値を持たず、まだ設定されていない場合、この関数は SQL_SUCCESS を返しますが、フィールドに返される値は未定義です。 記述子フィールドの初期化とフィールドの説明の詳細については、 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)の「記述子フィールドの初期化」を参照してください。 記述子の詳細については、「 [記述子](../../../odbc/reference/develop-app/descriptors.md)」を参照してください。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|複数の記述子フィールドの取得|[SQLGetDescRec 関数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|1つの記述子フィールドの設定|[SQLSetDescField 関数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|複数の記述子フィールドの設定|[SQLSetDescRec 関数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
