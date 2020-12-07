---
description: SQLGetDescRec 関数
title: SQLGetDescRec 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDescRec
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDescRec
helpviewer_keywords:
- SQLGetDescRec function [ODBC]
ms.assetid: 325e0907-8e87-44e8-a111-f39e636a9cbc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5237d8b1a1d070752219abd22936615060371a89
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461052"
---
# <a name="sqlgetdescrec-function"></a>SQLGetDescRec 関数
**互換性**  
 導入されたバージョン: ODBC 3.0 標準準拠: ISO 92  
  
 **まとめ**  
 **Sqlgetdescrec** は、記述子レコードの複数のフィールドの現在の設定または値を返します。 返されるフィールドには、列またはパラメーターデータの名前、データ型、およびストレージが記述されています。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLGetDescRec(  
      SQLHDESC        DescriptorHandle,  
      SQLSMALLINT     RecNumber,  
      SQLCHAR *       Name,  
      SQLSMALLINT     BufferLength,  
      SQLSMALLINT *   StringLengthPtr,  
      SQLSMALLINT *   TypePtr,  
      SQLSMALLINT *   SubTypePtr,  
      SQLLEN *        LengthPtr,  
      SQLSMALLINT *   PrecisionPtr,  
      SQLSMALLINT *   ScalePtr,  
      SQLSMALLINT *   NullablePtr);  
