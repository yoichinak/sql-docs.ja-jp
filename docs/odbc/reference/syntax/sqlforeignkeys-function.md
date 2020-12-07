---
description: SQLForeignKeys 関数
title: SQLForeignKeys 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLForeignKeys
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLForeignKeys
helpviewer_keywords:
- SQLForeignKeys function [ODBC]
ms.assetid: 07f3f645-f643-4d39-9a10-70a72f24e608
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 802153837d53c6886b44511fbdffe6efa6b83281
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491305"
---
# <a name="sqlforeignkeys-function"></a>SQLForeignKeys 関数
**互換性**  
 導入されたバージョン: ODBC 1.0 標準準拠: ODBC  
  
 **まとめ**  
 **SQLForeignKeys** は次を返すことができます。  
  
-   指定されたテーブル内の外部キーの一覧 (他のテーブルの主キーを参照する指定されたテーブル内の列)。  
  
-   指定されたテーブルの主キーを参照する他のテーブル内の外部キーの一覧。  
  
 ドライバーは、指定されたステートメントの結果セットとして各リストを返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLForeignKeys(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      PKCatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      PKSchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      PKTableName,  
     SQLSMALLINT    NameLength3,  
     SQLCHAR *      FKCatalogName,  
     SQLSMALLINT    NameLength4,  
     SQLCHAR *      FKSchemaName,  
     SQLSMALLINT    NameLength5,  
     SQLCHAR *      FKTableName,  
     SQLSMALLINT    NameLength6);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル。  
  
 *PKCatalogName*  
 代入主キーテーブルのカタログ名。 ドライバーが一部のテーブルのカタログをサポートしていても、他のテーブルではサポートされていない場合 (ドライバーが異なる Dbms からデータを取得する場合など)、空の文字列 ("") は、カタログを持たないテーブルを表します。 *PKCatalogName* に文字列検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *PKCatalogName* は識別子として扱われ、大文字小文字は区別されません。 SQL_FALSE の場合、 *PKCatalogName* は通常の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。 詳細については、「 [カタログ関数の引数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)」を参照してください。  
  
 *NameLength1*  
 代入長さ **PKCatalogName*(文字数)。  
  
 *PKSchemaName*  
 代入主キーテーブルのスキーマ名。 ドライバーがいくつかのテーブルのスキーマをサポートしていても、他のテーブルのスキーマをサポートしていない場合 (ドライバーが異なる Dbms からデータを取得する場合など)、空の文字列 ("") はスキーマを持たないテーブルを表します。 *PKSchemaName* に文字列検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *PKSchemaName* は識別子として扱われ、大文字小文字は区別されません。 SQL_FALSE の場合、 *PKSchemaName* は通常の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。  
  
 *NameLength2*  
 代入長さ **PKSchemaName*(文字数)。  
  
 *Pktablename)*  
 代入主キーテーブルの名前。 *Pktablename* に文字列検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *Pktablename* は識別子として扱われ、その大文字と小文字は区別されません。 SQL_FALSE の場合、 *Pktablename* は通常の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。  
  
 *NameLength3*  
 代入文字数で **Pktablename*の長さ。  
  
 *FKCatalogName*  
 代入外部キーテーブルのカタログ名。 ドライバーが一部のテーブルのカタログをサポートしていても、他のテーブルではサポートされていない場合 (ドライバーが異なる Dbms からデータを取得する場合など)、空の文字列 ("") は、カタログを持たないテーブルを表します。 *FKCatalogName* に文字列検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *FKCatalogName* は識別子として扱われ、大文字小文字は区別されません。 SQL_FALSE の場合、 *FKCatalogName* は通常の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。  
  
 *NameLength4*  
 代入長さ **FKCatalogName*(文字数)。  
  
 *FKSchemaName*  
 代入外部キーテーブルのスキーマ名。 ドライバーがいくつかのテーブルのスキーマをサポートしていても、他のテーブルのスキーマをサポートしていない場合 (ドライバーが異なる Dbms からデータを取得する場合など)、空の文字列 ("") はスキーマを持たないテーブルを表します。 *FKSchemaName* に文字列検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *FKSchemaName* は識別子として扱われ、大文字小文字は区別されません。 SQL_FALSE の場合、 *FKSchemaName* は通常の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。  
  
 *NameLength5*  
 代入長さ **FKSchemaName*(文字数)。  
  
 *FKTableName*  
 代入外部キーテーブルの名前。 *FKTableName* に文字列検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *FKTableName* は識別子として扱われ、大文字小文字は区別されません。 SQL_FALSE の場合、 *FKTableName* は通常の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。  
  
 *NameLength6*  
 代入長さ **FKTableName*(文字数)。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **SQLForeignKeys**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合、関連付けられた SQLSTATE 値を取得するには、 *Handletype* SQL_HANDLE_STMT と*StatementHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出します。 次の表に、 **SQLForeignKeys** によって通常返される SQLSTATE 値と、この関数のコンテキストでのそれぞれについて説明します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続されていたデータソースとの間の通信リンクが失敗しました。|  
