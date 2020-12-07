---
description: SQLTablePrivileges 関数
title: SQLTablePrivileges 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLTablePrivileges
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLTablePrivileges
helpviewer_keywords:
- SQLTablePrivileges function [ODBC]
ms.assetid: 8cfdb64f-64c5-47e6-ad57-0533ac630afa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bf50953a42d9a7557e3f57ebaa749f3cd116a0d8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421056"
---
# <a name="sqltableprivileges-function"></a>SQLTablePrivileges 関数
**互換性**  
 導入されたバージョン: ODBC 1.0 標準準拠: ODBC  
  
 **まとめ**  
 **Sqltableprivileges** は、テーブルの一覧と、各テーブルに関連付けられている権限を返します。 ドライバーは、指定されたステートメントの結果セットとして情報を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLTablePrivileges(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     TableName,  
     SQLSMALLINT   NameLength3);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル。  
  
 *CatalogName*  
 代入テーブルカタログ。 ドライバーが一部のテーブルのカタログをサポートしていても、他のテーブルではサポートされていない場合 (ドライバーが異なる Dbms からデータを取得する場合など)、空の文字列 ("") は、カタログを持たないテーブルを表します。 *CatalogName* に文字列検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *CatalogName* は識別子として扱われ、大文字小文字は区別されません。 SQL_FALSE の場合、 *CatalogName* は通常の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。 詳細については、「 [カタログ関数の引数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)」を参照してください。  
  
 *NameLength1*  
 代入**CatalogName*の文字数。  
  
 *SchemaName*  
 代入スキーマ名の文字列検索パターン。 ドライバーがいくつかのテーブルのスキーマをサポートしていても、他のテーブルのスキーマをサポートしていない場合 (ドライバーが異なる Dbms からデータを取得する場合など)、空の文字列 ("") はスキーマを持たないテーブルを表します。  
  
 SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *SchemaName* は識別子として扱われ、大文字小文字は区別されません。 SQL_FALSE の場合、 *SchemaName* はパターン値の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。  
  
 *NameLength2*  
 代入**SchemaName*の文字数。  
  
 *TableName*  
 代入テーブル名の文字列検索パターン。  
  
 SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *TableName* は識別子として扱われ、その大文字と小文字は区別されません。 SQL_FALSE の場合、 *TableName* はパターン値の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。  
  
 *NameLength3*  
 代入**TableName*の長さ (文字数)。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **Sqltableprivileges**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合、関連付けられた SQLSTATE 値は、 *handletype*が SQL_HANDLE_STMT で、*ハンドル*が*StatementHandle*である**SQLGetDiagRec**を呼び出すことによって取得できます。 次の表に、 **Sqltableprivileges** によって一般的に返される SQLSTATE 値の一覧を示し、この関数のコンテキストでそれぞれについて説明します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続されていたデータソースとの間の通信リンクが失敗しました。|  
