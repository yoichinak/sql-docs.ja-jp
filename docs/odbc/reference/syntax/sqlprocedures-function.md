---
description: SQLProcedures 関数
title: SQLProcedures 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLProcedures
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLProcedures
helpviewer_keywords:
- SQLProcedures function [ODBC]
ms.assetid: d0d9ef10-2fd4-44a5-9334-649f186f4ba0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0c4e44a708f96883891d44d629fdd3c945eb283a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487148"
---
# <a name="sqlprocedures-function"></a>SQLProcedures 関数
**互換性**  
 導入されたバージョン: ODBC 1.0 標準準拠: ODBC  
  
 **まとめ**  
 **Sqlprocedures** は、特定のデータソースに格納されているプロシージャ名の一覧を返します。 *プロシージャ* は、 *実行可能オブジェクト*、または入力パラメーターと出力パラメーターを使用して呼び出すことができる名前付きエンティティを記述するために使用される一般的な用語です。 プロシージャの詳細については、「」の [手順](../../../odbc/reference/develop-app/procedures-odbc.md)を参照してください。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLProcedures(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      ProcName,  
     SQLSMALLINT    NameLength3);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル。  
  
 *CatalogName*  
 代入プロシージャカタログ。 ドライバーが一部のテーブルのカタログをサポートしていても、他のテーブルではサポートされていない場合 (ドライバーが異なる Dbms からデータを取得する場合など)、空の文字列 ("") は、カタログを持たないテーブルを表します。 *CatalogName* に文字列検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *CatalogName* は識別子として扱われ、大文字小文字は区別されません。 SQL_FALSE の場合、 *CatalogName* は通常の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。 詳細については、「 [カタログ関数の引数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)」を参照してください。  
  
 *NameLength1*  
 代入**CatalogName*の文字数。  
  
 *SchemaName*  
 代入プロシージャスキーマ名の文字列検索パターン。 ドライバーがいくつかのプロシージャのスキーマをサポートしているが、他のプロシージャのスキーマをサポートしていない場合 (ドライバーがさまざまな Dbms からデータを取得する場合など)、空の文字列 ("") はスキーマを持たないプロシージャを表します。  
  
 SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *SchemaName* は識別子として扱われ、大文字小文字は区別されません。 SQL_FALSE の場合、 *SchemaName* はパターン値の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。  
  
 *NameLength2*  
 代入**SchemaName*の文字数。  
  
 *ProcName*  
 代入プロシージャ名の文字列検索パターン。  
  
 SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *ProcName* は識別子として扱われ、大文字小文字は区別されません。 SQL_FALSE の場合、 *ProcName* はパターン値の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。  
  
 *NameLength3*  
 代入**ProcName*の文字数。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **Sqlprocedures**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合、関連付けられた SQLSTATE 値を取得するには、 *Handletype* SQL_HANDLE_STMT と*StatementHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出します。 次の表に、 **Sqlprocedures** によって一般的に返される SQLSTATE 値の一覧を示し、この関数のコンテキストでそれぞれについて説明します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続されていたデータソースとの間の通信リンクが失敗しました。|  