|24000|カーソル状態が無効|*StatementHandle*でカーソルが開かれました。 **sqlfetch**または**sqlfetchscroll**が呼び出されました。 このエラーは、 **Sqlfetch** または **sqlfetchscroll** が SQL_NO_DATA 返されなかった場合にドライバーマネージャーによって返されます。また、 **Sqlfetch** または **sqlfetchscroll** が SQL_NO_DATA を返した場合は、ドライバーによって返されます。<br /><br /> *StatementHandle*でカーソルが開いていましたが、 **sqlfetch**または**sqlfetchscroll**が呼び出されていません。|  
|40001|シリアル化エラー|別のトランザクションでリソースのデッドロックが発生したため、トランザクションがロールバックされました。|  
|40003|ステートメントの完了が不明です|この関数の実行中に関連付けられた接続に失敗しました。トランザクションの状態を確認できません。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * \* Messagetext*バッファーの**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|*StatementHandle*に対して非同期処理が有効になりました。 関数が呼び出され、実行が完了する前に、 **SQLCancel** または **Sqlcancelhandle** が *StatementHandle*で呼び出された後、 *StatementHandle*で関数が再度呼び出されました。<br /><br /> 関数が呼び出され、実行が完了する前に、マルチスレッドアプリケーションの別のスレッドの*StatementHandle*で**SQLCancel**または**sqlcancelhandle**が呼び出されました。|  
|HY009|Null ポインターの使い方が正しくありません|(DM) 引数 *Pktablename* と *FKTableName* は両方とも null ポインターでした。<br /><br /> SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されています。 *FKCatalogName* または *PKCatalogName* 引数が null ポインターであり、SQL_CATALOG_NAME *InfoType* はカタログ名がサポートされていることを返します。<br /><br /> (DM) SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定され、 *FKSchemaName*、 *PKSchemaName*、 *FKTableName*、または *pktablename* 引数が null ポインターでした。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、SQLForeignKeys 関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または **Sqlmoreresults** が *StatementHandle* に対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。<br /><br /> (DM) 非同期的に実行されている関数 (この1つではない) が *StatementHandle* に対して呼び出され、この関数が呼び出されたときにまだ実行されています。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **Sqlbulkoperations**、 **SQLSetPos** が *StatementHandle* に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY090|文字列またはバッファーの長さが無効です|(DM) 名前の長さの引数のいずれかの値が0未満ですが SQL_NTS と等しくありません。|  
|||名前の長さの引数のいずれかの値が、対応する名前の最大長の値を超えました。 (「コメント」を参照してください)。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYC00|省略可能な機能は実装されていません|カタログ名が指定されていますが、ドライバーまたはデータソースがカタログをサポートしていません。<br /><br /> スキーマ名が指定されましたが、ドライバーまたはデータソースがスキーマをサポートしていません。|  
|||SQL_ATTR_CONCURRENCY および SQL_ATTR_CURSOR_TYPE statement 属性の現在の設定の組み合わせは、ドライバーまたはデータソースではサポートされていませんでした。<br /><br /> SQL_ATTR_USE_BOOKMARKS statement 属性が SQL_UB_VARIABLE に設定されており、SQL_ATTR_CURSOR_TYPE statement 属性が、ドライバーがブックマークをサポートしていないカーソルの種類に設定されました。|  
|HYT00|タイムアウトに達しました|データソースから結果セットが返される前に、クエリのタイムアウト期間が経過しました。 タイムアウト期間は、 **SQLSetStmtAttr**、SQL_ATTR_QUERY_TIMEOUT によって設定されます。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle* に関連付けられているドライバーでは、関数はサポートされていません。|  
|IM017|非同期通知モードでは、ポーリングは無効になっています|通知モデルが使用されるたびに、ポーリングは無効になります。|  
|IM018|**Sqlcompleteasync** は、このハンドルで前の非同期操作を完了するために呼び出されていません。|ハンドルに対する前の関数呼び出しが SQL_STILL_EXECUTING を返し、通知モードが有効になっている場合は、処理を完了するために、ハンドルに対して **Sqlcompleteasync** を呼び出す必要があります。|  
  
