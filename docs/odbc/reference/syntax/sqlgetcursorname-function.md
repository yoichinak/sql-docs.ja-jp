---
description: SQLGetCursorName 関数
title: Sqlgetカーソル名関数 |Microsoft Docs
ms.custom: ''
ms.date: 06/12/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetCursorName
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetCursorName
helpviewer_keywords:
- SQLGetCursorName function [ODBC]
ms.assetid: e6e92199-7bb6-447c-8987-049a4c6ce05d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 454a6630afb565381b8dfc457c5c34a1194ccf63
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461104"
---
# <a name="sqlgetcursorname-function"></a>SQLGetCursorName 関数
**互換性**  
 導入されたバージョン: ODBC 1.0 標準準拠: ISO 92  
  
 **まとめ**  
 **Sqlgetcursor name** は、指定したステートメントに関連付けられているカーソル名を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLGetCursorName(  
     SQLHSTMT        StatementHandle,  
     SQLCHAR *       CursorName,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   NameLengthPtr);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル。  
  
 *カーソル名*  
 Outputカーソル名を返すバッファーへのポインター。  
  
 *カーソル名*が NULL の場合、 *NameLengthPtr*は、*カーソル名*が指すバッファー内で返すことができる文字の合計数 (文字データの null 終端文字を除く) を返します。  
  
 *BufferLength*  
 代入 \**カーソル名*の長さ (文字数)。 
  
 *NameLengthPtr*  
 Output \**カーソル名*で返すことができる文字の合計数 (null 終端文字を除く) を返すメモリへのポインター。 戻り値として使用できる文字数が*Bufferlength*以上の場合は、cursor name のカーソル名 \* が*bufferlength*に切り捨てら*れ、* null 終端文字の長さを引いた値になります。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **Sqlgetcursorname**が SQL_ERROR または SQL_SUCCESS_WITH_INFO のいずれかを返す場合、関連付けられた SQLSTATE 値を取得するには、 *handletype*が SQL_HANDLE_STMT で、*ハンドル*が*StatementHandle*である**SQLGetDiagRec**を呼び出します。 次の表に、 **Sqlgetカーソル名** によって一般的に返される SQLSTATE 値の一覧を示します。この関数のコンテキストでは、それぞれについて説明します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データ、右側が切り捨てられました|バッファーカーソル名がカーソル名全体を返すの \* *CursorName*に十分な大きさではないため、カーソル名が切り詰められました。 切り捨てられていないカーソル名の長さは **NameLengthPtr*で返されます。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * \* Messagetext*バッファーの**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、 **Sqlgetカーソル名** 関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または **Sqlmoreresults** が *StatementHandle* に対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。<br /><br /> (DM) 非同期的に実行する関数が *StatementHandle* に対して呼び出されましたが、この関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **Sqlbulkoperations**、 **SQLSetPos** が *StatementHandle* に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY015|使用可能なカーソル名がありません|(DM) ドライバーは ODBC*2.x ドライバーでし* たが、ステートメントに開いているカーソルがなかったため、 **SQLSetCursorName**でカーソル名が設定されていませんでした。|  
|HY090|文字列またはバッファーの長さが無効です|(DM) 引数 *Bufferlength* に指定された値が0未満でした。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle* に関連付けられているドライバーでは、関数はサポートされていません。|  
  
## <a name="comments"></a>コメント  
 カーソル名は、位置指定の update および delete ステートメントでのみ使用されます (例:**更新**_テーブル名_..._カーソル名_**の現在の場所**)。 詳細については、「配置された [Update ステートメントと Delete ステートメント](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)」を参照してください。 アプリケーションがカーソル名を定義するために **SQLSetCursorName** を呼び出さない場合は、ドライバーによって名前が生成されます。 この名前は SQL_CUR 文字で始まります。  
  
> [!NOTE]
>  ODBC 2.x で*は、開い*ているカーソルがなく、 **SQLSetCursorName**の呼び出しによって名前が設定されていない場合、 **sqlgetcursor NAME** を呼び出すと SQLSTATE HY015 が返されます (カーソル名は使用できません)。 ODBC 3 *. x*では、これは無効です。 **Sqlgetcursor name** が呼び出されるタイミングに関係なく、ドライバーはカーソル名を返します。  
  
 **Sqlgetcursor name** は、明示的または暗黙的に作成された名前であるかどうかにかかわらず、カーソルの名前を返します。 **SQLSetCursorName**が呼び出されない場合、カーソル名は暗黙的に生成されます。 **SQLSetCursorName** は、カーソルが割り当てられた状態または準備済みの状態である限り、ステートメントのカーソルの名前を変更するために呼び出すことができます。  
  
 明示的または暗黙的に設定されたカーソル名は、関連付けられている*StatementHandle*が削除されるまで、設定されたままになります。これは、SQL_HANDLE_STMT の*Handletype*で**sqlfreehandle**を使用します。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|SQL ステートメントの実行|[SQLExecDirect 関数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|準備された SQL ステートメントの実行|[SQLExecute 関数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|実行するステートメントの準備|[SQLPrepare 関数](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|カーソル名の設定|[SQLSetCursorName 関数](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
