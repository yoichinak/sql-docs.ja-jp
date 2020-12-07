---
description: 非同期実行 (ポーリング メソッド)
title: 非同期実行 (ポーリングメソッド) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- asynchronous execution [ODBC]
ms.assetid: 8cd21734-ef8e-4066-afd5-1f340e213f9c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b2767a89347329ee084c8b055bcb444dc4e78117
ms.sourcegitcommit: 80701484b8f404316d934ad2a85fd773e26ca30c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93243531"
---
# <a name="asynchronous-execution-polling-method"></a>非同期実行 (ポーリング メソッド)
ODBC 3.8 および Windows 7 SDK より前の場合、非同期操作はステートメント関数でのみ許可されていました。 詳細については、このトピックの「 **ステートメントの実行** 」を参照してください。  
  
 Windows 7 SDK の ODBC 3.8 では、接続関連の操作に対する非同期実行が導入されました。 詳細については、このトピックの「 **接続操作を非同期で実行** する」セクションを参照してください。  
  
 Windows 7 SDK で、非同期ステートメントまたは接続操作の場合、アプリケーションは、ポーリングメソッドを使用して非同期操作が完了したと判断しました。 Windows 8 SDK 以降では、通知メソッドを使用して非同期操作が完了したことを確認できます。 詳細については、「 [非同期実行 (通知方法)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)」を参照してください。  
  
 既定では、ドライバーは ODBC 関数を同期的に実行します。つまり、アプリケーションは関数を呼び出しますが、関数の実行が完了するまで、ドライバーはアプリケーションに制御を返しません。 ただし、一部の関数は非同期に実行できます。つまり、アプリケーションは関数を呼び出し、最小処理を行った後、ドライバーはアプリケーションに制御を戻します。 その後、アプリケーションは、最初の関数の実行中に他の関数を呼び出すことができます。  
  
 非同期実行は、データソースで主に実行されるほとんどの関数 (接続の確立、SQL ステートメントの準備と実行、メタデータの取得、データのフェッチ、トランザクションのコミットなど) に対してサポートされています。 これは、データソースに対して実行されるタスクの実行に時間がかかる場合 (ログインプロセスや、大規模なデータベースに対する複雑なクエリなど) に最も役立ちます。  
  
 非同期処理が有効になっているステートメントまたは接続を使用して、アプリケーションが関数を実行すると、ドライバーは最小限の処理 (エラーの引数のチェックなど) を実行し、データソースに処理を行い、SQL_STILL_EXECUTING リターンコードを使用してアプリケーションに制御を返します。 その後、アプリケーションは他のタスクを実行します。 非同期関数が終了したことを確認するために、アプリケーションは、最初に使用したものと同じ引数を使用して関数を呼び出すことによって、ドライバーを一定の間隔でポーリングします。 関数がまだ実行されている場合は、SQL_STILL_EXECUTING を返します。実行が完了すると、SQL_SUCCESS、SQL_ERROR、SQL_NEED_DATA など、同期的に実行されたコードが返されます。  
  
 関数を同期的に実行するか、非同期的に実行するかは、ドライバーによって異なります。 たとえば、結果セットのメタデータがドライバーにキャッシュされているとします。 この場合、 **SQLDescribeCol** の実行にはかなりの時間がかかります。ドライバーは、人為的に遅延実行するのではなく、単に関数を実行する必要があります。 一方、ドライバーがデータソースからメタデータを取得する必要がある場合は、その実行中にアプリケーションに制御を返す必要があります。 したがって、アプリケーションは、最初に関数を非同期的に実行するときに、SQL_STILL_EXECUTING 以外のリターンコードを処理できる必要があります。  
  
## <a name="executing-statement-operations-asynchronously"></a>ステートメント操作の非同期実行  
 次のステートメント関数は、データソースに対して動作し、非同期的に実行できます。  

:::row:::
    :::column:::
        [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)  
        [SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)  
        [SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)  
        [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)  
        [SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)  
        [SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)  
        [SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)  
        [SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)  
        [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)  
    :::column-end:::
    :::column:::
        [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)  
        [SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)  
        [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)  
        [SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)  
        [SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)  
        [SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)  
        [SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)  
        [SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)  
        [SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)  
    :::column-end:::
    :::column:::
        [SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)  
        [SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)  
        [SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)  
        [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)  
        [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)  
        [SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)  
        [SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)  
        [SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)  
        [SQLTables](../../../odbc/reference/syntax/sqltables-function.md)  
    :::column-end:::
