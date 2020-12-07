---
description: SQLCancel 関数
title: SQLCancel 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCancel
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLCancel
helpviewer_keywords:
- SQLCancel function [ODBC]
ms.assetid: ac0b5972-627f-4440-8c5a-0e8da728726d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 040cd9034a8f754a26f577b7efd6e1307e4c90c5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448874"
---
# <a name="sqlcancel-function"></a>SQLCancel 関数
**互換性**  
 導入されたバージョン: ODBC 1.0 標準準拠: ISO 92  
  
 **まとめ**  
 **SQLCancel** は、ステートメントの処理を取り消します。  
  
 接続またはステートメントの処理を取り消すには、 [Sqlcancelhandle 関数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)を使用します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLCancel(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **SQLCancel**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合、関連付けられた SQLSTATE 値を取得するには、 *Handletype* SQL_HANDLE_STMT と*StatementHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出します。 次の表に、 **SQLCancel** によって一般的に返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)によって返されるエラーメッセージに* \* *は、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、 **SQLCancel** 関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) *StatementHandle*に関連付けられている接続ハンドルで非同期操作が進行中のため、操作を取り消すことができませんでした。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY018|サーバー拒否のキャンセル要求|サーバーがキャンセル要求を拒否しました。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle* に関連付けられているドライバーでは、関数はサポートされていません。|  
  
## <a name="comments"></a>コメント  
 **SQLCancel** は、ステートメントで次の種類の処理を取り消すことができます。  
  
-   ステートメントで非同期に実行されている関数。  
  
-   データを必要とするステートメントの関数。  
  
-   別のスレッドのステートメントで実行されている関数。  
  
 ODBC 2 の場合。*x*: ステートメントで処理が実行されていないときにアプリケーションが **SQLCancel** を呼び出した場合、 **SQLCancel** は、SQL_CLOSE オプションを指定した **SQLFreeStmt** と同じ効果を持ちます。この動作は、完全な場合にのみ定義され、アプリケーションは **SQLFreeStmt** または **sqlcloを** 呼び出してカーソルを閉じる必要があります。  
  
 **SQLCancel**を呼び出して、ステートメントまたはデータを必要とするステートメントの関数で非同期に実行されている関数を取り消すと、キャンセルされる関数によってポストされた診断レコードがクリアされ、 **SQLCancel**によって独自の診断レコードがポストされます。ただし、別のスレッドのステートメントで実行されている関数をキャンセルするために**SQLCancel**が呼び出された場合、キャンセルされる関数の診断レコードはクリアされず、独自の診断レコードがポストされません。  
  
## <a name="canceling-asynchronous-processing"></a>非同期処理の取り消し  
 アプリケーションは、関数を非同期に呼び出すと、関数を繰り返し呼び出して、処理が完了したかどうかを判断します。 関数がまだ処理中の場合は、SQL_STILL_EXECUTING を返します。 関数の処理が完了すると、別のコードが返されます。  
  
 SQL_STILL_EXECUTING を返す関数を呼び出すと、アプリケーションは **SQLCancel** を呼び出して関数を取り消すことができます。 キャンセル要求が成功すると、ドライバーは SQL_SUCCESS を返します。 このメッセージは、関数が実際にキャンセルされたことを示すものではありません。これは、キャンセル要求が処理されたことを示します。 関数が実際にキャンセルされた場合は、ドライバーに依存し、データソースに依存します。 アプリケーションは、リターンコードが SQL_STILL_EXECUTING されない限り、元の関数を引き続き呼び出す必要があります。 関数が正常にキャンセルされた場合、リターンコードは SQL_ERROR と SQLSTATE HY008 (操作が取り消されました) になります。 関数が通常の処理を完了した場合、リターンコードは SQL_SUCCESS か、関数が成功したか SQL_ERROR た場合は SQL_SUCCESS_WITH_INFO、関数が失敗した場合は HY008 (操作が取り消されました) を返します。  
  
