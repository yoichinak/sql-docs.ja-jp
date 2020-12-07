---
description: SQLColumnPrivileges 関数
title: SQLColumnPrivileges 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLColumnPrivileges
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLColumnPrivileges
helpviewer_keywords:
- SQLColumnPrivileges function [ODBC]
ms.assetid: ef233d9a-6ed5-4986-9d42-5e0b1a79fb6e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 29ac9ba44c0627e0aa72cc9e1bec087357864bb1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448788"
---
# <a name="sqlcolumnprivileges-function"></a>SQLColumnPrivileges 関数
**互換性**  
 導入されたバージョン: ODBC 1.0 標準準拠: ODBC  
  
 **まとめ**  
 **Sqlcolumnprivileges** は、指定されたテーブルの列と関連付けられている権限の一覧を返します。 ドライバーは、指定された *StatementHandle*の結果セットとして情報を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLColumnPrivileges(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     TableName,  
     SQLSMALLINT   NameLength3,  
     SQLCHAR *     ColumnName,  
     SQLSMALLINT   NameLength4);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル。  
  
 *CatalogName*  
 代入カタログ名。 ドライバーが異なる Dbms からデータを取得する場合など、一部のカタログの名前がサポートされているものの、他のカタログではサポートされていない場合、空の文字列 ("") は、名前のないカタログを表します。 *CatalogName* に文字列検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *CatalogName* は識別子として扱われ、大文字小文字は区別されません。 SQL_FALSE の場合、 *CatalogName* は通常の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。 詳細については、「 [カタログ関数の引数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)」を参照してください。  
  
 *NameLength1*  
 代入**CatalogName*の文字数。  
  
 *SchemaName*  
 代入スキーマ名。 ドライバーがいくつかのテーブルのスキーマをサポートしていても、他のテーブルのスキーマをサポートしていない場合 (ドライバーが異なる Dbms からデータを取得する場合など)、空の文字列 ("") はスキーマを持たないテーブルを表します。 *SchemaName* に文字列検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *SchemaName* は識別子として扱われます。 SQL_FALSE の場合、 *SchemaName* は通常の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。  
  
 *NameLength2*  
 代入**SchemaName*の文字数。  
  
 *TableName*  
 代入テーブル名。 この引数を null ポインターにすることはできません。 *TableName* に文字列検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *TableName* は識別子として扱われ、その大文字と小文字は区別されません。 SQL_FALSE の場合、 *TableName* は通常の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。  
  
 *NameLength3*  
 代入**TableName*の長さ (文字数)。  
  
 *[ColumnName]*  
 代入列名の文字列検索パターン。  
  
 SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *ColumnName* は識別子として扱われ、その大文字と小文字は区別されません。 SQL_FALSE の場合、 *ColumnName* はパターン値の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。  
  
 *NameLength4*  
 代入**ColumnName*の文字数。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **Sqlcolumnprivileges**で SQL_ERROR または SQL_SUCCESS_WITH_INFO が返された場合、関連付けられた SQLSTATE 値は、 *handletype*が SQL_HANDLE_STMT で、*ハンドル*が*StatementHandle*である**SQLGetDiagRec**を呼び出すことによって取得できます。 次の表に、 **Sqlcolumnprivileges** によって一般的に返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
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
|HY009|Null ポインターの使い方が正しくありません|*TableName*引数が null ポインターでした。<br /><br /> SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されました。 *CatalogName* 引数は null ポインターで、SQL_CATALOG_NAME *InfoType* はカタログ名がサポートされていることを返します。<br /><br /> (DM) SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定され、 *SchemaName* または *ColumnName* 引数が null ポインターでした。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、この関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または **Sqlmoreresults** が *StatementHandle* に対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。<br /><br /> (DM) 非同期的に実行されている関数 (この1つではない) が *StatementHandle* に対して呼び出され、この関数が呼び出されたときにまだ実行されています。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **Sqlbulkoperations**、 **SQLSetPos** が *StatementHandle* に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY090|文字列またはバッファーの長さが無効です|(DM) 名前の長さの引数のいずれかの値が0未満ですが SQL_NTS と等しくありません。|  
|||名前の長さの引数のいずれかの値が、対応する名前の最大長の値を超えました。 (「コメント」を参照してください)。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYC00|省略可能な機能は実装されていません|カタログ名が指定されていますが、ドライバーまたはデータソースがカタログをサポートしていません。<br /><br /> スキーマ名が指定されましたが、ドライバーまたはデータソースがスキーマをサポートしていません。<br /><br /> 列名に文字列検索パターンが指定されていますが、データソースはその引数の検索パターンをサポートしていません。<br /><br /> SQL_CONCURRENCY および SQL_CURSOR_TYPE statement 属性の現在の設定の組み合わせは、ドライバーまたはデータソースではサポートされていませんでした。<br /><br /> SQL_ATTR_USE_BOOKMARKS statement 属性が SQL_UB_VARIABLE に設定されており、SQL_ATTR_CURSOR_TYPE statement 属性が、ドライバーがブックマークをサポートしていないカーソルの種類に設定されました。|  
|HYT00|タイムアウトに達しました|データソースから結果セットが返される前に、クエリのタイムアウト期間が経過しました。 タイムアウト期間は、 **SQLSetStmtAttr**、SQL_ATTR_QUERY_TIMEOUT によって設定されます。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle* に関連付けられているドライバーでは、関数はサポートされていません。|  
|IM017|非同期通知モードでは、ポーリングは無効になっています|通知モデルが使用されるたびに、ポーリングは無効になります。|  
|IM018|**Sqlcompleteasync** は、このハンドルで前の非同期操作を完了するために呼び出されていません。|ハンドルに対する前の関数呼び出しが SQL_STILL_EXECUTING を返し、通知モードが有効になっている場合は、処理を完了するために、ハンドルに対して **Sqlcompleteasync** を呼び出す必要があります。|  
  
