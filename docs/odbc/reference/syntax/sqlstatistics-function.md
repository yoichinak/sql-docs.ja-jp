---
description: SQLStatistics 関数
title: SQLStatistics 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLStatistics
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLStatistics
helpviewer_keywords:
- SQLStatistics function [ODBC]
ms.assetid: 45210682-cfea-4e5d-9951-bcf1cbe10f41
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 71494644312b94adcd88bb85676541f7d18abd9d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421066"
---
# <a name="sqlstatistics-function"></a>SQLStatistics 関数
**互換性**  
 導入されたバージョン: ODBC 1.0 標準準拠: ISO 92  
  
 **まとめ**  
 **Sqlstatistics** は、テーブルに関連付けられた1つのテーブルとインデックスに関する統計の一覧を取得します。 ドライバーは、結果セットとして情報を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLStatistics(  
     SQLHSTMT        StatementHandle,  
     SQLCHAR *       CatalogName,  
     SQLSMALLINT     NameLength1,  
     SQLCHAR *       SchemaName,  
     SQLSMALLINT     NameLength2,  
     SQLCHAR *       TableName,  
     SQLSMALLINT     NameLength3,  
     SQLUSMALLINT    Unique,  
     SQLUSMALLINT    Reserved);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル。  
  
 *CatalogName*  
 代入カタログ名。 ドライバーが一部のテーブルのカタログをサポートしていても、他のテーブルではサポートされていない場合 (ドライバーがさまざまな Dbms からデータを取得する場合など)、空の文字列 ("") は、カタログを持たないテーブルを示します。 *CatalogName* に文字列検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *CatalogName* は識別子として扱われ、大文字小文字は区別されません。 SQL_FALSE の場合、 *CatalogName* は通常の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。 詳細については、「 [カタログ関数の引数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)」を参照してください。  
  
 *NameLength1*  
 代入**CatalogName*の文字数。  
  
 *SchemaName*  
 代入スキーマ名。 ドライバーがいくつかのテーブルのスキーマをサポートしていても、他のテーブルのスキーマをサポートしていない場合 (ドライバーが異なる Dbms からデータを取得する場合など)、空の文字列 ("") はスキーマを持たないテーブルを示します。 *SchemaName* に文字列検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *SchemaName* は識別子として扱われ、大文字小文字は区別されません。 SQL_FALSE の場合、 *SchemaName* は通常の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。  
  
 *NameLength2*  
 代入**SchemaName*の文字数。  
  
 *TableName*  
 代入テーブル名。 この引数を null ポインターにすることはできません。 *SchemaName* に文字列検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されている場合、 *TableName* は識別子として扱われ、その大文字と小文字は区別されません。 SQL_FALSE の場合、 *TableName* は通常の引数です。これは文字どおりに処理され、大文字と小文字が区別されます。  
  
 *NameLength3*  
 代入**TableName*の長さ (文字数)。  
  
 *[一意]*  
 代入インデックスの種類: SQL_INDEX_UNIQUE または SQL_INDEX_ALL。  
  
 *予約済み*  
 代入結果セットのカーディナリティ列とページ列の重要度を示します。 次のオプションは、カーディナリティ列とページ列の戻り値にのみ影響します。カーディナリティとページが返されない場合でも、インデックス情報が返されます。  
  
 SQL_ENSURE は、ドライバーが無条件に統計を取得することを要求します。 (Open Group standard にのみ準拠しており、ODBC 拡張機能をサポートしていないドライバーは、SQL_ENSURE をサポートできません)。  
  
 SQL_QUICK は、サーバーからすぐに使用できる場合にのみ、ドライバーがカーディナリティとページを取得することを要求します。 この場合、ドライバーで取得される値が最新であるかどうかは保証されません。 (Open Group standard に書き込まれたアプリケーションは、常に ODBC *3. x*互換のドライバーから SQL_QUICK 動作します)。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **Sqlstatistics**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合、関連付けられた SQLSTATE 値を取得するには、 *Handletype* SQL_HANDLE_STMT と*StatementHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出します。 次の表に、 **Sqlstatistics** によって通常返される SQLSTATE 値の一覧を示し、この関数のコンテキストでそれぞれについて説明します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続されていたデータソースとの間の通信リンクが失敗しました。|  
