---
description: SQLSetCursorName 関数
title: SQLSetCursorName 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetCursorName
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetCursorName
helpviewer_keywords:
- SQLSetCursorName function [ODBC]
ms.assetid: 4e055946-12d4-4589-9891-41617a50f34e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1a7deee4ecb37225260f011d4944e992f16d94e1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499491"
---
# <a name="sqlsetcursorname-function"></a>SQLSetCursorName 関数
**互換性**  
 導入されたバージョン: ODBC 1.0 標準準拠: ISO 92  
  
 **まとめ**  
 **SQLSetCursorName** は、カーソル名をアクティブステートメントに関連付けます。 アプリケーションが **SQLSetCursorName**を呼び出さない場合、ドライバーは SQL ステートメントの処理に必要なカーソル名を生成します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLSetCursorName(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CursorName,  
     SQLSMALLINT   NameLength);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル。  
  
 *カーソル名*  
 代入カーソル名。 効率的な処理を行うには、カーソル名に先頭または末尾のスペースを含めないでください。カーソル名に区切られた識別子が含まれている場合、区切り記号はカーソル名の最初の文字として配置する必要があります。  
  
 *NameLength*  
 代入**カーソル名*の長さ (文字数)。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **SQLSetCursorName**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合、関連付けられた SQLSTATE 値を取得するには、 *Handletype* SQL_HANDLE_STMT と*StatementHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出します。 次の表に、 **SQLSetCursorName** によって一般的に返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データ、右側が切り捨てられました|カーソル名が最大値を超えているため、使用可能な最大文字数のみが使用されました。|  
|24000|カーソル状態が無効|*StatementHandle*に対応するステートメントが既に実行されているか、カーソルが置かれた状態になっています。|  
|34000|カーソル名が無効|**Cursor name* で指定されたカーソル名は、ドライバーによって定義された最大長を超えたか、または "sqlcur 存在する" または "SQL_CUR" で開始されたため、無効でした。|  
|3C000|カーソル名が重複しています|**Cursor name* で指定されたカーソル名は既に存在します。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * \* Messagetext*バッファーの**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY009|Null ポインターの使い方が正しくありません|(DM) 引数の *カーソル名* は null ポインターでした。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この aynchronous 関数は、 **SQLSetCursorName** 関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) 非同期的に実行する関数が *StatementHandle* に対して呼び出されましたが、この関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **Sqlbulkoperations**、 **SQLSetPos** が *StatementHandle* に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY090|文字列またはバッファーの長さが無効です|(DM) 引数 *NameLength* は0未満ですが SQL_NTS と等しくありません。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle* に関連付けられているドライバーでは、関数はサポートされていません。|  
  
## <a name="comments"></a>コメント  
 カーソル名は、位置指定の update および delete ステートメントでのみ使用されます (例:**更新**_テーブル名_..._カーソル名_**の現在の場所**)。 詳細については、「配置された [Update ステートメントと Delete ステートメント](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)」を参照してください。 アプリケーションがカーソル名を定義するために **SQLSetCursorName** を呼び出さない場合、クエリステートメントの実行時に、ドライバーは SQL_CUR 文字で始まる名前を生成し、18文字を超えないようにします。  
  
 接続内のすべてのカーソル名は一意である必要があります。 カーソル名の最大長は、ドライバーによって定義されます。 相互運用性を最大にするには、アプリケーションでカーソル名を18文字以下に制限することをお勧めします。 ODBC 3.x で*は、カーソル*名が引用符で囲まれた識別子である場合は、大文字と小文字を区別して処理されます。また、SQL の構文で許可されない文字や、空白や予約済みのキーワードなど、特別に扱わない文字を含めることができます。 カーソル名を大文字と小文字を区別する方法で処理する必要がある場合は、引用符で囲まれた識別子として渡す必要があります。  
  
 明示的または暗黙的に設定されたカーソル名は、 **Sqlfreehandle**を使用して、関連付けられているステートメントが削除されるまで設定されたままになります。 **SQLSetCursorName** は、カーソルが割り当てられた状態または準備済みの状態である限り、ステートメントのカーソルの名前を変更するために呼び出すことができます。  
  
## <a name="code-example"></a>コード例  
 次の例では、アプリケーションで **SQLSetCursorName** を使用して、ステートメントのカーソル名を設定します。 次に、そのステートメントを使用して CUSTOMERS テーブルから結果を取得します。 最後に、位置指定更新を実行して John Smith の電話番号を変更します。 アプリケーションでは、 **select** ステートメントと **UPDATE** ステートメントに対して異なるステートメントハンドルを使用することに注意してください。  
  
 別のコード例については、「 [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)」を参照してください。  
  
```cpp  
#define NAME_LEN 50  
#define PHONE_LEN 10  
  
SQLHSTMT     hstmtSelect,  
SQLHSTMT     hstmtUpdate;  
SQLRETURN    retcode;  
SQLHDBC      hdbc;  
SQLCHAR      szName[NAME_LEN], szPhone[PHONE_LEN];  
SQLINTEGER   cbName, cbPhone;  
  
/* Allocate the statements and set the cursor name. */  
  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmtSelect);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmtUpdate);  
SQLSetCursorName(hstmtSelect, "C1", SQL_NTS);  
  
/* SELECT the result set and bind its columns to local buffers. */  
  
SQLExecDirect(hstmtSelect,  
      "SELECT NAME, PHONE FROM CUSTOMERS",  
      SQL_NTS);  
SQLBindCol(hstmtSelect, 1, SQL_C_CHAR, szName, NAME_LEN, &cbName);  
SQLBindCol(hstmtSelect, 2, SQL_C_CHAR, szPhone, PHONE_LEN, &cbPhone);  
  
/* Read through the result set until the cursor is */  
/* positioned on the row for John Smith. */  
  
do  
 retcode = SQLFetch(hstmtSelect);  
while ((retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) &&  
   (strcmp(szName, "Smith, John") != 0));  
  
/* Perform a positioned update of John Smith's name. */  
  
if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
   SQLExecDirect(hstmtUpdate,  
   "UPDATE EMPLOYEE SET PHONE=\"2064890154\" WHERE CURRENT OF C1",  
   SQL_NTS);  
}  
```  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|SQL ステートメントの実行|[SQLExecDirect 関数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|準備された SQL ステートメントの実行|[SQLExecute 関数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|カーソル名を返す|[SQLGetCursorName 関数](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|カーソルのスクロールオプションの設定|[SQLSetScrollOptions 関数](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