## <a name="comments"></a>コメント  
 **Sqlcolumnprivileges** は、TABLE_CAT、TABLE_SCHEM、TABLE_NAME、COLUMN_NAME、および特権によって並べ替えられた結果を標準の結果セットとして返します。  
  
> [!NOTE]  
>  **Sqlcolumnprivileges** は、すべての列に対する権限を返すことはできません。 たとえば、ドライバーは、擬似列 (Oracle ROWID など) の権限に関する情報を返さない場合があります。 アプリケーションでは、 **Sqlcolumnprivileges**によって返されるかどうかにかかわらず、任意の有効な列を使用できます。  
  
 VARCHAR 型の列の長さはテーブルには表示されません。実際の長さは、データソースによって異なります。 CATALOG_NAME、SCHEMA_NAME、TABLE_NAME、および COLUMN_NAME 列の実際の長さを確認するには、アプリケーションで、SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN、SQL_MAX_TABLE_NAME_LEN、および SQL_MAX_COLUMN_NAME_LEN の各オプションを指定して **SQLGetInfo** を呼び出すことができます。  
  
> [!NOTE]  
>  一般的な使用、引数、および ODBC カタログ関数の返されるデータの詳細については、「 [カタログ関数](../../../odbc/reference/develop-app/catalog-functions.md)」を参照してください。  
  
 ODBC 3 では、次の列の名前が変更されています。*x*。 アプリケーションは列番号でバインドされるため、列名の変更は旧バージョンとの互換性に影響しません。  
  
|ODBC 2.0 列|ODBC 3.*x* 列|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 次の表に、結果セット内の列の一覧を示します。 列 8 (IS_GRANTABLE) 以外の列は、ドライバーで定義できます。 アプリケーションでは、明示的な序数位置を指定するのではなく、結果セットの末尾からカウントすることで、ドライバー固有の列にアクセスする必要があります。 詳細については、「 [カタログ関数によって返されるデータ](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)」を参照してください。  
  
|列名|列番号|データ型|コメント|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|カタログ識別子。データソースに適用されない場合は NULL です。 ドライバーが一部のテーブルのカタログをサポートしていても、他のテーブルではサポートされていない場合 (ドライバーが異なる Dbms からデータを取得する場合など)、カタログを持たないテーブルに対して空の文字列 ("") が返されます。|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|スキーマ識別子。データソースに適用されない場合は NULL です。 ドライバーがいくつかのテーブルのスキーマをサポートしていても、他のテーブルではサポートされていない場合 (ドライバーが異なる Dbms からデータを取得する場合など) は、スキーマがないテーブルに対して空の文字列 ("") を返します。|  
|TABLE_NAME (ODBC 1.0)|3|Varchar not NULL|テーブル識別子。|  
|COLUMN_NAME (ODBC 1.0)|4|Varchar not NULL|列名。 ドライバーは、名前のない列に対して空の文字列を返します。|  
|権限の権限 (ODBC 1.0)|5|Varchar|特権を付与したユーザーの名前。データソースに適用されない場合は NULL です。<br /><br /> 権限が与えられている列の値がオブジェクトの所有者であるすべての行について、[権限の付与者] 列は "_SYSTEM" になります。|  
|権限付与対象ユーザー (ODBC 1.0)|6|Varchar not NULL|特権が付与されたユーザーの名前。|  
|特権 (ODBC 1.0)|7|Varchar not NULL|列特権を識別します。 次のいずれかを指定することができます (または、実装定義時にデータソースでサポートされている他のユーザー)。<br /><br /> SELECT: 権限付与対象ユーザーに対し、列のデータの取得が許可されます。<br /><br /> 挿入: 権限付与対象ユーザーは、関連付けられたテーブルに挿入される新しい行の列にデータを提供することが許可されます。<br /><br /> 更新: 権限付与対象ユーザーに対し、列のデータの更新を許可します。<br /><br /> 参照: 権限付与対象ユーザーは、制約内で列を参照することが許可されます (たとえば、一意、参照、またはテーブルチェックの制約)。|  
|IS_GRANTABLE (ODBC 1.0)|8|Varchar|権限付与対象ユーザーに対し、権限を他のユーザーに許可することが許可されているかどうかを示します。"YES"、"NO"、または "NULL" (不明な場合) または "NULL" (データソースに適用されない場合)。<br /><br /> 特権は、許可可能または not 許可可能のいずれかですが、両方ではありません。 **Sqlcolumnprivileges**によって返される結果セットには、IS_GRANTABLE 列を除くすべての列が同じ値を持つ2つの行が含まれることはありません。|  
  
## <a name="code-example"></a>コード例  
 同様の関数のコード例については、「 [Sqlcolumns 関数](../../../odbc/reference/syntax/sqlcolumns-function.md)」を参照してください。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|結果セット内の列へのバッファーのバインド|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|ステートメント処理の取り消し|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|テーブル内の列を返す|[SQLColumns 関数](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|データのブロックのフェッチまたは結果セットのスクロール|[SQLFetchScroll 関数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|複数行のデータのフェッチ|[SQLFetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|テーブルまたはテーブルの権限を取得する|[SQLTablePrivileges 関数](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
|データソース内のテーブルの一覧を取得する|[SQLTables 関数](../../../odbc/reference/syntax/sqltables-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
