---
description: 非同期実行 (通知方法)
title: 非同期実行 (通知方法) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e509dad9-5263-4a10-9a4e-03b84b66b6b3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19c201d71d42c40277ad67cef25922e55e97de12
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483125"
---
# <a name="asynchronous-execution-notification-method"></a>非同期実行 (通知方法)
ODBC を使用すると、接続およびステートメント操作を非同期に実行できます。 アプリケーションスレッドは、非同期モードで ODBC 関数を呼び出すことができます。また、関数は、操作が完了する前にを返すことができます。これにより、アプリケーションスレッドで他のタスクを実行できるようになります。 Windows 7 SDK で、非同期ステートメントまたは接続操作の場合、アプリケーションは、ポーリングメソッドを使用して非同期操作が完了したと判断しました。 詳細については、「 [非同期実行 (ポーリングメソッド)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)」を参照してください。 Windows 8 SDK 以降では、通知メソッドを使用して非同期操作が完了したことを確認できます。  
  
 ポーリングメソッドでは、アプリケーションは、操作の状態を要求するたびに非同期関数を呼び出す必要があります。 通知方法は、コールバックと ADO.NET での待機に似ています。 ただし、ODBC では、通知オブジェクトとして Win32 イベントが使用されます。  
  
 ODBC カーソルライブラリと ODBC 非同期通知は同時に使用できません。 両方の属性を設定すると、SQLSTATE S1119 (カーソルライブラリと非同期通知を同時に有効にすることはできません) でエラーが返されます。  
  
 ドライバー開発者向けの情報については、「 [非同期関数の完了通知](../../../odbc/reference/develop-driver/notification-of-asynchronous-function-completion.md) 」を参照してください。  
  
> [!NOTE]  
>  通知方法は、カーソルライブラリではサポートされていません。 通知方法が有効になっている場合、SQLSetConnectAttr 経由でカーソルライブラリを有効にしようとすると、アプリケーションでエラーメッセージが表示されます。  
  
## <a name="overview"></a>概要  
 ODBC 関数が非同期モードで呼び出されると、呼び出し元のアプリケーションにコントロールが返されます。その際、SQL_STILL_EXECUTING のリターンコードが直ちに返されます。 アプリケーションは、SQL_STILL_EXECUTING 以外のものを返すまで、関数を繰り返しポーリングする必要があります。 ポーリングループが原因で CPU 使用率が増加し、多くの非同期シナリオでパフォーマンスが低下します。  
  
 通知モデルが使用されるたびに、ポーリングモデルは無効になります。 アプリケーションでは、元の関数を再度呼び出すことはできません。 [Sqlcompleteasync 関数](../../../odbc/reference/syntax/sqlcompleteasync-function.md)を呼び出して、非同期操作を完了します。 非同期操作が完了する前にアプリケーションが元の関数を再び呼び出した場合、呼び出しは SQLSTATE IM017 (非同期通知モードではポーリングが無効) の SQL_ERROR を返します。  
  
 通知モデルを使用する場合、アプリケーションは **SQLCancel** または **sqlcancelhandle** を呼び出して、ステートメントまたは接続操作を取り消すことができます。 キャンセル要求が成功すると、ODBC は SQL_SUCCESS を返します。 このメッセージは、関数が実際にキャンセルされたことを示すものではありません。これは、キャンセル要求が処理されたことを示します。 関数が実際に取り消されたかどうかは、ドライバーに依存し、データソースに依存します。 操作が取り消されると、ドライバーマネージャーは引き続きイベントを通知します。 ドライバーマネージャーはリターンコードバッファーに SQL_ERROR を返し、キャンセルが成功したことを示す状態は SQLSTATE HY008 (操作が取り消されました) になります。 関数が通常の処理を完了した場合、ドライバーマネージャーは SQL_SUCCESS または SQL_SUCCESS_WITH_INFO を返します。  
  
### <a name="downlevel-behavior"></a>ダウンレベルの動作  
 この通知をサポートしている ODBC ドライバーマネージャーのバージョンは、ODBC 3.81 です。  
  
