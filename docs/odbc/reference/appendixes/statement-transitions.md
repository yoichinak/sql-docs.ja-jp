---
description: ステートメントの遷移
title: ステートメントの遷移 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transitioning states [ODBC], statement
- state transitions [ODBC], statement
- statement transitions [ODBC]
ms.assetid: 3d70e0e3-fe83-4b4d-beac-42c82495a05b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3515b1d6aea4cab66bc01ee3d071727e6cb8f447
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386518"
---
# <a name="statement-transitions"></a>ステートメントの遷移
ODBC ステートメントの状態は次のとおりです。  
  
|州|説明|  
|-----------|-----------------|  
|S0|未割り当てのステートメントです。 (接続状態は C4、C5、または C6 である必要があります。 詳細については、「 [接続の移行](../../../odbc/reference/appendixes/connection-transitions.md)」を参照してください。)|  
|S1|割り当てられたステートメント。|  
|S2|準備されたステートメントです。 結果セットは作成されません。|  
|S3|準備されたステートメントです。 (空の可能性がある) 結果セットが作成されます。|  
|S4|ステートメントが実行され、結果セットが作成されませんでした。|  
|S5|実行されたステートメントと、(空の可能性がある) 結果セットが作成されました。 カーソルが開いており、結果セットの最初の行の前に配置されています。|  
|S6|**Sqlfetch**または**sqlfetchscroll**で配置されたカーソル。|  
|S7|**SQLExtendedFetch**で配置されたカーソル。|  
|S8|関数にはデータが必要です。 **Sqlparamdata** が呼び出されていません。|  
|S9|関数にはデータが必要です。 **Sqlputdata** が呼び出されていません。|  
|S10|関数にはデータが必要です。 **Sqlputdata** が呼び出されました。|  
|S11|まだ実行中です。 非同期的に実行された関数が SQL_STILL_EXECUTING を返すと、ステートメントはこの状態のままになります。 ステートメントハンドルを受け取る関数が実行されている間、ステートメントは一時的にこの状態になります。 State S11 の一時的な住居は、 **SQLCancel**の状態テーブル以外の状態テーブルには表示されません。 ステートメントは一時的に状態 S11 にありますが、別のスレッドから **SQLCancel** を呼び出すことによって、関数を取り消すことができます。|  
|S12|非同期実行が取り消されました。 S12 では、アプリケーションは、SQL_STILL_EXECUTING 以外の値を返すまで、キャンセルされた関数を呼び出す必要があります。 関数が SQL_ERROR と SQLSTATE HY008 (操作が取り消されました) を返す場合にのみ、関数が正常に取り消されました。 SQL_SUCCESS など、その他の値が返された場合、取り消し操作は失敗し、関数は正常に実行されます。|  
  
 状態 S2 および S3 は準備済み状態と呼ばれ、カーソルの状態として状態 S5、S7、状態が S8 から S10 までの状態、および非同期状態として S11 および S12 という状態になります。 これらの各グループでは、グループ内の各状態で異なる場合にのみ、移行が個別に表示されます。ほとんどの場合、各グループの各状態の遷移は同じです。  
  
 次の表は、各 ODBC 関数がステートメントの状態にどのように影響するかを示しています。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]、[5]、[6]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[2]、[5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|S1 [3]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[4]、[5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
  
 [1] この行は、 *Handletype* が SQL_HANDLE_ENV されたときの遷移を示しています。  
  
 [2] この行は、 *Handletype* が SQL_HANDLE_DBC されたときの遷移を示しています。  
  
 [3] この行は、 *Handletype* が SQL_HANDLE_STMT されたときの遷移を示しています。  
  
 [4] この行は、 *Handletype* が SQL_HANDLE_DESC されたときの遷移を示しています。  
  
 [5] 有効なハンドルをポイントする*OutputHandlePtr*で**SQLAllocHandle**を呼び出すと、そのハンドルに対する以前の内容を考慮せずにハンドルが上書きされ、ODBC ドライバーで問題が発生する可能性があります。 ODBC アプリケーションプログラミングでは、 * \* OutputHandlePtr*に対して定義されているものと同じアプリケーション変数を使用して**SQLAllocHandle**を2回呼び出すことはできません。これを再割り当てする前に、 **sqlfreehandle**を呼び出してハンドルを解放します。 このような方法で ODBC ハンドルを上書きすると、ODBC ドライバーの一部で動作が一貫していないか、エラーが発生する可能性があります。  
  
## <a name="sqlbindcol"></a>SQLBindCol  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbindparameter"></a>SQLBindParameter  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbrowseconnect-sqlconnect-and-sqldriverconnect"></a>SQLBrowseConnect、SQLConnect、SQLDriverConnect  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|08002|08002|08002|08002|08002|08002|08002|  
  
## <a name="sqlbulkoperations"></a>SQLBulkOperations  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24000|次の表を参照|HY010|NS [c] HY010 o|  
  
## <a name="sqlbulkoperations-cursor-states"></a>SQLBulkOperations (カーソルの状態)  
  
|S5<br /><br /> 開始済み|S6<br /><br /> SQLFetch または SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|--[s] S8 [d] S11 [x]|--[s] S8 [d] S11 [x]|HY010|  
  
## <a name="sqlcancel"></a>SQLCancel  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|S1 [1] S2 [nr] および [2] S3 [r] および [2] S5 [3] と [5] S6 ([3] または [4]) と [6] S7 [4] と [7]|次の表を参照|  
  
 [1]   **SQLExecDirect** から SQL_NEED_DATA が返されました。  
  
 [2]   **Sqlexecute** によって SQL_NEED_DATA が返されました。  
  
 [3]   **Sqlbulkoperations** が SQL_NEED_DATA を返しました。  
  
 [4]   **SQLSetPos** によって SQL_NEED_DATA が返されました。  
  
 [5]   **Sqlfetch**、 **sqlfetchscroll**、または **SQLExtendedFetch** が呼び出されませんでした。  
  
 [6]   **Sqlfetch** または **sqlfetchscroll** が呼び出されました。  
  
 [7]   **SQLExtendedFetch** が呼び出されました。  
  
## <a name="sqlcancel-asynchronous-states"></a>SQLCancel (非同期の状態)  
  
|S11<br /><br /> 実行中|S12<br /><br /> 非同期の取り消し|  
|-----------------------------|-----------------------------|  
|NS [1] S12 [2]|S12|  
  
 [1] 関数の実行中に、ステートメントが一時的に状態 S11 にありました。 **SQLCancel** が別のスレッドから呼び出されました。  
  
 [2] ステートメントは、非同期的に SQL_STILL_EXECUTING 返された関数が状態 S11 にありました。  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|24000|24000|24000|S1 [np] S3 [p]|HY010|HY010|  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|次の表を参照|24000|--[s] S11 [x]|HY010|NS [c] HY010 o|  
  
## <a name="sqlcolattribute-prepared-states"></a>SQLColAttribute (準備された状態)  
  
|S2<br /><br /> 結果はありません|S3<br /><br /> 結果|  
|-----------------------|--------------------|  
|--[1] 07005 [2]|--[s] S11 x|  
  
 [1]   *FieldIdentifier* が SQL_DESC_COUNT でした。  
  
 [2]   *FieldIdentifier* が SQL_DESC_COUNT いませんでした。  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumnPrivileges、SQLColumns、SQLForeignKeys、SQLGetTypeInfo、Sqlcolumnprivileges、SQLProcedureColumns、SQLProcedures、Sql Columns、SQLStatistics、Sqlcolumnprivileges、および SQLTables  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S5 [s] S11 [x]|S1 [e] S5 [s] S11 [x]|S1 [e] および [1] S5 [s] および [1] S11 [x] と [1] 24000 [2]|次の表を参照|HY010|NS [c] HY010 o|  
  
 [1] 現在の結果が最後または唯一の結果であるか、または現在の結果がありません。 複数の結果の詳細については、「 [複数の結果](../../../odbc/reference/develop-app/multiple-results.md)」を参照してください。  
  
 [2] 現在の結果は最後の結果ではありません。  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables-cursor-states"></a>SQLColumnPrivileges、SQLColumns、SQLForeignKeys、SQLGetTypeInfo、Sqlcolumnprivileges、SQLProcedureColumns、SQLProcedures、Sql Columns、SQLStatistics、Sqlcolumnprivileges、および SQLTables (カーソル状態)  
  
|S5<br /><br /> 開始済み|S6<br /><br /> SQLFetch または SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000 [1]|24000|  
  
 [1] このエラーは、sqlfetch または**Sqlfetchscroll**が返され SQL_NO_DATA ず、 **Sqlfetch**または**sqlfetchscroll**が SQL_NO_DATA を返した場合にドライバーによって返され**た場合に**、ドライバーマネージャーによって返されます。  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH [1]|--|--|--|--|HY010|NS [c] および [3] HY010 [o] または [4]|  
|IH [2]|HY010|次の表を参照|24000|--[s] S11 x|HY010|NS [c] および [3] HY010 [o] または [4]|  
  
 [1] *SourceDescHandle* 引数が APD または IPD の場合、この行は遷移を示しています。  
  
 [2] *SourceDescHandle* 引数が IRD の場合、この行は遷移を示しています。  
  
 [3] *SourceDescHandle* 引数と *TargetDescHandle* 引数は、非同期的に実行されている **sqlcopydesc** 関数と同じです。  
  
 [4] *SourceDescHandle* 引数または *TargetDescHandle* 引数 (またはその両方) が、非同期的に実行されている **sqlcopydesc** 関数と異なっています。  
  
## <a name="sqlcopydesc-prepared-states"></a>SQLCopyDesc (準備された状態)  
  
|S2<br /><br /> 結果はありません|S3<br /><br /> 結果|  
|-----------------------|--------------------|  
|24000 [1]|--[s] S11 [x]|  
  
 1この行は、 *SourceDescHandle* 引数が IRD の場合の遷移を示しています。  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources ソースと Sqldatasources  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqldescribecol"></a>SQLDescribeCol  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|次の表を参照|24000|--[s] S11 [x]|HY010|NS [c] HY010 o|  
  
## <a name="sqldescribecol-prepared-states"></a>SQLDescribeCol (準備された状態)  
  
|S2<br /><br /> 結果はありません|S3<br /><br /> 結果|  
|-----------------------|--------------------|  
|07005|--[s] S11 [x]|  
  
## <a name="sqldescribeparam"></a>SQLDescribeParam  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|--[s] S11 [x]|HY010|HY010|HY010|NS [c] HY010 [o]|  
  
## <a name="sqldisconnect"></a>SQLDisconnect  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|S0 [1]|S0 [1]|S0 [1]|S0 [1]|HY010|HY010|  
  
 [1] **Sqldisconnect** を呼び出すと、接続に関連付けられているすべてのステートメントが解放されます。 さらに、これにより、接続状態が C2 に戻ります。ステートメントの状態が S0 の場合、接続状態は C4 である必要があります。  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--[2] または [3] S1 [1]|--[3] s1 [np] and ([1] または [2]) S1 [p] と [1] S2 [p] と [2]|--[3] s1 [np] and ([1] または [2]) S1 [p] および [1] S3 [p] と [2]|HY010|HY010|  
  
 [1] 参照 *型* の引数が SQL_COMMIT で、 **sqlgetinfo** は SQL_CURSOR_COMMIT_BEHAVIOR 情報型に対して SQL_CB_DELETE を返します。または、指定され *た種類の引数が* SQL_ROLLBACK で、 **sqlgetinfo** が SQL_CB_DELETE 情報型の SQL_CURSOR_ROLLBACK_BEHAVIOR を返します。  
  
 [2] 参照 *型* 引数が SQL_COMMIT で、 **sqlgetinfo** は SQL_CURSOR_COMMIT_BEHAVIOR 情報型に対して SQL_CB_CLOSE を返します。または、指定され *た種類の引数が* SQL_ROLLBACK で、 **sqlgetinfo** が SQL_CB_CLOSE 情報型の SQL_CURSOR_ROLLBACK_BEHAVIOR を返します。  
  
 [3] 参照 *型* 引数が SQL_COMMIT で、 **sqlgetinfo** は SQL_CURSOR_COMMIT_BEHAVIOR 情報型に対して SQL_CB_PRESERVE を返します。または、 *入力* 型引数が SQL_ROLLBACK で、 **sqlgetinfo** が SQL_CB_PRESERVE 情報型の SQL_CURSOR_ROLLBACK_BEHAVIOR を返します。  
  
## <a name="sqlexecdirect"></a>SQLExecDirect  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S4 [s] と [nr] S5 [s] と [r] S8 [d] S11 [x]|--[e] と [1] S1 [e] および [2] S4 [s] と [nr] S5 [s] と [r] S8 [d] S11 [x]|--[e]、[1]、[3] S1 [e]、[2]、[3] S4 [s]、[nr]、[3] S5 [s]、[r]、[3] S8 [d]、[3] S11 [x] および [3] 24000 [4]|次の表を参照|HY010|NS [c] HY010 [o]|  
  
 [1] エラーがドライバーマネージャーによって返されました。  
  
 [2] エラーはドライバーマネージャーによって返されませんでした。  
  
 [3] 現在の結果が最後または唯一の結果であるか、または現在の結果がありません。 複数の結果の詳細については、「 [複数の結果](../../../odbc/reference/develop-app/multiple-results.md)」を参照してください。  
  
 [4] 現在の結果は最後の結果ではありません。  
  
## <a name="sqlexecdirect-cursor-states"></a>SQLExecDirect (カーソルの状態)  
  
|S5<br /><br /> 開始済み|S6<br /><br /> SQLFetch または SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000 [1]|24000|  
  
 [1] このエラーは、 **Sqlfetch** または **sqlfetchscroll** が SQL_NO_DATA 返されなかった場合にドライバーマネージャーによって返されます。また、 **Sqlfetch** または **sqlfetchscroll** が SQL_NO_DATA を返した場合は、ドライバーによって返されます。  
  
## <a name="sqlexecute"></a>SQLExecute  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|HY010|次の表を参照|S2 [e]、p、および [1] S4 [s]、[p]、[nr]、[1] S5 [s]、[p]、[r]、[1] S8 [d]、[p]、[1] S11 [x]、[p]、[1] 24000 [p]、[2] HY010 [np]|「Cursor states テーブル」を参照してください。|HY010|NS [c] HY010 [o]|  
  
 [1] 現在の結果が最後または唯一の結果であるか、または現在の結果がありません。 複数の結果の詳細については、「 [複数の結果](../../../odbc/reference/develop-app/multiple-results.md)」を参照してください。  
  
 [2] 現在の結果は最後の結果ではありません。  
  
## <a name="sqlexecute-prepared-states"></a>SQLExecute (準備された状態)  
  
|S2<br /><br /> 結果はありません|S3<br /><br /> 結果|  
|-----------------------|--------------------|  
|S4 [s] S8 [d] S11 [x]|S5 [s] S8 [d] S11 [x]|  
  
## <a name="sqlexecute-cursor-states"></a>SQLExecute (カーソルの状態)  
  
|S5<br /><br /> 開始済み|S6<br /><br /> SQLFetch または SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000 [p] HY010 [np]|24000 [p]、[1] HY010 [np]|24000 [p] HY010 [np]|  
  
 [1] このエラーは、 **Sqlfetch** または **sqlfetchscroll** が SQL_NO_DATA 返されなかった場合にドライバーマネージャーによって返されます。また、 **Sqlfetch** または **sqlfetchscroll** が SQL_NO_DATA を返した場合は、ドライバーによって返されます。  
  
## <a name="sqlextendedfetch"></a>SQLExtendedFetch  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|S1010|S1010|24000|次の表を参照|S1010|NS [c] S1010 [o]|  
  
## <a name="sqlextendedfetch-cursor-states"></a>SQLExtendedFetch (カーソルの状態)  
  
|S5<br /><br /> 開始済み|S6<br /><br /> SQLFetch または SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|S7 [s] または [nf] S11 [x]|S1010|--[s] または [nf] S11 [x]|  
  
## <a name="sqlfetch-and-sqlfetchscroll"></a>SQLFetch と SQLFetchScroll  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24000|次の表を参照|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlfetch-and-sqlfetchscroll-cursor-states"></a>SQLFetch および SQLFetchScroll (カーソルの状態)  
  
|S5<br /><br /> 開始済み|S6<br /><br /> SQLFetch または SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|S6 [s] または [nf] S11 [x]|--[s] または [nf] S11 [x]|HY010|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|HY010|HY010|HY010|HY010|HY010|HY010|  
|IH [2]|S0|S0|S0|S0|HY010|HY010|  
|--[3]|--|--|--|--|--|--|  
  
 [1] この行は、 *Handletype* が SQL_HANDLE_ENV または SQL_HANDLE_DBC ときの遷移を示しています。  
  
 [2] この行は、 *Handletype* が SQL_HANDLE_STMT されたときの遷移を示しています。  
  
 [3] この行は、 *Handletype* が SQL_HANDLE_DESC され、記述子が明示的に割り当てられたときの遷移を示しています。  
  
## <a name="sqlfreestmt"></a>SQLFreeStmt  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH [1]|--|--|S1 [np] S2 [p]|S1 [np] S3 [p]|HY010|HY010|  
|IH [2]|--|--|--|--|HY010|HY010|  
  
 [1] *オプション* が SQL_CLOSE されたときの遷移を示しています。  
  
 [2] *オプション* が SQL_UNBIND または SQL_RESET_PARAMS の場合、この行は移行を示しています。 *オプション*の引数が SQL_DROP で、基になるドライバーが ODBC 3.x*ドライバーの*場合、ドライバーマネージャーはこれを、 *handletype*が SQL_HANDLE_STMT に設定された**sqlfreehandle**への呼び出しにマップします。 詳細については、「 [Sqlfreehandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)の遷移テーブル」を参照してください。  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetcursorname"></a>SQLGetCursorName  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|HY010|HY010|  
  
## <a name="sqlgetdata"></a>SQLGetData  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24000|次の表を参照|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlgetdata-cursor-states"></a>SQLGetData (カーソルの状態)  
  
|S5<br /><br /> 開始済み|S6<br /><br /> SQLFetch または SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|--[s] または [nf] S11 [x] 24000 [b] HY109 [i]|--[s] または [nf] S11 [x] 24000 [b] HY109 [i]|  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField と SQLGetDescRec  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--[1] または [2] HY010 [3]|次の表を参照|--[1] または [2] 24000 [3]|--[1]、[2]、または [3] S11 [3] および [x]|HY010|NS [c] または [4] HY010 [o] および [5]|  
  
 [1] *記述子ハンドル* 引数は、APD またはでした。  
  
 [2] *記述子ハンドル* 引数は IPD でした。  
  
 [3] *記述子ハンドル* 引数は IRD でした。  
  
 [4]*記述子ハンドル*引数が、非同期的に実行されている**SQLGetDescField**または**sqlgetdescrec**関数の*記述子ハンドル*引数と同じでした。  
  
 [5]*記述子ハンドル*引数が、非同期的に実行されている**SQLGetDescField**または**sqlgetdescrec**関数の*記述子ハンドル*引数と異なります。  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec-prepared-states"></a>SQLGetDescField と SQLGetDescRec (準備された状態)  
  
|S2<br /><br /> 結果はありません|S3<br /><br /> 結果|  
|-----------------------|--------------------|  
|--[1]、[2]、または [3] S11 [2] と [x]|--[1]、[2]、または [3] S11 [x]|  
  
 [1] *記述子ハンドル* 引数は、APD またはでした。  
  
 [2] *記述子ハンドル* 引数は IPD でした。  
  
 [3] *記述子ハンドル* 引数は IRD でした。 これらの関数は、 *記述子ハンドル* が IRD の場合は、状態 S2 の SQL_NO_DATA を常に返すことに注意してください。  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField と SQLGetDiagRec  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--|--|--|  
|IH [2]|--[3]|--[3]|--|--|--[3]|--[3]|  
  
 [1] この行は、 *Handletype* が SQL_HANDLE_ENV、SQL_HANDLE_DBC、または SQL_HANDLE_DESC の場合の遷移を示しています。  
  
 [2] この行は、 *Handletype* が SQL_HANDLE_STMT されたときの遷移を示しています。  
  
 [3]   **SQLGetDiagField** は、 *DiagIdentifier* が SQL_DIAG_ROW_COUNT 場合、常にこの状態のエラーを返します。  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--[1] 24000 [2]|--[1] 24000 [2]|--[1] 24000 [2]|次の表を参照|HY010|HY010|  
  
 [1] ステートメント属性が SQL_ATTR_ROW_NUMBER ませんでした。  
  
 [2] ステートメント属性が SQL_ATTR_ROW_NUMBER でした。  
  
## <a name="sqlgetstmtattr-cursor-states"></a>SQLGetStmtAttr (カーソルの状態)  
  
|S5<br /><br /> 開始済み|S6<br /><br /> SQLFetch または SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|--[1] 24000 [2]|--[1] または ([v] および [2]) 24000 [b] と [2] HY109 [i] と [2]|--[i] または ([v] および [2]) 24000 [b] と [2] HY109 [1] と [2]|  
  
 [1] *属性* 引数が SQL_ATTR_ROW_NUMBER ませんでした。  
  
 [2] *属性* 引数が SQL_ATTR_ROW_NUMBER でした。  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|--[1]|--[1]|--[s] と [2] S1 [nf]、[np]、および [4] S2 [nf]、[p]、[4] S5 [s] および [3] S11 [x]|S1 [nf]、[np]、[4] S3 [nf]、[p]、[4] S4 [s]、[2] S5 [s] および [3] S11 [x]|HY010|NS [c] HY010 [o]|  
  
 [1] 関数は、常にこの状態の SQL_NO_DATA を返します。  
  
 [2] 次の結果は行数です。  
  
 [3] 次の結果が結果セットになります。  
  
 [4] 現在の結果が最後の結果になります。  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlnumparams"></a>SQLNumParams  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|--[s] S11 [x]|--[s] S11 [x]|--[s] S11 [x]|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlnumresultcols"></a>SQLNumResultCols  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|--[s] S11 [x]|--[s] S11 [x]|--[s] S11 [x]|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlparamdata"></a>SQLParamData  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|HY010|HY010|次の表を参照|NS [c] HY010 [o]|  
  
## <a name="sqlparamdata-need-data-states"></a>SQLParamData (データの状態が必要)  
  
|S8<br /><br /> データが必要|S9<br /><br /> 配置する必要があります|S10<br /><br /> 配置可能|  
|----------------------|---------------------|---------------------|  
|S1 [e] と [1] S2 [e]、[nr]、および [2] S3 [e]、[r]、および [2] S5 [e] および [4] S6 [e] と [5] S7 [e] および [3] S9 [d] S11 [x]|HY010|S1 [e] と [1] S2 [e]、[nr]、および [2] S3 [e]、[r]、および [2] S4 [s]、[nr]、および ([1] または [2]) S5 [s]、[r]、and ([1] または [2]) S5 ([s] または [e]) および [4] S6 ([s] または [e]) と [5] S7 ([s] または [e]) と [3] S9 [d] S11 [x]|  
  
 [1]   **SQLExecDirect** から SQL_NEED_DATA が返されました。  
  
 [2]   **Sqlexecute** によって SQL_NEED_DATA が返されました。  
  
 [3]   **SQLSetPos** が state S7 から呼び出され、SQL_NEED_DATA が返されました。  
  
 [4]   **Sqlbulkoperations** が状態 S5 から呼び出され、SQL_NEED_DATA が返されました。  
  
 [5]   **SQLSetPos** または **sqlbulkoperations** が state S6 から呼び出され、SQL_NEED_DATA が返されました。  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S2 [s] と [nr] S3 [s] と [r] S11 [x]|--[s] または ([e] および [1]) S1 [e] と [2] S11 [x]|S1 [e] および [3] S2 [s]、[nr]、および [3] S3 [s]、[r]、[3] S11 [x]、[3] 24000 [4]|次の表を参照|HY010|NS [c] HY010 [o]|  
  
 [1] ステートメントを検証する以外の理由で準備が失敗しました (SQLSTATE は HY009 [無効な引数値] または HY090 [無効な文字列またはバッファー長])。  
  
 [2] ステートメントの検証中に準備が失敗しました (SQLSTATE は HY009 [無効な引数値] または HY090 [無効な文字列またはバッファー長])。  
  
 [3] 現在の結果が最後または唯一の結果であるか、または現在の結果がありません。 複数の結果の詳細については、「 [複数の結果](../../../odbc/reference/develop-app/multiple-results.md)」を参照してください。  
  
 [4] 現在の結果は最後の結果ではありません。  
  
## <a name="sqlprepare-cursor-states"></a>SQLPrepare (カーソルの状態)  
  
|S5<br /><br /> 開始済み|S6<br /><br /> SQLFetch または SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000|24000|  
  
## <a name="sqlputdata"></a>SQLPutData  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|HY010|HY010|次の表を参照|NS [c] HY010 [o]|  
  
## <a name="sqlputdata-need-data-states"></a>SQLPutData (データの状態が必要)  
  
|S8<br /><br /> データが必要|S9<br /><br /> 配置する必要があります|S10<br /><br /> 配置可能|  
|----------------------|---------------------|---------------------|  
|HY010|S1 [e] と [1] S2 [e]、[nr]、および [2] S3 [e]、[r]、および [2] S5 [e] および [4] S6 [e] と [5] S7 [e] および [3] S10 [s] S11 [x]|--[s] S1 [e] と [1] S2 [e]、[nr]、[2] S3 [e]、[r]、[2] S5 [e]、[4] S6 [e] と [5] S7 [e]、[3] S11 [x] HY011 [6]|  
  
 [1]   **SQLExecDirect** から SQL_NEED_DATA が返されました。  
  
 [2]   **Sqlexecute** によって SQL_NEED_DATA が返されました。  
  
 [3]   **SQLSetPos** が state S7 から呼び出され、SQL_NEED_DATA が返されました。  
  
 [4]   **Sqlbulkoperations** が状態 S5 から呼び出され、SQL_NEED_DATA が返されました。  
  
 [5]   **SQLSetPos** または **sqlbulkoperations** が state S6 から呼び出され、SQL_NEED_DATA が返されました。  
  
 [6] 1 つのパラメーターに対して **Sqlputdata** を1回以上呼び出し SQL_SUCCESS が返されました。その後、同じパラメーターに対して **sqlputdata** の呼び出しが行われ、 *StrLen_or_Ind* が SQL_NULL_DATA に設定されました。  
  
## <a name="sqlrowcount"></a>SQLRowCount  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|HY010|HY010|--|--|HY010|HY010|  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--[2] 24000 [3]|HY010|HY010|  
  
 [1] *属性* が接続属性の場合、この行は遷移を示しています。 *属性*がステートメント属性の場合の移行については、 **SQLSetStmtAttr**のステートメント遷移テーブルを参照してください。  
  
 [2] *属性* 引数が SQL_ATTR_CURRENT_CATALOG ませんでした。  
  
 [3] *属性* 引数が SQL_ATTR_CURRENT_CATALOG でした。  
  
## <a name="sqlsetcursorname"></a>SQLSetCursorName  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|24000|24000|HY010|HY010|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField と SQLSetDescRec  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH [1]|--|--|--|--|HY010|HY010|  
  
 [1] この行には、 *FieldIdentifier*引数が SQL_DESC_ARRAY_STATUS_PTR または SQL_DESC_ROWS_PROCESSED_PTR の場合に、APD、IPD、または ( **SQLSetDescField**) という*記述子ハンドル*引数が使用されている遷移が表示されます。 *FieldIdentifier*がその他の値の場合、IRD に対して**SQLSetDescField**を呼び出すと、エラーになります。  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|HY011|HY011|HY011|HY011|Y011|HY01|HY011|  
  
## <a name="sqlsetpos"></a>SQLSetPos  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24000|次の表を参照|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlsetpos-cursor-states"></a>SQLSetPos (カーソルの状態)  
  
|S5<br /><br /> 開始済み|S6<br /><br /> SQLFetch または SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|--[s] S8 [d] S11 [x] 24000 [b] HY109 [i]|--[s] S8 [d] S11 [x] 24000 [b] HY109 [i]|  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> れる|S5-S7<br /><br /> カーソル|S8-S10<br /><br /> データが必要|S11-S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--[1] HY011 [2]|--[1] 24000 [2]|--[1] 24000 [2]|HY010 [np] または [1] HY011 [p] と [2]|HY010 [np] または [1] HY011 [p] と [2]|  
  
 [1] *属性* 引数が SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE、SQL_ATTR_SIMULATE_CURSOR、SQL_ATTR_USE_BOOKMARKS、SQL_ATTR_CURSOR_SCROLLABLE、または SQL_ATTR_CURSOR_SENSITIVITY ではありませんでした。  
  
 [2] *属性* 引数が SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE、SQL_ATTR_SIMULATE_CURSOR、SQL_ATTR_USE_BOOKMARKS、SQL_ATTR_CURSOR_SCROLLABLE、または SQL_ATTR_CURSOR_SENSITIVITY でした。
