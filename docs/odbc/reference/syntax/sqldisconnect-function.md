---
description: SQLDisconnect 関数
title: SQLDisconnect 関数 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDisconnect
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLDisconnect
helpviewer_keywords:
- SQLDisconnect function [ODBC]
ms.assetid: 9e84a58e-db48-4821-a0cd-5c711fcbe36b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 604f5af6f425506996e7e15b7db73878f3d8b2c6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428944"
---
# <a name="sqldisconnect-function"></a>SQLDisconnect 関数
**互換性**  
 導入されたバージョン: ODBC 1.0 標準準拠: ISO 92  
  
 **まとめ**  
 **Sqldisconnect** は、特定の接続ハンドルに関連付けられている接続を閉じます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLDisconnect(  
     SQLHDBC     ConnectionHandle);  
```  
  
## <a name="arguments"></a>引数  
 *ConnectionHandle*  
 [入力] 接続ハンドル。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE、または SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>診断  
 **Sqldisconnect**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合、関連付けられた SQLSTATE 値は、 *handletype*が SQL_HANDLE_DBC で、 *connectionhandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出すことによって取得できます。 次の表に、 **Sqldisconnect** によって一般的に返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01002|切断エラー|切断中にエラーが発生しました。 ただし、切断は成功しました。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|08003|接続が開かれていません|(DM) 引数 *Connectionhandle* に指定された接続が開かれていませんでした。|  
|25000|トランザクション状態が無効|引数 *Connectionhandle*によって指定された接続の処理中にトランザクションが発生しました。 トランザクションはアクティブのままです。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * \* Messagetext*バッファーの**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|*Connectionhandle*に対して非同期処理が有効になりました。 関数が呼び出されました。 [Sqlcancelhandle 関数](../../../odbc/reference/syntax/sqlcancelhandle-function.md) の実行が、 *connectionhandle*で呼び出されました。 次に、 *Connectionhandle*で関数が再度呼び出されました。<br /><br /> 関数が呼び出され、 **Sqlcancelhandle** の実行が完了する前に、マルチスレッドアプリケーションの別のスレッドからの *connectionhandle* でが呼び出されました。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *Connectionhandle*に関連付けられている*StatementHandle*に対して呼び出されましたが、 **sqldisconnect**が呼び出されたときに実行されていました。<br /><br /> (DM) 非同期的に実行する関数 (この1つではない) が *Connectionhandle* に対して呼び出されましたが、この関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **sqlbulkoperations**、または**SQLSetPos**が、 *connectionhandle*に関連付けられ SQL_NEED_DATA 返された*StatementHandle*に対して呼び出されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYT01|接続タイムアウトの期限が切れました|接続タイムアウト期間は、データソースが要求に応答する前に期限切れになり、接続はアクティブのままになります。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *Connectionhandle* に関連付けられているドライバーでは、関数はサポートされていません。|  
|IM017|非同期通知モードでは、ポーリングは無効になっています|通知モデルが使用されるたびに、ポーリングは無効になります。|  
|IM018|**Sqlcompleteasync** は、このハンドルで前の非同期操作を完了するために呼び出されていません。|ハンドルに対する前の関数呼び出しが SQL_STILL_EXECUTING を返し、通知モードが有効になっている場合は、処理を完了するために、ハンドルに対して **Sqlcompleteasync** を呼び出す必要があります。|  
  
## <a name="comments"></a>コメント  
 **SQLBrowseConnect**が SQL_NEED_DATA を返してから別のリターンコードを返す前に、アプリケーションが**sqldisconnect**を呼び出すと、ドライバーは接続の参照プロセスをキャンセルし、接続を未接続状態に戻します。  
  
 接続ハンドルに関連付けられた不完全なトランザクションがあるときに、アプリケーションが **Sqldisconnect** を呼び出した場合、ドライバーは SQLSTATE 25000 (無効なトランザクション状態) を返します。これは、トランザクションが変更されず、接続が開いていることを示します。 不完全なトランザクションとは、 **SQLEndTran**でコミットまたはロールバックされていないトランザクションのことです。  
  
 接続に関連付けられているすべてのステートメントを解放する前に、アプリケーションが **Sqldisconnect** を呼び出した場合、ドライバーは、データソースから正常に切断された後、その接続に明示的に割り当てられているステートメントとすべての記述子を解放します。 ただし、接続に関連付けられている1つ以上のステートメントがまだ非同期で実行されている場合、 **Sqldisconnect** は SQLSTATE 値が HY010 (関数シーケンスエラー) の SQL_ERROR を返します。 また、接続が中断状態の場合、または**sqldisconnect**が**sqlcancelhandle**によって正常に取り消された場合、 **sqldisconnect**は、関連付けられているすべてのステートメントと、接続で明示的に割り当てられているすべての記述子を解放します。  
  
 アプリケーションが **Sqldisconnect**を使用する方法の詳細については、「 [データソースまたはドライバーからの切断](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)」を参照してください。  
  
## <a name="disconnecting-from-a-pooled-connection"></a>プールされた接続からの切断  
 共有環境に対して接続プールが有効になっていて、アプリケーションがその環境の接続で **Sqldisconnect** を呼び出した場合、接続は接続プールに返され、同じ共有環境を使用している他のコンポーネントでも使用できます。  
  
## <a name="code-example"></a>コード例  
 「 [サンプル ODBC プログラム](../../../odbc/reference/sample-odbc-program.md)」、「 [SQLBrowseConnect 関数](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)」、および「 [SQLConnect 関数](../../../odbc/reference/syntax/sqlconnect-function.md)」を参照してください。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|ハンドルの割り当て|[SQLAllocHandle 関数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|データ ソースに接続する|[SQLConnect 関数](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|接続文字列またはダイアログボックスを使用したデータソースへの接続|[SQLDriverConnect 関数](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|コミットまたはロールバック操作の実行|[SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|接続ハンドルの解放|[SQLFreeConnect 関数](../../../odbc/reference/syntax/sqlfreeconnect-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
