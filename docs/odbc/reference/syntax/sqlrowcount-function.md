---
description: SQLRowCount 関数
title: SQLRowCount 関数 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRowCount
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLRowCount
helpviewer_keywords:
- SQLRowCount function [ODBC]
ms.assetid: 61e00a8a-9b3b-45b9-b397-7fe818822416
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 666351fcd4758170baaf62fbd80cd45a554ab92a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499595"
---
# <a name="sqlrowcount-function"></a>SQLRowCount 関数
**互換性**  
 導入されたバージョン: ODBC 1.0 標準準拠: ISO 92  
  
 **まとめ**  
 **SQLRowCount** は、 **UPDATE**、 **INSERT**、または **DELETE** ステートメントの影響を受ける行の数を返します。 **Sqlbulkoperations**の SQL_ADD、SQL_UPDATE_BY_BOOKMARK、または SQL_DELETE_BY_BOOKMARK 操作です。または **SQLSetPos**の SQL_UPDATE 操作または SQL_DELETE 操作。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLRowCount(  
      SQLHSTMT   StatementHandle,  
      SQLLEN *   RowCountPtr);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル。  
  
 *RowCountPtr*  
 Output行数を返すバッファーを指します。 **UPDATE**、 **INSERT**、および**DELETE**ステートメントの場合、 **sqlbulkoperations**の SQL_ADD、SQL_UPDATE_BY_BOOKMARK、および SQL_DELETE_BY_BOOKMARK 操作、および**SQLSetPos**での SQL_UPDATE または SQL_DELETE 操作の場合、**rowcountptr*に返される値は、要求の影響を受けた行の数になります。または、影響を受ける行の数が使用できない場合は-1 になります。  
  
 **Sqlexecute**、 **SQLExecDirect**、 **sqlbulkoperations**、 **SQLSetPos、または sqlmoreresults**を呼び出すと、診断データ構造の SQL_DIAG_ROW_COUNT フィールドが行数に設定され、行カウントが実装に依存する方法でキャッシュされます。 **SQLRowCount** は、キャッシュされた行数の値を返します。 キャッシュされた行数の値は、ステートメントハンドルが準備済みまたは割り当て済みの状態に戻るか、ステートメントが再度実行さであるか、または **Sqlcloが** 呼び出されるまで有効です。 SQL_DIAG_ROW_COUNT フィールドが設定されてから関数が呼び出された場合、 **SQLRowCount** によって返される値は、関数呼び出しによって SQL_DIAG_ROW_COUNT フィールドが0にリセットされるため、SQL_DIAG_ROW_COUNT フィールドの値と異なる場合があります。  
  
 他のステートメントおよび関数の場合、ドライバーは \* *rowcountptr*に返される値を定義することがあります。 たとえば、一部のデータソースでは、行をフェッチする前に、 **SELECT** ステートメントまたはカタログ関数によって返される行の数を返すことができます。  
  
> [!NOTE]  
>  多くのデータソースは、フェッチする前に結果セットの行数を返すことはできません。相互運用性を最大にするには、アプリケーションがこの動作に依存しないようにする必要があります。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **SQLRowCount**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合、関連付けられた SQLSTATE 値を取得するには、 *Handletype* SQL_HANDLE_STMT と*StatementHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出します。 次の表に、 **SQLRowCount** によって一般的に返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * \* Messagetext*バッファーの**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、 **SQLRowCount** 関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または **Sqlmoreresults** が *StatementHandle* に対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。<br /><br /> (DM) 関数は、 **Sqlexecute**、 **SQLExecDirect**、 **Sqlbulkoperations**、または **SQLSetPos** を呼び出す前に、 *StatementHandle*に対して呼び出されました。<br /><br /> (DM) 非同期的に実行する関数が *StatementHandle* に対して呼び出されましたが、この関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **Sqlbulkoperations**、 **SQLSetPos** が *StatementHandle* に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle* に関連付けられているドライバーでは、関数はサポートされていません。|  
  
## <a name="comments"></a>コメント  
 ステートメントハンドルに対して最後に実行された SQL ステートメント**が UPDATE**、 **INSERT**、または**DELETE**ステートメントではなかった場合、または**sqlbulkoperations**への以前の呼び出しの操作引数が SQL_ADD、SQL_UPDATE_BY_BOOKMARK、または SQL_DELETE_BY_BOOKMARK ではない場合、または**SQLSetPos**への以前の呼び出しの*操作*引数が SQL_UPDATE または SQL_DELETE ではない場合、**rowcountptr*の*Operation* 詳細については、「 [影響を受ける行の数の決定](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)」を参照してください。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|SQL ステートメントの実行|[SQLExecDirect 関数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|準備された SQL ステートメントの実行|[SQLExecute 関数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
