---
description: SQLGetStmtAttr 関数
title: SQLGetStmtAttr 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetStmtAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetStmtAttr
helpviewer_keywords:
- SQLGetStmtAttr function [ODBC]
ms.assetid: e321d460-e997-4527-aee6-207cf5a498e9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a780f72b163628894671192fa11fa1fed906923f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421216"
---
# <a name="sqlgetstmtattr-function"></a>SQLGetStmtAttr 関数
**互換性**  
 導入されたバージョン: ODBC 3.0 標準準拠: ISO 92  
  
 **まとめ**  
 **SQLGetStmtAttr** は、ステートメント属性の現在の設定を返します。  
  
> [!NOTE]  
>  ドライバーマネージャーが ODBC 3 でこの関数をマップする方法の詳細については、「」を参照してください。*x* アプリケーションは ODBC 2 で動作しています。*x* ドライバー、「 [アプリケーションの旧バージョンとの互換性のための置換関数のマッピング](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLGetStmtAttr(  
     SQLHSTMT        StatementHandle,  
     SQLINTEGER      Attribute,  
     SQLPOINTER      ValuePtr,  
     SQLINTEGER      BufferLength,  
     SQLINTEGER *    StringLengthPtr);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル。  
  
 *属性*  
 代入取得する属性。  
  
 *ValuePtr*  
 Output *属性*で指定された属性の値を返すバッファーへのポインター。  
  
 *Valueptr*が NULL の場合でも、 *stringlength Ptr*は、 *valueptr*が指すバッファー内で返されるバイトの合計数 (文字データの NULL 終端文字を除く) を返します。  
  
 *BufferLength*  
 代入*属性*が ODBC 定義の属性であり、 *valueptr*が文字列またはバイナリバッファーを指している場合、この引数は valueptr の長さである必要があり \* *ValuePtr*ます。 *属性*が ODBC 定義の属性であり、 \* *valueptr*が整数の場合、 *bufferlength*は無視されます。 * \* Valueptr*で返される値が Unicode 文字列の場合 ( **SQLGetStmtAttrW**を呼び出した場合)、 *bufferlength*引数は偶数である必要があります。  
  
 *属性*がドライバーで定義された属性である場合、アプリケーションは、 *bufferlength*引数を設定することによって、ドライバーマネージャーに対する属性の性質を示します。 *Bufferlength* には次の値を指定できます。  
  
-   * \* Valueptr*が文字列へのポインターである場合、 *bufferlength*は文字列または SQL_NTS の長さになります。  
  
-   * \* Valueptr*がバイナリバッファーへのポインターである場合、アプリケーションは、SQL_LEN_BINARY_ATTR (*長さ*) マクロの結果を*bufferlength*に配置します。 これにより、 *Bufferlength*に負の値が挿入されます。  
  
-   * \* Valueptr*が文字列またはバイナリ文字列以外の値へのポインターである場合、 *bufferlength*には SQL_IS_POINTER 値を指定する必要があります。  
  
-   * \* Valueptr*に固定長データ型が含まれている場合は、 *bufferlength*が SQL_IS_INTEGER か SQL_IS_UINTEGER になります (必要に応じて)。  
  
 *Stringlength Ptr*  
 Output* \* Valueptr*で返すことができる合計バイト数 (null 終端文字を除く) を返すバッファーへのポインター。 *Valueptr*が null ポインターの場合、長さは返されません。 属性値が文字列であり、返されるバイト数が*Bufferlength*以上の場合、 * \* valueptr*内のデータは*bufferlength*の長さから null 終端文字の長さを引いた値に切り捨てられ、ドライバーによって null で終了されます。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **SQLGetStmtAttr**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合、関連付けられた SQLSTATE 値は、 *Handletype* SQL_HANDLE_STMT と*StatementHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出すことによって取得できます。 次の表に、 **SQLGetStmtAttr** によって一般的に返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データ、右側が切り捨てられました|* \* Valueptr*で返されたデータは、 *bufferlength*から null 終了文字の長さを引いた値に切り詰められました。 切り捨てられていない文字列値の長さは、**Stringlength ptr*で返されます。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|24000|カーソル状態が無効|引数 *属性* が SQL_ATTR_ROW_NUMBER されましたが、カーソルが開かれていないか、カーソルが結果セットの先頭または結果セットの末尾より前に配置されました。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 **SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因*が記述されてい*ます。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、 **SQLGetStmtAttr** 関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) 非同期的に実行する関数が *StatementHandle* に対して呼び出されましたが、この関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **Sqlbulkoperations**、 **SQLSetPos** が *StatementHandle* に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY090|文字列またはバッファーの長さが無効です|*(DM) \* valueptr* は文字列であり、bufferlength は0未満ですが SQL_NTS と等しくありません。|  
|HY092|属性またはオプションの識別子が無効です|引数 *属性* に指定された値は、ドライバーでサポートされている ODBC のバージョンに対して有効ではありませんでした。|  
|HY109|カーソル位置が無効です|*属性*引数が SQL_ATTR_ROW_NUMBER ましたが、行が削除されたか、またはフェッチできませんでした。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYC00|省略可能な機能は実装されていません|引数 *属性* に指定された値は、ドライバーでサポートされている odbc のバージョンの有効な odbc ステートメント属性でしたが、ドライバーではサポートされていませんでした。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle* に対応するドライバーでは、関数はサポートされていません。|  
  
## <a name="comments"></a>コメント  
 ステートメント属性の一般的な情報については、「 [ステートメント属性](../../../odbc/reference/develop-app/statement-attributes.md)」を参照してください。  
  
 **SQLGetStmtAttr**を呼び出すと、*属性*で指定したステートメント属性の値が* \* valueptr*に返されます。 この値には、SQLULEN 値または null で終わる文字列を指定できます。 値が SQLULEN 値の場合、一部のドライバーでは、バッファーの下位の32ビットまたは16ビットのみが書き込まれ、上位ビットは変更されません。 このため、アプリケーションでは SQLULEN のバッファーを使用し、この関数を呼び出す前に値を0に初期化する必要があります。 また、 *Bufferlength* および *stringlength ptr* 引数は使用されません。 値が null で終わる文字列の場合、アプリケーションは*bufferlength*引数内の文字列の最大長を指定し、ドライバーは* \* stringlength ptr*バッファー内のその文字列の長さを返します。  
  
 **SQLGetStmtAttr**を呼び出しているアプリケーションが ODBC 2 で動作できるようにします。*x*ドライバーは、ドライバーマネージャーで**SQLGetStmtAttr**の呼び出しを**SQLGetStmtOption**にマップします。  
  
 次のステートメント属性は読み取り専用であるため、 **SQLGetStmtAttr**で取得できますが、 **SQLSetStmtAttr**では設定できません。  
  
-   SQL_ATTR_IMP_PARAM_DESC  
  
-   SQL_ATTR_IMP_ROW_DESC  
  
-   SQL_ATTR_ROW_NUMBER  
  
 設定および取得できる属性の一覧については、「 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)」を参照してください。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|接続属性の設定を返す|[SQLGetConnectAttr 関数](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|接続属性の設定|[SQLSetConnectAttr 関数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|ステートメント属性の設定|[SQLSetStmtAttr 関数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