|24000|カーソル状態が無効|*StatementHandle*でカーソルが開かれました。 **sqlfetch**または**sqlfetchscroll**が呼び出されました。 このエラーは、sqlfetch または**Sqlfetchscroll**が SQL_NO_DATA 返されず、 **Sqlfetch**または**sqlfetchscroll**が SQL_NO_DATA を返した場合にドライバーによって返され**た場合に**、ドライバーマネージャーによって返されます。<br /><br /> *StatementHandle*でカーソルが開いていましたが、 **sqlfetch**または**sqlfetchscroll**が呼び出されていません。|  
|40001|シリアル化エラー|別のトランザクションでリソースのデッドロックが発生したため、トランザクションがロールバックされました。|  
|40003|ステートメントの完了が不明です|この関数の実行中に関連付けられた接続に失敗しました。トランザクションの状態を確認できません。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * \* Messagetext*バッファーの**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|*StatementHandle*に対して非同期処理が有効になりました。 関数が呼び出され、実行が完了する前に、 **SQLCancel** または **Sqlcancelhandle** が *StatementHandle*で呼び出された後、 *StatementHandle*で関数が再度呼び出されました。<br /><br /> 関数が呼び出され、実行が完了する前に、マルチスレッドアプリケーションの別のスレッドの*StatementHandle*で**SQLCancel**または**sqlcancelhandle**が呼び出されました。|  
|HY009|Null ポインターの使い方が正しくありません|*TableName*引数が null ポインターでした。<br /><br /> SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定されました。 *CatalogName* 引数は null ポインターで、SQL_CATALOG_NAME *InfoType* はカタログ名がサポートされていることを返します。<br /><br /> (DM) SQL_ATTR_METADATA_ID statement 属性が SQL_TRUE に設定され、 *SchemaName* 引数が null ポインターでした。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、 **Sqlstatistics** 関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または **Sqlmoreresults** が *StatementHandle* に対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。<br /><br /> (DM) 非同期的に実行されている関数 (この1つではない) が *StatementHandle* に対して呼び出され、この関数が呼び出されたときにまだ実行されています。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **Sqlbulkoperations**、 **SQLSetPos** が *StatementHandle* に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY090|文字列またはバッファーの長さが無効です|(DM) 名前の長さの引数のいずれかの値が0未満ですが SQL_NTS と等しくありません。<br /><br /> 名前の長さの引数のいずれかの値が、対応する名前の最大長の値を超えました。|  
|HY100|一意性オプションの型が有効範囲にありません|(DM) 無効な *一意* の値が指定されました。|  
|HY101|精度オプションの型が有効範囲にありません|(DM) 無効な *予約* 値が指定されました。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYC00|省略可能な機能は実装されていません|カタログが指定されましたが、ドライバーまたはデータソースがカタログをサポートしていません。<br /><br /> スキーマが指定されましたが、ドライバーまたはデータソースがスキーマをサポートしていません。<br /><br /> SQL_ATTR_CONCURRENCY および SQL_ATTR_CURSOR_TYPE statement 属性の現在の設定の組み合わせは、ドライバーまたはデータソースではサポートされていませんでした。<br /><br /> SQL_ATTR_USE_BOOKMARKS statement 属性が SQL_UB_VARIABLE に設定されており、SQL_ATTR_CURSOR_TYPE statement 属性が、ドライバーがブックマークをサポートしていないカーソルの種類に設定されました。|  
|HYT00|タイムアウトに達しました|データソースが要求された結果セットを返す前に、クエリのタイムアウト期間が経過しました。 タイムアウト期間は、 **SQLSetStmtAttr**、SQL_ATTR_QUERY_TIMEOUT によって設定されます。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle* に関連付けられているドライバーでは、関数はサポートされていません。|  
|IM017|非同期通知モードでは、ポーリングは無効になっています|通知モデルが使用されるたびに、ポーリングは無効になります。|  
|IM018|**Sqlcompleteasync** は、このハンドルで前の非同期操作を完了するために呼び出されていません。|ハンドルに対する前の関数呼び出しが SQL_STILL_EXECUTING を返し、通知モードが有効になっている場合は、処理を完了するために、ハンドルに対して **Sqlcompleteasync** を呼び出す必要があります。|  
  
