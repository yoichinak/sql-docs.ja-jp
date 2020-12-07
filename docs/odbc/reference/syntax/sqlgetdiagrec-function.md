---
description: SQLGetDiagRec 関数
title: SQLGetDiagRec 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDiagRec
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDiagRec
helpviewer_keywords:
- SQLGetDiagRec function [ODBC]
ms.assetid: ebdbac93-3d68-438f-8416-ef1f08e04269
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7f141891292fb80d53ba06e03329b66cbc8b826e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461015"
---
# <a name="sqlgetdiagrec-function"></a>SQLGetDiagRec 関数
**互換性**  
 導入されたバージョン: ODBC 3.0 標準準拠: ISO 92  
  
 **まとめ**  
 **SQLGetDiagRec** は、エラー、警告、および状態の情報を含む診断レコードの複数のフィールドの現在の値を返します。 呼び出しごとに1つの診断フィールドを返す **SQLGetDiagField**とは異なり、 **SQLGETDIAGREC** は、SQLSTATE、ネイティブエラーコード、診断メッセージテキストなど、診断レコードの一般的に使用されるいくつかのフィールドを返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLGetDiagRec(  
     SQLSMALLINT     HandleType,  
     SQLHANDLE       Handle,  
     SQLSMALLINT     RecNumber,  
     SQLCHAR *       SQLState,  
     SQLINTEGER *    NativeErrorPtr,  
     SQLCHAR *       MessageText,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   TextLengthPtr);  