|Application ODBC のバージョン|ドライバーマネージャーのバージョン|ドライバーのバージョン|動作|  
|------------------------------|----------------------------|--------------------|--------------|  
|任意の ODBC バージョンの新しいアプリケーション|ODBC 3.81|ODBC 3.80 ドライバー|ドライバーがこの機能をサポートしている場合、アプリケーションはこの機能を使用できます。それ以外の場合は、ドライバーマネージャーによってエラーが発生します。|  
|任意の ODBC バージョンの新しいアプリケーション|ODBC 3.81|ODBC 前3.80 ドライバー|ドライバーがこの機能をサポートしていない場合は、ドライバーマネージャーでエラーが発生します。|  
|任意の ODBC バージョンの新しいアプリケーション|ODBC 前3.81|どれでも可|アプリケーションでこの機能を使用すると、古いドライバーマネージャーによって新しい属性がドライバー固有の属性として考慮され、ドライバーでエラーが発生します。新しいドライバーマネージャーは、これらの属性をドライバーに渡しません。|  
  
 アプリケーションでは、この機能を使用する前に、ドライバーマネージャーのバージョンを確認する必要があります。 それ以外の場合、適切に記述されていないドライバーがエラーになり、ドライバーマネージャーのバージョンが ODBC 3.81 より前の場合、動作は未定義になります。  
  
## <a name="use-cases"></a>例  
 ここでは、非同期実行のユースケースとポーリング機構について説明します。  
  
### <a name="integrate-data-from-multiple-odbc-sources"></a>複数の ODBC ソースからのデータを統合する  
 データ統合アプリケーションは、複数のデータソースから非同期的にデータをフェッチします。 一部のデータは、リモートデータソースからのものであり、一部のデータはローカルファイルからのものです。 非同期操作が完了するまで、アプリケーションは続行できません。  
  
 操作を繰り返しポーリングして、完了しているかどうかを判断するのではなく、アプリケーションでイベントオブジェクトを作成し、ODBC 接続ハンドルまたは ODBC ステートメントハンドルに関連付けることができます。 次に、アプリケーションは、オペレーティングシステムの同期 Api を呼び出して、1つまたは複数のイベントオブジェクト (ODBC イベントとその他の Windows イベントの両方) を待機します。 ODBC は、対応する ODBC 非同期操作が完了するとイベントオブジェクトを通知します。  
  
 Windows では、Win32 イベントオブジェクトが使用され、ユーザーは統一されたプログラミングモデルを提供します。 他のプラットフォームのドライバーマネージャーは、これらのプラットフォームに固有のイベントオブジェクトの実装を使用できます。  
  
 次のコードサンプルは、接続とステートメントの非同期通知の使用方法を示しています。  
  
