---
description: SQLTables 関数
title: SQLTables 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLTables
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLTables
helpviewer_keywords:
- SQLTables function [ODBC]
ms.assetid: 60d5068a-7d7c-447c-acc6-f3f2cf73440c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a1eb095849362914074e2c1e7f02166db2712894
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421046"
---
# <a name="sqltables-function"></a>SQLTables 関数
**互換性**  
 導入されたバージョン: ODBC 1.0 標準準拠: グループを開く  
  
 **まとめ**  
 **Sqltables** は、特定のデータソースに格納されているテーブル名、カタログ名、スキーマ名、およびテーブル型の一覧を返します。 ドライバーは、結果セットとして情報を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLTables(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      TableName,  
     SQLSMALLINT    NameLength3,  
     SQLCHAR *      TableType,  
     SQLSMALLINT    NameLength4);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入取得した結果のステートメントハンドル。  
  
 *CatalogName*  
 代入カタログ名。 SQL_ODBC_VERSION 環境属性が SQL_OV_ODBC3 の場合、 *CatalogName* 引数は検索パターンを受け取ります。SQL_OV_ODBC2 が設定されている場合、検索パターンは受け入れられません。 ドライバーが一部のテーブルのカタログをサポートしていても、他のテーブルではサポートされていない場合 (ドライバーが異なる Dbms からデータを取得する場合など)、空の文字列 ("") は、カタログを持たないテーブルを示します。  
  
 SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *CatalogName* は識別子として扱われ、大文字小文字は区別されません。 SQL_FALSE の場合、 *CatalogName* はパターン値の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。 詳細については、「 [カタログ関数の引数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)」を参照してください。  
  
 *NameLength1*  
 代入**CatalogName*の文字数。  
  
 *SchemaName*  
 代入スキーマ名の文字列検索パターン。 ドライバーがいくつかのテーブルのスキーマをサポートしていても、他のテーブルのスキーマをサポートしていない場合 (ドライバーが異なる Dbms からデータを取得する場合など)、空の文字列 ("") はスキーマを持たないテーブルを示します。  
  
 SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *SchemaName* は識別子として扱われ、大文字小文字は区別されません。 SQL_FALSE の場合、 *SchemaName* はパターン値の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。  
  
 *NameLength2*  
 代入**SchemaName*の文字数。  
  
 *TableName*  
 代入テーブル名の文字列検索パターン。  
  
 SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *TableName* は識別子として扱われ、その大文字と小文字は区別されません。 SQL_FALSE の場合、 *TableName* はパターン値の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。  
  
 *NameLength3*  
 代入**TableName*の長さ (文字数)。  
  
 *TableType*  
 代入照合するテーブル型の一覧。  
  
 SQL_ATTR_METADATA_ID statement 属性は、 *TableType* 引数には影響しないことに注意してください。 *TableType* は、SQL_ATTR_METADATA_ID の設定に関係なく、値リストの引数です。  
  
 *NameLength4*  
 代入**TableType*の文字数。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **Sqltables**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合、関連付けられた SQLSTATE 値を取得するには、 *handletype*を SQL_HANDLE_STMT、 *StatementHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出します。 次の表に、 **Sqltables** によって通常返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続されていたデータソースとの間の通信リンクが失敗しました。|  