|24000|カーソル状態が無効|*StatementHandle*でカーソルが開かれました。 **sqlfetch**または**sqlfetchscroll**が呼び出されました。 このエラーは、 **Sqlfetch** または **sqlfetchscroll** が SQL_NO_DATA 返されなかった場合にドライバーマネージャーによって返されます。また、 **Sqlfetch** または **sqlfetchscroll** が SQL_NO_DATA を返した場合は、ドライバーによって返されます。<br /><br /> *StatementHandle*でカーソルが開いていましたが、 **sqlfetch**または**sqlfetchscroll**が呼び出されていません。|  
|40001|シリアル化エラー|リソースが別のトランザクションでデッドロックしているため、トランザクションがロールバックされました。|  
|40003|ステートメントの完了が不明です|この関数の実行中に関連付けられた接続に失敗しました。トランザクションの状態を確認できません。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * \* Messagetext*バッファーの**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|*StatementHandle*に対して非同期処理が有効になりました。 関数が呼び出され、実行が完了する前に、 **SQLCancel** または **Sqlcancelhandle** が *StatementHandle*で呼び出されました。 次に、 *StatementHandle*で関数が再度呼び出されました。<br /><br /> 関数が呼び出され、実行が完了する前に、マルチスレッドアプリケーションの別のスレッドの*StatementHandle*で**SQLCancel**または**sqlcancelhandle**が呼び出されました。|  
|HY009|Null ポインターの使い方が正しくありません|SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されました。 *CatalogName* 引数は null ポインターで、SQL_CATALOG_NAME *InfoType* はカタログ名がサポートされていることを返します。<br /><br /> (DM) SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定され、 *SchemaName* または *ProcName* 引数が null ポインターでした。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、この関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または **Sqlmoreresults** が *StatementHandle* に対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。<br /><br /> (DM) 非同期的に実行されている関数 (この1つではない) が *StatementHandle* に対して呼び出され、この関数が呼び出されたときにまだ実行されています。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **Sqlbulkoperations**、 **SQLSetPos** が *StatementHandle* に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY090|文字列またはバッファーの長さが無効です|(DM) 名前の長さの引数のいずれかの値が0未満ですが SQL_NTS と等しくありません。<br /><br /> 名前の長さの引数のいずれかの値が、対応する名前の最大長の値を超えました。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYC00|省略可能な機能は実装されていません|プロシージャカタログが指定されましたが、ドライバーまたはデータソースがカタログをサポートしていません。<br /><br /> プロシージャスキーマが指定されましたが、ドライバーまたはデータソースがスキーマをサポートしていません。<br /><br /> プロシージャスキーマまたはプロシージャ名に文字列検索パターンが指定されています。データソースは、これらの引数の1つ以上の検索パターンをサポートしていません。<br /><br /> SQL_ATTR_CONCURRENCY および SQL_ATTR_CURSOR_TYPE statement 属性の現在の設定の組み合わせは、ドライバーまたはデータソースではサポートされていませんでした。<br /><br /> SQL_ATTR_USE_BOOKMARKS statement 属性が SQL_UB_VARIABLE に設定されており、SQL_ATTR_CURSOR_TYPE statement 属性が、ドライバーがブックマークをサポートしていないカーソルの種類に設定されました。|  
|HYT00|タイムアウトに達しました|データソースが要求された結果セットを返す前に、クエリのタイムアウト期間が経過しました。 タイムアウト期間は、 **SQLSetStmtAttr**、SQL_ATTR_QUERY_TIMEOUT によって設定されます。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle* に関連付けられているドライバーは、この機能をサポートしていません。|  
|IM017|非同期通知モードでは、ポーリングは無効になっています|通知モデルが使用されるたびに、ポーリングは無効になります。|  
|IM018|**Sqlcompleteasync** は、このハンドルで前の非同期操作を完了するために呼び出されていません。|ハンドルに対する前の関数呼び出しが SQL_STILL_EXECUTING を返し、通知モードが有効になっている場合は、処理を完了するために、ハンドルに対して **Sqlcompleteasync** を呼び出す必要があります。|  
  
## <a name="comments"></a>コメント  
 **Sqlprocedures** は、要求された範囲内のすべてのプロシージャを一覧表示します。 ユーザーは、これらのプロシージャを実行する権限を持っている場合も、持っていない場合もあります。 ユーザー補助を確認するには、アプリケーションで **SQLGetInfo** を呼び出して、SQL_ACCESSIBLE_PROCEDURES 情報の値を確認します。 それ以外の場合、アプリケーションは、実行できないプロシージャをユーザーが選択した状況を処理できる必要があります。 この情報の使用方法については、「 [プロシージャ](../../../odbc/reference/develop-app/procedures-odbc.md)」を参照してください。  
  
> [!NOTE]  
>  一般的な使用、引数、および ODBC カタログ関数の返されるデータの詳細については、「 [カタログ関数](../../../odbc/reference/develop-app/catalog-functions.md)」を参照してください。  
  
 **Sqlprocedures** は、結果を PROCEDURE_CAT、PROCEDURE_SCHEMA、および PROCEDURE_NAME 順に並べ替えて、標準の結果セットとして返します。  
  
> [!NOTE]  
>  **Sqlprocedures** では、すべてのプロシージャが返されるとは限りません。 アプリケーションでは、 **Sqlprocedures**によって返されるかどうかにかかわらず、任意の有効なプロシージャを使用できます。  
  
 ODBC 3 *. x*では、次の列の名前が変更されました。 アプリケーションは列番号でバインドされるため、列名の変更は旧バージョンとの互換性に影響しません。  
  