```  
// This function opens NUMBER_OPERATIONS connections and executes one query on statement of each connection.  
// Asynchronous Notification is used  
  
#define NUMBER_OPERATIONS 5  
int AsyncNotificationSample(void)  
{  
    RETCODE     rc;  
  
    SQLHENV     hEnv              = NULL;  
    SQLHDBC     arhDbc[NUMBER_OPERATIONS]         = {NULL};  
    SQLHSTMT    arhStmt[NUMBER_OPERATIONS]        = {NULL};  
  
    HANDLE      arhDBCEvent[NUMBER_OPERATIONS]    = {NULL};  
    RETCODE     arrcDBC[NUMBER_OPERATIONS]        = {0};  
    HANDLE      arhSTMTEvent[NUMBER_OPERATIONS]   = {NULL};  
    RETCODE     arrcSTMT[NUMBER_OPERATIONS]       = {0};  
  
    rc = SQLAllocHandle(SQL_HANDLE_ENV, NULL, &hEnv);  
    if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
  
    rc = SQLSetEnvAttr(hEnv,  
        SQL_ATTR_ODBC_VERSION,  
        (SQLPOINTER) SQL_OV_ODBC3_80,  
        SQL_IS_INTEGER);  
    if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
  
    // Connection operations begin here  
  
    // Alloc NUMBER_OPERATIONS connection handles  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc = SQLAllocHandle(SQL_HANDLE_DBC, hEnv, &arhDbc[i]);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Enable DBC Async on all connection handles  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc= SQLSetConnectAttr(arhDbc[i], SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE, (SQLPOINTER)SQL_ASYNC_DBC_ENABLE_ON, SQL_IS_INTEGER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Application must create event objects  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        arhDBCEvent[i] = CreateEvent(NULL, FALSE, FALSE, NULL); // Auto-reset, initial state is not-signaled  
        if (!arhDBCEvent[i]) goto Cleanup;  
    }  
  
    // Enable notification on all connection handles  
    // Event  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc= SQLSetConnectAttr(arhDbc[i], SQL_ATTR_ASYNC_DBC_EVENT, arhDBCEvent[i], SQL_IS_POINTER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Initiate connect establishing  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLDriverConnect(arhDbc[i], NULL, (SQLTCHAR*)TEXT("Driver={ODBC Driver 11 for SQL Server};SERVER=dp-srv-sql2k;DATABASE=pubs;UID=sa;PWD=XYZ;"), SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
    }  
  
    // Can do some other staff before calling WaitForMultipleObjects  
    WaitForMultipleObjects(NUMBER_OPERATIONS, arhDBCEvent, TRUE, INFINITE); // Wait All  
  
    // Complete connect API calls  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLCompleteAsync(SQL_HANDLE_DBC, arhDbc[i], & arrcDBC[i]);  
    }  
  
    BOOL fFail = FALSE; // Whether some connection openning fails.  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if ( !SQL_SUCCEEDED(arrcDBC[i]) )   
            fFail = TRUE;  
    }  
  
    // If some SQLDriverConnect() fail, clean up.  
    if (fFail)  
    {  
        for (int i=0; i<NUMBER_OPERATIONS; i++)  
        {  
            if (SQL_SUCCEEDED(arrcDBC[i]) )   
            {  
                SQLDisconnect(arhDbc[i]); // This is also async  
            }  
            else  
            {  
                SetEvent(arhDBCEvent[i]); // Previous SQLDriverConnect() failed. No need to call SQLDisconnect().  
            }  
        }  
        WaitForMultipleObjects(NUMBER_OPERATIONS, arhDBCEvent, TRUE, INFINITE);   
        for (int i=0; i<NUMBER_OPERATIONS; i++)  
        {  
            if (SQL_SUCCEEDED(arrcDBC[i]) )   
            {     
                SQLCompleteAsync(SQL_HANDLE_DBC, arhDbc[i], &arrcDBC[i]);; // To Complete  
            }  
        }  
  
        goto Cleanup;  
    }  
  
    // Statement Operations begin here  
  
    // Alloc statement handle  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc = SQLAllocHandle(SQL_HANDLE_STMT, arhDbc[i], &arhStmt[i]);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Enable STMT Async on all statement handles  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc = SQLSetStmtAttr(arhStmt[i], SQL_ATTR_ASYNC_ENABLE, (SQLPOINTER)SQL_ASYNC_ENABLE_ON, SQL_IS_INTEGER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Create event objects  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        arhSTMTEvent[i] = CreateEvent(NULL, FALSE, FALSE, NULL); // Auto-reset, initial state is not-signaled  
        if (!arhSTMTEvent[i]) goto Cleanup;  
    }  
  
    // Enable notification on all statement handles  
    // Event  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc= SQLSetStmtAttr(arhStmt[i], SQL_ATTR_ASYNC_STMT_EVENT, arhSTMTEvent[i], SQL_IS_POINTER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Initiate SQLExecDirect() calls  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLExecDirect(arhStmt[i], (SQLTCHAR*)TEXT("select au_lname, au_fname from authors"), SQL_NTS);  
    }  
  
    // Can do some other staff before calling WaitForMultipleObjects  
    WaitForMultipleObjects(NUMBER_OPERATIONS, arhSTMTEvent, TRUE, INFINITE); // Wait All  
  
    // Now, call SQLCompleteAsync to complete the operation and get return code  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLCompleteAsync(SQL_HANDLE_STMT, arhStmt[i], &arrcSTMT[i]);  
    }  
  
    // Check return values  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if ( !SQL_SUCCEEDED(arrcSTMT[i]) ) goto Cleanup;  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        //Do some binding jobs here, set SQL_ATTR_ROW_ARRAY_SIZE   
    }  
  
    // Now, initiate fetching  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLFetch(arhStmt[i]);  
    }  
  
    // Can do some other staff before calling WaitForMultipleObjects  
    WaitForMultipleObjects(NUMBER_OPERATIONS, arhSTMTEvent, TRUE, INFINITE);   
  
    // Now, to complete the operations and get return code  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLCompleteAsync(SQL_HANDLE_STMT, arhStmt[i], &arrcSTMT[i]);  
    }  
  
    // Check return code  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if ( !SQL_SUCCEEDED(arrcSTMT[i]) ) goto Cleanup;  
    }  
  
    // USE fetched data here!!  
  
Cleanup:  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhStmt[NUMBER_OPERATIONS])  
        {  
            SQLFreeHandle(SQL_HANDLE_STMT, arhStmt[i]);  
            arhStmt[i] = NULL;  
        }  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhSTMTEvent[i])  
        {  
            CloseHandle(arhSTMTEvent[i]);  
            arhSTMTEvent[i] = NULL;  
        }  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhDbc[i])  
        {  
            SQLFreeHandle(SQL_HANDLE_DBC, arhDbc[i]);  
            arhDbc[i] = NULL;  
        }  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhDBCEvent[i])  
        {  
            CloseHandle(arhDBCEvent[i]);  
            arhDBCEvent[i] = NULL;  
        }  
    }  
  
    if (hEnv)  
    {  
        SQLFreeHandle(SQL_HANDLE_ENV, hEnv);  
        hEnv = NULL;  
    }  
  
    return 0;  
}  
  
```  
  