## <a name="comments"></a>コメント  
 この関数によって返される情報の使用方法については、「 [カタログデータの使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)」を参照してください。  
  
 \* *Pktablename*にテーブル名が含まれている場合、 **SQLForeignKeys**は、指定されたテーブルの主キーとそれを参照するすべての外部キーを含む結果セットを返します。 他のテーブルの外部キーの一覧には、指定されたテーブル内の unique 制約を指す外部キーは含まれません。  
  
 \* *FKTableName*にテーブル名が含まれている場合、 **SQLForeignKeys**は、他のテーブルの主キーを指す、指定されたテーブル内のすべての外部キー、および参照先の他のテーブルの主キーを含む結果セットを返します。 指定されたテーブル内の外部キーの一覧に、他のテーブルの unique 制約を参照する外部キーが含まれていません。  
  
 \* *Pktablename*と FKTableName の両方に \* *FKTableName*テーブル名が含まれている場合、 **SQLForeignKeys**は、 \* **pktablename*で指定されたテーブルの主キーを参照する、 *FKTableName*で指定されたテーブル内の外部キーを返します。 これは、最大で1つのキーにする必要があります。  
  
> [!NOTE]  
>  一般的な使用、引数、および ODBC カタログ関数の返されるデータの詳細については、「 [カタログ関数](../../../odbc/reference/develop-app/catalog-functions.md)」を参照してください。  
  
 **SQLForeignKeys** は、結果を標準の結果セットとして返します。 主キーに関連付けられている外部キーが要求された場合、結果セットは FKTABLE_CAT、FKTABLE_SCHEM、FKTABLE_NAME、および KEY_SEQ 順に並べ替えられます。 外部キーに関連付けられている主キーが要求された場合、結果セットは PKTABLE_CAT、PKTABLE_SCHEM、PKTABLE_NAME、および KEY_SEQ 順に並べ替えられます。 次の表に、結果セット内の列の一覧を示します。  
  
 VARCHAR 型の列の長さはテーブルには表示されません。実際の長さは、データソースによって異なります。 PKTABLE_CAT または FKTABLE_CAT の実際の長さ、PKTABLE_SCHEM または FKTABLE_SCHEM、PKTABLE_NAME または FKTABLE_NAME、PKCOLUMN_NAME または FKCOLUMN_NAME の各列を特定するために、アプリケーションは SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN、SQL_MAX_TABLE_NAME_LEN、および SQL_MAX_COLUMN_NAME_LEN の各オプションを使用して **SQLGetInfo** を呼び出すことができます。  
  
 ODBC 3 *. x*では、次の列の名前が変更されました。 アプリケーションは列番号でバインドされるため、列名の変更は旧バージョンとの互換性に影響しません。  
  
|ODBC 2.0 列|ODBC 3 *. x* 列|  
|---------------------|-----------------------|  
|PKTABLE_QUALIFIER|PKTABLE_CAT|  
|PKTABLE_OWNER|PKTABLE_SCHEM|  
|FKTABLE_QUALIFIER|FK_TABLE_CAT|  
|FKTABLE_OWNER|FKTABLE_SCHEM|  
  
 次の表に、結果セット内の列の一覧を示します。 列 14 (解説) 以外の列は、ドライバーで定義できます。 アプリケーションでは、明示的な序数位置を指定するのではなく、結果セットの末尾からカウントすることで、ドライバー固有の列にアクセスする必要があります。 詳細については、「 [カタログ関数によって返されるデータ](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)」を参照してください。  
  
