---
description: SQLNativeSql 関数
title: SQLNativeSql 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLNativeSql
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLNativeSql
helpviewer_keywords:
- SQLNativeSql function [ODBC]
ms.assetid: b8efc247-27ab-4a00-92b6-1400785783fe
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cbdf43d1120065f981d43e58490e328c6ef7691c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428904"
---
# <a name="sqlnativesql-function"></a>SQLNativeSql 関数
**互換性**  
 導入されたバージョン: ODBC 1.0 標準準拠: ODBC  
  
 **まとめ**  
 **Sqlnativesql** は、ドライバーによって変更された SQL 文字列を返します。 **Sqlnativesql** では、SQL ステートメントは実行されません。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLNativeSql(  
     SQLHDBC        ConnectionHandle,  
     SQLCHAR *      InStatementText,  
     SQLINTEGER     TextLength1,  
     SQLCHAR *      OutStatementText,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   TextLength2Ptr);  
```  
  
## <a name="arguments"></a>引数  
 *ConnectionHandle*  
 [入力] 接続ハンドル。  
  
 *InStatementText*  
 代入変換する SQL テキスト文字列。  
  
 *TextLength1*  
 代入**Instatementtext* テキスト文字列の長さ (文字数)。  
  
 *OutStatementText*  
 Output変換された SQL 文字列を返すバッファーへのポインター。  
  
 *OutStatementText*が NULL の場合、 *TextLength2Ptr*は、 *OutStatementText*によってポイントされたバッファー内で返すことができる文字の合計数 (文字データの null 終端文字を除く) を返します。  
  
 *BufferLength*  
 代入OutStatementText バッファー内の文字数 \* *OutStatementText* 。 * \* Instatementtext*で返される値が Unicode 文字列 ( **SQLNativeSqlW**を呼び出す場合) である場合、 *bufferlength*引数は偶数である必要があります。  
  
 *TextLength2Ptr*  
 OutputOutStatementText で返すことができる文字の合計数 (null 終了を除く) を返すバッファーへのポインター \* *OutStatementText*。 返すことのできる文字数が*Bufferlength*以上の場合、OutStatementText 内の翻訳された SQL 文字列 \* *OutStatementText*は*bufferlength*から null 終端文字の長さを引いた値に切り捨てられます。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **Sqlnativesql**が SQL_ERROR または SQL_SUCCESS_WITH_INFO のいずれかを返す場合、関連付けられた SQLSTATE 値は、 *Handletype* SQL_HANDLE_DBC および*connectionhandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出すことによって取得できます。 次の表に、 **Sqlnativesql** によって一般的に返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データ、右側が切り捨てられました|バッファー \* *OUTSTATEMENTTEXT*が sql 文字列全体を返すのに十分な大きさではないため、sql 文字列が切り捨てられました。 切り捨てられていない SQL 文字列の長さは **TextLength2Ptr*で返されます。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|08003|接続が開かれていません|*Connectionhandle*が接続状態ではありませんでした。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続されていたデータソースとの間の通信リンクが失敗しました。|  
|22007|無効な datetime 形式|**Instatementtext* に、無効な日付、時刻、またはタイムスタンプ値のエスケープ句が含まれていました。|  
|24000|カーソル状態が無効|ステートメント内で参照されているカーソルが、結果セットの先頭または結果セットの末尾の前に配置されました。 このエラーは、ネイティブの DBMS カーソル実装があるドライバーでは返されない場合があります。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * \* Messagetext*バッファーの**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY009|Null ポインターの使い方が正しくありません|(DM) **Instatementtext* は null ポインターでした。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が *Connectionhandle* に対して呼び出されましたが、この関数が呼び出されたときにまだ実行されていました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY090|文字列またはバッファーの長さが無効です|(DM) 引数 *TextLength1* は0未満でしたが、SQL_NTS と等しくありませんでした。|  
|||(DM) 引数 *Bufferlength* が0未満で、引数 *OutStatementText* が null ポインターではありませんでした。|  
|HY109|カーソル位置が無効です|カーソルの現在の行が削除されたか、またはフェッチされませんでした。 このエラーは、ネイティブの DBMS カーソル実装があるドライバーでは返されない場合があります。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *Connectionhandle* に関連付けられているドライバーでは、関数はサポートされていません。|  
  
## <a name="comments"></a>コメント  
 次に示すのは、スカラー関数 CONVERT を含む次の入力 SQL 文字列に対して **Sqlnativesql** が返す可能性のある例です。 列 empid がデータソースの整数型であるとします。  
  
```sql  
SELECT { fn CONVERT (empid, SQL_SMALLINT) } FROM employee  
```  
  
 Microsoft SQL Server のドライバーは、次の変換された SQL 文字列を返す場合があります。  
  
```sql  
SELECT convert (smallint, empid) FROM employee  
```  
  
 Driver for ORACLE Server は、次の変換された SQL 文字列を返す場合があります。  
  
```sql  
SELECT to_number (empid) FROM employee  
```  
  
 Ingres のドライバーは、次の変換された SQL 文字列を返す場合があります。  
  
```sql  
SELECT int2 (empid) FROM employee  
```  
  
 詳細については、「 [直接実行](../../../odbc/reference/develop-app/direct-execution-odbc.md) 」と「 [準備実行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)」を参照してください。  
  
## <a name="related-functions"></a>関連する関数  
 [なし] :  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
