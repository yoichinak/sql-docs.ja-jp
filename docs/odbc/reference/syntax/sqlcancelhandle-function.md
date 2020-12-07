---
description: SQLCancelHandle 関数
title: SQLCancelHandle 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
f1_keywords:
- SQLCancelHandle
helpviewer_keywords:
- SQLCancelHandle function [ODBC]
ms.assetid: 16049b5b-22a7-4640-9897-c25dd0f19d21
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3f466f63d6da9aa9a96b9e929ea2b59a3e43491d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448852"
---
# <a name="sqlcancelhandle-function"></a>SQLCancelHandle 関数
**互換性**  
 導入されたバージョン: ODBC 3.8 標準準拠: なし  
  
 ほとんどの ODBC 3.8 (およびそれ以降) のドライバーでは、この関数が実装されることが想定されています。 ドライバーがサポートしていない場合、*ハンドル*パラメーターの接続ハンドルを使用して**sqlcancelhandle**を呼び出すと、IM001 が SQL_ERROR 返され、メッセージ ' driver はこの関数をサポートしていません。 *handle*パラメーターとしてのステートメントハンドルを持つ**Sqlcancelhandle**の呼び出しは、ドライバーマネージャーによって**SQLCancel**への呼び出しにマップされ、ドライバーが**SQLCancel**を アプリケーションで **Sqlgetfunctions** を使用して、ドライバーが **sqlgetfunctions**をサポートしているかどうかを判断できます。  
  
 **まとめ**  
 **Sqlcancelhandle** は、接続またはステートメントの処理を取り消します。 *Handletype*が SQL_HANDLE_STMT 場合、ドライバーマネージャーは**sqlcancelhandle**への呼び出しを**SQLCancel**への呼び出しにマップします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLCancelHandle(  
      SQLSMALLINT  HandleType,  
      SQLHANDLE    Handle);  
