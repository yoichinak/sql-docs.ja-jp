---
description: SQLPrepare 関数
title: SQLPrepare 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLPrepare
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPrepare
helpviewer_keywords:
- SQLPrepare function [ODBC]
ms.assetid: 332e1b4b-b0ed-4e7a-aa4d-4f35f4f4476b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d3b5d68aae8033b0710ee052b001c7942eb1f7d6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487188"
---
# <a name="sqlprepare-function"></a>SQLPrepare 関数
**互換性**  
 導入されたバージョン: ODBC 1.0 標準準拠: ISO 92  
  
 **まとめ**  
 **SQLPrepare** は、SQL 文字列の実行を準備します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLPrepare(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     StatementText,  
     SQLINTEGER    TextLength);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル。  
  
 *StatementText*  
 代入SQL テキスト文字列。  
  
 *TextLength*  
 代入文字の長さ **StatementText* 。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **SQLPrepare**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合、関連付けられた SQLSTATE 値を取得するには、 *Handletype* SQL_HANDLE_STMT と*StatementHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出します。 次の表に、 **SQLPrepare** によって一般的に返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01S02|オプションの値が変更されました|実装の動作条件により、指定されたステートメント属性は無効でした。そのため、類似した値が一時的に置き換えられました。 (**SQLGetStmtAttr** を呼び出して、一時的に置換された値がどのようになるかを判断できます)。代替値は、カーソルが閉じられるまで *StatementHandle* に対して有効です。 変更できるステートメント属性は、SQL_ATTR_CONCURRENCY SQL_ATTR_CURSOR_TYPE SQL_ATTR_KEYSET_SIZE SQL_ATTR_MAX_LENGTH SQL_ATTR_MAX_ROWS SQL_ATTR_QUERY_TIMEOUT SQL_ATTR_SIMULATE_CURSOR<br /><br /> (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続されていたデータソースとの間の通信リンクが失敗しました。|  
|21S01|挿入する値の一覧が列の一覧と一致しません|\**StatementText* に **INSERT** ステートメントが含まれており、挿入される値の数が派生テーブルの次数と一致しませんでした。|  
|21S02|派生テーブルの次数が列の一覧と一致しません|\**StatementText* には **CREATE VIEW** ステートメントが含まれており、指定された名前の数は、クエリ仕様で定義されている派生テーブルと同じではありません。|  
|22018|キャストの指定に無効な文字値があります|**StatementText* には、リテラルまたはパラメーターを含む SQL ステートメントが含まれており、その値は、関連付けられているテーブル列のデータ型と互換性がありませんでした。|  
|22019|エスケープ文字が無効です|引数*StatementText*に**WHERE**句で**エスケープ**を含む**LIKE**述語が含まれており、エスケープ後のエスケープ文字の長さが 1**ではあり**ませんでした。|  
|22025|無効なエスケープシーケンスです|引数*StatementText*には、 **WHERE**句に "**LIKE** _pattern 値_**エスケープ**_エスケープ文字_" という文字が含まれており、パターン値のエスケープ文字の後の文字が "%" でも "_" でもありません。|  
|24000|カーソル状態が無効|(DM) *StatementHandle*でカーソルが開いていたため、 **sqlfetch** または **sqlfetchscroll** が呼び出されました。<br /><br /> *StatementHandle*でカーソルが開いていましたが、 **sqlfetch**または**sqlfetchscroll**が呼び出されていません。|  
|34000|カーソル名が無効|\**StatementText* に位置指定 **削除** または位置指定 **更新**が含まれており、準備中のステートメントによって参照されているカーソルが開いていません。|  
|3D000|無効なカタログ名|*StatementText*で指定されたカタログ名が無効でした。|  
|3F000|スキーマ名が無効です|*StatementText*で指定されたスキーマ名が無効でした。|  
|42000|構文エラーまたはアクセス違反|\**StatementText* に、準備可能ではない SQL ステートメントが含まれているか、構文エラーが含まれています。<br /><br /> **StatementText* には、ユーザーが必要な特権を持っていないステートメントが含まれていました。|  
|42 S01|ベーステーブルまたはビューが既に存在します|\**StatementText* に **CREATE TABLE** または **CREATE VIEW** ステートメントが含まれており、指定されたテーブル名またはビュー名が既に存在します。|  
|42 S02|ベーステーブルまたはビューが見つかりません|\**StatementText* に **drop Table** または **drop view** ステートメントが含まれており、指定されたテーブル名またはビュー名が存在しませんでした。<br /><br /> \**StatementText* に **ALTER TABLE** ステートメントが含まれており、指定されたテーブル名が存在しませんでした。<br /><br /> \**StatementText* に **CREATE VIEW** ステートメントが含まれており、クエリ仕様で定義されているテーブル名またはビュー名が存在しませんでした。<br /><br /> \**StatementText* に **CREATE INDEX** ステートメントが含まれており、指定されたテーブル名が存在しませんでした。<br /><br /> \**StatementText* に **GRANT** ステートメントまたは **REVOKE** ステートメントが含まれており、指定されたテーブル名またはビュー名が存在しませんでした。<br /><br /> \**StatementText* に **select** ステートメントが含まれており、指定されたテーブル名またはビュー名が存在しませんでした。<br /><br /> \**StatementText* に **DELETE**、 **INSERT**、または **UPDATE** ステートメントが含まれていますが、指定されたテーブル名が存在しませんでした。<br /><br /> \**StatementText* に **CREATE TABLE** ステートメントが含まれており、(作成されているテーブル以外のテーブルを参照している) 制約で指定されたテーブルが存在しませんでした。|  
|42 S11|インデックスは既に存在します|\**StatementText* に **CREATE INDEX** ステートメントが含まれており、指定されたインデックス名が既に存在します。|  
|42 S12|インデックスが見つかりません|\**StatementText* に **DROP INDEX** ステートメントが含まれており、指定されたインデックス名が存在しませんでした。|  
|42 S21|列は既に存在します|\**StatementText* に **ALTER TABLE** ステートメントが含まれており、 **ADD** 句で指定された列が一意でないか、ベーステーブル内の既存の列を識別しています。|  
|42 S22|列が見つかりません|\**StatementText* に **CREATE INDEX** ステートメントが含まれており、列リストで指定された1つ以上の列名が存在しませんでした。<br /><br /> \**StatementText* に **GRANT** ステートメントまたは **REVOKE** ステートメントが含まれており、指定された列名が存在しませんでした。<br /><br /> \**StatementText* に **select**、 **DELETE**、 **INSERT**、または **UPDATE** ステートメントが含まれており、指定された列名が存在しませんでした。<br /><br /> \**StatementText* に **CREATE TABLE** ステートメントが含まれており、制約 (作成されるテーブル以外のテーブルを参照している) で指定された列が存在しませんでした。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * \* Messagetext*バッファーの**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|*StatementHandle*に対して非同期処理が有効になりました。 関数が呼び出され、実行が完了する前に、 **SQLCancel** または **Sqlcancelhandle** が *StatementHandle*で呼び出された後、 *StatementHandle*で関数が再度呼び出されました。<br /><br /> 関数が呼び出され、実行が完了する前に、マルチスレッドアプリケーションの別のスレッドの*StatementHandle*で**SQLCancel**または**sqlcancelhandle**が呼び出されました。|  
|HY009|Null ポインターの使い方が正しくありません|(DM) *StatementText* は null ポインターでした。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、 **SQLPrepare** 関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または **Sqlmoreresults** が *StatementHandle* に対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。<br /><br /> (DM) 非同期的に実行されている関数 (この1つではない) が *StatementHandle* に対して呼び出され、この関数が呼び出されたときにまだ実行されています。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **Sqlbulkoperations**、 **SQLSetPos** が *StatementHandle* に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY090|文字列またはバッファーの長さが無効です|(DM) 引数 *TextLength* が0以下で、SQL_NTS と等しくない。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYC00|省略可能な機能は実装されていません|定義されているカーソルの種類では、同時実行の設定が無効でした。<br /><br /> SQL_ATTR_USE_BOOKMARKS statement 属性が SQL_UB_VARIABLE に設定されており、SQL_ATTR_CURSOR_TYPE statement 属性が、ドライバーがブックマークをサポートしていないカーソルの種類に設定されました。|  
|HYT00|タイムアウトに達しました|データソースが結果セットを返す前にタイムアウト期間が経過しました。 タイムアウト期間は、 **SQLSetStmtAttr**、SQL_ATTR_QUERY_TIMEOUT によって設定されます。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle* に関連付けられているドライバーでは、関数はサポートされていません。|  
|IM017|非同期通知モードでは、ポーリングは無効になっています|通知モデルが使用されるたびに、ポーリングは無効になります。|  
|IM018|**Sqlcompleteasync** は、このハンドルで前の非同期操作を完了するために呼び出されていません。|ハンドルに対する前の関数呼び出しが SQL_STILL_EXECUTING を返し、通知モードが有効になっている場合は、処理を完了するために、ハンドルに対して **Sqlcompleteasync** を呼び出す必要があります。|  
  
## <a name="comments"></a>コメント  
 アプリケーションは **SQLPrepare** を呼び出して、準備のためにデータソースに SQL ステートメントを送信します。 準備実行の詳細については、「 [実行の準備](../../../odbc/reference/develop-app/prepared-execution-odbc.md)」を参照してください。 アプリケーションでは、SQL ステートメントに1つ以上のパラメーターマーカーを含めることができます。 パラメーターマーカーを含めるには、アプリケーションで適切な位置に疑問符 (?) を SQL 文字列に埋め込みます。 パラメーターの詳細については、「 [ステートメントパラメーター](../../../odbc/reference/develop-app/statement-parameters.md)」を参照してください。  
  
> [!NOTE]  
>  アプリケーションで**SQLPrepare**を使用して、 **COMMIT**または**ROLLBACK**ステートメントを送信する準備と**SQLEXECUTE**を使用する場合、DBMS 製品間で相互運用することはできません。 トランザクションをコミットまたはロールバックするには、 **SQLEndTran**を呼び出します。  
  
 ドライバーでは、データソースによって使用される SQL の形式を使用するようにステートメントを変更し、準備のためにデータソースに送信することができます。 特に、ドライバーは、特定の機能の SQL 構文を定義するために使用されるエスケープシーケンスを変更します。 (SQL ステートメントの文法の詳細については、「 [ODBC でのエスケープシーケンス](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) 」および [「付録 C: sql 文法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)」を参照してください)。ドライバーの場合、ステートメントハンドルは、埋め込まれた SQL コード内のステートメント識別子に似ています。 データソースがステートメント識別子をサポートしている場合、ドライバーは、ステートメント識別子とパラメーター値をデータソースに送信できます。  
  
 ステートメントの準備が完了すると、アプリケーションはステートメントハンドルを使用して、後続の関数呼び出しでステートメントを参照します。 ステートメントハンドルに関連付けられた準備されたステートメントは、アプリケーションが SQL_DROP オプションを指定して**SQLFreeStmt**を呼び出すことでステートメントを解放するか、 **SQLPrepare**、 **SQLExecDirect**、またはいずれかのカタログ関数 (**sqlexecute**、 **sqlexecute**など) の呼び出しでステートメントハンドルを使用するまで、 **sqlexecute**を呼び出すことによって再実行できます。 アプリケーションによってステートメントが準備されると、結果セットの形式に関する情報を要求することができます。 実装によっては、 **SQLPrepare**の後に**SQLDescribeCol**または**SQLDescribeParam**を呼び出すと、 **sqlexecute**または**SQLExecDirect**の後に関数を呼び出すほど効率的ではない可能性があります。  
  
 アプリケーションが **SQLPrepare**を呼び出すと、一部のドライバーが構文エラーやアクセス違反を返すことができません。 ドライバーは、構文エラーとアクセス違反、構文エラーのみ、または構文エラーとアクセス違反のいずれも処理できません。 そのため、 **Sqlnumresultcols**、 **SQLDescribeCol**、 **Sqlcolattribute**、 **sqlexecute**などの後続の関連機能を呼び出すときに、アプリケーションはこれらの条件を処理できる必要があります。  
  
 ドライバーとデータソースの機能によっては、ステートメントの準備 (すべてのパラメーターがバインドされている場合) または実行時 (すべてのパラメーターがバインドされていない場合) に、パラメーター情報 (データ型など) がチェックされることがあります。 相互運用性を最大にするには、同じステートメントで新しい SQL ステートメントを準備する前に、アプリケーションで古い SQL ステートメントに適用されているすべてのパラメーターをバインド解除する必要があります。 これにより、古いパラメーター情報が新しいステートメントに適用されていることが原因で発生したエラーを回避できます。  
  
> [!IMPORTANT]  
>  **SQLEndTran**を明示的に呼び出すか、自動コミットモードで作業することにより、トランザクションをコミットすると、データソースによって、接続上のすべてのステートメントのアクセスプランが削除される可能性があります。 詳細については、「 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) での SQL_CURSOR_COMMIT_BEHAVIOR と SQL_CURSOR_ROLLBACK_BEHAVIOR の情報の種類」および「 [カーソルおよび準備されたステートメントに対するトランザクションの影響](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)」を参照してください。  
  
## <a name="code-example"></a>コード例  
 「 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)、 [sqlputdata](../../../odbc/reference/syntax/sqlputdata-function.md)、 [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)」を参照してください。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|ステートメントハンドルの割り当て|[SQLAllocHandle 関数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|結果セット内の列へのバッファーのバインド|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|バッファーをパラメーターにバインドする|[SQLBindParameter 関数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|ステートメント処理の取り消し|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|コミットまたはロールバック操作の実行|[SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|SQL ステートメントの実行|[SQLExecDirect 関数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|準備された SQL ステートメントの実行|[SQLExecute 関数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|ステートメントの影響を受ける行の数を返す|[SQLRowCount 関数](../../../odbc/reference/syntax/sqlrowcount-function.md)|  
|カーソル名の設定|[SQLSetCursorName 関数](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