:::row-end:::

 非同期ステートメントの実行は、データソースに応じて、ステートメントごとに、または接続ごとに制御されます。 つまり、アプリケーションでは、特定の関数が非同期に実行されることを指定しますが、特定のステートメントで実行される関数は非同期に実行されます。 サポートされているものを確認するために、アプリケーションは SQL_ASYNC_MODE のオプションを使用して [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) を呼び出します。 接続レベルの非同期実行 (ステートメントハンドルの場合) がサポートされている場合は SQL_AM_CONNECTION が返されます。ステートメントレベルの非同期実行がサポートされている場合は SQL_AM_STATEMENT。  
  
 特定のステートメントを使用して実行される関数を非同期に実行するように指定するには、アプリケーションは SQL_ATTR_ASYNC_ENABLE 属性を使用して **SQLSetStmtAttr** を呼び出し、SQL_ASYNC_ENABLE_ON に設定します。 接続レベルの非同期処理がサポートされている場合、SQL_ATTR_ASYNC_ENABLE statement 属性は読み取り専用となり、その値は、ステートメントが割り当てられた接続の接続属性と同じになります。 ステートメントの割り当て時刻またはそれ以降に statement 属性の値が設定されているかどうかは、ドライバーによって異なります。 設定しようとすると、SQL_ERROR と SQLSTATE HYC00 が返されます (省略可能な機能は実装されていません)。  
  
 特定の接続で実行される関数を非同期に実行するように指定するには、アプリケーションは SQL_ATTR_ASYNC_ENABLE 属性を使用して **SQLSetConnectAttr** を呼び出し、SQL_ASYNC_ENABLE_ON に設定します。 この接続で割り当てられた後続のステートメントハンドルはすべて、非同期実行に対して有効になります。この操作によって既存のステートメントハンドルが有効になるかどうかは、ドライバーによって定義されます。 SQL_ATTR_ASYNC_ENABLE が SQL_ASYNC_ENABLE_OFF に設定されている場合、接続のすべてのステートメントは同期モードになります。 接続にアクティブなステートメントがあるときに非同期実行が有効になっていると、エラーが返されます。  
  
 特定の接続でドライバーがサポートできる非同期モードでのアクティブな同時実行ステートメントの最大数を特定するには、アプリケーションは SQL_MAX_ASYNC_CONCURRENT_STATEMENTS オプションを使用して **SQLGetInfo** を呼び出します。  
  
 次のコードは、ポーリングモデルの動作を示しています。  
  
```  
SQLHSTMT  hstmt1;  
SQLRETURN rc;  
  
// Specify that the statement is to be executed asynchronously.  
SQLSetStmtAttr(hstmt1, SQL_ATTR_ASYNC_ENABLE, SQL_ASYNC_ENABLE_ON, 0);  
  
// Execute a SELECT statement asynchronously.  
while ((rc=SQLExecDirect(hstmt1,"SELECT * FROM Orders",SQL_NTS))==SQL_STILL_EXECUTING) {  
   // While the statement is still executing, do something else.  
   // Do not use hstmt1, because it is being used asynchronously.  
}  
  
// When the statement has finished executing, retrieve the results.  
```  
  
 関数が非同期的に実行されている間、アプリケーションは他の任意のステートメントで関数を呼び出すことができます。 アプリケーションでは、非同期ステートメントに関連付けられているものを除き、任意の接続で関数を呼び出すこともできます。 ただし、ステートメント操作によって SQL_STILL_EXECUTING が返された後、アプリケーションは、元の関数と次の関数 (ステートメントハンドルを使用した、またはそれに関連付けられた接続、環境ハンドル) のみを呼び出すことができます。  
  
-   [SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)  
  
-   [Sqlcancelhandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) (ステートメントハンドル上)  
  