|24000|カーソル状態が無効|*StatementHandle*でカーソルが開かれました。 **sqlfetch**または**sqlfetchscroll**が呼び出されました。 このエラーは、sqlfetch または**Sqlfetchscroll**が SQL_NO_DATA 返されず、 **Sqlfetch**または**sqlfetchscroll**が SQL_NO_DATA を返した場合にドライバーによって返され**た場合に**、ドライバーマネージャーによって返されます。<br /><br /> *StatementHandle*でカーソルが開いていましたが、 **sqlfetch**または**sqlfetchscroll**が呼び出されていません。|  
|40001|シリアル化エラー|リソースが別のトランザクションでデッドロックしているため、トランザクションがロールバックされました。|  
|40003|ステートメントの完了が不明です|この関数の実行中に関連付けられた接続に失敗しました。トランザクションの状態を確認できません。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * \* Messagetext*バッファーの**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|*StatementHandle*に対して非同期処理が有効になりました。 **Sqltableprivileges**関数が呼び出され、実行が完了する前に、 **SQLCancel**または**sqltableprivileges**が*StatementHandle*で呼び出されました。 その後、 *StatementHandle*で**sqltableprivileges**関数が再度呼び出されました。<br /><br /> **Sqltableprivileges**関数が呼び出され、実行が完了する前に、マルチスレッドアプリケーションの別のスレッドの*StatementHandle*で**SQLCancel**または**sqltableprivileges**が呼び出されました。|  
|HY009|Null ポインターの使い方が正しくありません|SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されました。 *CatalogName* 引数は null ポインターで、SQL_CATALOG_NAME *InfoType* はカタログ名がサポートされていることを返します。<br /><br /> (DM) SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定され、 *SchemaName* または *TableName* 引数が null ポインターでした。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、 **Sqltableprivileges** 関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または **Sqlmoreresults** が *StatementHandle* に対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。<br /><br /> (DM) 非同期的に実行されている関数 (この1つではない) が *StatementHandle* に対して呼び出され、この関数が呼び出されたときにまだ実行されています。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **Sqlbulkoperations**、 **SQLSetPos** が *StatementHandle* に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY090|文字列またはバッファーの長さが無効です|(DM) 名前の長さの引数のいずれかの値が0未満ですが SQL_NTS と等しくありません。<br /><br /> 名前の長さの引数のいずれかの値が、対応する修飾子または名前の最大長の値を超えました。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYC00|省略可能な機能は実装されていません|カタログが指定されましたが、ドライバーまたはデータソースがカタログをサポートしていません。<br /><br /> スキーマが指定されましたが、ドライバーまたはデータソースがスキーマをサポートしていません。<br /><br /> テーブルスキーマ、テーブル名、または列名に文字列検索パターンが指定されています。データソースは、これらの引数の1つ以上の検索パターンをサポートしていません。<br /><br /> SQL_ATTR_CONCURRENCY および SQL_ATTR_CURSOR_TYPE statement 属性の現在の設定の組み合わせは、ドライバーまたはデータソースではサポートされていませんでした。<br /><br /> SQL_ATTR_USE_BOOKMARKS statement 属性が SQL_UB_VARIABLE に設定されており、SQL_ATTR_CURSOR_TYPE statement 属性が、ドライバーがブックマークをサポートしていないカーソルの種類に設定されました。|  
|HYT00|タイムアウトに達しました|データソースから結果セットが返される前に、クエリのタイムアウト期間が経過しました。 タイムアウト期間は、 **SQLSetStmtAttr**、SQL_ATTR_QUERY_TIMEOUT によって設定されます。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle* に関連付けられているドライバーでは、関数はサポートされていません。|  
|IM017|非同期通知モードでは、ポーリングは無効になっています|通知モデルが使用されるたびに、ポーリングは無効になります。|  
|IM018|**Sqlcompleteasync** は、このハンドルで前の非同期操作を完了するために呼び出されていません。|ハンドルに対する前の関数呼び出しが SQL_STILL_EXECUTING を返し、通知モードが有効になっている場合は、処理を完了するために、ハンドルに対して **Sqlcompleteasync** を呼び出す必要があります。|  
  
## <a name="comments"></a>コメント  
 *SchemaName*引数と*TableName*引数では、検索パターンを使用できます。 有効な検索パターンの詳細については、「 [Pattern 値の引数](../../../odbc/reference/develop-app/pattern-value-arguments.md)」を参照してください。  
  
 **Sqltableprivileges** は、TABLE_CAT、TABLE_SCHEM、TABLE_NAME、特権、および権限付与対象ユーザーによって並べ替えられた、結果を標準の結果セットとして返します。  
  
 TABLE_CAT、TABLE_SCHEM、および TABLE_NAME 列の実際の長さを確認するには、アプリケーションで、SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN、および SQL_MAX_TABLE_NAME_LEN の各オプションを指定して **SQLGetInfo** を呼び出すことができます。  
  
> [!NOTE]  
>  一般的な使用、引数、および ODBC カタログ関数の返されるデータの詳細については、「 [カタログ関数](../../../odbc/reference/develop-app/catalog-functions.md)」を参照してください。  
  
 ODBC *3. x*では、次の列の名前が変更されました。 アプリケーションは列番号でバインドされるため、列名の変更は旧バージョンとの互換性に影響しません。  
  
