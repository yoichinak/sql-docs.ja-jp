---
description: SQLSetConnectAttr 関数
title: SQLSetConnectAttr 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetConnectAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetConnectAttr
helpviewer_keywords:
- SQLSetConnectAttr function [ODBC]
ms.assetid: 97fc7445-5a66-4eb9-8e77-10990b5fd685
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0e6e3e9722510b7a1a563de8546b2e4190696e10
ms.sourcegitcommit: 3bde506b2fa3bc82813dbe658d567b1b9eb4278b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/11/2020
ms.locfileid: "94498455"
---
# <a name="sqlsetconnectattr-function"></a>SQLSetConnectAttr 関数
**互換性**  
 導入されたバージョン: ODBC 3.0 標準準拠: ISO 92  
  
 **まとめ**  
 **SQLSetConnectAttr** は、接続の側面を制御する属性を設定します。  
  
> [!NOTE]
>  Odbc *2.x アプリケーションが* odbc *2.x ドライバーで* 動作しているときに、ドライバーマネージャーがこの関数をマップする方法の詳細については、「 [アプリケーションの下位互換性のための置換関数のマッピング](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLSetConnectAttr(  
     SQLHDBC       ConnectionHandle,  
     SQLINTEGER    Attribute,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    StringLength);  
```  
  
## <a name="arguments"></a>引数  
 *ConnectionHandle*  
 [入力] 接続ハンドル。  
  
 *属性*  
 代入設定する属性。 "Comments" に記載されています。  
  
 *ValuePtr*  
 代入 *属性* に関連付けられる値へのポインター。 *属性* の値に応じて、 *valueptr* は符号なし整数値になるか、null で終わる文字列を指します。 *属性* 引数の整数型は固定長でない場合があることに注意してください。詳細については、「コメント」セクションを参照してください。  
  
 *StringLength*  
 代入 *属性* が ODBC 定義の属性であり、 *valueptr* が文字列またはバイナリバッファーを指している場合、この引数は * *valueptr* の長さである必要があります。 文字列データの場合、この引数には文字列のバイト数を含める必要があります。  
  
 *属性* が ODBC 定義の属性であり、 *valueptr* が整数の場合、 *stringlength* は無視されます。  
  
 *属性* がドライバーで定義された属性の場合、アプリケーションは *stringlength* 引数を設定することによって、ドライバーマネージャーに対する属性の性質を示します。 *Stringlength* には次の値を指定できます。  
  
-   *Valueptr* が文字列へのポインターである場合、 *stringlength* は文字列または SQL_NTS の長さを示します。  
  
-   *Valueptr* がバイナリバッファーへのポインターである場合、アプリケーションは、SQL_LEN_BINARY_ATTR ( *長さ* ) マクロの結果を *stringlength* に配置します。 これにより、 *文字列長* に負の値が挿入されます。  
  
-   *Valueptr* が文字列またはバイナリ文字列以外の値へのポインターである場合、 *stringlength* には SQL_IS_POINTER 値を指定する必要があります。  
  
-   *Valueptr* に固定長の値が含まれている場合は、必要に応じて *stringlength* が SQL_IS_INTEGER か SQL_IS_UINTEGER になります。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE、または SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>診断  
 **SQLSetConnectAttr** が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返した場合、関連付けられた SQLSTATE 値を取得するには、 *handletype* SQL_HANDLE_DBC および *connectionhandle* の *ハンドル* を指定して **SQLGetDiagRec** を呼び出します。 次の表に、 **SQLSetConnectAttr** によって一般的に返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
 ドライバーは、オプションを設定した結果に関する情報を提供するために SQL_SUCCESS_WITH_INFO を返すことができます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01S02|オプションの値が変更されました|ドライバーは、 *Valueptr* に指定された値をサポートしておらず、同様の値に置き換えられました。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|08002|使用中の接続名|*属性* 引数が SQL_ATTR_ODBC_CURSORS ましたが、ドライバーは既にデータソースに接続されています。|  
|08003|接続が開かれていません|(DM) 開いている接続を必要とする *属性* 値が指定されましたが、 *connectionhandle* が connected 状態ではありませんでした。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続されていたデータソースとの間の通信リンクが失敗しました。|  
|24000|カーソル状態が無効|*属性* 引数が SQL_ATTR_CURRENT_CATALOG ましたが、結果セットが保留されていました。|  
|25000|ローカルトランザクション内の操作が無効です。|接続属性 SQL_ATTR_ENLIST_IN_DTC を設定することによって、分散トランザクション接続 (DTC) に参加しようとしているときに、ローカルトランザクション内で接続が行われました。<br /><br /> 接続は既に DTC に参加しています。<br /><br /> 接続が分散トランザクション接続に参加し、SQL_ATTR_AUTOCOMMIT を SQL_AUTOCOMMIT_OFF に設定してローカルトランザクションが開始されました。|  
|3D000|無効なカタログ名|*属性* 引数が SQL_CURRENT_CATALOG ましたが、指定されたカタログ名は無効です。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 *\* Messagetext* バッファーの **SQLGetDiagRec** によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|*Connectionhandle* に対して非同期処理が有効になりました。 **SQLSetConnectAttr** 関数が呼び出され、実行が完了する前に、 [sqlcancelhandle 関数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)が *connectionhandle* で呼び出された後、 **SQLSetConnectAttr** 関数が *connectionhandle* で再度呼び出されました。<br /><br /> または、 **SQLSetConnectAttr** 関数が呼び出され、実行が完了する前に、マルチスレッドアプリケーションの別のスレッドからの *Connectionhandle* で **sqlcancelhandle** が呼び出されました。|  
|HY009|Null ポインターの使い方が正しくありません|*属性* 引数が文字列値を必要とする接続属性を識別しましたが、 *valueptr* 引数が null ポインターでした。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *Connectionhandle* に関連付けられている *StatementHandle* に対して呼び出されましたが、 **SQLSetConnectAttr** が呼び出されたときに実行中でした。<br /><br /> (DM) 非同期的に実行する関数 (この1つではない) が *Connectionhandle* に対して呼び出されましたが、この関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute** 、 **SQLExecDirect** 、または **Sqlmoreresults** が、 *connectionhandle* に関連付けられたステートメントハンドルの1つに対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。<br /><br /> (DM) **Sqlexecute** 、 **SQLExecDirect** 、 **sqlbulkoperations** 、または **SQLSetPos** が、 *connectionhandle* に関連付けられ SQL_NEED_DATA 返された *StatementHandle* に対して呼び出されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。<br /><br /> (DM) **SQLBrowseConnect** が *connectionhandle* に対して呼び出され、SQL_NEED_DATA が返されました。 **SQLBrowseConnect** が返される前に、この関数が呼び出されました SQL_SUCCESS_WITH_INFO または SQL_SUCCESS です。|  
|HY011|属性を今設定することはできません|*属性* 引数が SQL_ATTR_TXN_ISOLATION ましたが、トランザクションが開いていました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY024|無効な属性値|指定された *属性* 値が指定されている場合、 *valueptr* に無効な値が指定されています。 (ドライバーマネージャーは、SQL_ATTR_ACCESS_MODE や SQL_ATTR_ASYNC_ENABLE などの個別の値のセットを受け入れる接続属性とステートメント属性に対してのみ、この SQLSTATE を返します。 他のすべての接続属性およびステートメント属性では、ドライバーは *Valueptr* に指定された値を確認する必要があります)。<br /><br /> *属性* 引数が SQL_ATTR_TRACEFILE または SQL_ATTR_TRANSLATE_LIB でしたが、 *valueptr* は空の文字列でした。|  
|HY090|文字列またはバッファーの長さが無効です|*(DM) \* valueptr* は文字列であり、 *stringlength* 引数は0未満ですが SQL_NTS ませんでした。|  
|HY092|属性またはオプションの識別子が無効です|(DM) 引数 *属性* に指定された値は、ドライバーでサポートされている ODBC のバージョンでは無効です。<br /><br /> (DM) 引数 *属性* に指定された値は読み取り専用属性でした。|  
|HY114|ドライバーは、接続レベルの非同期関数の実行をサポートしていません|(DM) 非同期の接続操作をサポートしていないドライバーに対して、SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE による非同期関数の実行を有効にしようとしました。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HY121|カーソルライブラリと Driver-Aware プーリングを同時に有効にすることはできません|詳細については、「 [ドライバー対応接続プール](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)」を参照してください。|  
|HYC00|省略可能な機能は実装されていません|引数 *属性* に指定された値は、ドライバーでサポートされている odbc のバージョンの有効な odbc 接続またはステートメント属性でしたが、ドライバーではサポートされていませんでした。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr** 、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *Connectionhandle* に関連付けられているドライバーでは、関数はサポートされていません。|  
|IM009|翻訳 DLL を読み込めません|ドライバーは、接続用に指定された変換 DLL を読み込めませんでした。 このエラーは、 *属性* が SQL_ATTR_TRANSLATE_LIB 場合にのみ返されます。|  
|IM017|非同期通知モードでは、ポーリングは無効になっています|通知モデルが使用されるたびに、ポーリングは無効になります。|  
|IM018|**Sqlcompleteasync** は、このハンドルで前の非同期操作を完了するために呼び出されていません。|ハンドルに対する前の関数呼び出しが SQL_STILL_EXECUTING を返し、通知モードが有効になっている場合は、処理を完了するために、ハンドルに対して **Sqlcompleteasync** を呼び出す必要があります。|  
|S1118|ドライバーは非同期通知をサポートしていません|SQL_ATTR_ASYNC_DBC_EVENT が (接続が確立された後に) 設定されましたが、非同期通知はドライバーでサポートされていません。|  
  
 *属性* が statement 属性の場合、 **SQLSetConnectAttr** は **SQLSetStmtAttr** によって返された sqlstates を返すことができます。  
  
## <a name="comments"></a>コメント  
 接続属性に関する一般的な情報については、「 [接続属性](../../../odbc/reference/develop-app/connection-attributes.md)」を参照してください。  
  
 現在定義されている属性と、その属性が導入されたバージョンの ODBC を、このセクションの後半の表に示します。さまざまなデータソースを利用するために、より多くの属性が定義されることが予想されます。 属性の範囲は ODBC によって予約されています。ドライバー開発者は、オープングループから独自のドライバー固有の使用のために値を予約する必要があります。  
  
> [!NOTE]
>  ODBC 3.x では、 **SQLSetConnectAttr** を呼び出して、接続レベルでステートメント属性を設定する機能が非推奨と *されました。* ODBC 3 *. x* アプリケーションでは、接続レベルでステートメント属性を設定しないでください。 ODBC 3 *. x* ステートメントの属性は、接続レベルでは設定できません。ただし、接続属性とステートメント属性の両方であり、接続レベルまたはステートメントレベルのどちらかで設定できるのは、SQL_ATTR_METADATA_ID 属性と SQL_ATTR_ASYNC_ENABLE 属性です。  
> 
>  Odbc 3.x ドライバーでは、odbc *2.x アプリケーションを* 接続レベルで設定する odbc 2.x アプリケーションを使用する必要がある *.x* 場合にのみ、この機能をサポートする必要が *あります。* 詳細については、「付録 G: 旧バージョンとの互換性のためのドライバーガイドライン」の「 [SQLSetConnectOption Mapping](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) 」を参照してください。  
  
 アプリケーションは、接続が割り当てられて解放されるまでの間に、いつでも **SQLSetConnectAttr** を呼び出すことができます。 接続に対してアプリケーションによって正常に設定された接続とステートメントのすべての属性は、 **Sqlfreehandle** が接続で呼び出されるまで保持されます。 たとえば、アプリケーションがデータソースに接続する前に **SQLSetConnectAttr** を呼び出した場合、アプリケーションがデータソースに接続したときにドライバーで **SQLSetConnectAttr** が失敗した場合でも、属性は永続化されます。アプリケーションがドライバー固有の属性を設定した場合、アプリケーションが接続上の別のドライバーに接続しても、属性は保持されます。  
  
 接続属性によっては、接続が確立される前にのみ設定できるものがあります。他のユーザーは、接続が確立された後にのみ設定できます。 次の表は、接続が確立される前または後に設定する必要がある接続属性を示しています。 または、接続の前または後に属性を設定できること *を示します* 。  
  
|属性|接続の前または後に設定しますか?|  
|---------------|-------------------------------------|  
|SQL_ATTR_ACCESS_MODE|いずれか [1]|  
|SQL_ATTR_ASYNC_DBC_EVENT|接続前/接続後|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE|いずれか [4]|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK|接続前/接続後|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT|接続前/接続後|  
|SQL_ATTR_ASYNC_ENABLE|[2]|  
|SQL_ATTR_AUTO_IPD|接続前/接続後|  
|SQL_ATTR_AUTOCOMMIT|いずれか [5]|  
|SQL_ATTR_CONNECTION_DEAD|After|  
|SQL_ATTR_CONNECTION_TIMEOUT|接続前/接続後|  
|SQL_ATTR_CURRENT_CATALOG|いずれか [1]|  
|SQL_ATTR_DBC_INFO_TOKEN|After|  
|SQL_ATTR_ENLIST_IN_DTC|After|  
|SQL_ATTR_LOGIN_TIMEOUT|以前|  
|SQL_ATTR_METADATA_ID|接続前/接続後|  
|SQL_ATTR_ODBC_CURSORS|以前|  
|SQL_ATTR_PACKET_SIZE|以前|  
|SQL_ATTR_QUIET_MODE|接続前/接続後|  
|SQL_ATTR_TRACE|接続前/接続後|  
|SQL_ATTR_TRACEFILE|接続前/接続後|  
|SQL_ATTR_TRANSLATE_LIB|After|  
|SQL_ATTR_TRANSLATE_OPTION|After|  
|SQL_ATTR_TXN_ISOLATION|いずれか [3]|  
  
 [1] SQL_ATTR_ACCESS_MODE および SQL_ATTR_CURRENT_CATALOG は、ドライバーに応じて、接続の前後に設定できます。 ただし、接続後のドライバーによっては、接続後の変更がサポートされないため、相互運用可能なアプリケーションは接続前にこれらを設定します。  
  
 [2] SQL_ATTR_ASYNC_ENABLE は、アクティブなステートメントが存在する前に設定する必要があります。  
  
 [3] SQL_ATTR_TXN_ISOLATION は、接続に開いているトランザクションがない場合にのみ設定できます。 一部の接続属性では、データソースが valueptr に指定された値をサポートしていない場合に、類似した値の置換がサポートされ \* *ValuePtr* ます。 このような場合、ドライバーは SQL_SUCCESS_WITH_INFO と SQLSTATE 01S02 (オプション値が変更されました) を返します。 たとえば、 *属性* が SQL_ATTR_PACKET_SIZE で、 \* *valueptr* が最大パケットサイズを超えている場合、ドライバーは最大サイズに置き換えます。 置換された値を特定するために、アプリケーションは **Sqlgetconnectattr** を呼び出します。  
  
 [4] 接続が開かれる前に SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE が設定されている場合、ドライバーマネージャーは、 **SQLBrowseConnect** 、 **SQLConnect** 、または **SQLDriverConnect** の呼び出し中にドライバーが読み込まれるときにドライバーの属性を設定します。 ドライバーマネージャーは、 **SQLBrowseConnect** 、 **SQLConnect** 、または **SQLDriverConnect** を呼び出す前に、接続先のドライバーを認識しないため、ドライバーが非同期接続操作をサポートしているかどうかがわかりません。 そのため、ドライバーマネージャーは常に SQL_SUCCESS を返します。 ただし、ドライバーが非同期接続操作をサポートしていない場合、 **SQLBrowseConnect** 、 **SQLConnect** 、または **SQLDriverConnect** の呼び出しは失敗します。  
  
 [5] SQL_ATTR_AUTOCOMMIT が FALSE に設定されている場合、トランザクションの一貫性を確保するために SQL_ERROR が返された場合、アプリケーションは SQLEndTran (SQL_ROLLBACK) を呼び出す必要があります。  
  
 Valueptr バッファーで設定される情報の形式は、 \* *ValuePtr* 指定した *属性* によって異なります。 **SQLSetConnectAttr** は、null で終わる文字列または整数値の2つの異なる形式のいずれかで属性情報を受け取ります。 各の形式は、属性の説明に記載されています。 **SQLSetConnectAttr** の *valueptr* 引数によってポイントされる文字列には、 *stringlength* バイトの長さがあります。  
  
 ODBC 2.x 以前で導入されたすべての属性の場合と同様に、長さが属性によって定義されている場合、 *stringlength* 引数は無視され *ます。*  
  
|*属性*|*Valueptr* コンテンツ|  
|-----------------|-------------------------|  
|SQL_ATTR_ACCESS_MODE (ODBC 1.0)|SQLUINTEGER 値です。 SQL_MODE_READ_ONLY は、更新が発生する SQL ステートメントをサポートするために接続が必要ないことを示すインジケーターとして、ドライバーまたはデータソースによって使用されます。 このモードを使用すると、ドライバーまたはデータソースに応じて、ロックの方法、トランザクション管理、またはその他の領域を最適化できます。 ドライバーは、このようなステートメントがデータソースに送信されるのを防ぐためには必要ありません。 読み取り専用接続中に読み取り専用ではない SQL ステートメントの処理を要求したときのドライバーとデータソースの動作は、実装によって定義されます。 既定値は SQL_MODE_READ_WRITE です。|  
|SQL_ATTR_ASYNC_DBC_EVENT (ODBC 3.8)|イベントハンドルである SQLPOINTER 値。<br /><br /> 非同期関数の完了通知は、SQL_ATTR_ASYNC_STMT_EVENT 属性を使用して **SQLSetConnectAttr** を呼び出し、イベントハンドルを指定することで有効になります。 **注:**  通知方法は、カーソルライブラリではサポートされていません。 通知方法が有効になっている場合、SQLSetConnectAttr 経由でカーソルライブラリを有効にしようとすると、アプリケーションでエラーメッセージが表示されます。|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE (ODBC 3.8)|接続ハンドルでの選択した関数の非同期実行を有効または無効にする SQLUINTEGER 値。 詳細については、「 [非同期実行 (ポーリングメソッド)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)」を参照してください。<br /><br /> SQL_ASYNC_DBC_ENABLE_ON = 指定された接続に関連する関数に対して非同期操作を有効にします。<br /><br /> SQL_ASYNC_DBC_ENABLE_OFF = (既定値) 指定した接続に関連する関数の非同期操作を無効にします。<br /><br /> SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE の設定は常に同期されます (つまり、SQL_STILL_EXECUTING を返すことはありません)。<br /><br /> ステートメント操作の非同期実行は、SQL_ATTR_ASYNC_ENABLE で有効になります。|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK (ODBC 3.8)|コンテキスト構造を指す SQLPOINTER 値。<br /><br /> ドライバーマネージャーだけが、この属性を使用してドライバーの **SQLSetStmtAttr** 関数を呼び出すことができます。|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT (ODBC 3.8)|コンテキスト構造を指す SQLPOINTER 値。<br /><br /> ドライバーマネージャーだけが、この属性を使用してドライバーの **SQLSetStmtAttr** 関数を呼び出すことができます。|  
|SQL_ATTR_ASYNC_ENABLE (ODBC 3.0)|指定された接続でステートメントを使用して呼び出された関数を非同期的に実行するかどうかを指定する SQLULEN 値。<br /><br /> SQL_ASYNC_ENABLE_OFF = ステートメント操作の接続レベルの非同期実行サポートを無効にします (既定)。<br /><br /> SQL_ASYNC_ENABLE_ON = ステートメント操作の接続レベルの非同期実行サポートを有効にします。<br /><br /> この属性は、SQL_ASYNC_MODE 情報の種類を持つ **SQLGetInfo** が SQL_AM_CONNECTION または SQL_AM_STATEMENT を返すかどうかを設定できます。|  
|SQL_ATTR_AUTO_IPD (ODBC 3.0)|**SQLPrepare** の呼び出し後の IPD の自動作成がサポートされているかどうかを指定する読み取り専用の SQLUINTEGER 値。<br /><br /> SQL_TRUE = **SQLPrepare** の呼び出し後の IPD の自動作成は、ドライバーによってサポートされています。<br /><br /> SQL_FALSE = **SQLPrepare** の呼び出し後の IPD の自動作成は、ドライバーではサポートされていません。 準備されたステートメントをサポートしていないサーバーでは、IPD を自動的に設定することはできません。<br /><br /> SQL_ATTR_AUTO_IPD 接続属性に対して SQL_TRUE が返された場合は、IPD の自動作成を有効または無効にするようにステートメント属性 SQL_ATTR_ENABLE_AUTO_IPD を設定できます。 SQL_ATTR_AUTO_IPD が SQL_FALSE 場合、SQL_ATTR_ENABLE_AUTO_IPD を SQL_TRUE に設定することはできません。 SQL_ATTR_ENABLE_AUTO_IPD の既定値は SQL_ATTR_AUTO_IPD の値と同じです。<br /><br /> この接続属性は **Sqlgetconnectattr** からは返すことができますが、 **SQLSetConnectAttr** では設定できません。|  
|SQL_ATTR_AUTOCOMMIT (ODBC 1.0)|自動コミットモードと手動コミットモードのどちらを使用するかを指定する SQLUINTEGER 値。<br /><br /> SQL_AUTOCOMMIT_OFF = ドライバーは手動コミットモードを使用し、アプリケーションは **SQLEndTran** を使用してトランザクションを明示的にコミットまたはロールバックする必要があります。<br /><br /> SQL_AUTOCOMMIT_ON = 自動コミットモードが使用されています。 各ステートメントは、実行された直後にコミットされます。 これは既定値です。 SQL_ATTR_AUTOCOMMIT が SQL_AUTOCOMMIT_ON に設定されている場合、その接続で開いているトランザクションはコミットされ、手動コミットモードから自動コミットモードに変更されます。<br /><br /> 詳細については、「 [コミットモード](../../../odbc/reference/develop-app/commit-mode.md)」を参照してください。 **重要:**  データソースによっては、ステートメントがコミットされるたびに、接続のすべてのステートメントのアクセスプランが削除され、カーソルが閉じられることがあります。自動コミットモードでは、各非クエリステートメントが実行された後、またはクエリのカーソルが閉じられた後に、このエラーが発生する可能性があります。 詳細については、「 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) での SQL_CURSOR_COMMIT_BEHAVIOR と SQL_CURSOR_ROLLBACK_BEHAVIOR の情報の種類」および「 [カーソルおよび準備されたステートメントに対するトランザクションの影響](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)」を参照してください。 <br /><br /> 自動コミットモードでバッチが実行されると、2つの処理が可能になります。 バッチ全体を autocommitable 単位として処理することも、バッチ内の各ステートメントを autocommitable 単位として処理することもできます。 一部のデータソースでは、これらの動作の両方をサポートしているため、どちらか一方を選択する方法があります。 バッチを autocommitable 単位として扱うか、バッチ内の個々のステートメントが autocommitable かどうかをドライバーで定義します。|  
|SQL_ATTR_CONNECTION_DEAD<br /><br /> (ODBC 3.5)|接続の状態を示す読み取り専用の SQLUINTEGER 値。 SQL_CD_TRUE した場合、接続は失われています。 SQL_CD_FALSE した場合、接続はアクティブなままです。|  
|SQL_ATTR_CONNECTION_TIMEOUT (ODBC 3.0)|接続の要求が完了するまで待機する秒数に対応する SQLUINTEGER 値。この値を経過すると、アプリケーションに返されます。 クエリの実行またはログインに関連付けられていない状況でタイムアウトする可能性がある場合、ドライバーは SQLSTATE HYT00 (タイムアウト期限切れ) を返す必要があります。<br /><br /> *Valueptr* が 0 (既定値) の場合、タイムアウトはありません。|  
|SQL_ATTR_CURRENT_CATALOG (ODBC 2.0)|データソースによって使用されるカタログの名前を含む文字列。 たとえば、SQL Server では、カタログはデータベースであるため、ドライバーは **USE** _database_ ステートメントをデータソースに送信します。ここで、 *database* は \* *valueptr* に指定されたデータベースです。 1層ドライバーの場合、カタログはディレクトリである可能性があるため、ドライバーは現在のディレクトリを * *Valueptr* に指定されたディレクトリに変更します。|  
|SQL_ATTR_DBC_INFO_TOKEN (ODBC 3.8|[SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)の ( \* *prating* パラメーターが100と等しくない場合に、接続情報トークンを DBC handle に戻すために使用される sqlpointer 値。<br /><br /> SQL_ATTR_DBC_INFO_TOKEN が設定されています。 **Sqlgetconnectattr** または **SQLGetConnectOption** を使用してこの値を取得することはできません。 アプリケーションではこの属性を設定しないようにする必要があるため、ドライバーマネージャーの **SQLSetConnectAttr** は SQL_ATTR_DBC_INFO_TOKEN を受け入れません。<br /><br /> SQL_ATTR_DBC_INFO_TOKEN 設定後にドライバーから SQL_ERROR が返された場合は、プールから取得した接続だけが解放されます。 ドライバーマネージャーは、プールから別の接続を取得しようとします。 詳細については [、「ODBC ドライバーでの Connection-Pool 認識の開発](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md) 」を参照してください。|  
|SQL_ATTR_ENLIST_IN_DTC (ODBC 3.0)|Microsoft コンポーネントサービスによってコーディネートされた分散トランザクションで ODBC ドライバーを使用するかどうかを指定する SQLPOINTER 値。<br /><br /> SQL Server にエクスポートするトランザクションを指定する DTC OLE トランザクションオブジェクトを渡すか、SQL_DTC_DONE 接続の DTC 関連付けを終了します。<br /><br /> クライアントは、Microsoft 分散トランザクションコーディネーター (MS DTC) OLE ITransactionDispenser:: BeginTransaction メソッドを呼び出して MS DTC トランザクションを開始し、トランザクションを表す MS DTC トランザクションオブジェクトを作成します。 次に、アプリケーションは、SQL_ATTR_ENLIST_IN_DTC オプションを指定して SQLSetConnectAttr を呼び出し、トランザクションオブジェクトを ODBC 接続に関連付けます。 関連のあるすべてのデータベース操作は、MS DTC トランザクションで保護されます。 アプリケーションでは、SQL_DTC_DONE 値を指定して SQLSetConnectAttr を呼び出し、接続と DTC の関連付けを完了します。 詳細については、MS DTC のドキュメントを参照してください。|  
|SQL_ATTR_LOGIN_TIMEOUT (ODBC 1.0)|ログイン要求の完了を待機する秒数に対応する SQLUINTEGER 値。この値を経過すると、アプリケーションに返されます。 既定値はドライバーに依存します。 *Valueptr* が0の場合、タイムアウトは無効になり、接続試行は無制限に待機します。<br /><br /> 指定されたタイムアウトがデータソースの最大ログインタイムアウトを超えた場合、ドライバーはその値を置き換え、SQLSTATE 01S02 (オプション値が変更されました) を返します。|  
|SQL_ATTR_METADATA_ID (ODBC 3.0)|カタログ関数の文字列引数を処理する方法を決定する SQLUINTEGER 値。<br /><br /> SQL_TRUE の場合、カタログ関数の文字列引数は識別子として扱われます。 大文字と小文字は区別されません。 区切られていない文字列の場合、ドライバーは末尾のスペースを削除し、文字列は大文字に折りたたまれます。 区切られた文字列の場合、ドライバーは先頭または末尾のスペースを削除し、区切り記号の間に何があるかを文字どおりに取ります。 これらの引数のいずれかが null ポインターに設定されている場合、関数は SQL_ERROR と SQLSTATE HY009 (null ポインターの無効な使用) を返します。<br /><br /> SQL_FALSE した場合、カタログ関数の文字列引数は識別子として扱われません。 大文字と小文字は区別されます。 引数によっては、文字列検索パターンを含むかどうかを指定できます。<br /><br /> 既定値は SQL_FALSE です。<br /><br /> 値の一覧を取得する **Sqltables** の *TableType* 引数は、この属性の影響を受けません。<br /><br /> SQL_ATTR_METADATA_ID は、ステートメントレベルで設定することもできます。 (これは、ステートメント属性でもある唯一の接続属性です)。<br /><br /> 詳細については、「 [カタログ関数の引数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)」を参照してください。|  
|SQL_ATTR_ODBC_CURSORS (ODBC 2.0)|ドライバーマネージャーで ODBC カーソルライブラリを使用する方法を指定する SQLULEN 値:<br /><br /> SQL_CUR_USE_IF_NEEDED = ドライバーマネージャーでは、必要な場合にのみ ODBC カーソルライブラリが使用されます。 ドライバーが **Sqlfetchscroll** の SQL_FETCH_PRIOR オプションをサポートしている場合、ドライバーマネージャーはドライバーのスクロール機能を使用します。 それ以外の場合は、ODBC カーソルライブラリを使用します。<br /><br /> SQL_CUR_USE_ODBC = ドライバーマネージャーは ODBC カーソルライブラリを使用します。<br /><br /> SQL_CUR_USE_DRIVER = ドライバーマネージャーは、ドライバーのスクロール機能を使用します。 これが既定の設定です。<br /><br /> ODBC カーソルライブラリの詳細については、「 [付録 F: Odbc カーソルライブラリ](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md)」を参照してください。 **警告:**  カーソルライブラリは、今後のバージョンの Windows では削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 Microsoft では、ドライバーのカーソル機能を使用することをお勧めします。|  
|SQL_ATTR_PACKET_SIZE (ODBC 2.0)|ネットワークパケットサイズ (バイト単位) を指定する SQLUINTEGER 値。 **注:**  多くのデータソースでは、このオプションがサポートされていないか、またはのみを返しますが、ネットワークパケットのサイズを設定することはできません。 <br /><br /> 指定したサイズが最大パケットサイズを超えた場合、またはパケットの最小サイズより小さい場合、ドライバーはその値を置き換え、SQLSTATE 01S02 (オプションの値が変更されました) を返します。<br /><br /> 接続が既に確立された後にアプリケーションがパケットサイズを設定した場合、ドライバーは SQLSTATE HY011 を返します (属性を設定することはできません)。|  
|SQL_ATTR_QUIET_MODE (ODBC 2.0)|ウィンドウハンドル (HWND)。<br /><br /> ウィンドウハンドルが null ポインターの場合、ドライバーはダイアログボックスを表示しません。<br /><br /> ウィンドウハンドルが null ポインターでない場合は、アプリケーションの親ウィンドウハンドルである必要があります。 これは既定値です。 ドライバーは、このハンドルを使用してダイアログボックスを表示します。 **注:**  SQL_ATTR_QUIET_MODE 接続属性は、 **SQLDriverConnect** によって表示されるダイアログボックスには適用されません。|  
|SQL_ATTR_TRACE (ODBC 1.0)|トレースを実行するかどうかをドライバーマネージャーに通知する SQLUINTEGER 値。<br /><br /> SQL_OPT_TRACE_OFF = トレースオフ (既定)<br /><br /> SQL_OPT_TRACE_ON = トレースオン<br /><br /> トレースがオンになっている場合、ドライバーマネージャーは各 ODBC 関数呼び出しをトレースファイルに書き込みます。 **注:**  トレースがオンの場合、ドライバーマネージャーは任意の関数から SQLSTATE IM013 (Trace file error) を返すことができます。 <br /><br /> アプリケーションでは、SQL_ATTR_TRACEFILE オプションを使用してトレースファイルを指定します。 ファイルが既に存在する場合は、ドライバーマネージャーによってファイルに追加されます。 それ以外の場合は、ファイルを作成します。 トレースがオンで、トレースファイルが指定されていない場合は、ドライバーマネージャーがファイル SQL に書き込みます。ルートディレクトリにログインします。<br /><br /> アプリケーションで変数 **ODBCSharedTraceFlag** を設定して、トレースを動的に有効にすることができます。 トレースは、現在実行中のすべての ODBC アプリケーションに対して有効になります。 アプリケーションがトレースをオフにすると、そのアプリケーションに対してのみ無効になります。<br /><br /> アプリケーションが SQL_HANDLE_ENV の *Handletype* を使用して **SQLAllocHandle** を呼び出すときに、システム情報の **Trace** キーワードが1に設定されている場合、すべてのハンドルに対してトレースが有効になります。 **SQLAllocHandle** を呼び出したアプリケーションに対してのみ有効になります。<br /><br /> SQL_ATTR_TRACE の *属性* を指定して **SQLSetConnectAttr** を呼び出す場合、 *connectionhandle* 引数が有効である必要はなく、 *connectionhandle* が NULL の場合は SQL_ERROR を返しません。 この属性は、すべての接続に適用されます。|  
|SQL_ATTR_TRACEFILE (ODBC 1.0)|トレースファイルの名前を格納している null で終わる文字列。<br /><br /> SQL_ATTR_TRACEFILE 属性の既定値は、システム情報で **Tracefile** キーワードを使用して指定されます。 詳細については、「 [ODBC サブキー](../../../odbc/reference/install/odbc-subkey.md)」を参照してください。<br /><br /> SQL_ATTR_TRACEFILE の *属性* を指定して **SQLSetConnectAttr** を呼び出す場合、 *connectionhandle* 引数が有効である必要はなく、 *connectionhandle* が無効である場合は SQL_ERROR を返しません。 この属性は、すべての接続に適用されます。|  
|SQL_ATTR_TRANSLATE_LIB (ODBC 1.0)|文字セット変換などのタスクを実行するためにドライバーがアクセスする関数 **SQLDriverToDataSource** および **sqldatasourcetodriver** を含むライブラリの名前を含む null で終わる文字列。 このオプションは、ドライバーがデータソースに接続している場合にのみ指定できます。 この属性の設定は、接続間で保持されます。 データの変換の詳細については、「 [Translation dll](../../../odbc/reference/develop-app/translation-dlls.md) および [Translation dll 関数リファレンス](../../../odbc/reference/syntax/translation-dll-api-reference.md)」を参照してください。|  
|SQL_ATTR_TRANSLATE_OPTION (ODBC 1.0)|翻訳 DLL に渡される32ビットフラグ値。 この属性は、ドライバーがデータソースに接続している場合にのみ指定できます。 データの変換については、「 [Translation dll](../../../odbc/reference/develop-app/translation-dlls.md)」を参照してください。|  
|SQL_ATTR_TXN_ISOLATION (ODBC 1.0)|現在の接続のトランザクション分離レベルを設定する32ビットビットマスク。 このオプションを指定して **SQLSetConnectAttr** を呼び出す前に、アプリケーションは **SQLEndTran** を呼び出して、接続時に開いているすべてのトランザクションをコミットまたはロールバックする必要があります。<br /><br /> *Valueptr* の有効な値は、SQL_TXN_ISOLATION_OPTIONS と等しい *InfoType* を指定して **SQLGetInfo** を呼び出すことによって決定できます。<br /><br /> トランザクション分離レベルの詳細については、「 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 」と「 [トランザクション分離レベル](../../../odbc/reference/develop-app/transaction-isolation-levels.md)」の SQL_DEFAULT_TXN_ISOLATION 情報の種類についての説明を参照してください。|  
  
 [1] これらの関数は、記述子がアプリケーション記述子ではなく実装記述子である場合にのみ、非同期的に呼び出すことができます。  
  
## <a name="code-example"></a>コード例  
 「 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)」を参照してください。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|ハンドルの割り当て|[SQLAllocHandle 関数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|接続属性の設定を返す|[SQLGetConnectAttr 関数](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
