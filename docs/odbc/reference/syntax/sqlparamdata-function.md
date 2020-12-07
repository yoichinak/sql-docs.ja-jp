---
description: SQLParamData 関数
title: SQLParamData 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLParamData
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLParamData
helpviewer_keywords:
- SQLParamData function [ODBC]
ms.assetid: 68fe010d-9539-4e5b-a260-c8d32423b1db
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d44b3bd5017e5ef5cebb40c9bbbaccdde7368bbf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487255"
---
# <a name="sqlparamdata-function"></a>SQLParamData 関数
**互換性**  
 導入されたバージョン: ODBC 1.0 標準準拠: ISO 92  
  
 **まとめ**  
 **Sqlparamdata** を **sqlparamdata** と共に使用して、ステートメントの実行時にパラメーターデータを指定し、 **SQLGetData** を使用してストリーム出力パラメーターデータを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLParamData(  
     SQLHSTMT       StatementHandle,  
     SQLPOINTER *   ValuePtrPtr);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル。  
  
 *ValuePtrPtr*  
 Output**SQLBindParameter**に指定された*parametervalueptr*バッファーのアドレス (パラメーターデータの場合) または**SQLBindCol**で指定された*targetvalueptr*バッファーのアドレス (列データの場合) を返すバッファーへのポインター。これは、SQL_DESC_DATA_PTR 記述子レコードフィールドに含まれます。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NEED_DATA、SQL_NO_DATA、SQL_STILL_EXECUTING、SQL_ERROR、SQL_INVALID_HANDLE、SQL_PARAM_DATA_AVAILABLE。  
  