-   [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
-   [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
-   [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
-   [SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)  
  
-   [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
-   [SQLDataSources](../../../odbc/reference/syntax/sqldatasources-function.md)  
  
-   [SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)  
  
-   [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)  
  
-   [SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
-   [SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md)  
  
 アプリケーションが非同期ステートメントまたはそのステートメントに関連付けられた接続を使用して他の関数を呼び出す場合、関数は SQLSTATE HY010 (関数シーケンスエラー) を返します。たとえば、のようになります。  
  
```  
SQLHDBC       hdbc1, hdbc2;  
SQLHSTMT      hstmt1, hstmt2, hstmt3;  
SQLCHAR *     SQLStatement = "SELECT * FROM Orders";  
SQLUINTEGER   InfoValue;  
SQLRETURN     rc;  
  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt2);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc2, &hstmt3);  
  
// Specify that hstmt1 is to be executed asynchronously.  
SQLSetStmtAttr(hstmt1, SQL_ATTR_ASYNC_ENABLE, SQL_ASYNC_ENABLE_ON, 0);  
  
// Execute hstmt1 asynchronously.  
while ((rc = SQLExecDirect(hstmt1, SQLStatement, SQL_NTS)) == SQL_STILL_EXECUTING) {  
   // The following calls return HY010 because the previous call to  
   // SQLExecDirect is still executing asynchronously on hstmt1. The  
   // first call uses hstmt1 and the second call uses hdbc1, on which  
   // hstmt1 is allocated.  
   SQLExecDirect(hstmt1, SQLStatement, SQL_NTS);   // Error!  
   SQLGetInfo(hdbc1, SQL_UNION, (SQLPOINTER) &InfoValue, 0, NULL);   // Error!  
  
   // The following calls do not return errors. They use a statement  
   // handle other than hstmt1 or a connection handle other than hdbc1.  
   SQLExecDirect(hstmt2, SQLStatement, SQL_NTS);   // OK  
   SQLTables(hstmt3, NULL, 0, NULL, 0, NULL, 0, NULL, 0);   // OK  
   SQLGetInfo(hdbc2, SQL_UNION, (SQLPOINTER) &InfoValue, 0, NULL);   // OK  
}  
```  
  
 アプリケーションが非同期的に実行されているかどうかを判断するために関数を呼び出す場合は、元のステートメントハンドルを使用する必要があります。 これは、非同期実行がステートメントごとに追跡されるためです。 また、アプリケーションでは、他の引数に有効な値を指定する必要があります。元の引数は、ドライバーマネージャーで過去のエラーチェックを実行します。 ただし、ドライバーがステートメントハンドルを確認し、ステートメントが非同期に実行されていると判断した後は、他のすべての引数は無視されます。  
  
 関数が非同期的に実行されている間、つまり SQL_STILL_EXECUTING が返された後、別のコードを返す前に、アプリケーションは同じステートメントハンドルを使用して **SQLCancel** または **sqlcancelhandle** を呼び出すことによって、その関数を取り消すことができます。 これは、関数の実行をキャンセルすることは保証されていません。 たとえば、関数は既に完了している可能性があります。 さらに、 **SQLCancel** または **sqlcancelhandle** によって返されるコードは、関数をキャンセルしようとしたが、実際に関数をキャンセルしたかどうかではなく、成功したかどうかのみを示します。 関数が取り消されたかどうかを判断するために、アプリケーションは関数を再度呼び出します。 関数が取り消された場合は、SQL_ERROR と SQLSTATE HY008 (操作が取り消されました) を返します。 関数がキャンセルされなかった場合は、SQL_SUCCESS、SQL_STILL_EXECUTING、SQL_ERROR などの別のコードが返されます。  
  
 ドライバーがステートメントレベルの非同期処理をサポートしているときに、特定のステートメントの非同期実行を無効にするには、アプリケーションは SQL_ATTR_ASYNC_ENABLE 属性を使用して **SQLSetStmtAttr** を呼び出し、SQL_ASYNC_ENABLE_OFF に設定します。 ドライバーが接続レベルの非同期処理をサポートしている場合、アプリケーションは **SQLSetConnectAttr** を呼び出して、SQL_ATTR_ASYNC_ENABLE を SQL_ASYNC_ENABLE_OFF に設定します。これにより、接続でのすべてのステートメントの非同期実行が無効になります。  
  
 アプリケーションは、元の関数の繰り返しループで診断レコードを処理する必要があります。 非同期関数の実行中に **SQLGetDiagField** または **SQLGetDiagRec** が呼び出されると、診断レコードの現在の一覧が返されます。 元の関数呼び出しが繰り返されるたびに、以前の診断レコードがクリアされます。  
  
## <a name="executing-connection-operations-asynchronously"></a>接続操作の非同期実行  
 ODBC 3.8 より前では、ステートメント関連の操作 (prepare、execute、fetch など)、およびカタログメタデータ操作に対して、非同期実行が許可されていました。 ODBC 3.8 以降では、接続関連の操作 (接続、切断、コミット、ロールバックなど) に対して非同期実行を行うこともできます。  
  
 ODBC 3.8 の詳細については、「 [odbc 3.8 の新機能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)」を参照してください。  
  
 次のシナリオでは、接続操作を非同期的に実行すると便利です。  
  
-   少数のスレッドが大量のデバイスを管理し、非常に高いデータ速度を使用している場合。 応答性とスケーラビリティを最大化するには、すべての操作を非同期にすることをお勧めします。  
  
-   複数の接続でデータベース操作を重複させて、経過した転送時間を短縮する場合。  
  
-   効率的な非同期 ODBC 呼び出しと接続操作をキャンセルする機能により、アプリケーションは、タイムアウトを待つことなく、ユーザーが低速な操作をキャンセルできるようにします。  
  
 次の関数は、接続ハンドルに対して動作し、非同期的に実行できるようになりました。  

:::row:::
    :::column:::
        [SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)  
        [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)  
    :::column-end:::
    :::column:::
        [SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)  
        [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)  
    :::column-end:::
    :::column:::
        [SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)  
        [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)  
    :::column-end:::
:::row-end:::

 ドライバーがこれらの関数に対する非同期操作をサポートしているかどうかを判断するために、アプリケーションは SQL_ASYNC_DBC_FUNCTIONS で **SQLGetInfo** を呼び出します。 非同期操作がサポートされている場合は SQL_ASYNC_DBC_CAPABLE が返されます。 非同期操作がサポートされていない場合は SQL_ASYNC_DBC_NOT_CAPABLE が返されます。  
  
 特定の接続で実行される関数を非同期に実行するように指定するには、アプリケーションが **SQLSetConnectAttr** を呼び出し、SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 属性を SQL_ASYNC_DBC_ENABLE_ON に設定します。 接続を確立する前に接続属性を設定することは、常に同期的に実行されます。 また、 **SQLSetConnectAttr** を使用して接続属性 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE を設定する操作は、常に同期的に実行されます。  
  
 アプリケーションでは、接続を確立する前に非同期操作を有効にすることができます。 ドライバーマネージャーは、接続を確立する前に使用するドライバーを決定できないため、ドライバーマネージャーは常に **SQLSetConnectAttr** で成功を返します。 ただし、ODBC ドライバーが非同期操作をサポートしていない場合、接続に失敗する可能性があります。  
  
 一般に、特定の接続ハンドルまたはステートメントハンドルに関連付けられている関数は、非同期的に1つしか実行できません。 ただし、接続ハンドルには、複数のステートメントハンドルを関連付けることができます。 接続ハンドルで実行される非同期操作がない場合は、関連付けられたステートメントハンドルで非同期操作を実行できます。 同様に、関連付けられているステートメントハンドルで非同期操作が進行中でない場合は、接続ハンドルに対して非同期操作を行うことができます。 現在非同期操作を実行しているハンドルを使用して非同期操作を実行しようとすると、"関数シーケンスエラー" という HY010 が返されます。  
  
 接続操作によって SQL_STILL_EXECUTING が返された場合、アプリケーションは、元の関数とその接続ハンドルに対して、次の関数のみを呼び出すことができます。  
  
-   **Sqlcancelhandle** (接続ハンドル上)  
  
-   **SQLGetDiagField**  
  
-   **SQLGetDiagRec**  
  
-   **SQLAllocHandle** (ENV/DBC の割り当て)  
  
-   **SQLAllocHandleStd** (ENV/DBC の割り当て)  
  
-   **SQLGetEnvAttr**  
  
-   **SQLGetConnectAttr**  
  
-   **SQLDataSources**  
  
-   **SQLDrivers**  
  
-   **SQLGetInfo**  
  
-   **SQLGetFunctions**  
  
 アプリケーションは、元の関数の繰り返しループで診断レコードを処理する必要があります。 非同期関数の実行中に SQLGetDiagField または SQLGetDiagRec が呼び出されると、診断レコードの現在の一覧が返されます。 元の関数呼び出しが繰り返されるたびに、以前の診断レコードがクリアされます。  
  
 接続が非同期的に開かれたり閉じられたりしている場合は、アプリケーションが元の関数呼び出しで SQL_SUCCESS または SQL_SUCCESS_WITH_INFO を受け取ると、操作が完了します。  
  
 ODBC 3.8、 **Sqlcancelhandle** に新しい関数が追加されました。 この関数は、6つの接続関数 ( **SQLBrowseConnect** 、 **SQLConnect** 、 **sqldisconnect** 、 **SQLDriverConnect** 、 **SQLEndTran** 、および **SQLSetConnectAttr** ) を取り消します。 アプリケーションは **Sqlgetfunctions** を呼び出して、ドライバーが **sqlgetfunctions** をサポートしているかどうかを判断する必要があります。 **SQLCancel** と同様、 **sqlcancelhandle** が成功を返す場合は、操作が取り消されたという意味ではありません。 アプリケーションは、元の関数を再度呼び出して、操作が取り消されたかどうかを判断する必要があります。 **Sqlcancelhandle** を使用すると、接続ハンドルまたはステートメントハンドルに対する非同期操作を取り消すことができます。 **Sqlcancelhandle** を使用してステートメントハンドルに対する操作を取り消すことは、 **SQLCancel** の呼び出しと同じです。  
  
 **Sqlcancelhandle** と非同期接続の両方の操作を同時にサポートする必要はありません。 ドライバーは非同期接続操作をサポートできますが、 **Sqlcancelhandle** はサポートできません。また、その逆も可能です。  
  
 Odbc 3.8 ドライバーおよび odbc 3.8 Driver Manager を使用して、odbc 3.x および odbc 2.x アプリケーションで非同期接続操作と **Sqlcancelhandle** を使用することもできます。 古いアプリケーションで、以降のバージョンの ODBC の新機能を使用できるようにする方法については、「 [互換性マトリックス](../../../odbc/reference/develop-app/compatibility-matrix.md)」を参照してください。  
  
### <a name="connection-pooling"></a>接続のプール  
 接続プールが有効になっている場合、非同期操作は、( **SQLConnect** および **SQLDriverConnect** を使用した) 接続を確立し、 **sqldisconnect** を使用して接続を終了するために最小限しかサポートされません。 ただし、アプリケーションでは、 **SQLConnect** 、 **SQLDriverConnect** 、および **sqldisconnect** からの SQL_STILL_EXECUTING 戻り値を引き続き処理できる必要があります。  
  
 接続プールが有効になっている場合、非同期操作では **SQLEndTran** と **SQLSetConnectAttr** がサポートされます。  
  
## <a name="examples"></a>例  
  
### <a name="a-enable-asynchronous-execution-of-connection-functions"></a>A. 接続関数の非同期実行を有効にする

 次の例では、 **SQLSetConnectAttr** を使用して、接続関連の関数の非同期実行を有効にする方法を示します。  
  
```  
BOOL AsyncConnect (SQLHANDLE hdbc)   
{  
   SQLRETURN r;  
   SQLHANDLE hdbc;  
  
   // Enable asynchronous execution of connection functions.  
   // This must be executed synchronously, that is r != SQL_STILL_EXECUTING  
   r = SQLSetConnectAttr(  
         hdbc,   
         SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE,  
         reinterpret_cast<SQLPOINTER> (SQL_ASYNC_DBC_ENABLE_ON),  
         0);  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO)   
   {  
      return FALSE;  
   }  
  
   TCHAR szConnStrIn[256] = _T("DSN=AsyncDemo");  
  
   r = SQLDriverConnect(hdbc, NULL, (SQLTCHAR *) szConnStrIn, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
  
   if (r == SQL_ERROR)   
   {  
      // Use SQLGetDiagRec to process the error.  
      // If SQLState is HY114, the driver does not support asynchronous execution.  
      return FALSE;  
   }  
  
   while (r == SQL_STILL_EXECUTING)   
   {  
      // Do something else.  
  
      // Check for completion, with the same set of arguments.  
      r = SQLDriverConnect(hdbc, NULL, (SQLTCHAR *) szConnStrIn, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
   }  
  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO)   
   {  
      return FALSE;  
   }  
  
   return TRUE;  
}  
  
```  
  
### <a name="b-asynchronous-commit-operations"></a>B. 非同期コミット操作 

 この例では、非同期コミット操作を示します。 このようにしてロールバック操作を行うこともできます。  
  
```  
BOOL AsyncCommit ()   
{  
   SQLRETURN r;   
  
   // Assume that SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE is SQL_ASYNC_DBC_ENABLE_ON.  
  
   r = SQLEndTran(SQL_HANDLE_DBC, hdbc, SQL_COMMIT);  
   while (r == SQL_STILL_EXECUTING)   
   {  
      // Do something else.  
  
      // Check for completion with the same set of arguments.  
      r = SQLEndTran(SQL_HANDLE_DBC, hdbc, SQL_COMMIT);  
   }  
  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO)   
   {  
      return FALSE;  
   }  
   return TRUE;  
}  
```  
  
## <a name="see-also"></a>参照  
 [ステートメントの実行 (ODBC)](../../../odbc/reference/develop-app/executing-statements-odbc.md)
