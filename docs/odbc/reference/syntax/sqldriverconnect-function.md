---
title: SQLDriverConnect 関数 |Microsoft Docs
description: SQLDriverConnect 関数は ODBC API 標準の一部です。このリファレンスドキュメントでは、その構文について説明しています。
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDriverConnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDriverConnect
helpviewer_keywords:
- SQLDriverConnect function [ODBC]
ms.assetid: e299be1d-5c74-4ede-b6a3-430eb189134f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d9ff73c570e607f687ff8293587b8dbcef551926
ms.sourcegitcommit: dc8a30a4a27e15fc6671ca2674da9b7c637ec255
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2020
ms.locfileid: "88745902"
---
# <a name="sqldriverconnect-function"></a>SQLDriverConnect 関数
**互換性**  
 導入されたバージョン: ODBC 1.0 標準準拠: ODBC  
  
 **まとめ**  
 **SQLDriverConnect** は、 **SQLConnect**の代わりになります。 **SQLConnect**の3つの引数よりも多くの接続情報を必要とするデータソース、すべての接続情報をユーザーに求めるダイアログボックス、システム情報で定義されていないデータソースをサポートします。 詳細については、「 [SQLDriverConnect を使用した接続](../develop-app/connecting-with-sqldriverconnect.md)」を参照してください。  

## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLDriverConnect(  
     SQLHDBC         ConnectionHandle,  
     SQLHWND         WindowHandle,  
     SQLCHAR *       InConnectionString,  
     SQLSMALLINT     StringLength1,  
     SQLCHAR *       OutConnectionString,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLength2Ptr,  
     SQLUSMALLINT    DriverCompletion);  
