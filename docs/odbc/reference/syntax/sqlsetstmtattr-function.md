---
description: SQLSetStmtAttr 関数
title: SQLSetStmtAttr 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetStmtAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetStmtAttr
helpviewer_keywords:
- SQLSetStmtAttr function [ODBC]
ms.assetid: 7abc5260-733a-48d4-9974-2d1a6a9ea5f6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7572a907a1111e1c6aa96a2761e8551d3265b2d6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421096"
---
# <a name="sqlsetstmtattr-function"></a>SQLSetStmtAttr 関数
**互換性**  
 導入されたバージョン: ODBC 3.0 標準準拠: ISO 92  
  
 **まとめ**  
 **SQLSetStmtAttr** は、ステートメントに関連する属性を設定します。  
  
> [!NOTE]
>  *Odbc 2.x アプリケーションが*odbc *2.x ドライバーで*動作しているときに、ドライバーマネージャーがこの関数をマップする方法の詳細については、「[アプリケーションの下位互換性のための置換関数のマッピング](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLSetStmtAttr(  
     SQLHSTMT      StatementHandle,  
     SQLINTEGER    Attribute,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    StringLength);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル。  
  
 *属性*  
 代入設定するオプション。「コメント」に記載されています。  
  
 *ValuePtr*  
 代入 *属性*に関連付けられる値。 *属性*の値に応じて、 *valueptr*は次のいずれかになります。  
  
-   ODBC 記述子ハンドル。  
  
-   SQLUINTEGER 値です。  
  
-   SQLULEN 値。  
  
-   次のいずれかへのポインター。  
  
    -   Null で終わる文字列。  
  
    -   バイナリバッファーです。  
  
    -   SQLLEN、SQLULEN、または SQLULEN のある型の値または配列。  
  
    -   ドライバーで定義された値。  
  
 *属性*引数がドライバー固有の値の場合、 *valueptr*に符号付き整数を指定できます。  
  
 *StringLength*  
 代入*属性*が ODBC 定義の属性であり、 *valueptr*が文字列またはバイナリバッファーを指している場合、この引数は valueptr の長さである必要があり \* *ValuePtr*ます。 *属性*が ODBC 定義の属性であり、 *valueptr*が整数の場合、 *stringlength*は無視されます。  
  
 *属性*がドライバーで定義された属性の場合、アプリケーションは*stringlength*引数を設定することによって、ドライバーマネージャーに対する属性の性質を示します。 *Stringlength* には次の値を指定できます。  
  
-   *Valueptr*が文字列へのポインターである場合、 *stringlength*は文字列または SQL_NTS の長さを示します。  
  
-   *Valueptr*がバイナリバッファーへのポインターである場合、アプリケーションは、SQL_LEN_BINARY_ATTR (*長さ*) マクロの結果を*stringlength*に配置します。 これにより、 *文字列長*に負の値が挿入されます。  
  
-   *Valueptr*が文字列またはバイナリ文字列以外の値へのポインターである場合、 *stringlength*には SQL_IS_POINTER 値を指定する必要があります。  
  
-   *Valueptr*に固定長の値が含まれている場合は、必要に応じて*stringlength*が SQL_IS_INTEGER か SQL_IS_UINTEGER になります。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **SQLSetStmtAttr**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合、関連付けられた SQLSTATE 値は、 *Handletype* SQL_HANDLE_STMT と*StatementHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出すことによって取得できます。 次の表に、 **SQLSetStmtAttr** によって一般的に返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01S02|オプションの値が変更されました|ドライバーが *Valueptr*に指定された値をサポートしていないか、または *valueptr* に指定された値が実装の動作条件により無効であったため、ドライバーは同様の値に置き換えられました。 (**SQLGetStmtAttr** は、一時的に置き換えられる値を決定するために呼び出すことができます。)代替値は、カーソルが閉じられるまで *StatementHandle* に対して有効です。この時点で、statement 属性は前の値に戻ります。 変更できるステートメント属性は次のとおりです。<br /><br /> SQL_ ATTR_CONCURRENCY SQL_ ATTR_CURSOR_TYPE SQL_ ATTR_KEYSET_SIZE SQL_ ATTR_MAX_LENGTH SQL_ ATTR_MAX_ROWS SQL_ ATTR_QUERY_TIMEOUT SQL_ATTR_ROW_ARRAY_SIZE SQL_ ATTR_SIMULATE_CURSOR<br /><br /> (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続されていたデータソースとの間の通信リンクが失敗しました。|  
|24000|カーソル状態が無効|*属性*が SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE、SQL_ATTR_SIMULATE_CURSOR、または SQL_ATTR_USE_BOOKMARKS で、カーソルが開いていました。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * \* Messagetext*バッファーの**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY009|Null ポインターの使い方が正しくありません|*属性*引数が文字列属性を必要とし、 *valueptr*引数が null ポインターであるステートメント属性を識別しました。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、 **SQLSetStmtAttr** 関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または **Sqlmoreresults** が *StatementHandle* に対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。<br /><br /> (DM) 非同期的に実行する関数が *StatementHandle* に対して呼び出されましたが、この関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **Sqlbulkoperations**、 **SQLSetPos** が *StatementHandle* に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。|  
|HY011|属性を今設定することはできません|*属性*が SQL_ATTR_CONCURRENCY、SQL_ ATTR_CURSOR_TYPE、SQL_ ATTR_SIMULATE_CURSOR、または SQL_ ATTR_USE_BOOKMARKS で、ステートメントが準備されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY017|自動的に割り当てられた記述子ハンドルの使い方が正しくありません|(DM) *属性* 引数が SQL_ATTR_IMP_ROW_DESC または SQL_ATTR_IMP_PARAM_DESC でした。<br /><br /> (DM) *属性* 引数が SQL_ATTR_APP_ROW_DESC または SQL_ATTR_APP_PARAM_DESC でした。 *valueptr* の値は、APD またはに最初に割り当てられたハンドル以外の、暗黙的に割り当てられた記述子ハンドルでした。|  
|HY024|無効な属性値|指定された *属性* 値が指定されている場合、 *valueptr*に無効な値が指定されています。 (ドライバーマネージャーは、SQL_ATTR_ACCESS_MODE や SQL_ ATTR_ASYNC_ENABLE などの個別の値のセットを受け入れる接続属性とステートメント属性に対してのみ、この SQLSTATE を返します。 他のすべての接続属性およびステートメント属性では、ドライバーは *Valueptr*に指定された値を確認する必要があります)。<br /><br /> *属性*引数が SQL_ATTR_APP_ROW_DESC または SQL_ATTR_APP_PARAM_DESC でしたが、 *Valueptr*は、 *StatementHandle*引数と同じ接続上にない明示的に割り当てられた記述子ハンドルでした。|  
|HY090|文字列またはバッファーの長さが無効です|(DM) * \* valueptr*は文字列であり、 *stringlength*引数は0未満ですが SQL_NTS ませんでした。|  
|HY092|属性またはオプションの識別子が無効です|(DM) 引数 *属性* に指定された値は、ドライバーでサポートされている ODBC のバージョンでは無効です。<br /><br /> (DM) 引数 *属性* に指定された値は読み取り専用属性でした。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYC00|省略可能な機能は実装されていません|引数 *属性* に指定された値は、ドライバーでサポートされている odbc のバージョンに対して有効な odbc ステートメント属性でしたが、ドライバーではサポートされていませんでした。<br /><br /> *属性*引数が SQL_ATTR_ASYNC_ENABLE、SQL_ASYNC_MODE の*InfoType*を持つ**SQLGetInfo**を呼び出すと SQL_AM_CONNECTION が返されます。<br /><br /> *属性*引数が SQL_ATTR_ENABLE_AUTO_IPD ましたが、接続属性 SQL_ATTR_AUTO_IPD の値が SQL_FALSE でした。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle* に関連付けられているドライバーでは、関数はサポートされていません。|  
|S1118|ドライバーは非同期通知をサポートしていません|SQL_ATTR_ASYNC_STMT_EVENT を設定するために **SQLSetStmtAttr** を呼び出した場合非同期通知は、ドライバーではサポートされていません。|  
  
## <a name="comments"></a>コメント  
 ステートメントのステートメント属性は、 **SQLSetStmtAttr** への別の呼び出しによって変更されるか、 **sqlfreehandle**を呼び出すことによってステートメントが削除されるまで、有効なままになります。 SQL_CLOSE、SQL_UNBIND、または SQL_RESET_PARAMS オプションを使用して **SQLFreeStmt** を呼び出すと、ステートメントの属性はリセットされません。  
  
 一部のステートメント属性では、データソースが *Valueptr*に指定された値をサポートしていない場合に、類似した値の置換がサポートされます。 このような場合、ドライバーは SQL_SUCCESS_WITH_INFO と SQLSTATE 01S02 (オプション値が変更されました) を返します。 たとえば、 *属性* が SQL_ATTR_CONCURRENCY、 *valueptr* が SQL_CONCUR_ROWVER であり、データソースがこれをサポートしていない場合、ドライバーは SQL_CONCUR_VALUES に置き換えられ SQL_SUCCESS_WITH_INFO を返します。 置き換えられた値を特定するために、アプリケーションは **SQLGetStmtAttr**を呼び出します。  
  
 *Valueptr*で設定される情報の形式は、指定された*属性*によって異なります。 **SQLSetStmtAttr** は、2つの異なる形式 (文字列または整数値) のいずれかで属性情報を受け取ります。 各の形式は、属性の説明に記載されています。 この形式は、 **SQLGetStmtAttr**の各属性に対して返される情報に適用されます。 **SQLSetStmtAttr**の*valueptr*引数によってポイントされる文字列は、*文字列長*の長さを持ちます。  
  
> [!NOTE]
>  ODBC 3.x では、 **SQLSetConnectAttr**を呼び出して、接続レベルでステートメント属性を設定する機能が非推奨とされまし*た。* ODBC *3. x* アプリケーションでは、接続レベルでステートメント属性を設定しないでください。 ODBC *3. x* ステートメントの属性は、接続レベルでは設定できません。ただし、接続属性とステートメント属性の両方である SQL_ATTR_METADATA_ID および SQL_ATTR_ASYNC_ENABLE 属性は、接続レベルまたはステートメントレベルのどちらかで設定できます。  
> 
> [!NOTE]
>  Odbc *3.x ドライバーで* は *、odbc 2.x アプリケーションを* 接続レベルで設定 *する odbc 2.x* アプリケーションを使用する必要がある場合にのみ、この機能をサポートする必要があります。 詳細については、「付録 G: 旧バージョンとの互換性のためのドライバーガイドライン」の「 [SQLSetConnectOption Mapping](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) 」の「接続レベルでのステートメントオプションの設定」を参照してください。  
  
## <a name="statement-attributes-that-set-descriptor-fields"></a>記述子フィールドを設定するステートメント属性  
 多くのステートメント属性は、記述子のヘッダーフィールドに対応しています。 これらの属性を設定すると、実際には記述子フィールドの設定になります。 **SQLSetDescField**ではなく**SQLSetStmtAttr**を呼び出すことによってフィールドを設定すると、その関数呼び出しに対して記述子ハンドルを取得する必要がないという利点があります。  
  
> [!CAUTION]  
>  あるステートメントに対して **SQLSetStmtAttr** を呼び出すと、他のステートメントに影響を与える可能性があります。 このエラーは、ステートメントに関連付けられている APD またはが明示的に割り当てられ、他のステートメントにも関連付けられている場合に発生します。 **SQLSetStmtAttr**は APD またはを変更するため、この記述子が関連付けられているすべてのステートメントに変更が適用されます。 これが必要な動作でない場合は、 **SQLSetStmtAttr**を再度呼び出す前に、アプリケーションで他のステートメントとこの記述子の関連付けを解除する必要があります ( **SQLSetStmtAttr**を呼び出すことによって、SQL_ATTR_APP_ROW_DESC または SQL_ATTR_APP_PARAM_DESC フィールドを別の記述子ハンドルに設定します)。  
  
 対応するステートメント属性が設定された結果として記述子フィールドが設定されている場合、このフィールドは、 *StatementHandle* 引数によって識別されるステートメントに現在関連付けられている適用可能な記述子に対してのみ設定されます。また、属性の設定は、今後そのステートメントに関連付けられる記述子には影響しません。 ステートメント属性でもある記述子フィールドが **SQLSetDescField**の呼び出しによって設定されている場合は、対応するステートメント属性が設定されます。 明示的に割り当てられた記述子がステートメントから関連付けられていない場合、ヘッダーフィールドに対応するステートメント属性は、暗黙的に割り当てられた記述子内のフィールドの値に戻ります。  
  
 ステートメントが割り当てられると (「 [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)」を参照)、4つの記述子ハンドルが自動的に割り当てられ、ステートメントに関連付けられます。 明示的に割り当てられた記述子ハンドルは、 **SQLAllocHandle** を *fhandletype* SQL_HANDLE_DESC と共に呼び出して記述子ハンドルを割り当ててから、 **SQLSetStmtAttr** を呼び出して記述子ハンドルをステートメントに関連付けることによって、ステートメントに関連付けることができます。  
  
 次の表のステートメント属性は、記述子ヘッダーのフィールドに対応しています。  
  
|Statement 属性|ヘッダーフィールド|順.|  
|-------------------------|------------------|-----------|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_DESC_BIND_OFFSET_PTR|APD|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_DESC_BIND_TYPE|APD|  
|SQL_ATTR_PARAM_OPERATION_PTR|SQL_DESC_ARRAY_STATUS_PTR|APD|  
|SQL_ATTR_PARAM_STATUS_PTR|SQL_DESC_ARRAY_STATUS_PTR|IPD|  
|SQL_ATTR_PARAMS_PROCESSED_PTR|SQL_DESC_ROWS_PROCESSED_PTR|IPD|  
|SQL_ATTR_PARAMSET_SIZE|SQL_DESC_ARRAY_SIZE|APD|  
|SQL_ATTR_ROW_ARRAY_SIZE|SQL_DESC_ARRAY_SIZE|ブロ|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR|SQL_DESC_BIND_OFFSET_PTR|ブロ|  
|SQL_ATTR_ROW_BIND_TYPE|SQL_DESC_BIND_TYPE|ブロ|  
|SQL_ATTR_ROW_OPERATION_PTR|SQL_DESC_ARRAY_STATUS_PTR|ブロ|  
|SQL_ATTR_ROW_STATUS_PTR|SQL_DESC_ARRAY_STATUS_PTR|IRD|  
|SQL_ATTR_ROWS_FETCHED_PTR|SQL_DESC_ROWS_PROCESSED_PTR|IRD|  
  
## <a name="statement-attributes"></a>ステートメント属性  
 次の表に、現在定義されている属性と ODBC のバージョンを示します。さまざまなデータソースを利用するために、ドライバーによってより多くの属性が定義されることが予想されます。 属性の範囲は ODBC によって予約されています。ドライバー開発者は、オープングループから独自のドライバー固有の使用のために値を予約する必要があります。 詳細については、「 [ドライバー固有のデータ型、記述子の型、情報の種類、診断の種類、および属性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)」を参照してください。  
  
|属性|*Valueptr* コンテンツ|  
|---------------|-------------------------|  
|SQL_ATTR_APP_PARAM_DESC (ODBC 3.0)|ステートメントハンドルで **Sqlexecute** と **SQLExecDirect** を呼び出すための APD へのハンドル。 この属性の初期値は、ステートメントが最初に割り当てられたときに暗黙的に割り当てられた記述子です。 この属性の値が SQL_NULL_DESC に設定されている場合、または最初に記述子に割り当てられたハンドルである場合、ステートメントハンドルに関連付けられていた明示的に割り当てられた APD handle はそのハンドルから関連付けが解除され、ステートメントハンドルは暗黙的に割り当てられた APD ハンドルに戻ります。<br /><br /> この属性を、別のステートメントまたは同じステートメントで暗黙的に設定された別の記述子ハンドルに暗黙的に割り当てられた記述子ハンドルに設定することはできません。暗黙的に割り当てられた記述子ハンドルを複数のステートメントまたは記述子ハンドルに関連付けることはできません。|  
|SQL_ATTR_APP_ROW_DESC (ODBC 3.0)|ステートメントハンドルの後続のフェッチのためののハンドル。 この属性の初期値は、ステートメントが最初に割り当てられたときに暗黙的に割り当てられた記述子です。 この属性の値が SQL_NULL_DESC に設定されている場合、または最初に記述子に割り当てられたハンドルである場合、ステートメントハンドルに関連付けられていた、明示的に割り当てられたハンドルは関連付け解除され、ステートメントハンドルは暗黙的に割り当てられたハンドルに戻ります。<br /><br /> この属性を、別のステートメントまたは同じステートメントで暗黙的に設定された別の記述子ハンドルに暗黙的に割り当てられた記述子ハンドルに設定することはできません。暗黙的に割り当てられた記述子ハンドルを複数のステートメントまたは記述子ハンドルに関連付けることはできません。|  
|SQL_ATTR_ASYNC_ENABLE (ODBC 1.0)|指定したステートメントで呼び出された関数が非同期に実行されるかどうかを指定する SQLULEN 値。<br /><br /> SQL_ASYNC_ENABLE_OFF = ステートメントレベルの非同期実行サポートを無効にします (既定)。<br /><br /> SQL_ASYNC_ENABLE_ON = ステートメントレベルの非同期実行サポートを有効にします。<br /><br /> 詳細については、「 [非同期実行 (ポーリングメソッド)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)」を参照してください。<br /><br /> ステートメントレベルの非同期実行がサポートされているドライバーの場合、ステートメント属性 SQL_ATTR_ASYNC_ENABLE は読み取り専用です。 この値は、ステートメントハンドルが割り当てられたときと同じ名前を持つ接続レベル属性の値と同じです。<br /><br /> **SQLSetStmtAttr**を呼び出して、SQL_ASYNC_MODE *InfoType*が返され SQL_AM_CONNECTION が SQLSTATE HYC00 を返したときに SQL_ATTR_ASYNC_ENABLE を設定します (省略可能な機能は実装されていません)。 詳細については、「 [SQLSetConnectAttr 関数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) 」を参照してください。|  
|SQL_ATTR_ASYNC_STMT_EVENT (ODBC 3.8)|イベントハンドルである SQLPOINTER 値。<br /><br /> 非同期関数の完了通知は、 **SQLSetStmtAttr** を呼び出して **SQL_ATTR_ASYNC_STMT_EVENT** 属性を設定し、イベントハンドルを指定することによって有効になります。|  
|SQL_ATTR_ASYNC_STMT_PCALLBACK (ODBC 3.8)|非同期コールバック関数への SQLPOINTER。<br /><br /> ドライバーマネージャーだけが、この属性を使用してドライバーの **SQLSetStmtAttr** 関数を呼び出すことができます。|  
|SQL_ATTR_ASYNC_STMT_PCONTEXT (ODBC 3.8)|コンテキスト構造への SQLPOINTER<br /><br /> ドライバーマネージャーだけが、この属性を使用してドライバーの **SQLSetStmtAttr** 関数を呼び出すことができます。|  
|SQL_ATTR_CONCURRENCY (ODBC 2.0)|カーソルの同時実行を指定する SQLULEN 値。<br /><br /> SQL_CONCUR_READ_ONLY = カーソルは読み取り専用です。 更新は許可されていません。<br /><br /> SQL_CONCUR_LOCK = カーソルは、行を更新できるように、十分なロックレベルを使用します。<br /><br /> SQL_CONCUR_ROWVER = カーソルは、オプティミスティック同時実行制御を使用して、SQLBase ROWID や Sybase TIMESTAMP などの行バージョンを比較します。<br /><br /> SQL_CONCUR_VALUES = カーソルはオプティミスティック同時実行制御を使用して、値を比較します。<br /><br /> SQL_ATTR_CONCURRENCY の既定値は SQL_CONCUR_READ_ONLY です。<br /><br /> この属性は、開いているカーソルには指定できません。 詳細については、「 [同時実行の型](../../../odbc/reference/develop-app/concurrency-types.md)」を参照してください。<br /><br /> SQL_ATTR_CURSOR_TYPE *属性* が SQL_ATTR_CONCURRENCY の現在の値をサポートしていない型に変更された場合は、実行時に SQL_ATTR_CONCURRENCY の値が変更され、 **SQLExecDirect** または **SQLPrepare** が呼び出されたときに警告が発行されます。<br /><br /> ドライバーが **SELECT FOR UPDATE** ステートメントをサポートしているときに、SQL_ATTR_CONCURRENCY の値が SQL_CONCUR_READ_ONLY に設定されているときにステートメントが実行されると、エラーが返されます。 SQL_ATTR_CONCURRENCY の値が、ドライバーが SQL_ATTR_CURSOR_TYPE の一部の値に対してサポートしている値に変更され SQL_ATTR_CURSOR_TYPE の現在の値ではない場合、SQL_ATTR_CURSOR_TYPE の値は実行時に変更され、SQLSTATE 01S02 (オプションの値が変更されました) は、 **SQLExecDirect** または **SQLPrepare** が呼び出されたときに発行されます。<br /><br /> 指定された同時実行がデータソースでサポートされていない場合、ドライバーは別の同時実行を置き換え、SQLSTATE 01S02 (オプションの値が変更されました) を返します。 SQL_CONCUR_VALUES の場合、ドライバーは SQL_CONCUR_ROWVER に置き換えられます。また、その逆も同様です。 SQL_CONCUR_LOCK の場合、ドライバーは、順に、SQL_CONCUR_ROWVER または SQL_CONCUR_VALUES に置き換えます。 置換された値の有効性は、実行時までチェックされません。<br /><br /> SQL_ATTR_CONCURRENCY とその他のカーソル属性の関係の詳細については、「 [カーソルの特性とカーソルの種類](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)」を参照してください。|  
|SQL_ATTR_CURSOR_SCROLLABLE (ODBC 3.0)|アプリケーションが必要とするサポートレベルを指定する SQLULEN 値。 この属性を設定すると、 **SQLExecDirect** と **sqlexecute**の後続の呼び出しに影響します。<br /><br /> SQL_NONSCROLLABLE = スクロール可能なカーソルは、ステートメントハンドルでは必要ありません。 アプリケーションがこのハンドルで **Sqlfetchscroll** を呼び出す場合、 *fetchorientation* の有効な値は SQL_FETCH_NEXT だけです。 これは既定値です。<br /><br /> SQL_SCROLLABLE = スクロール可能なカーソルがステートメントハンドルに必要です。 **Sqlfetchscroll**を呼び出すと、アプリケーションで任意の有効な*fetchorientation*値を指定して、シーケンシャルモード以外のモードでカーソルを配置できます。<br /><br /> スクロール可能なカーソルの詳細については、「スクロール可能な [カーソル](../../../odbc/reference/develop-app/scrollable-cursors.md)」を参照してください。 SQL_ATTR_CURSOR_SCROLLABLE とその他のカーソル属性の関係の詳細については、「[カーソルの特性とカーソルの種類](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)」を参照してください。|  
|SQL_ATTR_CURSOR_SENSITIVITY (ODBC 3.0)|ステートメントハンドルのカーソルが別のカーソルによって結果セットに加えられた変更を表示するかどうかを指定する SQLULEN 値。 この属性を設定すると、 **SQLExecDirect** と **sqlexecute**の後続の呼び出しに影響します。 アプリケーションでは、この属性の値を読み取って、初期状態またはアプリケーションによって最後に設定された状態を取得することができます。<br /><br /> SQL_UNSPECIFIED = カーソルの種類が指定されていないこと、およびステートメントハンドルのカーソルによって別のカーソルによって結果セットに加えられた変更が表示されるかどうかを指定します。 ステートメントハンドルのカーソルによって、none、some、またはすべての変更が表示される場合があります。 これは既定値です。<br /><br /> SQL_INSENSITIVE = ステートメントハンドルのすべてのカーソルは、他のカーソルによって行われた変更を反映せずに結果セットを表示します。 非依存カーソルは読み取り専用です。 これは、読み取り専用の同時実行を持つ静的カーソルに対応します。<br /><br /> SQL_SENSITIVE = ステートメントハンドルのすべてのカーソルは、別のカーソルによって結果セットに対して行われたすべての変更を表示します。<br /><br /> SQL_ATTR_CURSOR_SENSITIVITY とその他のカーソル属性の関係の詳細については、「 [カーソルの特性とカーソルの種類](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)」を参照してください。|  
|SQL_ATTR_CURSOR_TYPE (ODBC 2.0)|カーソルの種類を指定する SQLULEN 値。<br /><br /> SQL_CURSOR_FORWARD_ONLY = カーソルは前方にのみスクロールします。<br /><br /> SQL_CURSOR_STATIC = 結果セットのデータは静的です。<br /><br /> SQL_CURSOR_KEYSET_DRIVEN = ドライバーは、SQL_ATTR_KEYSET_SIZE statement 属性で指定された行数のキーを保存して使用します。<br /><br /> SQL_CURSOR_DYNAMIC = ドライバーは、行セット内の行のキーのみを保存して使用します。<br /><br /> 既定値は SQL_CURSOR_FORWARD_ONLY です。 SQL ステートメントが準備された後に、この属性を指定することはできません。<br /><br /> 指定されたカーソルの種類がデータソースでサポートされていない場合、ドライバーは別の種類のカーソルを置き換え、SQLSTATE 01S02 (オプションの値が変更されました) を返します。 混合カーソルまたは動的カーソルの場合、ドライバーはキーセットドリブンカーソルまたは静的カーソルを順番に置き換えます。 キーセットドリブンカーソルの場合、ドライバーは静的カーソルに置き換えられます。<br /><br /> スクロール可能なカーソルの種類の詳細については、「スクロール可能な [カーソルの種類](../../../odbc/reference/develop-app/scrollable-cursor-types.md)」を参照してください。 SQL_ATTR_CURSOR_TYPE とその他のカーソル属性の関係の詳細については、「 [カーソルの特性とカーソルの種類](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)」を参照してください。|  
|SQL_ATTR_ENABLE_AUTO_IPD (ODBC 3.0)|IPD の自動作成が実行されるかどうかを指定する SQLULEN 値:<br /><br /> SQL_TRUE = **SQLPrepare**の呼び出し後の IPD の自動作成をオンにします。 SQL_FALSE = **SQLPrepare**の呼び出し後の IPD の自動作成をオフにします。 (サポートされている場合、アプリケーションは **SQLDescribeParam**を呼び出すことによって IPD フィールド情報を取得できます)。ステートメント属性 SQL_ATTR_ENABLE_AUTO_IPD の既定値は SQL_FALSE です。 詳細については、「 [IPD の自動作成](../../../odbc/reference/develop-app/automatic-population-of-the-ipd.md)」を参照してください。|  
|SQL_ATTR_FETCH_BOOKMARK_PTR (ODBC 3.0)|\*バイナリブックマーク値を指す SQLLEN。 SQL_FETCH_BOOKMARK に等しい*Ffetchorientation*を使用して**sqlfetchscroll**を呼び出すと、ドライバーはこのフィールドからブックマーク値を取得します。 このフィールドの既定値は null ポインターです。 詳細については、「 [ブックマークによるスクロール](../../../odbc/reference/develop-app/scrolling-by-bookmark.md)」を参照してください。<br /><br /> このフィールドでポイントされている値は、行セットバッファーにキャッシュされているブックマークを使用する、 **Sqlbulkoperations**のブックマーク、ブックマークによる更新、またはブックマーク操作によるフェッチでは使用されません。|  
|SQL_ATTR_IMP_PARAM_DESC (ODBC 3.0)|IPD へのハンドル。 この属性の値は、ステートメントが最初に割り当てられたときに割り当てられた記述子です。 アプリケーションでこの属性を設定することはできません。<br /><br /> この属性は、 **SQLGetStmtAttr** を呼び出すことによって取得できますが、 **SQLSetStmtAttr**を呼び出すことによって設定することはできません。|  
|SQL_ATTR_IMP_ROW_DESC (ODBC 3.0)|IRD へのハンドル。 この属性の値は、ステートメントが最初に割り当てられたときに割り当てられた記述子です。 アプリケーションでこの属性を設定することはできません。<br /><br /> この属性は、 **SQLGetStmtAttr** を呼び出すことによって取得できますが、 **SQLSetStmtAttr**を呼び出すことによって設定することはできません。|  
|SQL_ATTR_KEYSET_SIZE (ODBC 2.0)|キーセットドリブンカーソルのキーセットの行数を指定する SQLULEN。 キーセットのサイズが 0 (既定値) の場合、カーソルは完全キーセットドリブンです。 キーセットのサイズが0より大きい場合、カーソルは混合されています (キーセットとキーセットの外部にあります)。 既定のキーセットサイズは0です。 キーセットドリブンカーソルの詳細については、「 [キーセットドリブンカーソル](../../../odbc/reference/develop-app/keyset-driven-cursors.md)」を参照してください。<br /><br /> 指定されたサイズが最大キーセットサイズを超えた場合、ドライバーはそのサイズに置き換えられ、SQLSTATE 01S02 (オプション値が変更されました) を返します。<br /><br /> **Sqlfetch** または **sqlfetchscroll** は、キーセットのサイズが0より大きく、行セットのサイズよりも小さい場合に、エラーを返します。|  
|SQL_ATTR_MAX_LENGTH (ODBC 1.0)|ドライバーが文字またはバイナリ列から返すデータの最大量を指定する SQLULEN 値。 *Valueptr*が使用可能なデータの長さよりも小さい場合、 **Sqlfetch**または**SQLGetData**はデータを切り捨て、SQL_SUCCESS を返します。 *Valueptr*が 0 (既定値) の場合、ドライバーは使用可能なすべてのデータを返します。<br /><br /> 指定された長さが、データソースが返すことができるデータの最小量よりも小さい場合、またはデータソースが返すことができるデータの最大量よりも大きい場合、ドライバーはその値を置き換え、SQLSTATE 01S02 (オプション値が変更されました) を返します。<br /><br /> この属性の値は、開いているカーソルに設定できます。ただし、この設定はすぐには有効にならない場合があります。この場合、ドライバーは SQLSTATE 01S02 (オプション値が変更されました) を返し、属性を元の値にリセットします。<br /><br /> この属性はネットワークトラフィックを削減するためのものであり、多層ドライバーのデータソース (ドライバーではなく) で実装できる場合にのみサポートする必要があります。 アプリケーションでは、このメカニズムを使用してデータを切り捨てることはできません。受信したデータを切り捨てるには、アプリケーションで、 **SQLBindCol**または**SQLGetData**の*bufferlength*引数に最大バッファー長を指定する必要があります。|  
|SQL_ATTR_MAX_ROWS (ODBC 1.0)|**SELECT**ステートメントのアプリケーションに返す行の最大数に対応する SQLULEN 値。 \* *Valueptr*が 0 (既定値) の場合、ドライバーはすべての行を返します。<br /><br /> この属性は、ネットワークトラフィックを減らすことを目的としています。 概念的には、結果セットが作成されるときに適用され、結果セットを最初の *Valueptr* 行に限定します。 結果セットの行数が *Valueptr*よりも大きい場合、結果セットは切り捨てられます。<br /><br /> SQL_ATTR_MAX_ROWS は、カタログ関数によって返されるものを含め、 *ステートメント*のすべての結果セットに適用されます。 カーソルの行数の値に対して最大値を設定 SQL_ATTR_MAX_ROWS。<br /><br /> ドライバーは、SQL_ATTR_MAX_ROWS が適切に実装されることを保証できない場合に、 **sqlfetch** または **sqlfetchscroll** の SQL_ATTR_MAX_ROWS 動作をエミュレートしないようにする必要があります (結果セットのサイズの制限をデータソースで実装することはできません)。<br /><br /> SQL_ATTR_MAX_ROWS が SELECT ステートメント以外のステートメント (カタログ関数など) に適用されるかどうかはドライバーによって定義されます。<br /><br /> この属性の値は、開いているカーソルに設定できます。ただし、この設定はすぐには有効にならない場合があります。この場合、ドライバーは SQLSTATE 01S02 (オプション値が変更されました) を返し、属性を元の値にリセットします。|  
|SQL_ATTR_METADATA_ID (ODBC 3.0)|カタログ関数の文字列引数の処理方法を決定する SQLULEN 値。<br /><br /> SQL_TRUE の場合、カタログ関数の文字列引数は識別子として扱われます。 大文字と小文字は区別されません。 区切られていない文字列の場合、ドライバーは末尾のスペースを削除し、文字列は大文字に折りたたまれます。 区切られた文字列の場合、ドライバーは先頭または末尾のスペースを削除し、区切り記号の間にある任意のものを文字どおりに取ります。 これらの引数のいずれかが null ポインターに設定されている場合、関数は SQL_ERROR と SQLSTATE HY009 (null ポインターの無効な使用) を返します。<br /><br /> SQL_FALSE した場合、カタログ関数の文字列引数は識別子として扱われません。 大文字と小文字は区別されます。 引数によっては、文字列検索パターンを含むかどうかを指定できます。<br /><br /> 既定値は SQL_FALSE です。<br /><br /> 値の一覧を取得する**Sqltables**の*TableType*引数は、この属性の影響を受けません。<br /><br /> 接続レベルで SQL_ATTR_METADATA_ID を設定することもできます。 (It および SQL_ATTR_ASYNC_ENABLE は、接続属性でもある唯一のステートメント属性です)。<br /><br /> 詳細については、「 [カタログ関数の引数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)」を参照してください。|  
|SQL_ATTR_NOSCAN (ODBC 1.0)|ドライバーがエスケープシーケンスの SQL 文字列をスキャンする必要があるかどうかを示す SQLULEN 値。<br /><br /> SQL_NOSCAN_OFF = ドライバーは、SQL 文字列をスキャンしてエスケープシーケンス (既定値) にします。<br /><br /> SQL_NOSCAN_ON = ドライバーは、エスケープシーケンスの SQL 文字列をスキャンしません。 代わりに、ドライバーによってステートメントがデータソースに直接送信されます。<br /><br /> 詳細については、「 [ODBC でのエスケープシーケンス](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)」を参照してください。|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR (ODBC 3.0)|動的パラメーターのバインドを変更するポインターに追加されたオフセットを指す SQLULEN * 値。 このフィールドが null 以外の場合、ドライバーはポインターを逆参照し、逆参照された値を記述子レコードの各遅延フィールド (SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、および SQL_DESC_OCTET_LENGTH_PTR) に追加し、バインド時に新しいポインター値を使用します。 既定では null に設定されています。<br /><br /> バインドオフセットは、常に、SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、および SQL_DESC_OCTET_LENGTH_PTR の各フィールドに直接追加されます。 オフセットが別の値に変更された場合でも、新しい値は記述子フィールドの値に直接追加されます。 新しいオフセットは、フィールド値に前のオフセットと共に追加されることはありません。<br /><br /> 詳細については、「 [パラメーターバインドオフセット](../../../odbc/reference/develop-app/parameter-binding-offsets.md)」を参照してください。<br /><br /> このステートメント属性を設定すると、APD ヘッダーの SQL_DESC_BIND_OFFSET_PTR フィールドが設定されます。|  
|SQL_ATTR_PARAM_BIND_TYPE (ODBC 3.0)|動的パラメーターに使用されるバインディング方向を示す SQLULEN 値。<br /><br /> このフィールドは SQL_PARAM_BIND_BY_COLUMN (既定) に設定され、列方向のバインドを選択します。<br /><br /> 行方向のバインドを選択するには、このフィールドに、一連の動的パラメーターにバインドされる構造体またはバッファーのインスタンスの長さを設定します。 この長さには、バインドされたすべてのパラメーターの領域と、構造体またはバッファーの埋め込みが含まれる必要があります。これにより、バインドされたパラメーターのアドレスが指定された長さでインクリメントされた場合、結果は次のパラメーターのセットで同じパラメーターの先頭をポイントします。 ANSI C で *sizeof* 演算子を使用すると、この動作は保証されます。<br /><br /> 詳細については、「 [パラメーターの配列のバインド](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)」を参照してください。<br /><br /> このステートメント属性を設定すると、APD ヘッダーの SQL_DESC_ BIND_TYPE フィールドが設定されます。|  
|SQL_ATTR_PARAM_OPERATION_PTR (ODBC 3.0)|\*SQL ステートメントの実行中にパラメーターを無視するために使用される sqlus悪意のある値の配列を指す sqlus悪意のある値。 各値は SQL_PARAM_PROCEED (実行するパラメーターの場合) または SQL_PARAM_IGNORE (パラメーターを無視する場合) のいずれかに設定されます。<br /><br /> APD 内の SQL_DESC_ARRAY_STATUS_PTR が指す配列の status 値を SQL_PARAM_IGNORE に設定することによって、処理中に一連のパラメーターを無視できます。 状態値が SQL_PARAM_PROCEED に設定されている場合、または配列内の要素が設定されていない場合は、一連のパラメーターが処理されます。<br /><br /> このステートメント属性は null ポインターに設定できます。この場合、ドライバーはパラメーターステータス値を返しません。 この属性はいつでも設定できますが、次に **SQLExecDirect** または **sqlexecute** が呼び出されるまで、新しい値は使用されません。<br /><br /> バインドされたパラメーターがない場合、この属性は無視されます。<br /><br /> 詳細については、「 [パラメーターの配列の使用](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)」を参照してください。<br /><br /> このステートメント属性を設定すると、APD ヘッダーの SQL_DESC_ARRAY_STATUS_PTR フィールドが設定されます。|  
|SQL_ATTR_PARAM_STATUS_PTR (ODBC 3.0)|\* **Sqlexecute**または**SQLExecDirect**の呼び出し後に、パラメーター値の各行の状態情報を含む sqlus悪意のある値の配列を指す sqlus悪意のある値。 このフィールドは、PARAMSET_SIZE が1より大きい場合にのみ必要です。<br /><br /> 状態の値には、次の値を含めることができます。<br /><br /> SQL_PARAM_SUCCESS: このパラメーターのセットに対して SQL ステートメントが正常に実行されました。<br /><br /> SQL_PARAM_SUCCESS_WITH_INFO: このパラメーターのセットに対して SQL ステートメントが正常に実行されました。ただし、警告情報は診断データ構造で使用できます。<br /><br /> SQL_PARAM_ERROR: この一連のパラメーターを処理中にエラーが発生しました。 診断データ構造では、追加のエラー情報を利用できます。<br /><br /> SQL_PARAM_UNUSED: このパラメーターセットは使用されていませんでした。以前のパラメーターセットによって、後続の処理を中止したエラーが発生したか、または SQL_ATTR_PARAM_OPERATION_PTR によって指定された配列のパラメーターセットに SQL_PARAM_IGNORE が設定されていることが原因である可能性があります。<br /><br /> SQL_PARAM_DIAG_UNAVAILABLE: ドライバーは、パラメーターの配列をモノリシック単位として処理するため、このレベルのエラー情報は生成されません。<br /><br /> このステートメント属性は null ポインターに設定できます。この場合、ドライバーはパラメーターステータス値を返しません。 この属性はいつでも設定できますが、次に **Sqlexecute** または **SQLExecDirect** が呼び出されるまで、新しい値は使用されません。 この属性を設定すると、ドライバーによって実装される出力パラメーターの動作に影響することがあります。<br /><br /> 詳細については、「 [パラメーターの配列の使用](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)」を参照してください。<br /><br /> このステートメント属性を設定すると、IPD ヘッダーの SQL_DESC_ARRAY_STATUS_PTR フィールドが設定されます。|  
|SQL_ATTR_PARAMS_PROCESSED_PTR (ODBC 3.0)|\*エラーセットを含む、処理されたパラメーターのセットの数を返すバッファーを指す SQLULEN レコードフィールド。 Null ポインターの場合、数値は返されません。<br /><br /> このステートメント属性を設定すると、IPD ヘッダーの SQL_DESC_ROWS_PROCESSED_PTR フィールドが設定されます。<br /><br /> この属性が指すバッファーを格納する **SQLExecDirect** または **sqlexecute** の呼び出しが SQL_SUCCESS または SQL_SUCCESS_WITH_INFO を返さない場合、バッファーの内容は定義されていません。<br /><br /> 詳細については、「 [パラメーターの配列の使用](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)」を参照してください。|  
|SQL_ATTR_PARAMSET_SIZE (ODBC 3.0)|各パラメーターの値の数を指定する SQLULEN 値。 SQL_ATTR_PARAMSET_SIZE が1より大きい場合は、APD ポイントの配列を SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、および SQL_DESC_OCTET_LENGTH_PTR します。 各配列のカーディナリティは、このフィールドの値と同じです。<br /><br /> バインドされたパラメーターがない場合、この属性は無視されます。<br /><br /> 詳細については、「 [パラメーターの配列の使用](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)」を参照してください。<br /><br /> このステートメント属性を設定すると、APD ヘッダーの SQL_DESC_ARRAY_SIZE フィールドが設定されます。|  
|SQL_ATTR_QUERY_TIMEOUT (ODBC 1.0)|アプリケーションに戻る前に、SQL ステートメントの実行を待機する秒数に対応する SQLULEN 値。 *Valueptr*が 0 (既定値) の場合、タイムアウトはありません。<br /><br /> 指定されたタイムアウトがデータソースの最大タイムアウト値を超えた場合、または最小タイムアウトより小さい場合、 **SQLSetStmtAttr** はその値を置き換え、SQLSTATE 01S02 (オプション値が変更されました) を返します。<br /><br /> アプリケーションでは、 **select**ステートメントがタイムアウトした場合に、ステートメントを再利用するために**sqlcloを**呼び出す必要がないことに注意してください。<br /><br /> このステートメント属性に設定されているクエリタイムアウトは、同期モードと非同期モードの両方で有効です。|  
|SQL_ATTR_RETRIEVE_DATA (ODBC 2.0)|SQLULEN 値:<br /><br /> SQL_RD_ON = **Sqlfetchscroll**と、ODBC 3.x では、 **sqlfetch**はカーソルを指定された場所に配置した後に*データを取得*します。 これは既定値です。<br /><br /> SQL_RD_OFF = **Sqlfetchscroll** 、および ODBC *3. x*では、 **sqlfetch** はカーソルを置いた後にデータを取得しません。<br /><br /> アプリケーションでは、SQL_RETRIEVE_DATA を SQL_RD_OFF に設定することにより、行が存在することを確認したり、行を取得するオーバーヘッドを発生させることなく行のブックマークを取得したりできます。 詳細については、「 [行のスクロールとフェッチ](../../../odbc/reference/develop-app/scrolling-and-fetching-rows-odbc.md)」を参照してください。<br /><br /> この属性の値は、開いているカーソルに設定できます。ただし、この設定はすぐには有効にならない場合があります。この場合、ドライバーは SQLSTATE 01S02 (オプション値が変更されました) を返し、属性を元の値にリセットします。|  
|SQL_ATTR_ROW_ARRAY_SIZE (ODBC 3.0)|Sqlfetch または**Sqlulen**への各呼び出しによって返される**SQLFetch**行の数を指定する sqlulen 値。 これは、 **Sqlbulkoperations**の一括ブックマーク操作で使用されるブックマーク配列内の行の数でもあります。 既定値は 1 です。<br /><br /> 指定した行セットのサイズがデータソースでサポートされている最大行セットサイズを超えた場合、ドライバーはその値を置き換え、SQLSTATE 01S02 (オプション値が変更されました) を返します。<br /><br /> 詳細については、「 [行セットサイズ](../../../odbc/reference/develop-app/rowset-size.md)」を参照してください。<br /><br /> このステートメント属性を設定すると、そのヘッダーの SQL_DESC_ARRAY_SIZE フィールドが設定されます。|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR (ODBC 3.0)|列データのバインドを変更するポインターに追加されたオフセットを指す SQLULEN * 値。 このフィールドが null 以外の場合、ドライバーはポインターを逆参照し、逆参照された値を記述子レコードの各遅延フィールド (SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、および SQL_DESC_OCTET_LENGTH_PTR) に追加し、バインド時に新しいポインター値を使用します。 既定では null に設定されています。<br /><br /> このステートメント属性を設定すると、そのヘッダーの SQL_DESC_BIND_OFFSET_PTR フィールドが設定されます。|  
|SQL_ATTR_ROW_BIND_TYPE (ODBC 1.0)|関連付けられたステートメントで **sqlfetch** または **sqlulen** が呼び出されたときに使用されるバインドの向きを設定する sqlulen 値。 列方向のバインドを選択するには、値を SQL_BIND_BY_COLUMN に設定します。 行方向のバインドを選択するには、値を、構造体の長さ、または結果の列がバインドされるバッファーのインスタンスの長さに設定します。<br /><br /> 長さが指定されている場合、バインドされた列のアドレスが指定された長さでインクリメントされるときに、結果が次の行の同じ列の先頭を指すように、バインドされたすべての列と、構造体またはバッファーの埋め込みの領域が含まれている必要があります。 ANSI C の構造体または共用体で **sizeof** 演算子を使用すると、この動作は保証されます。<br /><br /> 列方向のバインドは、 **Sqlfetch** および **sqlfetchscroll**の既定のバインドの方向です。<br /><br /> 詳細については、「 [ブロックカーソルで使用するバインド列](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)」を参照してください。<br /><br /> このステートメント属性を設定すると、そのヘッダーの SQL_DESC_BIND_TYPE フィールドが設定されます。|  
|SQL_ATTR_ROW_NUMBER (ODBC 2.0)|結果セット全体の現在の行番号を示す SQLULEN 値。 現在の行の数を特定できない場合、または現在の行がない場合、ドライバーは0を返します。<br /><br /> この属性は、 **SQLGetStmtAttr** を呼び出すことによって取得できますが、 **SQLSetStmtAttr**を呼び出すことによって設定することはできません。|  
|SQL_ATTR_ROW_OPERATION_PTR (ODBC 3.0)|\* **SQLSetPos**を使用した一括操作中に行を無視するために使用される sqlus悪意のある値の配列を指す sqlus悪意のある値。 各値は、SQL_ROW_PROCEED (一括操作に含める行の場合) または SQL_ROW_IGNORE (一括操作から除外する行の場合) のいずれかに設定されます。 ( **Sqlbulkoperations**の呼び出し中に、この配列を使用して行を無視することはできません)。<br /><br /> このステートメント属性は null ポインターに設定できます。この場合、ドライバーは行の状態の値を返しません。 この属性はいつでも設定できますが、新しい値は、次に **SQLSetPos** が呼び出されるまで使用されません。<br /><br /> 詳細については、「SQLSetPos を使用して行 [セットの行を更新](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md) する」および「 [sqlsetpos を使用](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)して行セットの行を削除する」を参照してください。<br /><br /> このステートメント属性を設定すると、の SQL_DESC_ARRAY_STATUS_PTR フィールドが設定されます。|  
|SQL_ATTR_ROW_STATUS_PTR (ODBC 3.0)|\*Sqlfetch または**Sqlfetchscroll**の呼び出し後に行の状態の値を含む sqlus悪意のある値の**SQLFetch**配列を指す sqlus悪意のある値。 配列には、行セット内の行と同じ数の要素があります。<br /><br /> このステートメント属性は null ポインターに設定できます。この場合、ドライバーは行の状態の値を返しません。 この属性はいつでも設定できますが、次に **Sqlbulkoperations**、 **sqlfetch**、 **Sqlbulkoperations**、または **SQLSetPos** が呼び出されるまで、新しい値は使用されません。<br /><br /> 詳細については、「フェッチされ [た行数と状態](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)」を参照してください。<br /><br /> このステートメント属性を設定すると、IRD ヘッダーの SQL_DESC_ARRAY_STATUS_PTR フィールドが設定されます。<br /><br /> この属性は、ODBC 2.x ドライバーによって、 **SQLExtendedFetch**の呼び出しで*rgbRowStatus*配列にマップさ*れます。*|  
|SQL_ATTR_ROWS_FETCHED_PTR (ODBC 3.0)|\*Sqlfetch または**Sqlulen**の呼び出し後にフェッチされた行の数を返すバッファーを指す**SQLFetch** sqlulen の値。 SQL_REFRESH の*操作*引数を使用して**SQLSetPos**を呼び出したときに実行された一括操作の影響を受ける行の数、または**sqlulen**によって実行される一括操作の影響を受ける行の数。 この数値には、エラー行が含まれます。<br /><br /> 詳細については、「フェッチされ [た行数と状態](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)」を参照してください。<br /><br /> このステートメント属性を設定すると、IRD ヘッダーの SQL_DESC_ROWS_PROCESSED_PTR フィールドが設定されます。<br /><br /> この属性が指すバッファーをいっぱいにする **Sqlfetch** または **sqlfetchscroll** の呼び出しが SQL_SUCCESS または SQL_SUCCESS_WITH_INFO を返さない場合、バッファーの内容は未定義になります。|  
|SQL_ATTR_SIMULATE_CURSOR (ODBC 2.0)|配置された update ステートメントと delete ステートメントをシミュレートするドライバーが、このようなステートメントが1つの行にのみ影響することを保証するかどうかを指定する SQLULEN 値。<br /><br /> 位置指定の update および delete ステートメントをシミュレートするために、ほとんどのドライバーは、現在の行の各列の値を指定する**where**句を含む、検索された**update**ステートメントまたは**delete**ステートメントを作成します。 これらの列で一意のキーが構成されていない限り、このようなステートメントは複数の行に影響を与える可能性があります。<br /><br /> このようなステートメントが1つの行にのみ影響することを保証するために、ドライバーは一意のキーの列を特定し、それらの列を結果セットに追加します。 アプリケーションで、結果セット内の列が一意のキーを構成することを保証する場合、ドライバーはその必要はありません。 これにより、実行時間が短縮される可能性があります。<br /><br /> SQL_SC_NON_UNIQUE = ドライバーは、シミュレートされた位置指定 update ステートメントまたは delete ステートメントが1行にしか影響しないことを保証しません。これを行うのは、アプリケーションの役割です。 ステートメントが複数の行に影響する場合、 **Sqlexecute**、 **SQLExecDirect**、または **SQLSetPos** は SQLSTATE 01001 (カーソル操作の競合) を返します。<br /><br /> SQL_SC_TRY_UNIQUE = ドライバーは、シミュレートされた位置指定 update ステートメントまたは delete ステートメントが1行にのみ影響することを保証しようとします。 ドライバーは、一意のキーがない場合など、複数の行に影響する可能性がある場合でも、常にこのようなステートメントを実行します。 ステートメントが複数の行に影響する場合、 **Sqlexecute**、 **SQLExecDirect**、または **SQLSetPos** は SQLSTATE 01001 (カーソル操作の競合) を返します。<br /><br /> SQL_SC_UNIQUE = ドライバーは、シミュレートされた位置指定更新または削除ステートメントが1行にのみ影響することを保証します。 ドライバーが特定のステートメントに対してこれを保証できない場合、 **SQLExecDirect** または **SQLPrepare** はエラーを返します。<br /><br /> データソースで、位置指定の update および delete ステートメントのネイティブ SQL サポートが提供されていて、ドライバーでカーソルがシミュレートされていない場合は、SQL_SC_UNIQUE が SQL_SIMULATE_CURSOR に要求されると SQL_SUCCESS が返されます。 SQL_SC_TRY_UNIQUE または SQL_SC_NON_UNIQUE が要求された場合、SQL_SUCCESS_WITH_INFO が返されます。 データソースが SQL_SC_TRY_UNIQUE レベルのサポートを提供し、ドライバーがサポートされていない場合は、SQL_SC_TRY_UNIQUE に対して SQL_SUCCESS が返され、SQL_SC_NON_UNIQUE に対して SQL_SUCCESS_WITH_INFO が返されます。<br /><br /> 指定されたカーソルシミュレーションの種類がデータソースでサポートされていない場合、ドライバーは別のシミュレーションの種類に置き換えられ、SQLSTATE 01S02 (オプション値が変更されました) を返します。 SQL_SC_UNIQUE の場合、ドライバーは、順に、SQL_SC_TRY_UNIQUE または SQL_SC_NON_UNIQUE に置き換えます。 SQL_SC_TRY_UNIQUE の場合、ドライバーは SQL_SC_NON_UNIQUE に置き換えられます。<br /><br /> 既定値は SQL_SC_UNIQUE です。<br /><br /> 詳細については、「 [位置指定更新と Delete ステートメントのシミュレート](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)」を参照してください。|  
|SQL_ATTR_USE_BOOKMARKS (ODBC 2.0)|アプリケーションがカーソル付きのブックマークを使用するかどうかを指定する SQLULEN 値。<br /><br /> SQL_UB_OFF = オフ (既定値)<br /><br /> SQL_UB_VARIABLE = アプリケーションは、カーソル付きでブックマークを使用します。サポートされている場合は、ドライバーによって可変長のブックマークが提供されます。 SQL_UB_FIXED は ODBC 3.x では非推奨とさ*れます。* Odbc *2.x アプリケーションで* は、odbc *2.x ドライバー (* 4 バイトの固定長のブックマークのみをサポート) を使用する場合でも、常に可変長のブックマークを使用する必要があります。 これは、固定長のブックマークが可変長ブックマークの特殊なケースであるためです。 ODBC 2.x ドライバーを使用する場合、ドライバーマネージャーは SQL_UB_VARIABLE を SQL_UB_FIXED にマップ*します。*<br /><br /> カーソルでブックマークを使用するには、アプリケーションでこの属性を指定してから、カーソルを開く前に SQL_UB_VARIABLE 値を指定する必要があります。<br /><br /> 詳細については、「 [ブックマークの取得](../../../odbc/reference/develop-app/retrieving-bookmarks.md)」を参照してください。|  
  
 [1] これらの関数は、記述子がアプリケーション記述子ではなく実装記述子である場合にのみ、非同期的に呼び出すことができます。  
  
 「 [列方向のバインド](../../../odbc/reference/develop-app/column-wise-binding.md) 」と「 [行方向のバインド](../../../odbc/reference/develop-app/row-wise-binding.md)」を参照してください。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|ステートメント処理の取り消し|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|接続属性の設定を返す|[SQLGetConnectAttr 関数](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|ステートメント属性の設定を返す|[SQLGetStmtAttr 関数](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|接続属性の設定|[SQLSetConnectAttr 関数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|記述子の1つのフィールドの設定|[SQLSetDescField 関数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