## <a name="comments"></a>コメント  
 **Sqlstatistics** は、1つのテーブルに関する情報を、NON_UNIQUE、種類、INDEX_QUALIFIER、INDEX_NAME、および ORDINAL_POSITION 順に並べ替えて、標準の結果セットとして返します。 結果セットは、テーブルの統計情報 (結果セットのカーディナリティとページ列) を、各インデックスに関する情報と組み合わせて使用します。 この情報の使用方法については、「 [カタログデータの使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)」を参照してください。  
  
 TABLE_CAT、TABLE_SCHEM、TABLE_NAME、および COLUMN_NAME 列の実際の長さを確認するには、アプリケーションで、SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN、SQL_MAX_TABLE_NAME_LEN、および SQL_MAX_COLUMN_NAME_LEN の各オプションを指定して **SQLGetInfo** を呼び出すことができます。  
  
> [!NOTE]  
>  一般的な使用、引数、および ODBC カタログ関数の返されるデータの詳細については、「 [カタログ関数](../../../odbc/reference/develop-app/catalog-functions.md)」を参照してください。  
  
 ODBC *3. x*では、次の列の名前が変更されました。 アプリケーションは列番号でバインドされるため、列名の変更は旧バージョンとの互換性に影響しません。  
  
|ODBC 2.0 列|ODBC *3. x* 列|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|SEQ_IN_INDEX|ORDINAL_POSITION|  
|COLLATION|ASC_OR_DESC|  
  
 次の表に、結果セット内の列の一覧を示します。 このドライバーでは、列 13 (FILTER_CONDITION) を超える追加の列を定義できます。 アプリケーションでは、明示的な序数位置を指定するのではなく、結果セットの末尾からカウントすることで、ドライバー固有の列にアクセスする必要があります。 詳細については、「 [カタログ関数によって返されるデータ](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)」を参照してください。  
  