|24000|カーソル状態が無効|*StatementHandle*でカーソルが開かれました。 **sqlfetch**または**sqlfetchscroll**が呼び出されました。 このエラーは、sqlfetch または**Sqlfetchscroll**が SQL_NO_DATA 返されず、 **Sqlfetch**または**sqlfetchscroll**が SQL_NO_DATA を返した場合にドライバーによって返され**た場合に**、ドライバーマネージャーによって返されます。<br /><br /> *StatementHandle*でカーソルが開いていましたが、 **sqlfetch**または**sqlfetchscroll**が呼び出されていません。|  
|40001|シリアル化エラー|別のトランザクションでリソースのデッドロックが発生したため、トランザクションがロールバックされました。|  
|40003|ステートメントの完了が不明です|この関数の実行中に関連付けられた接続に失敗しました。トランザクションの状態を確認できません。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * \* Messagetext*バッファーの**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|*StatementHandle*に対して非同期処理が有効になりました。 関数が呼び出され、実行が完了する前に、 **SQLCancel** または **Sqlcancelhandle** が *StatementHandle*で呼び出されました。 次に、 *StatementHandle*で関数が再度呼び出されました。<br /><br /> 関数が呼び出され、実行が完了する前に、マルチスレッドアプリケーションの別のスレッドの*StatementHandle*で**SQLCancel**または**sqlcancelhandle**が呼び出されました。|  
|HY009|Null ポインターの使い方が正しくありません|SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されました。 *CatalogName* 引数は null ポインターで、SQL_CATALOG_NAME *InfoType* はカタログ名がサポートされていることを返します。<br /><br /> (DM) SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定され、 *SchemaName* または *TableName* 引数が null ポインターでした。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、SQLTables が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または **Sqlmoreresults** が *StatementHandle* に対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。<br /><br /> (DM) 非同期的に実行されている関数 (この1つではない) が *StatementHandle* に対して呼び出され、この関数が呼び出されたときにまだ実行されています。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **Sqlbulkoperations**、 **SQLSetPos** が *StatementHandle* に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY090|文字列またはバッファーの長さが無効です|(DM) 長さの引数の1つの値が0未満ですが SQL_NTS と等しくありません。<br /><br /> 名前の長さの引数のいずれかの値が、対応する名前の最大長の値を超えました。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYC00|省略可能な機能は実装されていません|カタログが指定されましたが、ドライバーまたはデータソースがカタログをサポートしていません。<br /><br /> スキーマが指定されましたが、ドライバーまたはデータソースがスキーマをサポートしていません。<br /><br /> カタログ名、テーブルスキーマ、またはテーブル名に文字列検索パターンが指定されています。データソースは、これらの引数の1つ以上の検索パターンをサポートしていません。<br /><br /> SQL_ATTR_CONCURRENCY および SQL_ATTR_CURSOR_TYPE statement 属性の現在の設定の組み合わせは、ドライバーまたはデータソースではサポートされていませんでした。<br /><br /> SQL_ATTR_USE_BOOKMARKS statement 属性が SQL_UB_VARIABLE に設定されており、SQL_ATTR_CURSOR_TYPE statement 属性が、ドライバーがブックマークをサポートしていないカーソルの種類に設定されました。|  
|HYT00|タイムアウトに達しました|データソースが要求された結果セットを返す前に、クエリのタイムアウト期間が経過しました。 タイムアウト期間は、 **SQLSetStmtAttr**、SQL_ATTR_QUERY_TIMEOUT によって設定されます。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle* に関連付けられているドライバーでは、関数はサポートされていません。|  
|IM017|非同期通知モードでは、ポーリングは無効になっています|通知モデルが使用されるたびに、ポーリングは無効になります。|  
|IM018|**Sqlcompleteasync** は、このハンドルで前の非同期操作を完了するために呼び出されていません。|ハンドルに対する前の関数呼び出しが SQL_STILL_EXECUTING を返し、通知モードが有効になっている場合は、処理を完了するために、ハンドルに対して **Sqlcompleteasync** を呼び出す必要があります。|  
  
## <a name="comments"></a>コメント  
 **Sqltables** は、要求された範囲内のすべてのテーブルを一覧表示します。 ユーザーは、これらのテーブルのいずれかに対して SELECT 権限を持っている場合も、持っていない場合もあります。 ユーザー補助を確認するために、アプリケーションは次のことを実行できます。  
  
-   **SQLGetInfo**を呼び出し、SQL_ACCESSIBLE_TABLES 情報の種類を確認します。  
  
-   **Sqltableprivileges**を呼び出して、各テーブルの権限を確認します。  
  
 それ以外の場合、アプリケーションは、 **SELECT** 権限が許可されていないテーブルをユーザーが選択する状況を処理できる必要があります。  
  
 *SchemaName*引数と*TableName*引数では、検索パターンを使用できます。 SQL_ODBC_VERSION 環境属性が SQL_OV_ODBC3 の場合、 *CatalogName* 引数は検索パターンを受け取ります。SQL_OV_ODBC2 が設定されている場合、検索パターンは受け入れられません。 SQL_OV_ODBC3 が設定されている場合、ODBC 3 *. x* ドライバーでは、 *CatalogName* 引数のワイルドカード文字を文字どおりに処理するようにエスケープする必要があります。 有効な検索パターンの詳細については、「 [Pattern 値の引数](../../../odbc/reference/develop-app/pattern-value-arguments.md)」を参照してください。  
  