```  
  
## <a name="arguments"></a>引数  
 *DescriptorHandle*  
 代入記述子ハンドル。  
  
 *RecNumber*  
 代入アプリケーションが情報をシークする記述子レコードを示します。 記述子レコードは1から番号が付けられ、レコード番号0はブックマークレコードです。 *Recnumber*引数は SQL_DESC_COUNT の値以下である必要があります。 *Recnumber*が SQL_DESC_COUNT 以下で、行に列またはパラメーターのデータが含まれていない場合、 **Sqlgetdescrec**を呼び出すと、フィールドの既定値が返されます。 (詳細については、 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)の「記述子フィールドの初期化」を参照してください)。  
  
 *名前*  
 Output記述子レコードの SQL_DESC_NAME フィールドを返すバッファーへのポインター。  
  
 *Name*が NULL の場合でも、 *stringlength Ptr*は、*名前*で指定されたバッファー内で返すことができる文字の合計数 (文字データの null 終端文字を除く) を返します。  
  
 *BufferLength*  
 代入**名前* バッファーの長さ (文字数)。  
  
 *Stringlength Ptr*  
 Output名前バッファーで返すことができるデータの文字数を返すバッファーへのポインター \* *Name* 。 null 終了文字は除きます。 文字数が*Bufferlength*以上の場合、名前に含まれるデータは、 \* *Name* *bufferlength*から null 終端文字の長さを引いた値に切り捨てられ、ドライバーによって null で終了されます。  
  
 *TypePtr*  
 Output記述子レコードの SQL_DESC_TYPE フィールドの値を返すバッファーを指すポインターです。  
  
 *SubTypePtr*  
 Output型が SQL_DATETIME または SQL_INTERVAL であるレコードの場合、これは SQL_DESC_DATETIME_INTERVAL_CODE フィールドの値を返すバッファーへのポインターです。  
  
 *Length Ptr*  
 Output記述子レコードの SQL_DESC_OCTET_LENGTH フィールドの値を返すバッファーを指すポインターです。  
  
 *PrecisionPtr*  
 Output記述子レコードの SQL_DESC_PRECISION フィールドの値を返すバッファーを指すポインターです。  
  
 *ScalePtr*  
 Output記述子レコードの SQL_DESC_SCALE フィールドの値を返すバッファーを指すポインターです。  
  
 *NullablePtr*  
 Output記述子レコードの SQL_DESC_NULLABLE フィールドの値を返すバッファーを指すポインターです。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_NO_DATA、または SQL_INVALID_HANDLE。  
  
 *Recnumber*が現在の記述子レコードの数より大きい場合、SQL_NO_DATA が返されます。  
  
 SQL_NO_DATA が返されるのは、 *記述子ハンドル* が IRD ハンドルで、ステートメントが prepared または実行状態であるが、開いているカーソルが関連付けられていない場合です。  
  
## <a name="diagnostics"></a>診断  
 **Sqlgetdescrec**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返した場合、関連付けられた SQLSTATE 値を取得するには、 *handletype*が SQL_HANDLE_DESC であり、*記述子ハンドル*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出します。 次の表に、 **Sqlgetdescrec** によって通常返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データ、右側が切り捨てられました|バッファー \* *名*が、記述子フィールド全体を返すのに十分な大きさではありませんでした。 このため、フィールドは切り捨てられました。 切り詰められていない記述子フィールドの長さは、**Stringlength ptr*で返されます。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|07009|無効な記述子のインデックス|*FieldIdentifier*引数がレコードフィールドで、 *recnumber*引数が0に設定され、*記述子ハンドル*引数が IPD ハンドルでした。<br /><br /> (DM) *Recnumber* 引数が0に設定され、SQL_ATTR_USE_BOOKMARKS statement 属性が SQL_UB_OFF に設定されました。また、 *記述子 HANDLE* 引数は IRD ハンドルでした。<br /><br /> *Recnumber*引数が0未満でした。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続されていたデータソースとの間の通信リンクが失敗しました。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * \* Messagetext*バッファーの**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY007|関連付けられたステートメントは準備されていません|*記述子ハンドル* は IRD に関連付けられていましたが、関連付けられたステートメントハンドルは準備状態または実行済み状態ではありませんでした。|  
|HY010|関数のシーケンスエラー|(DM) *記述子ハンドル* が、この関数が呼び出されたときに非同期的に実行されている関数 (この関数ではない) が呼び出された *StatementHandle* に関連付けられました。<br /><br /> (DM)*記述子ハンドル*は、 **sqlexecute**、 **SQLExecDirect**、 **sqlbulkoperations**、または**SQLSetPos**が呼び出され SQL_NEED_DATA 返された*StatementHandle*に関連付けられました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。<br /><br /> (DM) 実行中の非同期関数が、 *記述子ハンドル*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、 **Sqlgetdescrec** が呼び出されたときにまだ実行されていました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *記述子ハンドル* に関連付けられているドライバーでは、関数はサポートされていません。|  
  
## <a name="comments"></a>コメント  
 アプリケーションは **Sqlgetdescrec** を呼び出して、1つの列またはパラメーターに対して次の記述子フィールドの値を取得できます。  
  
-   SQL_DESC_NAME  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE (種類が SQL_DATETIME または SQL_INTERVAL であるレコードの場合)  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_NULLABLE  
  
 **Sqlgetdescrec** は、ヘッダーフィールドの値を取得しません。  
  
 アプリケーションでは、フィールドに対応する引数を null ポインターに設定することによって、フィールドの設定が返されないようにすることができます。  
  
 アプリケーションが **Sqlgetdescrec** を呼び出して、特定の記述子の種類に対して定義されていないフィールドの値を取得する場合、関数は SQL_SUCCESS を返しますが、フィールドに返される値は定義されていません。 たとえば、APD またはの SQL_DESC_NAME または SQL_DESC_NULLABLE フィールドに対して **Sqlgetdescrec** を呼び出すと、SQL_SUCCESS が返されますが、フィールドの値は未定義になります。  
  
 アプリケーションが **Sqlgetdescrec** を呼び出して特定の記述子の種類に対して定義されているフィールドの値を取得するときに、既定値を持たず、まだ設定されていない場合、関数は SQL_SUCCESS を返しますが、フィールドに返される値は未定義です。 詳細については、「 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)」の「記述子フィールドの初期化」を参照してください。  
  
 フィールドの値は、 **SQLGetDescField**を呼び出すことによって個別に取得することもできます。 記述子ヘッダーまたはレコード内のフィールドの説明については、「 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)」を参照してください。 記述子の詳細については、「 [記述子](../../../odbc/reference/develop-app/descriptors.md)」を参照してください。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|列のバインド|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|パラメーターのバインド|[SQLBindParameter 関数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|記述子フィールドを取得する|[SQLGetDescField 関数](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|複数の記述子フィールドの設定|[SQLSetDescRec 関数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