|ODBC 2.0 列|ODBC 3 *. x* 列|  
|---------------------|-----------------------|  
|PROCEDURE_QUALIFIER|PROCEDURE_CAT|  
|手順 _OWNER|手順 _SCHEM|  
  
 PROCEDURE_CAT、PROCEDURE_SCHEM、および PROCEDURE_NAME 列の実際の長さを確認するには、アプリケーションで、SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN、および SQL_MAX_PROCEDURE_NAME_LEN の各オプションを指定して **SQLGetInfo** を呼び出すことができます。  
  
 次の表に、結果セット内の列の一覧を示します。 列 8 (PROCEDURE_TYPE) 以外の列は、ドライバーで定義できます。 アプリケーションでは、明示的な序数位置を指定するのではなく、結果セットの末尾からカウントすることで、ドライバー固有の列にアクセスする必要があります。 詳細については、「 [カタログ関数によって返されるデータ](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)」を参照してください。  
  
|列名|列番号|データ型|コメント|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT (ODBC 2.0)|1|Varchar|プロシージャカタログ識別子。データソースに適用されない場合は NULL です。 ドライバーがいくつかのプロシージャのカタログをサポートしていても、他のプロシージャに対してはサポートされていない場合 (ドライバーが異なる Dbms からデータを取得する場合など)、カタログを持たないプロシージャに対して空の文字列 ("") が返されます。|  
|PROCEDURE_SCHEM (ODBC 2.0)|2|Varchar|プロシージャスキーマ識別子。データソースに適用されない場合は NULL です。 ドライバーがいくつかのプロシージャのスキーマをサポートしていて、他のプロシージャに対してはサポートされていない場合 (ドライバーが異なる Dbms からデータを取得する場合など)、スキーマを持たないプロシージャに対して空の文字列 ("") が返されます。|  
|PROCEDURE_NAME (ODBC 2.0)|3|Varchar not NULL|プロシージャ識別子。|  
|NUM_INPUT_PARAMS (ODBC 2.0)|4|該当なし|将来使用するために予約されています。 アプリケーションは、これらの結果列に返されるデータに依存しないようにする必要があります。|  
|NUM_OUTPUT_PARAMS (ODBC 2.0)|5|該当なし|将来使用するために予約されています。 アプリケーションは、これらの結果列に返されるデータに依存しないようにする必要があります。|  
|NUM_RESULT_SETS (ODBC 2.0)|6|該当なし|将来使用するために予約されています。 アプリケーションは、これらの結果列に返されるデータに依存しないようにする必要があります。|  
|解説 (ODBC 2.0)|7|Varchar|プロシージャの説明。|  
|PROCEDURE_TYPE (ODBC 2.0)|8|Smallint|プロシージャの種類を定義します。<br /><br /> SQL_PT_UNKNOWN: プロシージャが値を返すかどうかを判断できません。<br /><br /> SQL_PT_PROCEDURE: 返されたオブジェクトはプロシージャです。つまり、戻り値はありません。<br /><br /> SQL_PT_FUNCTION: 返されたオブジェクトは関数です。つまり、戻り値があります。|  
  
 *SchemaName*引数と*ProcName*引数では、検索パターンを使用できます。 有効な検索パターンの詳細については、「 [Pattern 値の引数](../../../odbc/reference/develop-app/pattern-value-arguments.md)」を参照してください。  
  
## <a name="code-example"></a>コード例  
 「 [プロシージャ呼び出し](../../../odbc/reference/develop-app/procedure-calls.md)」を参照してください。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|結果セット内の列へのバッファーのバインド|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|ステートメント処理の取り消し|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|1つの行またはデータのブロックを順方向専用にフェッチする|[SQLFetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|データのブロックのフェッチまたは結果セットのスクロール|[SQLFetchScroll 関数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|ドライバーまたはデータソースに関する情報を返す|[SQLGetInfo 関数](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|プロシージャのパラメーターと結果セット列を返す|[SQLProcedureColumns 関数](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|  
|ストアドプロシージャを呼び出す構文|[ステートメントの実行](../../../odbc/reference/develop-app/executing-statements-odbc.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