```  
  
## <a name="arguments"></a>引数  
 *ConnectionHandle*  
 [入力] 接続ハンドル。  
  
 *WindowHandle*  
 代入ウィンドウハンドル。 アプリケーションは親ウィンドウのハンドルを渡すことができます (該当する場合)。または、ウィンドウハンドルが適用されない場合、または **SQLDriverConnect** によってダイアログボックスが表示されない場合は null ポインターを渡すことができます。  
  
 *InConnectionString*  
 代入完全な接続文字列 (「コメント」の構文を参照)、部分的な接続文字列、または空の文字列。  
  
 *StringLength1*  
 代入長さ **Inconnectionstring*(文字列が Unicode の場合)、または文字列が ANSI または DBCS の場合はバイト。  
  
 *OutConnectionString*  
 Output完了した接続文字列のバッファーへのポインター。 ターゲットデータソースへの接続に成功すると、このバッファーには完了した接続文字列が含まれます。 アプリケーションでは、このバッファーに対して少なくとも1024文字を割り当てる必要があります。  
  
 *Outconnectionstring*が NULL の場合でも、 *StringLength2Ptr*は、 *outconnectionstring*が指すバッファー内で返すことができる文字の合計数 (文字データの null 終端文字を除く) を返します。  
  
 *BufferLength*  
 代入**Outconnectionstring* バッファーの長さ (文字数)。  
  
 *StringLength2Ptr*  
 OutputOutconnectionstring で返すことができる文字の合計数 (null 終了文字を除く) を返すバッファーへのポインター \* *OutConnectionString*。 返される文字数が*Bufferlength*以上の場合、outconnectionstring 内の完了した接続文字列 \* *OutConnectionString*が*bufferlength*に切り捨てられ、null 終了文字の長さを引いた値になります。  
  
 *DriverCompletion*  
 代入ドライバーマネージャーまたはドライバーが、より多くの接続情報の入力を求める必要があるかどうかを示すフラグ。  
  
 SQL_DRIVER_PROMPT、SQL_DRIVER_COMPLETE、SQL_DRIVER_COMPLETE_REQUIRED、または SQL_DRIVER_NOPROMPT。  
  
 (詳細については、「コメント」を参照してください)。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_ERROR、SQL_INVALID_HANDLE、または SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>診断  
 **SQLDriverConnect**が SQL_ERROR または SQL_SUCCESS_WITH_INFO のいずれかを返す場合、関連する SQLSTATE 値は、 *fhandletype* SQL_HANDLE_DBC と*connectionhandle*の*hhandle*を指定して**SQLGetDiagRec**を呼び出すことによって取得できます。 次の表に、 **SQLDriverConnect** によって一般的に返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データ、右側が切り捨てられました|バッファー \* *outconnectionstring*は接続文字列全体を返すのに十分な大きさではないため、接続文字列が切り捨てられました。 切り捨てられていない接続文字列の長さは **StringLength2Ptr*で返されます。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01S00|接続文字列の属性が無効です|接続文字列 (*Inconnectionstring*) に無効な attribute キーワードが指定されましたが、ドライバーはデータソースに接続できました。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01S02|オプションの値が変更されました|ドライバーは、 **SQLSetConnectAttr**の*valueptr*引数が指す指定された値をサポートしておらず、同様の値に置き換えられました。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01S08|ファイル DSN の保存エラー|* \* Inconnectionstring*内の文字列には**FILEDSN**キーワードが含まれていましたが、dsn ファイルは保存されませんでした。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01S09|無効なキーワード|(DM) * \* inconnectionstring*内の文字列には**SAVEFILE**キーワードが含まれていますが、**ドライバー**または**FILEDSN**キーワードは含まれていません。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|08001|クライアントが接続を確立できません|ドライバーは、データソースとの接続を確立できませんでした。|  
|08002|使用中の接続名|(DM) 指定された *Connectionhandle* は、データソースとの接続を確立するために既に使用されており、接続は開いたままです。|  
|08004|サーバーが接続を拒否しました|データソースは、実装定義の理由により、接続の確立を拒否しました。|  
|08S01|通信リンクの失敗|**SQLDriverConnect**関数が処理を完了する前に、ドライバーと、ドライバーが接続しようとしていたデータソースとの間の通信リンクが失敗しました。|  
|28000|認証の指定が無効です|接続文字列 (*Inconnectionstring*) で指定されているユーザー id または認証文字列、またはその両方が、データソースによって定義された制限に違反しています。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * \* Szmessagetext*バッファーの**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY000|一般的なエラー: ファイル dsn が無効です|(DM) **Inconnectionstring* 内の文字列に FILEDSN キーワードが含まれていましたが、dsn ファイルの名前が見つかりませんでした。|  
|HY000|一般的なエラー: ファイルバッファーを作成できません|(DM) **Inconnectionstring* 内の文字列には FILEDSN キーワードが含まれていますが、dsn ファイルは読み取れませんでした。|  
|HY001|メモリ割り当てエラー|ドライバーマネージャーは、 **SQLDriverConnect** 関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。<br /><br /> ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|*Connectionhandle*に対して非同期処理が有効になりました。 関数が呼び出され、実行が完了する前に、 [Sqlcancelhandle 関数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)が*connectionhandle*で呼び出されました。その後、 *connectionhandle*で**SQLDriverConnect**関数が再度呼び出されました。<br /><br /> または、 **SQLDriverConnect**関数が呼び出され、実行が完了する前に、マルチスレッドアプリケーションの別のスレッドからの*Connectionhandle*で**sqlcancelhandle**が呼び出されました。|  
|HY010|関数のシーケンスエラー|(DM) 別の非同期実行関数 ( **SQLDriverConnect**ではない) が *connectionhandle* に対して呼び出されましたが、 **SQLDriverConnect** 関数が呼び出されたときにまだ実行されていました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、 **SQLDriverConnect** 関数の呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY090|文字列またはバッファーの長さが無効です|(DM) 引数 *StringLength1* に指定された値が0未満であり、SQL_NTS と等しくありませんでした。<br /><br /> (DM) 引数 *Bufferlength* に指定された値が0未満でした。|  
|HY092|属性またはオプションの識別子が無効です|(DM) *Drivercompletion* 引数が SQL_DRIVER_PROMPT、 *WindowHandle* 引数が null ポインターでした。|  
|HY110|無効なドライバーの完了|(DM) 引数 *Drivercompletion* に指定された値は、SQL_DRIVER_PROMPT、SQL_DRIVER_COMPLETE、SQL_DRIVER_COMPLETE_REQUIRED、または SQL_DRIVER_NOPROMPT と等しくありませんでした。<br /><br /> (DM) 接続プーリングが有効になりましたが、引数 *Drivercompletion* に指定された値が SQL_DRIVER_NOPROMPT と一致しませんでした。|  
|HYC00|省略可能な機能は実装されていません|ドライバーは、アプリケーションが要求した ODBC 動作のバージョンをサポートしていません。|  
|HYT00|タイムアウトに達しました|データソースへの接続が完了する前に、ログインのタイムアウト期間が経過しました。 タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_LOGIN_TIMEOUT によって設定されます。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) 指定されたデータソース名に対応するドライバーが関数をサポートしていません。|  
|IM002|データソースが見つからず、既定のドライバーが指定されていません|(DM) 接続文字列 (*Inconnectionstring*) で指定されたデータソース名がシステム情報に見つかりませんでした。また、既定のドライバー仕様はありませんでした。<br /><br /> (DM) ODBC データソースと既定のドライバー情報がシステム情報に見つかりませんでした。|  
|IM003|指定されたドライバーを読み込めませんでした|(DM) システム情報で指定されているか、 **driver** キーワードによって指定されたデータソースの指定に含まれるドライバが見つからないか、他の何らかの理由で読み込めませんでした。|  
|IM004|SQL_HANDLE_ENV のドライバーの **SQLAllocHandle** に失敗しました|(DM) **SQLDriverConnect**中、ドライバーマネージャーはドライバーの **SQLAllocHandle** 関数を *fhandletype* SQL_HANDLE_ENV で呼び出し、ドライバーがエラーを返しました。|  
|IM005|SQL_HANDLE_DBC のドライバーの **SQLAllocHandle** に失敗しました。|(DM) **SQLDriverConnect**中、ドライバーマネージャーはドライバーの **SQLAllocHandle** 関数を *fhandletype* SQL_HANDLE_DBC で呼び出し、ドライバーがエラーを返しました。|  
|IM006|ドライバーの **SQLSetConnectAttr** に失敗しました|(DM) **SQLDriverConnect**中に、ドライバーマネージャーがドライバーの **SQLSetConnectAttr** 関数を呼び出し、ドライバーがエラーを返しました。|  
|IM007|データソースまたはドライバーが指定されていません。ダイアログが禁止されています|接続文字列にデータソース名またはドライバーが指定されていません。 *Drivercompletion* が SQL_DRIVER_NOPROMPT でした。|  
|IM008|失敗したダイアログ|ドライバーはログインダイアログボックスを表示しようとしましたが、失敗しました。<br /><br /> *WindowHandle* は null ポインターであり、 *drivercompletion* は SQL_DRIVER_NO_PROMPT ませんでした。|  
|IM009|翻訳 DLL を読み込めません|ドライバーは、データソースまたは接続用に指定された変換 DLL を読み込めませんでした。|  
|IM010|データソース名が長すぎます|(DM) DSN キーワードの属性値が SQL_MAX_DSN_LENGTH 文字を超えています。|  
|IM011|ドライバー名が長すぎます|(DM) **DRIVER** キーワードの属性値が255文字を超えています。|  
|IM012|DRIVER キーワード構文エラー|(DM) **DRIVER** キーワードのキーワードと値のペアに構文エラーが含まれています。<br /><br /> (DM) * \* inconnectionstring*内の文字列には**FILEDSN**キーワードが含まれていましたが、dsn ファイルには**DRIVER**キーワードまたは**dsn**キーワードが含まれていませんでした。|  
|IM014|指定された DSN には、ドライバーとアプリケーションのアーキテクチャの不一致が含まれています|(DM) 32 ビットアプリケーションは、64ビットドライバーに接続する DSN を使用します。または、その逆も同様です。|  
|IM015|SQL_HANDLE_DBC_INFO_HANDLE のドライバーの SQLDriverConnect に失敗しました|ドライバーが SQL_ERROR を返した場合、ドライバーマネージャーはアプリケーションに SQL_ERROR を返し、接続は失敗します。<br /><br /> SQL_HANDLE_DBC_INFO_TOKEN の詳細については、「 [ODBC ドライバーでの接続プールの認識の開発](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)」を参照してください。|  
|IM017|非同期通知モードでは、ポーリングは無効になっています|通知モデルが使用されるたびに、ポーリングは無効になります。|  
|IM018|**Sqlcompleteasync** は、このハンドルで前の非同期操作を完了するために呼び出されていません。|ハンドルに対する前の関数呼び出しが SQL_STILL_EXECUTING を返し、通知モードが有効になっている場合は、処理を完了するために、ハンドルに対して **Sqlcompleteasync** を呼び出す必要があります。|  
|S1118|ドライバーは非同期通知をサポートしていません|ドライバーが非同期通知をサポートしていない場合、SQL_ATTR_ASYNC_DBC_EVENT または SQL_ATTR_ASYNC_DBC_RETCODE_PTR を設定することはできません。|  
  
## <a name="comments"></a>説明  
 接続文字列の構文は次のとおりです。  
  
 *接続文字列* :: = *空文字列*[;] &#124; *属性*[;] &#124; *属性*; *接続文字列*  
  
 *空の文字列*:: =*属性*:: =*属性-キーワード* = *属性-値*&#124; DRIVER = [{]*属性-値*[}]  
  
 *属性-キーワード* :: = DSN &#124; UID &#124; PWD &#124; *ドライバー定義-attribute-キーワード*  
  
 *属性-値* :: = *文字文字列*  
  
 *ドライバー定義-属性-キーワード* :: = *識別子*  
  
 *文字文字列*に0個以上の文字が含まれています。*識別子*に1つ以上の文字が含まれています。*属性キーワードで*は大文字と小文字が区別されません。*属性-値*は大文字と小文字が区別されます。また、 **DSN**キーワードの値は空白だけで構成されていません。  
  
 接続文字列と初期化ファイルの文法のために、 **[] {} ()、;? という文字を含むキーワードと属性値が使用されています \* 。=! @** かっこで囲まれていないことを避ける必要があります。 **DSN**キーワードの値は、空白のみで構成することはできません。また、先頭に空白を含めることはできません。 システム情報の文法により、キーワードとデータソース名に円記号 () を含めることはできません \\ 。  
  
 属性にセミコロン (;) が含まれていない限り、アプリケーションでは、属性 **値の周囲** に中かっこを追加する必要はありません。この場合、中かっこが必要です。 ドライバーが受け取る属性値に中かっこが含まれている場合、ドライバーはそれらを削除せずに、返された接続文字列の一部にする必要があります。  
  
 {} **[] {} ()、;? \* のいずれかの文字を含む、かっこ () で囲まれた DSN または接続文字列値=! @** は、ドライバーにそのまま渡されます。 ただし、キーワードでこれらの文字を使用する場合、ドライバーマネージャーは、ファイル Dsn を操作するときにエラーを返しますが、通常の接続文字列の接続文字列をドライバーに渡します。 キーワード値には、埋め込みかっこを使用しないようにしてください。  
  
 接続文字列には、任意の数のドライバー定義キーワードを含めることができます。 **Driver キーワードは**システム情報の情報を使用しないため、ドライバーは、接続文字列の情報のみを使用してデータソースに接続できるように、十分なキーワードを定義する必要があります。 (詳細については、このセクションで後述する「ドライバーのガイドライン」を参照してください)。ドライバーは、データソースに接続するために必要なキーワードを定義します。  
  
 次の表では、 **DSN**、 **FILEDSN**、 **DRIVER**、 **UID**、 **PWD**、および **SAVEFILE** キーワードの属性値について説明します。  
  
|Keyword|属性値の説明|  
|-------------|---------------------------------|  
|**DSN**|**SQLDriverConnect**の**sqldatasources**または [データソース] ダイアログボックスによって返されるデータソースの名前。|  
|**FILEDSN**|データソース用の接続文字列の作成元となる、dsn ファイルの名前。 これらのデータソースは、ファイルデータソースと呼ばれます。|  
|**DRIVER**|**Sqldrivers**関数によって返されるドライバーの説明。 たとえば、Rdb や SQL Server などです。|  
|**UID**|ユーザー ID。|  
|**PWD**|ユーザー ID に対応するパスワード。または、ユーザー ID にパスワードがない場合は空の文字列 (PWD =;)。|  
|**SAVEFILE**|現在の正常な接続の作成に使用されたキーワードの属性値を保存する必要がある、dsn ファイルのファイル名。|  
  
 アプリケーションでデータソースまたはドライバーを選択する方法の詳細については、「 [データソースまたはドライバーの選択](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)」を参照してください。  
  
 接続文字列でキーワードが繰り返し使用されている場合、ドライバーは最初に見つかったキーワードに関連付けられている値を使用します。 **DSN**と**ドライバー**のキーワードが同じ接続文字列に含まれている場合、ドライバーマネージャーとドライバーでは、どちらかのキーワードが最初に使用されます。  
  
 **FILEDSN**キーワードと**DSN**キーワードは相互に排他的です。どちらかのキーワードが最初に使用され、2番目のキーワードは無視されます。 一方、 **FILEDSN** キーワードと **DRIVER** キーワードは相互に排他的ではありません。 **FILEDSN**が指定された接続文字列にキーワードがある場合、dsn ファイル内の同じキーワードの属性値ではなく、接続文字列のキーワードの属性値が使用されます。  
  
 **FILEDSN**キーワードが使用されている場合は、dsn ファイルで指定されたキーワードを使用して接続文字列が作成されます。 (詳細については、このセクションで後述する「ファイルデータソース」を参照してください)。 **UID** キーワードは省略可能です。 **DRIVER** キーワードだけを使用して、dsn ファイルを作成できます。 **PWD**キーワードは、dsn ファイルには格納されません。 . Dsn ファイルの保存と読み込みの既定のディレクトリは、 **CommonFileDir** によって指定されたパスを HKEY_LOCAL_MACHINE \software\microsoft\ Windows\CurrentVersion と "Odbc\ データソース" で組み合わせたものになります。 (CommonFileDir が "C:\Program Files\Common Files" の場合、既定のディレクトリは "C:\Program Files\Common Files\ODBC\Data Sources" になります)。  
  
> [!NOTE]  
>  Dsn ファイルは、インストーラー DLL 内の [SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md) 関数と [SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md) 関数を呼び出すことによって直接操作できます。  
  
 **SAVEFILE**キーワードが使用されている場合、現在の正常な接続の作成に使用されるキーワードの属性値は、 **SAVEFILE**キーワードの属性値の名前を持つ. dsn ファイルとして保存されます。 **SAVEFILE**キーワードは、 **DRIVER**キーワード、 **FILEDSN**キーワード、またはその両方と組み合わせて使用する必要があります。または、関数が SQLSTATE 01S09 (無効なキーワード) と共に SQL_SUCCESS_WITH_INFO を返します。 **SAVEFILE**キーワードは、接続文字列の**DRIVER**キーワードの前に記述する必要があります。指定しないと、結果は未定義になります。  
  
## <a name="driver-manager-guidelines"></a>ドライバーマネージャーのガイドライン  
 ドライバーマネージャーは、ドライバーの**SQLDriverConnect**関数の*inconnectionstring*引数でドライバーに渡す接続文字列を構築します。 ドライバーマネージャーは、アプリケーションによって渡される *Inconnectionstring* 引数を変更しません。  
  
 ドライバーマネージャーの動作は、 *Drivercompletion* 引数の値に基づいています。  
  
-   SQL_DRIVER_PROMPT: 接続文字列に **driver**、 **DSN**、または **FILEDSN** キーワードが含まれていない場合、ドライバーマネージャーは [データソース] ダイアログボックスを表示します。 このメソッドは、ダイアログボックスによって返されるデータソース名と、アプリケーションによって渡されるその他のキーワードから接続文字列を構築します。 ダイアログボックスによって返されるデータソース名が空の場合は、ドライバーマネージャーによって、キーワードと値のペア DSN = Default が指定されます。 (このダイアログボックスには、"Default" という名前のデータソースは表示されません)。  
  
-   SQL_DRIVER_COMPLETE または SQL_DRIVER_COMPLETE_REQUIRED: アプリケーションによって指定された接続文字列に **DSN** キーワードが含まれている場合、ドライバーマネージャーは、アプリケーションで指定された接続文字列をコピーします。 それ以外の場合、 *Drivercompletion* が SQL_DRIVER_PROMPT ときと同じ操作を実行します。  
  
-   SQL_DRIVER_NOPROMPT: ドライバーマネージャーは、アプリケーションによって指定された接続文字列をコピーします。  
  
 アプリケーションによって指定された接続文字列に **driver** キーワードが含まれている場合、ドライバーマネージャーは、アプリケーションによって指定された接続文字列をコピーします。  
  
 ドライバーマネージャーは、構築された接続文字列を使用して、使用するドライバーを決定し、そのドライバーに接続して、作成した接続文字列をドライバーに渡します。ドライバーマネージャーとドライバーの相互作用の詳細については、「 [SQLConnect 関数](../../../odbc/reference/syntax/sqlconnect-function.md)」の「コメント」セクションを参照してください。 接続文字列に **driver** キーワードが含まれていない場合、ドライバーマネージャーは、次のように使用するドライバーを決定します。  
  
1.  接続文字列に **DSN** キーワードが含まれている場合、ドライバーマネージャーは、データソースに関連付けられているドライバーをシステム情報から取得します。  
  
2.  接続文字列に **DSN** キーワードが含まれていない場合、またはデータソースが見つからない場合は、ドライバーマネージャーによって、既定のデータソースに関連付けられているドライバーがシステム情報から取得されます。 (詳細については、「 [Default サブキー](../../../odbc/reference/install/default-subkey.md)」を参照してください)。ドライバーマネージャーは、接続文字列の **DSN** キーワードの値を "DEFAULT" に変更します。  
  
3.  接続文字列の **DSN** キーワードが "DEFAULT" に設定されている場合、ドライバーマネージャーは、既定のデータソースに関連付けられているドライバーをシステム情報から取得します。  
  
4.  データソースが見つからず、既定のデータソースが見つからない場合、ドライバーマネージャーは SQLSTATE IM002 (データソースが見つからず、既定のドライバーが指定されていません) で SQL_ERROR を返します。  
  
## <a name="file-data-sources"></a>[ファイル データ ソース]  
 **SQLDriverConnect**の呼び出しでアプリケーションによって指定された接続文字列に**FILEDSN**キーワードが含まれており、このキーワードが**dsn**または**DRIVER**キーワードによって置き換えられていない場合、DRIVER Manager は、dsn ファイルと*inconnectionstring*引数の情報を使用して接続文字列を作成します。 ドライバーマネージャーは次のように処理されます。  
  
1.  Dsn ファイルのファイル名が有効かどうかを確認します。 そうでない場合は、SQLSTATE IM014 (ファイル DSN の無効な名前) で SQL_ERROR を返します。 ファイル名が空の文字列 ("") で、SQL_DRIVER_NOPROMPT が指定されていない場合、[ **ファイルを開く** ] ダイアログボックスが表示されます。 ファイル名に有効なパスが含まれていても、ファイル名またはファイル名が無効で、SQL_DRIVER_NOPROMPT が指定されていない場合、[ **ファイルを開く** ] ダイアログボックスには、現在のディレクトリがファイル名に指定されているものに設定された状態で表示されます。 ファイル名が空の文字列 ("") である場合、またはファイル名に有効なパスが含まれていても、ファイル名または無効なファイル名が指定されていない場合、SQL_DRIVER_NOPROMPT が指定されていると、SQLSTATE IM014 (ファイル DSN の無効な名前) で SQL_ERROR が返されます。  
  
2.  Dsn ファイルの [ODBC] セクションのすべてのキーワードを読み取ります。 **Driver**キーワードが存在しない場合は、IM012 (driver キーワード構文エラー) を含む SQL_ERROR を返します。ただし、dsn ファイルは unshareable であり、そのためには**dsn**キーワードだけが含まれます。  
  
     ファイルデータソースが unshareable の場合、Driver Manager は **DSN** キーワードの値を読み取り、必要に応じて、unshareable file データソースが指すユーザーまたはシステムデータソースに接続します。 手順 3. ~ 5. は実行されません。  
  
3.  ドライバーの接続文字列を構築します。 ドライバー接続文字列は、dsn ファイルで指定されたキーワードと、元のアプリケーション接続文字列で指定されたキーワードの和集合です。 キーワードが重複するドライバー接続文字列を構築するための規則は次のとおりです。  
  
    -   **Driver**キーワードがアプリケーション接続文字列内に存在し、 **driver**キーワードによって指定されたドライバーが dsn ファイルとアプリケーション接続文字列で同じでない場合、dsn ファイル内のドライバー情報は無視され、アプリケーション接続文字列のドライバー情報が使用されます。 **DRIVER**キーワードによって指定されたドライバーが、dsn ファイルとアプリケーションの接続文字列で同じである場合、すべてのキーワードが重なっていると、アプリケーション接続文字列で指定されたドライバーは、. dsn ファイルで指定されているものよりも優先されます。  
  
    -   新しい接続文字列では、 **FILEDSN** キーワードが削除されます。  
  
4.  ドライバーの \\ \> キーワードに \<Driver Name> よって指定された**DRIVER**<ドライバー名 \ ドライバー HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST.INIレジストリエントリを検索して、ドライバーを読み込みます。  
  
5.  新しい接続文字列をドライバーに渡します。  
  
 . Dsn ファイルの例については、「 [ファイルデータソースを使用した接続](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)」を参照してください。  
  
## <a name="savefile-keyword"></a>SAVEFILE キーワード  
 アプリケーションによって指定された接続文字列に **SAVEFILE** キーワードが含まれている場合、ドライバーマネージャーは接続文字列を dsn ファイルに保存します。 ドライバーマネージャーは次のように処理されます。  
  
1.  **SAVEFILE**キーワードの属性値として含まれている、dsn ファイルのファイル名が有効かどうかを確認します。 そうでない場合は、SQLSTATE IM014 (ファイル DSN の無効な名前) で SQL_ERROR を返します。 ファイル名の有効性は、標準のシステム名前付け規則によって決まります。 ファイル名が空の文字列 ("") で、 *Drivercompletion* 引数が SQL_DRIVER_NOPROMPT でない場合、ファイル名は有効です。 ファイル名が既に存在する場合、 *Drivercompletion* が SQL_DRIVER_NOPROMPT と、ファイルは上書きされます。 *Drivercompletion*が SQL_DRIVER_PROMPT、SQL_DRIVER_COMPLETE、または SQL_DRIVER_COMPLETE_REQUIRED の場合、ファイルを上書きするかどうかを指定するダイアログボックスが表示されます。 が入力されていない場合は、[ **ファイルの保存** ] ダイアログボックスが表示されます。  
  
2.  ドライバーが SQL_SUCCESS を返し、ファイル名が空の文字列ではない場合、ドライバーマネージャーは、 *Outconnectionstring* 引数で返された接続情報を、このセクションの前の「接続文字列」セクションで指定された形式で、指定されたファイルに書き込みます。  
  
3.  ドライバーが SQL_SUCCESS を返し、ファイル名が空の文字列 ("") の場合、ドライバーマネージャーは、 *hwnd*が指定された [**ファイルの保存**] コモンダイアログボックスを呼び出し、 *outconnectionstring*で返された接続情報を、このセクションの前の「接続文字列」セクションで指定された形式で、[ファイルの保存] コモンダイアログボックスで指定され  
  
4.  ドライバーが SQL_SUCCESS を返すと、アプリケーションへの接続文字列を含む *Outconnectionstring* 引数が返されます。  
  
5.  ドライバーが SQL_SUCCESS_WITH_INFO または SQL_ERROR を返した場合、ドライバーマネージャーは SQLSTATE をアプリケーションに返します。  
  
## <a name="driver-guidelines"></a>ドライバーのガイドライン  
 ドライバーは、ドライバーマネージャーによって渡された接続文字列に **DSN** または **ドライバー** のキーワードが含まれているかどうかを確認します。 接続文字列に **driver** キーワードが含まれている場合、ドライバーはシステム情報からデータソースに関する情報を取得できません。 接続文字列に **dsn** キーワードが含まれている場合、または **dsn** キーワードまたは **driver** キーワードが含まれていない場合、ドライバーは次のようにシステム情報からデータソースに関する情報を取得できます。  
  
1.  接続文字列に **DSN** キーワードが含まれている場合、ドライバーは指定されたデータソースの情報を取得します。  
  
2.  接続文字列に **dsn** キーワードが含まれていない場合、指定されたデータソースが見つからない場合、または **dsn** キーワードが "DEFAULT" に設定されている場合、ドライバーは既定のデータソースの情報を取得します。  
  
 ドライバーは、システム情報から取得した情報を使用して、接続文字列で渡された情報を拡張します。 システム情報の情報が接続文字列の情報と重複する場合、ドライバーは接続文字列の情報を使用します。  
  
 *Drivercompletion*の値に基づいて、ドライバーはユーザーにユーザー ID やパスワードなどの接続情報の入力を求め、データソースに接続します。  
  
-   SQL_DRIVER_PROMPT: ドライバーは、接続文字列の値とシステム情報 (存在する場合) を初期値として使用して、ダイアログボックスを表示します。 ユーザーがダイアログボックスを終了すると、ドライバーはデータソースに接続します。 また、inconnectionstring で**DSN**または**DRIVER**キーワードの値から接続文字列を作成し、 \* *InConnectionString*ダイアログボックスから返された情報を作成します。 この接続文字列は、**Outconnectionstring* バッファーに配置されます。  
  
-   SQL_DRIVER_COMPLETE または SQL_DRIVER_COMPLETE_REQUIRED: 接続文字列に十分な情報が含まれており、その情報が正しい場合、ドライバーはデータソースに接続し、 \* *inconnectionstring*を \* *outconnectionstring*にコピーします。 情報が不足しているか、正しくない場合、ドライバーは *Drivercompletion* が SQL_DRIVER_PROMPT 場合と同じ操作を実行します。ただし、 *drivercompletion* が SQL_DRIVER_COMPLETE_REQUIRED 場合、ドライバーは、データソースへの接続に必要のない情報について、コントロールを無効にします。  
  
-   SQL_DRIVER_NOPROMPT: 接続文字列に十分な情報が含まれている場合、ドライバーはデータソースに接続し、 \* *inconnectionstring*を \* *outconnectionstring*にコピーします。 それ以外の場合、ドライバーは **SQLDriverConnect**の SQL_ERROR を返します。  
  
 データソースへの接続に成功すると、ドライバーは \* *StringLength2Ptr*を **outconnectionstring*で返すことができる出力接続文字列の長さに設定します。  
  
 ドライバーマネージャーまたはドライバーによって表示されるダイアログボックスをユーザーがキャンセルした場合、 **SQLDriverConnect** は SQL_NO_DATA を返します。  
  
 接続プロセス中のドライバーマネージャーとドライバーの相互作用の詳細については、「 [SQLConnect 関数](../../../odbc/reference/syntax/sqlconnect-function.md)」を参照してください。  
  
 ドライバーが **SQLDriverConnect**をサポートしている場合、ドライバーのシステム情報の driver キーワードセクションには、2番目の文字が "Y" に設定された **connectfunctions** キーワードが含まれている必要があります。  
  
## <a name="connecting-when-connection-pooling-is-enabled"></a>接続プールが有効になっている場合の接続  
 接続プールを使用すると、既に作成されている接続をアプリケーションで再利用できます。 **SQLDriverConnect**が呼び出されると、ドライバーマネージャーは、接続プール用に指定された環境内の接続のプールの一部である接続を使用して接続を試みます。 接続プールの詳細については、「 [SQLConnect 関数](../../../odbc/reference/syntax/sqlconnect-function.md)」を参照してください。  
  
 プールが有効になっている接続で SQLDisconnect を呼び出す前に、アプリケーションで SQL_ATTR_RESET_CONNECTION を設定できます。 詳細については、「 [SQLSetConnectAttr 関数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)」を参照してください。  
  
 プールされた接続に接続するためにアプリケーションが **SQLDriverConnect** を呼び出す場合、次の制限が適用されます。  
  
-   接続文字列で **SAVEFILE** キーワードが指定されている場合、接続プール処理は実行されません。  
  
-   接続プールが有効になっている場合、 **SQLDriverConnect**は*drivercompletion*引数 SQL_DRIVER_NOPROMPT でのみ呼び出すことができます。他の*Drivercompletion*で**SQLDriverConnect**が呼び出されると、SQLSTATE HY110 (無効なドライバーの完了) が返されます。  
  
## <a name="connection-attributes"></a>接続属性  
 **SQLSetConnectAttr**を使用して設定された SQL_ATTR_LOGIN_TIMEOUT 接続属性は、アプリケーションに戻る前に、ドライバーによって正常に接続されたログイン要求の完了を待機する秒数を定義します。 接続文字列を入力するように求められた場合は、ドライバーが接続プロセスを開始するときに、各ログイン要求の待機期間が開始されます。  
  
 既定では、ドライバーは SQL_MODE_READ_WRITE アクセスモードで接続を開きます。 アクセスモードを SQL_MODE_READ_ONLY に設定するには、 **SQLDriverConnect**を呼び出す前に、アプリケーションで SQL_ATTR_ACCESS_MODE 属性を指定して**SQLSetConnectAttr**を呼び出す必要があります。  
  
 既定の変換ライブラリがデータソースのシステム情報に指定されている場合は、ドライバーによって読み込まれます。 SQL_ATTR_TRANSLATE_LIB 属性を指定して **SQLSetConnectAttr** を呼び出すことによって、別の変換ライブラリを読み込むことができます。 SQL_ATTR_TRANSLATE_OPTION オプションを指定して **SQLSetConnectAttr** を呼び出すことによって、翻訳オプションを指定できます。  
  
 詳細については、「 [SQLDriverConnect を使用した接続](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)」を参照してください。  
  
```cpp  
// SQLDriverConnect_ref.cpp  
// compile with: odbc32.lib user32.lib  
#include <windows.h>  
#include <sqlext.h>  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
  
   SQLCHAR OutConnStr[255];  
   SQLSMALLINT OutConnStrLen;  
  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
  
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            retcode = SQLDriverConnect( // SQL_NULL_HDBC  
               hdbc,   
               desktopHandle,   
               (SQLCHAR*)"driver=SQL Server",   
               _countof("driver=SQL Server"),  
               OutConnStr,  
               255,   
               &OutConnStrLen,  
               SQL_DRIVER_PROMPT );  
  
            // Allocate statement handle  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {                 
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
  
               // Process data  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               }  
  
               SQLDisconnect(hdbc);  
            }  
  
            SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
         }  
      }  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
   }  
}  
```  
  
 「 [サンプル ODBC プログラム](../../../odbc/reference/sample-odbc-program.md)」も参照してください。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|ハンドルの割り当て|[SQLAllocHandle 関数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|データソースへの接続に必要な値の検出と列挙|[SQLBrowseConnect 関数](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|データ ソースに接続する|[SQLConnect 関数](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|データソースからの切断|[SQLDisconnect 関数](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|ドライバーの説明と属性を返す|[SQLDrivers 関数](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|ハンドルの解放|[SQLFreeHandle 関数](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|接続属性の設定|[SQLSetConnectAttr 関数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
