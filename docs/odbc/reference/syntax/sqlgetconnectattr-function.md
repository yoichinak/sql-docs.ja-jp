---
description: SQLGetConnectAttr 関数
title: SQLGetConnectAttr 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetConnectOption
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConnectAttr
helpviewer_keywords:
- SQLGetConnectAttr function [ODBC]
ms.assetid: 2cb4ffa8-19d3-4664-8c2f-6682cdcc3f33
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 457ba462c277ec4b5fa44030557861507823dc04
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487275"
---
# <a name="sqlgetconnectattr-function"></a>SQLGetConnectAttr 関数
**互換性**  
 導入されたバージョン: ODBC 3.0 標準準拠: ISO 92  
  
 **まとめ**  
 **Sqlgetconnectattr** は、接続属性の現在の設定を返します。  
  
> [!NOTE]
>  Odbc*2.x アプリケーションが* odbc*2.x ドライバーで* 動作しているときに、ドライバーマネージャーがこの関数をマップする方法の詳細については、「 [アプリケーションの下位互換性のための置換関数のマッピング](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLGetConnectAttr(  
     SQLHDBC        ConnectionHandle,  
     SQLINTEGER     Attribute,  
     SQLPOINTER     ValuePtr,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>引数  
 *ConnectionHandle*  
 [入力] 接続ハンドル。  
  
 *属性*  
 代入取得する属性。  
  
 *ValuePtr*  
 Output *属性*によって指定された属性の現在の値を返すメモリへのポインター。 整数型の属性の場合、一部のドライバーでは、バッファーの下位の32ビットまたは16ビットのみが書き込まれ、上位ビットは変更されません。 このため、アプリケーションでは SQLULEN のバッファーを使用し、この関数を呼び出す前に値を0に初期化する必要があります。  
  
 *Valueptr*が NULL の場合でも、 *stringlength Ptr*は、 *valueptr*が指すバッファー内で返されるバイトの合計数 (文字データの NULL 終端文字を除く) を返します。  
  
 *BufferLength*  
 代入*属性*が ODBC 定義の属性であり、 *valueptr*が文字列またはバイナリバッファーを指している場合、この引数は valueptr の長さである必要があり \* *ValuePtr*ます。 *属性*が ODBC 定義の属性であり、 \* *valueptr*が整数の場合、 *bufferlength*は無視されます。 * \* Valueptr*の値が Unicode 文字列の場合 ( **Sqlgetconnectattrw**を呼び出すとき)、 *bufferlength*引数は偶数である必要があります。  
  
 *属性*がドライバーで定義された属性である場合、アプリケーションは、 *bufferlength*引数を設定することによって、ドライバーマネージャーに対する属性の性質を示します。 *Bufferlength* には次の値を指定できます。  
  
-   * \* Valueptr*が文字列へのポインターである場合、 *bufferlength*は文字列の長さです。  
  
-   * \* Valueptr*がバイナリバッファーへのポインターである場合、アプリケーションは、SQL_LEN_BINARY_ATTR (*長さ*) マクロの結果を*bufferlength*に配置します。 これにより、 *Bufferlength*に負の値が挿入されます。  
  
-   * \* Valueptr*が文字列またはバイナリ文字列以外の値へのポインターである場合、 *bufferlength*には SQL_IS_POINTER 値を指定する必要があります。  
  
-   * \* Valueptr*に固定長データ型が含まれている場合、 *bufferlength*は必要に応じて SQL_IS_INTEGER か SQL_IS_UINTEGER になります。  
  
 *Stringlength Ptr*  
 OutputValueptr で返すことができる合計バイト数 (null 終端文字を除く) を返すバッファーへのポインター \* *ValuePtr*。 \* *Valueptr*が null ポインターの場合、長さは返されません。 属性値が文字列であり、返されるバイト数が*Bufferlength*から null 終端文字の長さを引いた値よりも大きい場合、 * \* valueptr*内のデータは、null 終了文字の長さを差し引いた*bufferlength*に切り捨てられ、ドライバーによって null で終了されます。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **Sqlgetconnectattr**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合、関連付けられた SQLSTATE 値を診断データ構造から取得するには、 *handletype*が SQL_HANDLE_DBC で、 *connectionhandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出します。 次の表に、 **Sqlgetconnectattr** によって通常返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データ、右側が切り捨てられました|Valueptr で返されたデータは、 \* *ValuePtr* *bufferlength*から null 終了文字の長さを引いた値に切り詰められました。 切り捨てられていない文字列値の長さは、**Stringlength ptr*で返されます。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|08003|接続が開かれていません|(DM) 開いている接続を必要とする *属性* 値が指定されました。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続されていたデータソースとの間の通信リンクが失敗しました。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 **SQLGetDiagField**の引数*messagetext*によって診断データ構造から返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY010|関数のシーケンスエラー|(DM) **SQLBrowseConnect** が *connectionhandle* に対して呼び出され、SQL_NEED_DATA が返されました。 **SQLBrowseConnect**が返される前に、この関数が呼び出されました SQL_SUCCESS_WITH_INFO または SQL_SUCCESS です。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または **Sqlmoreresults** が *connectionhandle* に対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY090|文字列またはバッファーの長さが無効です|(DM) * \* valueptr*は文字列であり、bufferlength は0未満ですが SQL_NTS と等しくありません。|  
|HY092|属性またはオプションの識別子が無効です|引数 *属性* に指定された値は、ドライバーでサポートされている ODBC のバージョンに対して有効ではありませんでした。|  
|HY114|ドライバーは、接続レベルの非同期関数の実行をサポートしていません|(DM) 非同期の接続操作をサポートしていないドライバーに対して、SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE による非同期関数の実行を有効にしようとしました。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYC00|省略可能な機能は実装されていません|引数 *属性* に指定された値は、ドライバーでサポートされている odbc のバージョンの有効な odbc 接続属性でしたが、ドライバーではサポートされませんでした。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *Connectionhandle* に対応するドライバーでは、関数はサポートされていません。|  
  
## <a name="comments"></a>コメント  
 接続属性に関する一般的な情報については、「 [接続属性](../../../odbc/reference/develop-app/connection-attributes.md)」を参照してください。  
  
 設定できる属性の一覧については、「 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)」を参照してください。 *属性*で文字列を返す属性が指定されている場合、 *valueptr*は文字列のバッファーへのポインターである必要があることに注意してください。 返される文字列の最大長 (null 終端文字を含む) は、 *Bufferlength* バイトになります。  
  
 属性によっては、アプリケーションは **Sqlgetconnectattr**を呼び出す前に接続を確立する必要がありません。 ただし、 **sqlgetconnectattr** が呼び出され、指定された属性が既定値を持たず、 **SQLSetConnectAttr**の前の呼び出しで設定されていない場合、 **sqlgetconnectattr** は SQL_NO_DATA を返します。  
  
 *属性*がトレースファイルまたは SQL_ATTR_ tracefile SQL_ATTR_ 場合、 *connectionhandle*が有効である必要はありません。また、 **Sqlgetconnectattr**は、 *connectionhandle*が無効である場合に SQL_ERROR または SQL_INVALID_HANDLE を返しません。 これらの属性は、すべての接続に適用されます。 **Sqlgetconnectattr** は、別の引数が無効な場合に SQL_ERROR または SQL_INVALID_HANDLE を返します。  
  
 アプリケーションでは **SQLSetConnectAttr**を使用してステートメント属性を設定できますが、アプリケーションでは、 **Sqlgetconnectattr** を使用してステートメント属性値を取得することはできません。ステートメント属性の設定を取得するには、 **SQLGetStmtAttr** を呼び出す必要があります。  
  
 SQL_ATTR_AUTO_IPD と SQL_ATTR_CONNECTION_DEAD の両方の接続属性は、 **Sqlgetconnectattr** の呼び出しで返すことができますが、 **SQLSetConnectAttr**の呼び出しでは設定できません。  
  
> [!NOTE]  
>  **Sqlgetconnectattr**の非同期サポートはありません。 **Sqlgetconnectattr**を実装する場合、ドライバーは、サーバーから情報が送信または要求される回数を最小限に抑えることで、パフォーマンスを向上させることができます。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|ステートメント属性の設定を返す|[SQLGetStmtAttr 関数](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|接続属性の設定|[SQLSetConnectAttr 関数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|環境属性の設定|[SQLSetEnvAttr 関数](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|ステートメント属性の設定|[SQLSetStmtAttr 関数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