### <a name="determining-if-a-driver-supports-asynchronous-notification"></a>ドライバーが非同期通知をサポートしているかどうかを確認する  
 Odbc アプリケーションは、 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)を呼び出すことによって、odbc ドライバーが非同期通知をサポートしているかどうかを判断できます。 その結果、ODBC ドライバーマネージャーは、SQL_ASYNC_NOTIFICATION でドライバーの **SQLGetInfo** を呼び出します。  
  
```  
SQLUINTEGER InfoValue;  
SQLLEN      cbInfoLength;  
  
SQLRETURN retcode;  
retcode = SQLGetInfo (hDbc,   
                      SQL_ASYNC_NOTIFICATION,   
                      &InfoValue,  
                      sizeof(InfoValue),  
                      NULL);  
if (SQL_SUCCEEDED(retcode))  
{  
if (SQL_ASYNC_NOTIFICATION_CAPABLE == InfoValue)  
      {  
          // The driver supports asynchronous notification  
      }  
      else if (SQL_ASYNC_NOTIFICATION_NOT_CAPABLE == InfoValue)  
      {  
          // The driver does not support asynchronous notification  
      }  
}  
```  
  
### <a name="associating-a-win32-event-handle-with-an-odbc-handle"></a>Win32 イベントハンドルと ODBC ハンドルの関連付け  
 アプリケーションは、対応する Win32 関数を使用して Win32 イベントオブジェクトを作成します。 アプリケーションでは、1つの Win32 イベントハンドルを1つの ODBC 接続ハンドルまたは1つの ODBC ステートメントハンドルに関連付けることができます。  
  
 接続属性 SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE および SQL_ATTR_ASYNC_DBC_EVENT ODBC が非同期モードで実行されるかどうか、および ODBC が接続ハンドルの通知モードを有効にするかどうかを決定します。 ステートメント属性 SQL_ATTR_ASYNC_ENABLE および SQL_ATTR_ASYNC_STMT_EVENT ODBC が非同期モードで実行されるかどうか、および ODBC がステートメントハンドルの通知モードを有効にするかどうかを決定します。  
  
|SQL_ATTR_ASYNC_ENABLE または SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE|SQL_ATTR_ASYNC_STMT_EVENT または SQL_ATTR_ASYNC_DBC_EVENT|モード|  
|-------------------------------------------------------------------------|-------------------------------------------------------------------|----------|  
|有効にする|null 以外|非同期通知|  
|有効にする|null|非同期ポーリング|  
|無効にする|any|同期|  
  
 アプリケーションでは、非同期操作モードを一時的にに無効にすることができます。 接続レベルの非同期操作が無効になっている場合、ODBC は SQL_ATTR_ASYNC_DBC_EVENT の値を無視します。 ステートメントレベルの非同期操作が無効になっている場合、ODBC は SQL_ATTR_ASYNC_STMT_EVENT の値を無視します。  
  
 **SQLSetStmtAttr**と**SQLSetConnectAttr**の同期呼び出し  
 -   **SQLSetConnectAttr** は非同期操作をサポートしますが、SQL_ATTR_ASYNC_DBC_EVENT 設定する **SQLSetConnectAttr** の呼び出しは常に同期です。  
  