```  
  
## <a name="arguments"></a>引数  
 *HandleType*  
 代入処理を cacel するハンドルの型。 有効な値は、SQL_HANDLE_DBC または SQL_HANDLE_STMT です。  
  
 *扱え*  
 代入処理を取り消すハンドル。  
  
 *Handle*が*handletype*によって指定された型の有効なハンドルでない場合、 **sqlcancelhandle**は SQL_INVALID_HANDLE を返します。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **Sqlcancelhandle**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合、関連付けられた SQLSTATE 値は、 *handletype*が SQL_HANDLE_STMT、ステートメントハンドル*ハンドル*、または SQL_HANDLE_DBC の*handletype*と接続ハンドル*ハンドル*を指定して**SQLGetDiagRec**を呼び出すことによって取得できます。  
  
 次の表に、 **Sqlcancelhandle** によって一般的に返される SQLSTATE 値と、この関数のコンテキストでのそれぞれについて説明します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)によって返されるエラーメッセージに* \* *は、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY010|関数のシーケンスエラー|*ハンドル*に関連付けられているステートメントハンドルの1つに対して、ステートメント関連の非同期関数が呼び出され、 *handletype*が SQL_HANDLE_DBC に設定されました。 **Sqlcancelhandle**が呼び出されたときに、非同期関数がまだ実行されていました。<br /><br /> (DM) *Handletype* 引数が SQL_HANDLE_STMT ました。関連付けられた接続ハンドルで非同期に実行する関数が呼び出されました。関数は、この関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または **sqlmoreresults** が *ハンドル* に関連付けられているいずれかのステートメントハンドルに対して呼び出され、 *handletype* が SQL_HANDLE_DBC に設定され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。<br /><br /> **SQLBrowseConnect** が *connectionhandle*に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、参照プロセスが完了する前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY092|属性またはオプションの識別子が無効です|*Handletype* が SQL_HANDLE_ENV または SQL_HANDLE_DESC に設定されました。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *ハンドル* に関連付けられているドライバーでは、関数はサポートされていません。|  
  
 *Handletype*を SQL_HANDLE_STMT に設定して**sqlcancelhandle**を呼び出すと、関数**SQLCancel**によって返されるすべての SQLSTATE を返すことができます。  
  
## <a name="comments"></a>コメント  
 この関数は **SQLCancel** に似ていますが、接続またはステートメントハンドルだけではなく、パラメーターとしてのハンドルを受け取る場合があります。 *Handletype*が SQL_HANDLE_STMT 場合、ドライバーマネージャーは**sqlcancelhandle**への呼び出しを**SQLCancel**への呼び出しにマップします。 これにより、ドライバーが**Sqlcancelhandle**を実装していない場合でも、アプリケーションは**sqlcancelhandle**を使用してステートメント操作を取り消すことができます。  
  
 ステートメント操作のキャンセルの詳細については、「 [SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)」を参照してください。  
  
 *ハンドル*で処理中の操作がない場合、 **sqlcancelhandle**への呼び出しは無効です。  
  
 接続ハンドルの**Sqlcancelhandle**は、次の種類の処理を取り消すことができます。  
  
-   接続で非同期に実行されている関数。  
  
-   別のスレッドの接続ハンドルで実行されている関数。  
  
 接続で非同期に実行されている関数をキャンセルするために **sqlcancelhandle** が呼び出されると、 **sqlcancelhandle** によって通知された診断レコードが、取り消される操作によって返されるものに追加されます。ただし、別のスレッドの接続で実行されている関数をキャンセルしても、 **Sqlcancelhandle** は診断レコードを返しません。  
  
 **Sqlcancelhandle**を使用して**SQLEndTran**を取り消すと、接続が中断状態になることがあります。 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。  
  
> [!NOTE]  
>  Windows 7 より前の Windows オペレーティングシステムに展開されるアプリケーションで **Sqlcancelhandle** を使用する方法については、「 [互換性マトリックス](../../../odbc/reference/develop-app/compatibility-matrix.md)」を参照してください。  
  
#### <a name="canceling-connection-related-asynchronous-processing"></a>接続関連の非同期処理の取り消し  
 関数が SQL_STILL_EXECUTING を返す場合、アプリケーションは **Sqlcancelhandle** を呼び出して操作を取り消すことができます。 キャンセル要求が成功した場合、 **Sqlcancelhandle** は SQL_SUCCESS を返します。 これは、元の関数が取り消されたことを意味するわけではありません。これは、キャンセル要求が処理されたことを示します。 操作が取り消された場合、ドライバーとデータソースによって判断されます。 アプリケーションは、リターンコードが SQL_STILL_EXECUTING されない限り、元の関数を引き続き呼び出す必要があります。 元の関数が取り消された場合、リターンコードは SQL_ERROR と SQLSTATE HY008 (操作が取り消されました) になります。 元の関数が通常の処理 (キャンセルされていない) を完了した場合、リターンコードは SQL_SUCCESS または SQL_SUCCESS_WITH_INFO になります。 SQL_ERROR また、元の関数が失敗した場合は、HY008 (操作が取り消されました) 以外の SQLSTATE が返されます。  
  
#### <a name="canceling-functions-executing-on-another-thread"></a>別のスレッドで実行している関数を取り消しています  
 マルチスレッドアプリケーションでは、アプリケーションは別のスレッドで実行されている操作を取り消すことができます。 操作を取り消すには、アプリケーションは関数で使用されるハンドルを使用して、別のスレッドで **Sqlcancelhandle** を呼び出します。 ドライバーとオペレーティングシステムによって、操作がどのように取り消されるかが決まります。 **Sqlcancelhandle**リターンコードは、ドライバーが要求を処理したかどうかを示し、SQL_SUCCESS または SQL_ERROR (診断情報は返されません) を返します。 元の関数の処理が取り消された場合、元の関数は SQL_ERROR と SQLSTATE HY008 (操作が取り消されました) を返します。  
  
 関数をキャンセルするために、別のスレッドで **Sqlcancelhandle** が呼び出されたときに関数が実行されている場合は、関数が成功し、SQL_SUCCESS が返されてからキャンセルを有効にすることができます。 **Sqlcancelhandle**が操作をキャンセルできるようになる前に操作が完了している場合、 **sqlcancelhandle**を呼び出すことはできません。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|ステートメントハンドルで非同期に実行されている関数をキャンセルする、データが必要なステートメントで関数を取り消す、または別のスレッドのステートメントで実行される関数をキャンセルする。|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダーファイル](../../../odbc/reference/install/odbc-header-files.md)   
 [非同期実行 (ポーリングメソッド)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