> [!NOTE]  
>  一般的な使用、引数、および ODBC カタログ関数の返されるデータの詳細については、「 [カタログ関数](../../../odbc/reference/develop-app/catalog-functions.md)」を参照してください。  
  
 カタログ、スキーマ、およびテーブル型の列挙をサポートするために、 **Sqltables**の*CatalogName*、 *SchemaName*、 *TableName*、および*TableType*の各引数に対して次の特殊なセマンティクスが定義されています。  
  
-   *CatalogName*が SQL_ALL_CATALOGS で、 *SchemaName*と*TableName*が空の文字列の場合、結果セットには、データソースの有効なカタログの一覧が含まれます。 (TABLE_CAT 列を除くすべての列に Null 値が含まれています)。  
  
-   *SchemaName*が SQL_ALL_SCHEMAS で、 *CatalogName*と*TableName*が空の文字列の場合、結果セットには、データソースの有効なスキーマの一覧が含まれます。 (TABLE_SCHEM 列を除くすべての列に Null 値が含まれています)。  
  
-   *TableType*が SQL_ALL_TABLE_TYPES で、 *CatalogName*、 *SchemaName*、および*TableName*が空の文字列の場合、結果セットには、データソースに対して有効なテーブル型の一覧が含まれます。 (TABLE_TYPE 列を除くすべての列に Null 値が含まれています)。  
  
 *TableType*が空の文字列でない場合は、対象の型のコンマ区切り値のリストが含まれている必要があります。各値は、単一引用符 (') で囲むことも、引用符で囲まないようにすることもできます。たとえば、' TABLE '、' VIEW '、TABLE、VIEW などです。 アプリケーションでは、テーブルの種類を常に大文字で指定する必要があります。ドライバーは、データソースで必要とされる任意のケースにテーブルの種類を変換する必要があります。 データソースが指定されたテーブル型をサポートしていない場合、 **Sqltables** はその型の結果を返しません。  
  
 **Sqltables** は、TABLE_TYPE、TABLE_CAT、TABLE_SCHEM、および TABLE_NAME 順に並べ替えられた結果を標準の結果セットとして返します。 この情報の使用方法については、「 [カタログデータの使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)」を参照してください。  
  
 TABLE_CAT、TABLE_SCHEM、および TABLE_NAME 列の実際の長さを確認するために、アプリケーションは SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN、および SQL_MAX_TABLE_NAME_LEN の情報の種類を使用して **SQLGetInfo** を呼び出すことができます。  
  
 ODBC 3 *. x*では、次の列の名前が変更されました。 アプリケーションは列番号でバインドされるため、列名の変更は旧バージョンとの互換性に影響しません。  
  
|ODBC 2.0 列|ODBC 3 *. x* 列|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 次の表に、結果セット内の列の一覧を示します。 列 5 (解説) 以外の列は、ドライバーで定義できます。 アプリケーションでは、明示的な序数位置を指定するのではなく、結果セットの末尾からカウントすることで、ドライバー固有の列にアクセスする必要があります。 詳細については、「 [カタログ関数によって返されるデータ](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)」を参照してください。  
  
|列名|列番号|データ型|コメント|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|カタログ名。データソースに適用されない場合は NULL です。 ドライバーが一部のテーブルのカタログをサポートしていても、他のテーブルではサポートされていない場合 (ドライバーが異なる Dbms からデータを取得する場合など)、カタログを持たないテーブルに対して空の文字列 ("") が返されます。|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|スキーマ名;データソースに適用されない場合は NULL です。 ドライバーがいくつかのテーブルのスキーマをサポートしていても、他のテーブルではサポートされていない場合 (ドライバーが異なる Dbms からデータを取得する場合など) は、スキーマがないテーブルに対して空の文字列 ("") を返します。|  
|TABLE_NAME (ODBC 1.0)|3|Varchar|テーブル名。|  
|TABLE_TYPE (ODBC 1.0)|4|Varchar|テーブル型の名前。"テーブル"、"表示"、"システムテーブル"、"グローバル一時"、"ローカル一時"、"エイリアス"、"シノニム"、またはデータソース固有の型名のいずれかです。<br /><br /> "ALIAS" と "シノニム" の意味は、ドライバーによって異なります。|  
|解説 (ODBC 1.0)|5|Varchar|テーブルの説明。|  
  
## <a name="example"></a>例  
 次のサンプルコードでは、ハンドルと接続は解放されません。 ハンドルとステートメントを解放するコードサンプルについては、「 [Sqlfreehandle 関数](../../../odbc/reference/syntax/sqlfreehandle-function.md) と [SQLFreeStmt 関数](../../../odbc/reference/syntax/sqlfreestmt-function.md) 」を参照してください。  
  
```cpp  
// SQLTables.cpp  
// compile with: user32.lib odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
#include <strsafe.h>  
  
// simple helper functions  
int MySQLSuccess(SQLRETURN rc) {  
   return (rc == SQL_SUCCESS || rc == SQL_SUCCESS_WITH_INFO);  
}  
  
struct DataBinding {  
   SQLSMALLINT TargetType;  
   SQLPOINTER TargetValuePtr;  
   SQLINTEGER BufferLength;  
   SQLLEN StrLen_or_Ind;  
};  
  
void printCatalog(const struct DataBinding* catalogResult) {  
   if (catalogResult[0].StrLen_or_Ind != SQL_NULL_DATA)   
      printf("Catalog Name = %s\n", (char *)catalogResult[0].TargetValuePtr);  
}  
  
// remember to disconnect and free memory, and free statements and handles  
int main() {  
   int bufferSize = 1024, i, numCols = 5;  
   struct DataBinding* catalogResult = (struct DataBinding*) malloc( numCols * sizeof(struct DataBinding) );  
   wchar_t* dbName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize );  
   wchar_t* userName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize );  
  
   // declare and initialize the environment, connection, statement handles  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   SQLRETURN retCode;  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLWCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen;  
  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, -1);  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
   retCode = SQLDriverConnect(hdbc, desktopHandle, (SQLCHAR*)"Driver={SQL Server}", SQL_NTS, (SQLCHAR*)connStrbuffer, 1024 + 1, &connStrBufferLen, SQL_DRIVER_PROMPT);  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
   retCode = SQLGetInfo(hdbc, SQL_DATABASE_NAME, dbName, (SQLSMALLINT)bufferSize, (SQLSMALLINT *)&bufferSize);  
   retCode = SQLGetInfo(hdbc, SQL_USER_NAME, userName, (SQLSMALLINT)bufferSize, (SQLSMALLINT *)&bufferSize);  
  
   bufferSize = 1024;  
  
   // allocate memory for the binding  
   // free this memory when done  
   for ( i = 0 ; i < numCols ; i++ ) {  
      catalogResult[i].TargetType = SQL_C_CHAR;  
      catalogResult[i].BufferLength = (bufferSize + 1);  
      catalogResult[i].TargetValuePtr = malloc( sizeof(unsigned char)*catalogResult[i].BufferLength );  
   }  
  
   // setup the binding (can be used even if the statement is closed by closeStatementHandle)  
   for ( i = 0 ; i < numCols ; i++ )  
      retCode = SQLBindCol(hstmt, (SQLUSMALLINT)i + 1, catalogResult[i].TargetType, catalogResult[i].TargetValuePtr, catalogResult[i].BufferLength, &(catalogResult[i].StrLen_or_Ind));  
  
   // all catalogs query  
   printf( "A list of names of all catalogs\n" );  
   retCode = SQLTables( hstmt, (SQLCHAR*)SQL_ALL_CATALOGS, SQL_NTS, (SQLCHAR*)"", SQL_NTS, (SQLCHAR*)"", SQL_NTS, (SQLCHAR*)"", SQL_NTS );  
   for ( retCode = SQLFetch(hstmt) ;  MySQLSuccess(retCode) ; retCode = SQLFetch(hstmt) )  
      printCatalog( catalogResult );  
}  
```  
  
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
|テーブルまたはテーブルの権限を取得する|[SQLTablePrivileges 関数](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