-   **SQLSetStmtAttr** では、非同期実行はサポートされていません。  
  
 エラー-出力シナリオ  
 接続を作成する前に **SQLSetConnectAttr** を呼び出すと、ドライバーマネージャーは使用するドライバーを決定できません。 そのため、ドライバーマネージャーは **SQLSetConnectAttr** の成功を返しますが、ドライバーで属性を設定する準備ができていない可能性があります。 アプリケーションが接続関数を呼び出すと、ドライバーマネージャーによってこれらの属性が設定されます。 ドライバーで非同期操作がサポートされていないため、ドライバーマネージャーでエラーが発生することがあります。  
  
 接続属性の継承  
 通常、接続のステートメントは、接続属性を継承します。 ただし、属性 SQL_ATTR_ASYNC_DBC_EVENT は継承できないため、接続操作にのみ影響します。  
  
 Odbc アプリケーションでは、イベントハンドルを ODBC 接続ハンドルに関連付けるために、ODBC API **SQLSetConnectAttr** を呼び出し、属性およびイベントハンドルとして SQL_ATTR_ASYNC_DBC_EVENT を属性値として指定します。 新しい ODBC 属性 SQL_ATTR_ASYNC_DBC_EVENT は SQL_IS_POINTER 型です。  
  
```  
HANDLE hEvent;  
hEvent = CreateEvent(   
            NULL,                // default security attributes  
            FALSE,               // auto-reset event  
            FALSE,               // initial state is non-signaled  
            NULL                 // no name  
            );  
```  
  
 通常、アプリケーションは自動リセットイベントオブジェクトを作成します。 ODBC では、イベントオブジェクトはリセットされません。 非同期 ODBC 関数を呼び出す前に、アプリケーションでオブジェクトがシグナル状態になっていないことを確認する必要があります。  
  
```  
SQLRETURN retcode;  
retcode = SQLSetConnectAttr ( hDBC,  
                              SQL_ATTR_ASYNC_DBC_EVENT, // Attribute name  
                              (SQLPOINTER) hEvent,      // Win32 Event handle  
                              SQL_IS_POINTER);          // Length Indicator  
```  
  
 SQL_ATTR_ASYNC_DBC_EVENT は、ドライバーでは設定されない、ドライバーマネージャーのみの属性です。  
  
 SQL_ATTR_ASYNC_DBC_EVENT の既定値は NULL です。 ドライバーが非同期通知をサポートしていない場合、SQL_ATTR_ASYNC_DBC_EVENT の取得または設定では、SQLSTATE HY092 (無効な属性/オプション識別子) の SQL_ERROR が返されます。  
  
 ODBC 接続ハンドルで設定された最後の SQL_ATTR_ASYNC_DBC_EVENT 値が NULL ではなく、アプリケーションが SQL_ASYNC_DBC_ENABLE_ON で属性 SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE を設定して非同期モードを有効にした場合、非同期モードをサポートする ODBC 接続関数を呼び出すと完了通知が返されます。 ODBC 接続ハンドルに設定されている最後の SQL_ATTR_ASYNC_DBC_EVENT 値が NULL の場合、非同期モードが有効かどうかに関係なく、ODBC はアプリケーションに通知を送信しません。  
  
 アプリケーションでは、属性 SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE を設定する前または後に SQL_ATTR_ASYNC_DBC_EVENT を設定できます。  
  
 アプリケーションでは、接続関数 (**SQLConnect**、 **SQLBrowseConnect**、または **SQLDriverConnect**) を呼び出す前に、ODBC 接続ハンドルの SQL_ATTR_ASYNC_DBC_EVENT 属性を設定できます。 ODBC ドライバーマネージャーでは、アプリケーションが使用する ODBC ドライバーが認識されないため、SQL_SUCCESS が返されます。 アプリケーションが接続関数を呼び出すと、ODBC ドライバーマネージャーは、ドライバーが非同期通知をサポートしているかどうかを確認します。 ドライバーが非同期通知をサポートしていない場合、ODBC ドライバーマネージャーは SQLSTATE S1_118 で SQL_ERROR を返します (ドライバーは非同期通知をサポートしていません)。 ドライバーが非同期通知をサポートしている場合、ODBC ドライバーマネージャーはドライバーを呼び出し、対応する属性 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK および SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT を設定します。  
  
 同様に、アプリケーションは ODBC ステートメントハンドルで **SQLSetStmtAttr** を呼び出し、ステートメントレベルの非同期通知を有効または無効にする SQL_ATTR_ASYNC_STMT_EVENT 属性を指定します。 接続が確立されると、ステートメント関数は常に呼び出されるため、 **SQLSetStmtAttr** は、対応するドライバーが非同期操作をサポートしていない場合、またはドライバーが非同期操作をサポートしているが非同期通知をサポートしていない場合に、SQLSTATE S1_118 (ドライバーは非同期通知をサポートしません) を使用して SQL_ERROR を返します。  
  