|列名|列番号|データ型|コメント|  
|-----------------|-------------------|---------------|--------------|  
|PKTABLE_CAT (ODBC 1.0)|1|Varchar|主キーテーブルカタログ名。データソースに適用されない場合は NULL です。 ドライバーが一部のテーブルのカタログをサポートしていても、他のテーブルではサポートされていない場合 (ドライバーが異なる Dbms からデータを取得する場合など)、カタログを持たないテーブルに対して空の文字列 ("") が返されます。|  
|PKTABLE_SCHEM (ODBC 1.0)|2|Varchar|主キーテーブルのスキーマ名です。データソースに適用されない場合は NULL です。 ドライバーがいくつかのテーブルのスキーマをサポートしていても、他のテーブルではサポートされていない場合 (ドライバーが異なる Dbms からデータを取得する場合など) は、スキーマがないテーブルに対して空の文字列 ("") を返します。|  
|PKTABLE_NAME (ODBC 1.0)|3|Varchar not NULL|主キーテーブルの名前。|  
|PKCOLUMN_NAME (ODBC 1.0)|4|Varchar not NULL|主キー列の名前。 ドライバーは、名前のない列に対して空の文字列を返します。|  
|FKTABLE_CAT (ODBC 1.0)|5|Varchar|外部キーテーブルカタログ名;データソースに適用されない場合は NULL です。 ドライバーが一部のテーブルのカタログをサポートしていても、他のテーブルではサポートされていない場合 (ドライバーが異なる Dbms からデータを取得する場合など)、カタログを持たないテーブルに対して空の文字列 ("") が返されます。|  
|FKTABLE_SCHEM (ODBC 1.0)|6|Varchar|外部キーテーブルスキーマ名;データソースに適用されない場合は NULL です。 ドライバーがいくつかのテーブルのスキーマをサポートしていても、他のテーブルではサポートされていない場合 (ドライバーが異なる Dbms からデータを取得する場合など) は、スキーマがないテーブルに対して空の文字列 ("") を返します。|  
|FKTABLE_NAME (ODBC 1.0)|7|Varchar not NULL|外部キーテーブルの名前。|  
|FKCOLUMN_NAME (ODBC 1.0)|8|Varchar not NULL|外部キー列の名前。 ドライバーは、名前のない列に対して空の文字列を返します。|  
|KEY_SEQ (ODBC 1.0)|9|Smallint (NULL 以外)|キーの列シーケンス番号 (1 から始まります)。|  
|UPDATE_RULE (ODBC 1.0)|10|Smallint|SQL 操作が **更新**されるときに、外部キーに適用されるアクションです。 には、次のいずれかの値を指定できます。 (参照されるテーブルは主キーを持つテーブルです。参照元のテーブルは、外部キーを持つテーブルです)。<br /><br /> SQL_CASCADE: 参照されるテーブルの主キーが更新されると、参照元のテーブルの外部キーも更新されます。<br /><br /> SQL_NO_ACTION: 参照されるテーブルの主キーの更新によって参照元のテーブルで "ぶら下がり参照" が発生する場合 (つまり、参照元のテーブルの行には、参照先のテーブルに対応する行が存在しない場合)、更新は拒否されます。 参照元のテーブルの外部キーの更新によって、参照先のテーブルの主キーの値として存在しない値が導入された場合、更新は拒否されます。 (このアクションは、ODBC 2.x の SQL_RESTRICT 操作と同じ*です)。*<br /><br /> SQL_SET_NULL: 主キーの1つ以上のコンポーネントが変更されるように、参照先のテーブル内の1つ以上の行が更新された場合、主キーの変更されたコンポーネントに対応する、参照元のテーブルの外部キーのコンポーネントは、参照元のテーブルの一致するすべての行で NULL に設定されます。<br /><br /> SQL_SET_DEFAULT: 主キーの1つ以上のコンポーネントが変更されるように、参照先のテーブル内の1つ以上の行が更新されると、主キーの変更されたコンポーネントに対応する、参照元のテーブル内の外部キーのコンポーネントは、参照元のテーブルの一致するすべての行で適用可能な既定値に設定されます<br /><br /> データソースに適用されない場合は NULL です。|  
|DELETE_RULE (ODBC 1.0)|11|Smallint|SQL 操作が **削除**されるときに、外部キーに適用されるアクションです。 には、次のいずれかの値を指定できます。 (参照されるテーブルは主キーを持つテーブルです。参照元のテーブルは、外部キーを持つテーブルです)。<br /><br /> SQL_CASCADE: 参照先のテーブルの行が削除されると、参照元のテーブル内の一致するすべての行も削除されます。<br /><br /> SQL_NO_ACTION: 参照先のテーブル内の行を削除すると、参照元のテーブルで "ぶら下がり参照" が発生する場合があります (つまり、参照元のテーブルの行が参照先のテーブルに存在しない場合)、更新は拒否されます。 (このアクションは、ODBC 2.x の SQL_RESTRICT 操作と同じ*です)。*<br /><br /> SQL_SET_NULL: 参照されるテーブルの1つ以上の行が削除されると、参照元のテーブルのすべての一致する行で、参照元のテーブルの外部キーの各コンポーネントが NULL に設定されます。<br /><br /> SQL_SET_DEFAULT: 参照されるテーブルの1つ以上の行が削除されると、参照元のテーブルのすべての一致する行で、参照元のテーブルの外部キーの各コンポーネントが該当する既定値に設定されます。<br /><br /> データソースに適用されない場合は NULL です。|  
|FK_NAME (ODBC 2.0)|12|Varchar|外部キー名。 データソースに適用されない場合は NULL です。|  
|PK_NAME (ODBC 2.0)|13|Varchar|主キー名。 データソースに適用されない場合は NULL です。|  
|DEFERRABILITY (ODBC 3.0)|14|Smallint|SQL_INITIALLY_DEFERRED、SQL_INITIALLY_IMMEDIATE、SQL_NOT_DEFERRABLE。|  
  