## <a name="diagnostics"></a>診断  
 **Sqlparamdata**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合、関連付けられた SQLSTATE 値を取得するには、 *Handletype* SQL_HANDLE_STMT と*StatementHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出します。 次の表に、 **Sqlparamdata** によって通常返される SQLSTATE 値と、この関数のコンテキストでのそれぞれについて説明します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|07006|制限されたデータ型の属性違反|バインドされたパラメーターの**SQLBindParameter**の*ValueType*引数によって識別されるデータ値を、 **SQLBindParameter**の*ParameterType*引数で識別されるデータ型に変換できませんでした。<br /><br /> SQL_PARAM_INPUT_OUTPUT または SQL_PARAM_OUTPUT としてバインドされたパラメーターに対して返されたデータ値を、 **SQLBindParameter**の*ValueType*引数で識別されるデータ型に変換できませんでした。<br /><br /> (1 つ以上の行のデータ値を変換できなかったが、1つ以上の行が正常に返された場合、この関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続されていたデータソースとの間の通信リンクが失敗しました。|  
|22026|文字列データの長さが合致しません|**SQLGetInfo**の SQL_NEED_LONG_DATA_LEN 情報の種類は "Y" であり、long 型パラメーター (データ型は SQL_LONGVARCHAR、SQL_LONGVARBINARY、または長いデータソース固有のデータ型) に対して送信されたデータの量が、 **SQLBindParameter**の*StrLen_or_IndPtr*引数で指定された値を超えています。<br /><br /> **SQLGetInfo**の SQL_NEED_LONG_DATA_LEN 情報の種類は "Y" で、long 型の列 (データ型は SQL_LONGVARCHAR、SQL_LONGVARBINARY、または長いデータソース固有のデータ型) に対して送信されたデータの数が、 **sqlbulkoperations**で追加または更新されたか、 **SQLSetPos**で更新されたデータ行の列に対応する長さのバッファーに指定された|  
|40001|シリアル化エラー|別のトランザクションでリソースのデッドロックが発生したため、トランザクションがロールバックされました。|  
|40003|ステートメントの完了が不明です|この関数の実行中に関連付けられた接続に失敗しました。トランザクションの状態を確認できません。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * \* Messagetext*バッファーの**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|*StatementHandle*に対して非同期処理が有効になりました。 関数が呼び出され、実行が完了する前に、 **SQLCancel** または **Sqlcancelhandle** が *StatementHandle*で呼び出されました。次に、関数が *StatementHandle*で再び呼び出されます。<br /><br /> 関数が呼び出され、実行が完了する前に、マルチスレッドアプリケーションの別のスレッドの*StatementHandle*で**SQLCancel**または**sqlcancelhandle**が呼び出されました。|  
|HY010|関数のシーケンスエラー|(DM) 前の関数呼び出しは、リターンコードが SQL_NEED_DATA されているか、前の関数呼び出しが**Sqlputdata**への呼び出しであった**SQLExecDirect**、 **sqlexecute**、 **sqlbulkoperations**、 **SQLSetPos**の呼び出しではありませんでした。<br /><br /> 前の関数呼び出しは **Sqlparamdata**の呼び出しでした。<br /><br /> (DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、 **Sqlparamdata** 関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) 非同期的に実行されている関数 (この1つではない) が *StatementHandle* に対して呼び出され、この関数が呼び出されたときにまだ実行されています。<br /><br /> **Sqlexecute**、 **SQLExecDirect**、 **Sqlbulkoperations**、または **SQLSetPos** が *StatementHandle* に対して呼び出され、SQL_NEED_DATA が返されました。 **SQLCancel** は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle* に対応するドライバーでは、関数はサポートされていません。|  
|IM017|非同期通知モードでは、ポーリングは無効になっています|通知モデルが使用されるたびに、ポーリングは無効になります。|  
|IM018|**Sqlcompleteasync** は、このハンドルで前の非同期操作を完了するために呼び出されていません。|ハンドルに対する前の関数呼び出しが SQL_STILL_EXECUTING を返し、通知モードが有効になっている場合は、処理を完了するために、ハンドルに対して **Sqlcompleteasync** を呼び出す必要があります。|  
  
 SQL ステートメントでパラメーターのデータを送信しているときに **Sqlparamdata** が呼び出されると、ステートメントを実行するために呼び出された関数 (**Sqlexecute** または **SQLExecDirect**) から返されるすべての SQLSTATE を返すことができます。 **Sqlbulkoperations**で更新または追加された列または**sqlsetpos**で更新されている列のデータの送信中に呼び出された場合は、 **Sqlbulkoperations**または**sqlsetpos**で返すことができる SQLSTATE を返すことができます。  
  
## <a name="comments"></a>コメント  
 **Sqlparamdata** を呼び出すと、 **Sqlexecute** または **SQLExecDirect**の呼び出しで使用されるパラメーターデータ、または **sqlparamdata** への呼び出しによって行が更新または追加されたとき、または **SQLSetPos**の呼び出しによって更新されるときに使用される列データを指定できます。 実行時に、 **Sqlparamdata** は、ドライバーが必要とするデータを示すインジケーターをアプリケーションに返します。  
  
 アプリケーションが **Sqlexecute**、 **SQLExecDirect**、 **sqlbulkoperations**、または **SQLSetPos**を呼び出すと、ドライバーは実行時データのデータが必要な場合に SQL_NEED_DATA を返します。 次に、アプリケーションは **Sqlparamdata** を呼び出して、送信するデータを決定します。 ドライバーがパラメーターデータを必要とする場合、ドライバーは、アプリケーションが行セットバッファーに格納した値を* \* valueptrptr*出力バッファーに返します。 アプリケーションはこの値を使用して、ドライバーが要求しているパラメーターデータを判断できます。 ドライバーが列データを必要とする場合、ドライバーは、次のように、列が最初にバインドされたアドレスを* \* valueptrptr*バッファーに返します。  
  
 *バインド*されたアドレス  + *バインドオフセット*+ ((*行番号*-1) x*要素サイズ*)  
  
 ここでは、変数が次の表に示すように定義されています。  
  
|変数|説明|  
|--------------|-----------------|  
|*バインドされたアドレス*|**SQLBindCol**の*targetvalueptr*引数で指定されたアドレス。|  
|*バインドオフセット*|SQL_ATTR_ROW_BIND_OFFSET_PTR statement 属性で指定したアドレスに格納されている値。|  
|*行番号*|行セット内の行の1から始まる番号。 単一行フェッチ (既定値) の場合、これは1です。|  
|*要素のサイズ*|データと長さ/インジケーターバッファーの両方に対する SQL_ATTR_ROW_BIND_TYPE statement 属性の値。|  
  
 また、SQL_NEED_DATA も返されます。これは、データを送信するために **Sqlputdata** を呼び出す必要があることをアプリケーションに示すインジケーターです。  
  
 アプリケーションは、列またはパラメーターの実行時データデータを送信するために必要な回数だけ **Sqlputdata** を呼び出します。 列またはパラメーターのすべてのデータが送信されると、アプリケーションは **Sqlparamdata** を再度呼び出します。 **Sqlparamdata**が再度 SQL_NEED_DATA を返した場合は、別のパラメーターまたは列に対してデータを送信する必要があります。 そのため、アプリケーションは **Sqlputdata**を再び呼び出します。 すべてのパラメーターまたは列に対して実行中のデータがすべて送信された場合、 **Sqlparamdata**は SQL_SUCCESS または SQL_SUCCESS_WITH_INFO を返します。 * \* valueptrptr*の値は未定義であり、SQL ステートメントを実行するか、 **sqlparamdata**または**SQLSetPos**呼び出しを処理できます。  
  
 **Sqlparamdata**によって、データソースの行に影響を与えない、検索された update ステートメントまたは delete ステートメントのパラメーターデータが渡された場合、 **sqlparamdata**を呼び出すと SQL_NO_DATA が返されます。  
  
 ステートメントの実行時に実行時データパラメーターのデータを渡す方法の詳細については、「 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) 」の「パラメーター値の引き渡し」と「 [長い形式のデータの送信](../../../odbc/reference/develop-app/sending-long-data.md)」を参照してください。 実行時データ列のデータを更新または追加する方法の詳細については、「 [sqlsetpos](../../../odbc/reference/syntax/sqlsetpos-function.md)での Sqlsetpos の使用」、「 [sqlbulkoperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)」の「ブックマークを使用した一括更新の実行」、および「Long Data」と「SQLSetPos」および「 [sqlbulkoperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)」を参照してください。  
  
 **Sqlparamdata** を呼び出して、ストリーム出力パラメーターを取得できます。 **Sqlmoreresults**、 **sqlexecute**、 **SQLGetData**、または**SQLExecDirect**が SQL_PARAM_DATA_AVAILABLE を返す場合は、 **sqlparamdata**を呼び出して、使用可能な値を持つパラメーターを特定します。 SQL_PARAM_DATA_AVAILABLE およびストリーム出力パラメーターの詳細については、「 [SQLGetData を使用した出力パラメーターの取得](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)」を参照してください。  
  
## <a name="code-example"></a>コード例  
 「 [Sqlputdata](../../../odbc/reference/syntax/sqlputdata-function.md)」を参照してください。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|バッファーをパラメーターにバインドする|[SQLBindParameter 関数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|ステートメント処理の取り消し|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|ステートメント内のパラメーターに関する情報を返す|[SQLDescribeParam 関数](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|SQL ステートメントの実行|[SQLExecDirect 関数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|準備された SQL ステートメントの実行|[SQLExecute 関数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|実行時にパラメーターデータを送信する|[SQLPutData 関数](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダーファイル](../../../odbc/reference/install/odbc-header-files.md)   
 [SQLGetData を使用した出力パラメーターの取得](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