```  
  
## <a name="arguments"></a>引数  
 *HandleType*  
 代入診断が必要なハンドルの種類を記述するハンドル型識別子。 次のいずれかである必要があります。  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN ハンドルは、ドライバーマネージャーとドライバーによってのみ使用されます。 アプリケーションでは、このハンドルの種類を使用しないでください。 SQL_HANDLE_DBC_INFO_TOKEN の詳細については、「 [ODBC ドライバーでの接続プールの認識の開発](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)」を参照してください。  
  
 *扱え*  
 代入 *Handletype*によって示される型の診断データ構造体のハンドル。 *Handletype*が SQL_HANDLE_ENV の場合、*ハンドル*は共有環境ハンドルまたは非共有環境ハンドルのどちらかになります。  
  
 *RecNumber*  
 代入アプリケーションが情報を検索するときに使用するステータスレコードを示します。 ステータスレコードには1から番号が付けられます。  
  
 *SQLState*  
 Output診断レコード *Recnumber*の5文字の SQLSTATE コード (および終了 NULL) を返すバッファーへのポインター。 最初の2文字はクラスを示しています。次の3つはサブクラスを示しています。 この情報は、SQL_DIAG_SQLSTATE 診断フィールドに含まれています。 詳細については、「 [Sqlstates](../../../odbc/reference/develop-app/sqlstates.md)」を参照してください。  
  
 *すべてのエラー Ptr*  
 Outputデータソースに固有のネイティブエラーコードを返すバッファーへのポインター。 この情報は、SQL_DIAG_NATIVE 診断フィールドに含まれています。  
  
 *[MessageText]*  
 Output診断メッセージのテキスト文字列を返すバッファーへのポインター。 この情報は、SQL_DIAG_MESSAGE_TEXT 診断フィールドに含まれています。 文字列の形式については、「 [診断メッセージ](../../../odbc/reference/develop-app/diagnostic-messages.md)」を参照してください。  
  
 *Messagetext*が NULL の場合でも、 *textlength Ptr*は、 *messagetext*が指すバッファーで返すことができる文字の合計数 (文字データの null 終端文字を除く) を返します。  
  
 *BufferLength*  
 代入**Messagetext* バッファーの長さ (文字数)。 診断メッセージテキストの最大長はありません。  
  
 *Textlength Ptr*  
 Output* \* Messagetext*で返すことができる文字の合計数 (null 終端文字に必要な文字数を除く) を返すバッファーへのポインター。 返すことのできる文字数が*bufferlength*よりも大きい場合、 * \* messagetext*の診断メッセージテキストは*bufferlength*に切り捨てられ、null 終了文字の長さを超えます。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **SQLGetDiagRec** は自身の診断レコードを通知しません。 次の戻り値を使用して、独自の実行結果を報告します。  
  
-   SQL_SUCCESS: 関数は正常に診断情報を返しました。  
  
-   SQL_SUCCESS_WITH_INFO: \* *messagetext*バッファーが小さすぎて、要求された診断メッセージを保持できませんでした。 診断レコードが生成されませんでした。 切り捨てが発生したことを確認するには、アプリケーションで *Bufferlength* と実際に使用可能なバイト数を比較する必要があります。これは **stringlength ptr*に書き込まれます。  
  
-   SQL_INVALID_HANDLE: *Handletype* と *handle* によって示されたハンドルが有効なハンドルではありませんでした。  
  
-   SQL_ERROR: 次のいずれかが発生しました。  
  
    -   *Recnumber* が負または0でした。  
  
    -   *Bufferlength* が0未満でした。  
  
    -   非同期通知を使用すると、ハンドルの非同期操作が完了しませんでした。  
  
-   SQL_NO_DATA: *recnumber* が、handle に指定されたハンドルに存在する診断レコードの数を超えてい *ます。* また、*ハンドル*の診断レコードが存在しない場合は、正の*値*に対しても SQL_NO_DATA が返されます。  
  
## <a name="comments"></a>コメント  
 通常、アプリケーションは、ODBC 関数の前回の呼び出しが SQL_ERROR または SQL_SUCCESS_WITH_INFO を返したときに、 **SQLGetDiagRec** を呼び出します。 ただし、任意の ODBC 関数が呼び出されるたびに0個以上の診断レコードをポストすることができるため、アプリケーションは、任意の ODBC 関数呼び出しの後に **SQLGetDiagRec** を呼び出すことができます。 アプリケーションは **SQLGetDiagRec** を複数回呼び出して、診断データ構造内のレコードの一部またはすべてを返すことができます。 ODBC では、一度に保存できる診断レコードの数に制限はありません。  
  
 **SQLGetDiagRec** を使用して、診断データ構造のヘッダーからフィールドを返すことはできません。 ( *Recnumber* 引数には0より大きい値を指定する必要があります)。アプリケーションは、この目的で **SQLGetDiagField** を呼び出す必要があります。  
  
 **SQLGetDiagRec** は、 *handle* 引数で指定されたハンドルに最後に関連付けられた診断情報のみを取得します。 アプリケーションが別の ODBC 関数 ( **SQLGetDiagRec**、 **SQLGetDiagField**、または **SQLError**を除く) を呼び出す場合、同じハンドルでの以前の呼び出しの診断情報は失われます。  
  
 アプリケーションでは、 **SQLGetDiagRec**が SQL_SUCCESS を返す限り、ループし、 *recnumber*をインクリメントして、すべての診断レコードをスキャンできます。 **SQLGetDiagRec**への呼び出しは、ヘッダーフィールドとレコードフィールドに対して非破壊です。 アプリケーションでは、 **SQLGetDiagRec**、 **SQLGetDiagField**、または**SQLError**を除く他の関数が中間で呼び出されている限り、後で**SQLGetDiagRec**を再度呼び出して、レコードからフィールドを取得できます。 また、 **SQLGetDiagField** を呼び出して [SQL_DIAG_NUMBER] フィールドの値を取得し、その回数が多くなる **SQLGetDiagRec** を呼び出すことによって、使用可能な診断レコードの合計数を取得することもできます。  
  
 診断データ構造のフィールドの説明については、「 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)」を参照してください。 詳細については、「 [SQLGetDiagRec と SQLGetDiagField の使用](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) 」および「 [SQLGetDiagRec と SQLGetDiagField の実装](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)」を参照してください。  
  
 非同期に実行されている API 以外の API を呼び出すと、HY010 "関数シーケンスエラー" が生成されます。 ただし、非同期操作が完了する前にエラーレコードを取得することはできません。  
  
## <a name="handletype-argument"></a>HandleType 引数  
 各ハンドルの種類には、関連付けられた診断情報を含めることができます。 *Handletype*引数は、 *handle*引数のハンドル型を表します。  
  
 環境、接続、ステートメント、記述子ハンドルに対して、一部のヘッダーフィールドとレコードフィールドを返すことはできません。 フィールドが適用されないハンドルは、 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)の "ヘッダーフィールド" セクションと "レコードフィールド" セクションに示されます。  
  
 *Handletype*が SQL_HANDLE_SENV の場合、 **SQLGetDiagRec**を呼び出すと SQL_INVALID_HANDLE が返されます。これは、共有環境ハンドルを表します。 ただし、 *Handletype* が SQL_HANDLE_ENV の場合、 *ハンドル* は共有環境ハンドルまたは非共有環境ハンドルのいずれかになります。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|診断レコードのフィールドまたは診断ヘッダーのフィールドを取得する|[SQLGetDiagField 関数](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダーファイル](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC のサンプル プログラム](../../../odbc/reference/sample-odbc-program.md)