## <a name="code-example"></a>コード例  
 次の表に示すように、この例では、ORDERS、LINES、および CUSTOMERS という3つのテーブルを使用します。  
  
|ORDERS|波線|企業|  
|------------|-----------|---------------|  
|ORDERID|ORDERID|CUSTID|  
|CUSTID|波線|NAME|  
|OPENDATE|PARTID|先|  
|売上高|済|電話|  
|状態|||  
  
 ORDERS テーブルで、CUSTID は、販売が行われた顧客を識別します。 これは CUSTOMERS テーブルの CUSTID を参照する外部キーです。  
  
 LINES テーブルで、ORDERID は、品目が関連付けられている販売注文を識別します。 ORDERS テーブルの ORDERID を参照する外部キーです。  
  
 この例では、 **Sqlprimarykeys** を呼び出して ORDERS テーブルの主キーを取得します。 結果セットには1つの行が含まれます。次の表に、有意な列を示します。  
  
|TABLE_NAME|COLUMN_NAME|KEY_SEQ|  
|-----------------|------------------|--------------|  
|ORDERS|ORDERID|1|  
  
 次に、 **SQLForeignKeys** を呼び出して、ORDERS テーブルの主キーを参照する他のテーブル内の外部キーを取得します。 結果セットには1つの行が含まれます。次の表に、有意な列を示します。  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|ORDERS|CUSTID|波線|CUSTID|1|  
  
 最後に、この例では、 **SQLForeignKeys** を呼び出して、他のテーブルの主キーを参照する ORDERS テーブル内の外部キーを取得します。 結果セットには1つの行が含まれます。次の表に、有意な列を示します。  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|企業|CUSTID|ORDERS|CUSTID|1|  
  