|ODBC 2.0 列|ODBC *3. x* 列|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 次の表に、結果セット内の列の一覧を示します。 列 7 (IS_GRANTABLE) を超える追加の列は、ドライバーで定義できます。 アプリケーションでは、明示的な序数位置を指定するのではなく、結果セットの末尾からカウントすることで、ドライバー固有の列にアクセスする必要があります。 詳細については、「 [カタログ関数によって返されるデータ](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)」を参照してください。  
  
|列名|列番号|データ型|コメント|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|カタログ名。データソースに適用されない場合は NULL です。 ドライバーが一部のテーブルのカタログをサポートしていても、他のテーブルではサポートされていない場合 (ドライバーが異なる Dbms からデータを取得する場合など)、カタログを持たないテーブルに対して空の文字列 ("") が返されます。|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|スキーマ名;データソースに適用されない場合は NULL です。 ドライバーがいくつかのテーブルのスキーマをサポートしていても、他のテーブルではサポートされていない場合 (ドライバーが異なる Dbms からデータを取得する場合など) は、スキーマがないテーブルに対して空の文字列 ("") を返します。|  
|TABLE_NAME (ODBC 1.0)|3|Varchar not NULL|テーブル名。|  
|権限の権限 (ODBC 1.0)|4|Varchar|特権を付与したユーザーの名前。データソースに適用されない場合は NULL です。<br /><br /> 権限が与えられている列の値がオブジェクトの所有者であるすべての行について、[権限の付与者] 列は "_SYSTEM" になります。|  
|権限付与対象ユーザー (ODBC 1.0)|5|Varchar not NULL|特権が付与されたユーザーの名前。|  
|特権 (ODBC 1.0)|6|Varchar not NULL|テーブル特権。 次のいずれか、またはデータソース固有の特権を指定できます。<br /><br /> SELECT: 権限付与対象ユーザーに対し、テーブルの1つ以上の列のデータの取得が許可されます。<br /><br /> 挿入: 権限付与対象ユーザーは、1つまたは複数の列のデータを含む新しい行をテーブルに挿入できます。<br /><br /> 更新: 権限付与対象ユーザーは、テーブルの1つまたは複数の列のデータを更新できます。<br /><br /> 削除: 権限付与対象ユーザーは、テーブルからデータ行を削除できます。<br /><br /> 参照: 権限付与対象ユーザーは、制約内のテーブルの1つまたは複数の列を参照できます (たとえば、一意、参照、またはテーブルチェック制約)。<br /><br /> 特定のテーブル特権によって権限付与対象ユーザーに許可されたアクションのスコープは、データソースに依存します。 たとえば、更新権限が与えられている場合、権限付与対象ユーザーは、あるデータソース上のテーブル内のすべての列を更新できます。また、権限付与対象ユーザーが別のデータソースに対する更新権限を持っている列だけを更新することもできます。|  
|IS_GRANTABLE (ODBC 1.0)|7|Varchar|権限付与対象ユーザーに対し、権限を他のユーザーに許可することが許可されているかどうかを示します。"YES"、"NO"、または unknown の場合は NULL、データソースには適用されません。<br /><br /> 特権は、許可可能または not 許可可能のいずれかですが、両方ではありません。 **Sqlcolumnprivileges**によって返される結果セットには、IS_GRANTABLE 列を除くすべての列が同じ値を持つ2つの行が含まれることはありません。|  
  
## <a name="code-example"></a>コード例  
 同様の関数のコード例については、「 [Sqlcolumns](../../../odbc/reference/syntax/sqlcolumns-function.md)」を参照してください。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|結果セット内の列へのバッファーのバインド|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|ステートメント処理の取り消し|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|1つまたは複数の列に対する権限を返す|[SQLColumnPrivileges 関数](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|テーブル内の列を返す|[SQLColumns 関数](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|1つの行またはデータのブロックを順方向専用にフェッチする|[SQLFetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|データのブロックのフェッチまたは結果セットのスクロール|[SQLFetchScroll 関数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|テーブルの統計とインデックスの取得|[SQLStatistics 関数](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|データソース内のテーブルの一覧を取得する|[SQLTables 関数](../../../odbc/reference/syntax/sqltables-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