```  
SQLRETURN retcode;  
retcode = SQLSetStmtAttr ( hSTMT,  
                           SQL_ATTR_ASYNC_STMT_EVENT, // Attribute name   
                           (SQLPOINTER) hEvent,       // Win32 Event handle  
                           SQL_IS_POINTER);           // length Indicator  
```  
  
 SQL_ATTR_ASYNC_STMT_EVENT は、NULL に設定できますが、ドライバーマネージャーのみの属性であり、ドライバーでは設定されません。  
  
 SQL_ATTR_ASYNC_STMT_EVENT の既定値は NULL です。 ドライバーが非同期通知をサポートしていない場合、SQL_ATTR_ASYNC_ STMT_EVENT 属性を取得または設定すると、SQLSTATE HY092 (無効な属性/オプション識別子) の SQL_ERROR が返されます。  
  
 アプリケーションでは、同じイベントハンドルを複数の ODBC ハンドルに関連付けることはできません。 それ以外の場合、2つの非同期の ODBC 関数呼び出しが、同じイベントハンドルを共有する2つのハンドルで完了すると、1つの通知が失われます。 接続ハンドルから同じイベントハンドルを継承するステートメントハンドルを使用しないようにするには、アプリケーションが接続ハンドルに SQL_ATTR_ASYNC_STMT_EVENT を設定していると、ODBC は SQLSTATE IM016 (ステートメント属性を接続ハンドルに設定できません) で SQL_ERROR を返します。  
  
### <a name="calling-asynchronous-odbc-functions"></a>非同期 ODBC 関数の呼び出し  
 非同期通知を有効にし、非同期操作を開始した後、アプリケーションは任意の ODBC 関数を呼び出すことができます。 関数が非同期操作をサポートする関数のセットに属している場合、その関数が失敗したか成功したかに関係なく、操作が完了すると、アプリケーションは完了通知を受け取ります。  唯一の例外は、アプリケーションが ODBC 関数を無効な接続またはステートメントハンドルで呼び出すことです。 この場合、ODBC はイベントハンドルを取得せず、シグナル状態に設定します。  
  
 アプリケーションは、対応する ODBC ハンドルで非同期操作を開始する前に、関連付けられているイベントオブジェクトがシグナル状態でないことを確認する必要があります。 ODBC では、イベントオブジェクトはリセットされません。  
  
### <a name="getting-notification-from-odbc"></a>ODBC から通知を受け取る  
 アプリケーションスレッドは、 **WaitForSingleObject** を呼び出して1つのイベントハンドルを待機するか、または **WaitForMultipleObjects** を呼び出してイベントハンドルの配列を待機し、1つまたはすべてのイベントオブジェクトがシグナル状態になるか、タイムアウト間隔が経過するまで中断させることができます。  
  
```  
DWORD dwStatus = WaitForSingleObject(  
                        hEvent,  // The event associated with the ODBC handle  
                        5000     // timeout is 5000 millisecond   
);  
  
If (dwStatus == WAIT_TIMEOUT)  
{  
    // time-out interval elapsed before all the events are signaled.   
}  
Else  
{  
    // Call the corresponding Asynchronous ODBC API to complete all processing and retrieve the return code.  
}  
```