```cpp  
#define TAB_LEN SQL_MAX_TABLE_NAME_LEN + 1  
#define COL_LEN SQL_MAX_COLUMN_NAME_LEN + 1  
  
LPSTR   szTable;              /* Table to display */  
  
UCHAR szPkTable[TAB_LEN];   /* Primary key table name */  
UCHAR szFkTable[TAB_LEN];   /* Foreign key table name */  
UCHAR szPkCol[COL_LEN];     /* Primary key column */  
UCHAR szFkCol[COL_LEN];     /* Foreign key column */  
  
SQLHSTMT      hstmt;  
SQLINTEGER    cbPkTable, cbPkCol, cbFkTable, cbFkCol, cbKeySeq;  
SQLSMALLINT   iKeySeq;  
SQLRETURN     retcode;  
  
// Bind the columns that describe the primary and foreign keys.  
// Ignore the table schema, name, and catalog for this example.  
  
SQLBindCol(hstmt, 3, SQL_C_CHAR, szPkTable, TAB_LEN, &cbPkTable);  
SQLBindCol(hstmt, 4, SQL_C_CHAR, szPkCol, COL_LEN, &cbPkCol);  
SQLBindCol(hstmt, 5, SQL_C_SSHORT, &iKeySeq, TAB_LEN, &cbKeySeq);  
SQLBindCol(hstmt, 7, SQL_C_CHAR, szFkTable, TAB_LEN, &cbFkTable);  
SQLBindCol(hstmt, 8, SQL_C_CHAR, szFkCol, COL_LEN, &cbFkCol);  
  
strcpy_s(szTable, sizeof(szTable), "ORDERS");  
  
/* Get the names of the columns in the primary key. */  
  
retcode = SQLPrimaryKeys(hstmt,  
         NULL, 0,             /* Catalog name */  
         NULL, 0,             /* Schema name */  
         szTable, SQL_NTS);   /* Table name */  
  
while ((retcode == SQL_SUCCESS) || (retcode == SQL SUCCESS_WITH_INFO)) {  
  
   /* Fetch and display the result set. This will be a list of the */  
   /* columns in the primary key of the ORDERS table. */  
  
   retcode = SQLFetch(hstmt);  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
      fprintf(out, "Table: %s Column: %s Key Seq: %hd \n", szPkTable, szPkCol,  
      iKeySeq);  
}  
  
/* Close the cursor (the hstmt is still allocated). */  
  
SQLFreeStmt(hstmt, SQL_CLOSE);  
  
/* Get all the foreign keys that refer to ORDERS primary key.*/   
  
retcode = SQLForeignKeys(hstmt,  
         NULL, 0,            /* Primary catalog */  
         NULL, 0,            /* Primary schema */  
         szTable, SQL_NTS,   /* Primary table */  
         NULL, 0,            /* Foreign catalog */  
         NULL, 0,            /* Foreign schema */  
         NULL, 0);           /* Foreign table */  
  
while ((retcode == SQL_SUCCESS) || (retcode == SQL_SUCCESS_WITH_INFO)) {  
  
/* Fetch and display the result set. This will be all of the */  
/* foreign keys in other tables that refer to the ORDERS */  
/* primary key. */  
  
   retcode = SQLFetch(hstmt);  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
      fprintf(out, "%-s ( %-s ) <-- %-s ( %-s )\n", szPkTable,  
               szPkCol, szFkTable, szFkCol);  
}  
  
/* Close the cursor (the hstmt is still allocated). */  
  
SQLFreeStmt(hstmt, SQL_CLOSE);  
  
/* Get all the foreign keys in the ORDERS table. */  
  
retcode = SQLForeignKeys(hstmt,  
         NULL, 0,             /* Primary catalog */  
         NULL, 0,             /* Primary schema */  
         NULL, 0,             /* Primary table */  
         NULL, 0,             /* Foreign catalog */  
         NULL, 0,             /* Foreign schema */  
         szTable, SQL_NTS);   /* Foreign table */  
  
while ((retcode == SQL_SUCCESS) || (retcode == SQL_SUCCESS_WITH_INFO)) {  
  
/* Fetch and display the result set. This will be all of the */  
/* primary keys in other tables that are referred to by foreign */  
/* keys in the ORDERS table. */  
  
   retcode = SQLFetch(hstmt);  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
      fprintf(out, "%-s ( %-s )--> %-s ( %-s )\n", szFkTable, szFkCol, szPkTable, szPkCol);  
}  
  
/* Free the hstmt. */  
SQLFreeStmt(hstmt, SQL_DROP);  
```  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|結果セット内の列へのバッファーのバインド|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|ステートメント処理の取り消し|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|1つの行またはデータのブロックを順方向専用にフェッチする|[SQLFetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|データのブロックのフェッチまたは結果セットのスクロール|[SQLFetchScroll 関数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|主キーの列を返す|[SQLPrimaryKeys 関数](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
|テーブルの統計とインデックスの取得|[SQLStatistics 関数](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