> [!NOTE]  
>  ODBC 3.5 では、ステートメントに対して処理が実行されていない場合の **SQLCancel** の呼び出しは、SQL_CLOSE オプションを使用した **SQLFreeStmt** として扱われませんが、まったく影響を与えることはありません。 カーソルを閉じるには、アプリケーションは**SQLCancel**ではなく**sqlcloを**呼び出す必要があります。  
  
 非同期処理の詳細については、「 [非同期実行](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)」を参照してください。  
  
## <a name="canceling-functions-that-need-data"></a>データを必要とする関数の取り消し  
 **Sqlexecute**または**SQLExecDirect**が SQL_NEED_DATA を返し、実行時データのすべてのパラメーターについてデータが送信される前に、アプリケーションは**SQLCancel**を呼び出してステートメントの実行を取り消すことができます。 ステートメントがキャンセルされると、アプリケーションは **Sqlexecute** または **SQLExecDirect** を再度呼び出すことができます。 詳細については、「 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)」を参照してください。  
  
 **Sqlbulkoperations**または**SQLSetPos**によって SQL_NEED_DATA が返された後、実行時データのすべての列についてデータが送信される前に、アプリケーションは**SQLCancel**を呼び出して操作を取り消すことができます。 操作が取り消された後、アプリケーションは **Sqlbulkoperations** または **SQLSetPos** を再度呼び出すことができます。取り消すと、カーソルの状態または現在のカーソル位置には影響しません。 詳細については、「 [Sqlbulkoperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md) または [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)」を参照してください。  
  
## <a name="canceling-functions-executing-on-another-thread"></a>別のスレッドで実行している関数を取り消しています  
 マルチスレッドアプリケーションでは、アプリケーションは別のスレッドで実行されている関数を取り消すことができます。 関数を取り消すには、アプリケーションは、対象の関数で使用されるものと同じステートメントハンドルを使用して、別のスレッドで **SQLCancel** を呼び出します。 関数がどのようにキャンセルされるかは、ドライバーとオペレーティングシステムによって異なります。 非同期的に実行されている関数をキャンセルする場合と同様に、 **SQLCancel** のリターンコードは、ドライバーが要求を正常に処理したかどうかのみを示します。 SQL_SUCCESS または SQL_ERROR のみを返すことができます。診断情報は返されません。 元の関数が取り消された場合は、SQL_ERROR と SQLSTATE HY008 (操作が取り消されました) が返されます。  
  
 **SQLCancel**が別のスレッドで呼び出され、ステートメントの実行をキャンセルしたときに SQL ステートメントが実行されている場合は、実行が成功し、キャンセルも成功している間に SQL_SUCCESS が返される可能性があります。 この場合、ドライバーマネージャーは、ステートメントの実行によって開かれたカーソルがキャンセルによって閉じられることを前提としているので、アプリケーションはカーソルを使用できません。  
  
 スレッド処理の詳細については、「 [マルチスレッド](../../../odbc/reference/develop-app/multithreading.md)」を参照してください。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|バッファーをパラメーターにバインドする|[SQLBindParameter 関数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Bulk insert または update 操作の実行|[SQLBulkOperations 関数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|**SQLCancel**の機能に加えて、接続ハンドルで非同期に実行されている関数をキャンセルします。|[SQLCancelHandle 関数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|SQL ステートメントの実行|[SQLExecDirect 関数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|準備された SQL ステートメントの実行|[SQLExecute 関数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|ステートメントハンドルの解放|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|診断レコードのフィールドまたは診断ヘッダーのフィールドを取得する|[SQLGetDiagField 関数](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
|診断データ構造の複数のフィールドの取得|[SQLGetDiagRec 関数](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|  
|データを送信する次のパラメーターを返す|[SQLParamData 関数](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|実行時にパラメーターデータを送信する|[SQLPutData 関数](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|行セットへのカーソルの配置、行セット内のデータの更新、または結果セット内のデータの更新または削除|[SQLSetPos 関数](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