|列名|列番号|データ型|コメント|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|統計またはインデックスが適用されるテーブルのカタログ名。データソースに適用されない場合は NULL です。 ドライバーが一部のテーブルのカタログをサポートしていても、他のテーブルではサポートされていない場合 (ドライバーが異なる Dbms からデータを取得する場合など)、カタログを持たないテーブルに対して空の文字列 ("") が返されます。|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|統計またはインデックスが適用されるテーブルのスキーマ名。データソースに適用されない場合は NULL です。 ドライバーがいくつかのテーブルのスキーマをサポートしていても、他のテーブルではサポートされていない場合 (ドライバーが異なる Dbms からデータを取得する場合など) は、スキーマがないテーブルに対して空の文字列 ("") を返します。|  
|TABLE_NAME (ODBC 1.0)|3|Varchar not NULL|統計またはインデックスが適用されるテーブルのテーブル名。|  
|NON_UNIQUE (ODBC 1.0)|4|Smallint|インデックスで重複する値が許可されていないかどうかを示します。<br /><br /> インデックス値が一意でない可能性がある場合は SQL_TRUE します。<br /><br /> インデックス値が一意である必要がある場合は SQL_FALSE します。<br /><br /> TYPE が SQL_TABLE_STAT の場合、NULL が返されます。|  
|INDEX_QUALIFIER (ODBC 1.0)|5|Varchar|**DROP INDEX**の実行時にインデックス名を修飾するために使用される識別子です。インデックス修飾子がデータソースでサポートされていない場合、または型が SQL_TABLE_STAT 場合、NULL が返されます。 この列に null 以外の値が返された場合は、 **DROP INDEX** ステートメントでインデックス名を修飾するために使用する必要があります。それ以外の場合は、TABLE_SCHEM を使用してインデックス名を修飾する必要があります。|  
|INDEX_NAME (ODBC 1.0)|6|Varchar|インデックス名;TYPE が SQL_TABLE_STAT の場合、NULL が返されます。|  
|型 (ODBC 1.0)|7|Smallint (NULL 以外)|返される情報の種類:<br /><br /> SQL_TABLE_STAT ([カーディナリティ] 列または [ページ] 列の) テーブルの統計情報を示します。<br /><br /> SQL_INDEX_BTREE B ツリーインデックスを示します。<br /><br /> SQL_INDEX_CLUSTERED は、クラスター化インデックスを示します。<br /><br /> SQL_INDEX_CONTENT コンテンツインデックスを示します。<br /><br /> SQL_INDEX_HASHED は、ハッシュされたインデックスを示します。<br /><br /> SQL_INDEX_OTHER 別の種類のインデックスを示します。|  
|ORDINAL_POSITION (ODBC 1.0)|8|Smallint|インデックス内の列のシーケンス番号 (1 から始まります)。TYPE が SQL_TABLE_STAT の場合、NULL が返されます。|  
|COLUMN_NAME (ODBC 1.0)|9|Varchar|列名。 列が SALARY + 特典などの式に基づいている場合、式が返されます。式を特定できない場合は、空の文字列が返されます。 TYPE が SQL_TABLE_STAT の場合、NULL が返されます。|  
|ASC_OR_DESC (ODBC 1.0)|10|Char(1)|列の並べ替え順序: "A" (昇順)降順の場合は "D"。列の並べ替え順序がデータソースでサポートされていない場合、または型が SQL_TABLE_STAT 場合、NULL が返されます。|  
|カーディナリティ (ODBC 1.0)|11|Integer|テーブルまたはインデックスのカーディナリティ型が SQL_TABLE_STAT の場合は、テーブル内の行の数型が SQL_TABLE_STAT でない場合は、インデックス内の一意の値の数。値がデータソースから使用できない場合、NULL が返されます。|  
|ページ (ODBC 1.0)|12|Integer|インデックスまたはテーブルを格納するために使用されるページ数。型が SQL_TABLE_STAT の場合、テーブルのページ数型が SQL_TABLE_STAT でない場合は、インデックスのページ数値がデータソースから使用できない場合、またはデータソースに適用できない場合は NULL が返されます。|  
|FILTER_CONDITION (ODBC 2.0)|13|Varchar|インデックスがフィルター選択されたインデックスの場合は、給与 > 3万; のようなフィルター条件になります。フィルター条件を特定できない場合、これは空の文字列になります。<br /><br /> NULL インデックスがフィルター選択されたインデックスでない場合は、インデックスがフィルター選択されたインデックスであるか、型が SQL_TABLE_STAT かどうかを判断できません。|  
  
 結果セットの行がテーブルに対応している場合、ドライバーは TYPE を SQL_TABLE_STAT に設定し、NON_UNIQUE、INDEX_QUALIFIER、INDEX_NAME、ORDINAL_POSITION、COLUMN_NAME、および ASC_OR_DESC を NULL に設定します。 カーディナリティまたはページがデータソースから使用できない場合、ドライバーはそれらを NULL に設定します。  
  
## <a name="code-example"></a>コード例  
 同様の関数のコード例については、「 [Sqlcolumns](../../../odbc/reference/syntax/sqlcolumns-function.md)」を参照してください。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|結果セット内の列へのバッファーのバインド|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|ステートメント処理の取り消し|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|1つの行またはデータのブロックを順方向専用にフェッチします。|[SQLFetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|データのブロックのフェッチまたは結果セットのスクロール|[SQLFetchScroll 関数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|外部キーの列を返す|[SQLForeignKeys 関数](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|  
|主キーの列を返す|[SQLPrimaryKeys 関数](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
