---
description: SQLBrowseConnect 関数
title: SQLBrowseConnect 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBrowseConnect
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBrowseConnect
helpviewer_keywords:
- SQLBrowseConnect function [ODBC]
ms.assetid: b7f1be66-e6c7-4790-88ec-62b7662103c0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 712dbb366e25098c7956ffbb9c8733a437339297
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499635"
---
# <a name="sqlbrowseconnect-function"></a>SQLBrowseConnect 関数
**互換性**  
 導入されたバージョン: ODBC 1.0 標準準拠: ODBC  
  
 **まとめ**  
 **SQLBrowseConnect** は、データソースへの接続に必要な属性と属性値を検出および列挙する反復的な方法をサポートしています。 **SQLBrowseConnect**を呼び出すたびに、一連の属性と属性値が返されます。 すべてのレベルが列挙されると、データソースへの接続が完了し、 **SQLBrowseConnect**によって完全な接続文字列が返されます。 SQL_SUCCESS または SQL_SUCCESS_WITH_INFO のリターンコードは、すべての接続情報が指定されており、アプリケーションがデータソースに接続されていることを示します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLBrowseConnect(  
     SQLHDBC         ConnectionHandle,  
     SQLCHAR *       InConnectionString,  
     SQLSMALLINT     StringLength1,  
     SQLCHAR *       OutConnectionString,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLength2Ptr);  
```  
  
## <a name="arguments"></a>引数  
 *ConnectionHandle*  
 [入力] 接続ハンドル。  
  
 *InConnectionString*  
 代入要求の接続文字列を参照します (「コメント」の「*Inconnectionstring* 引数」を参照してください)。  
  
 *StringLength1*  
 代入文字の長さ **Inconnectionstring* 。  
  
 *OutConnectionString*  
 Output参照結果の接続文字列を返す文字バッファーへのポインター ("Comments" の*Outconnectionstring* 引数を参照してください)。  
  
 *Outconnectionstring*が NULL の場合でも、 *StringLength2Ptr*は、 *outconnectionstring*が指すバッファー内で返すことができる文字の合計数 (文字データの null 終端文字を除く) を返します。  
  
 *BufferLength*  
 代入**Outconnectionstring* バッファーの長さ (文字数)。  
  
 *StringLength2Ptr*  
 OutputOutconnectionstring で返すことができる文字の合計数 (null 終端を除く) \* *OutConnectionString*。 返すことのできる文字数が*Bufferlength*以上の場合、 \* *outconnectionstring*内の接続文字列は*bufferlength*に切り捨てられ、null 終了文字の長さを引いたものになります。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NEED_DATA、SQL_ERROR、SQL_INVALID_HANDLE、または SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>診断  
 **SQLBrowseConnect**が SQL_ERROR、SQL_SUCCESS_WITH_INFO、または SQL_NEED_DATA を返す場合、関連付けられた SQLSTATE 値は、 *Handletype* SQL_HANDLE_STMT と*connectionhandle のハンドル*を指定して**SQLGetDiagRec**を呼び出すことによって取得できます。 次の表に、 **SQLBrowseConnect** によって一般的に返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データ、右側が切り捨てられました|バッファー \* *outconnectionstring*は、参照結果の接続文字列全体を返すのに十分な大きさではないため、文字列が切り捨てられました。 Buffer **StringLength2Ptr* には、切り捨てられていない参照結果の接続文字列の長さが含まれています。 (関数は SQL_NEED_DATA を返します)。|  
|01S00|接続文字列の属性が無効です|参照要求の接続文字列 (*Inconnectionstring*) に無効な attribute キーワードが指定されました。 (関数は SQL_NEED_DATA を返します)。<br /><br /> 現在の接続レベルには適用されない、参照要求接続文字列 (*Inconnectionstring*) で属性キーワードが指定されました。 (関数は SQL_NEED_DATA を返します)。|  
|01S02|変更された値|ドライバーは、 **SQLSetConnectAttr**の*valueptr*引数に指定された値をサポートしておらず、同様の値に置き換えられました。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|08001|クライアントが接続を確立できません|ドライバーは、データソースとの接続を確立できませんでした。|  
|08002|使用中の接続名|(DM) 指定された接続は、データソースとの接続を確立するために既に使用されており、接続が開かれていました。|  
|08004|サーバーが接続を拒否しました|データソースは、実装定義の理由により、接続の確立を拒否しました。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続しようとしていたデータソースとの間の通信リンクが失敗しました。|  
|28000|認証の指定が無効です|参照要求の接続文字列 (*Inconnectionstring*) で指定されているユーザー id または認証文字列、またはその両方が、データソースによって定義された制限に違反しています。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * \* Messagetext*バッファーの**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|(DM) ドライバーマネージャーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。<br /><br /> ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|[Sqlcancelhandle 関数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)を呼び出して、非同期操作が取り消されました。 次に、 *Connectionhandle*で元の関数が再度呼び出されました。<br /><br /> マルチスレッドアプリケーションの別のスレッドからの*Connectionhandle*で**sqlcancelhandle**を呼び出して、操作が取り消されました。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数 (この1つではない) が *Connectionhandle* に対して呼び出されましたが、この関数が呼び出されたときにまだ実行されていました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY090|文字列またはバッファーの長さが無効です|(DM) 引数 *StringLength1* に指定された値が0未満であり、SQL_NTS と等しくありませんでした。<br /><br /> (DM) 引数 *Bufferlength* に指定された値が0未満でした。|  
|HY114|ドライバーは、接続レベルの非同期関数の実行をサポートしていません|(DM) アプリケーションは、接続を確立する前に、接続ハンドルで非同期操作を有効にしました。 ただし、ドライバーは接続ハンドルでの非同期操作をサポートしていません。|  
|HYT00|タイムアウトに達しました|データソースへの接続が完了する前に、ログインのタイムアウト期間が経過しました。 タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_LOGIN_TIMEOUT によって設定されます。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) 指定されたデータソース名に対応するドライバーが関数をサポートしていません。|  
|IM002|データソースが見つからず、既定のドライバーが指定されていません|(DM) 参照要求の接続文字列 (*Inconnectionstring*) で指定されたデータソース名がシステム情報に見つからなかったか、既定のドライバー仕様がありませんでした。<br /><br /> (DM) ODBC データソースと既定のドライバー情報がシステム情報に見つかりませんでした。|  
|IM003|指定されたドライバーを読み込めませんでした|(DM) システム情報で指定されているか、 **driver** キーワードによって指定されたデータソースの指定に含まれるドライバが見つからないか、他の何らかの理由で読み込めませんでした。|  
|IM004|SQL_HANDLE _ENV のドライバーの **SQLAllocHandle** に失敗しました|(DM) **SQLBrowseConnect**中、ドライバーマネージャーは、 *handletype*が SQL_HANDLE_ENV のドライバーの**SQLAllocHandle**関数を呼び出しましたが、ドライバーはエラーを返しました。|  
|IM005|SQL_HANDLE_DBC のドライバーの **SQLAllocHandle** に失敗しました|(DM) **SQLBrowseConnect**中、ドライバーマネージャーは、 *handletype*が SQL_HANDLE_DBC のドライバーの**SQLAllocHandle**関数を呼び出しましたが、ドライバーはエラーを返しました。|  
|IM006|ドライバーの **SQLSetConnectAttr** に失敗しました|(DM) **SQLBrowseConnect**中に、ドライバーマネージャーがドライバーの **SQLSetConnectAttr** 関数を呼び出し、ドライバーがエラーを返しました。|  
|IM009|翻訳 DLL を読み込めません|ドライバーは、データソースまたは接続用に指定された変換 DLL を読み込めませんでした。|  
|IM010|データソース名が長すぎます|(DM) DSN キーワードの属性値が SQL_MAX_DSN_LENGTH 文字を超えています。|  
|IM011|ドライバー名が長すぎます|(DM) DRIVER キーワードの属性値が255文字を超えています。|  
|IM012|DRIVER キーワード構文エラー|(DM) DRIVER キーワードのキーワードと値のペアに構文エラーが含まれています。|  
|IM014|指定された DSN には、ドライバーとアプリケーションのアーキテクチャの不一致が含まれています|(DM) 32 ビットアプリケーションは、64ビットドライバーに接続する DSN を使用します。または、その逆も同様です。|  
|IM017|非同期通知モードでは、ポーリングは無効になっています|通知モデルが使用されるたびに、ポーリングは無効になります。|  
|IM018|**Sqlcompleteasync** は、このハンドルで前の非同期操作を完了するために呼び出されていません。|ハンドルに対する前の関数呼び出しが SQL_STILL_EXECUTING を返し、通知モードが有効になっている場合は、処理を完了するために、ハンドルに対して **Sqlcompleteasync** を呼び出す必要があります。|  
|S1118|ドライバーは非同期通知をサポートしていません|ドライバーが非同期通知をサポートしていない場合、SQL_ATTR_ASYNC_DBC_EVENT または SQL_ATTR_ASYNC_DBC_RETCODE_PTR を設定することはできません。|  
  
## <a name="inconnectionstring-argument"></a>InConnectionString 引数  
 参照要求の接続文字列の構文は次のとおりです。  
  
 *接続文字列* :: = *属性*[ `;` ] &#124; *属性* `;` *接続文字列*;<br>
 *attribute* :: = *attribute-keyword* `=` *属性-value* &#124; `DRIVER=` [ `{` ]*属性-値*[ `}` ]<br>
 *属性-キーワード* :: = `DSN` &#124; `UID` &#124; `PWD` &#124; *ドライバー定義-attribute-キーワード*<br>
 *属性-値* :: = *文字文字列*<br>
 *ドライバー定義-属性-キーワード* :: = *識別子*<br>
  
 *文字文字列*に0個以上の文字が含まれています。*識別子*に1つ以上の文字が含まれています。*属性キーワードで*は大文字と小文字が区別されません。*属性-値*は大文字と小文字が区別されます。また、 **DSN**キーワードの値は空白だけで構成されていません。 接続文字列と初期化ファイルの文法のために、 **[] {} ()、;? という文字を含むキーワードと属性値が使用されています \* 。=! @** は避けてください。 システム情報の文法により、キーワードとデータソース名に円記号 () を含めることはできません \\ 。 ODBC 2 の場合。DRIVER キーワードの属性値の周囲には、 *x* ドライバーと中かっこが必要です。  
  
 参照要求の接続文字列でキーワードが繰り返し使用されている場合、ドライバーは最初に見つかったキーワードに関連付けられている値を使用します。 **DSN**と**ドライバー**のキーワードが同じ参照要求の接続文字列に含まれている場合、ドライバーマネージャーとドライバーでは、いずれかのキーワードが最初に使用されます。  
  
 アプリケーションでデータソースまたはドライバーを選択する方法の詳細については、「 [データソースまたはドライバーの選択](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)」を参照してください。  
  
## <a name="outconnectionstring-argument"></a>OutConnectionString 引数  
 参照結果の接続文字列は、接続属性の一覧です。 接続属性は、属性キーワードとそれに対応する属性値で構成されます。 参照結果の接続文字列の構文は次のとおりです。  
  
 *接続文字列* :: = *属性*[ `;` ] &#124; *属性* `;` *の接続文字列*<br>
 *attribute* :: = [ `*` ]*属性-キーワード* `=` *属性-値*<br>
 *属性-* keyword:: = *ODBC-attribute* -attribute-attribute *-attribute-attribute &#124;-* keyword<br>
 *ODBC 属性-keyword* = { `UID` &#124; `PWD` } [ `:` *ローカライズ*さ*れた識別子] ドライバー定義*属性-キーワード:: =*識別子*[ `:` *ローカライズ*された識別子]*属性-value* :: = 属性-値 `{` *リスト* `}` &#124; `?` (かっこはリテラルで、ドライバーによって返されます)。<br>
 *属性-値リスト*:: =*文字*文字列 [ローカライズされた文字列 `:` *localized-character string*] &#124;*文字文字列*[ローカライズされた文字列] `:` *localized-character string* `,` *属性値リスト*<br>
  
 ここでは、 *文字文字列* とローカライズされた *文字列に* 0 個以上の文字が含まれています。 *識別子* およびローカライズされた *識別子に* は1つ以上の文字が含まれます。 *属性キーワードで* は大文字と小文字が区別されません。および *属性値* は大文字と小文字が区別されます。 接続文字列と初期化ファイルの文法、キーワード、ローカライズされた識別子、および文字 **[] {} ()、;? \*=! @** は避けてください。 システム情報の文法により、キーワードとデータソース名に円記号 () を含めることはできません \\ 。  
  
 参照結果の接続文字列の構文は、次のセマンティックルールに従って使用されます。  
  
-   アスタリスク () が \* *属性キーワード*の前にある場合、 *属性* は省略可能で、次に **SQLBrowseConnect**を呼び出したときに省略できます。  
  
-   属性キーワード **UID** と **PWD** は、 **SQLDriverConnect**で定義されているものと同じ意味を持ちます。  
  
-   ドライバーによっ *て定義* される-attribute キーワードは、属性値を指定できる属性の種類を指定します。 たとえば、 **サーバー**、 **データベース**、 **ホスト**、 **DBMS**などがあります。  
  
-   *ODBC-属性-* キーワードと *ドライバー定義属性* -キーワードには、ローカライズされた、またはユーザーフレンドリなバージョンのキーワードが含まれています。 これは、アプリケーションによってダイアログボックスのラベルとして使用される場合があります。 ただし、参照要求文字列をドライバーに渡すときには、 **UID**、 **PWD**、または *識別子* だけを使用する必要があります。  
  
-   {*Attribute-値リスト*} は、対応する *属性キーワード*に対して有効な実際の値の列挙体です。 中かっこ () は {} 選択肢の一覧を示していないことに注意してください。これらはドライバーによって返されます。 たとえば、サーバー名の一覧やデータベース名の一覧などがあります。  
  
-   *属性値*が単一の疑問符 (?) の場合、1つの値が*属性-キーワード*に対応します。 たとえば、UID = ジョンズ;PWD = Sesame。  
  
-   **SQLBrowseConnect**を呼び出すたびに、接続プロセスの次のレベルを満たすために必要な情報のみが返されます。 ドライバーは、各呼び出しでコンテキストが常に決定できるように、状態情報を接続ハンドルに関連付けます。  
  
## <a name="using-sqlbrowseconnect"></a>SQLBrowseConnect の使用  
 **SQLBrowseConnect** には、割り当てられた接続が必要です。 ドライバーマネージャーは、最初の参照要求接続文字列で指定されたデータソース名に対応する、またはで指定されたドライバーを読み込みます。このエラーが発生した場合の詳細については、「 [SQLConnect 関数](../../../odbc/reference/syntax/sqlconnect-function.md)」の「コメント」セクションを参照してください。 ドライバーは、参照プロセス中にデータソースとの接続を確立することがあります。 **SQLBrowseConnect**が SQL_ERROR を返すと、未処理の接続が終了し、接続が未接続状態に戻ります。  
  
> [!NOTE]  
>  **SQLBrowseConnect** では、接続プールはサポートされていません。 接続プールが有効になっている間に **SQLBrowseConnect** が呼び出された場合、SQLSTATE HY000 (一般エラー) が返されます。  
  
 **SQLBrowseConnect**が接続時に初めて呼び出されるときは、参照要求の接続文字列に**DSN**キーワードまたは**DRIVER**キーワードが含まれている必要があります。 参照要求の接続文字列に **DSN** キーワードが含まれている場合、ドライバーマネージャーは、対応するデータソースの仕様をシステム情報で検索します。  
  
-   対応するデータソースの仕様が検出されると、関連するドライバー DLL が読み込まれます。ドライバーは、データソースに関する情報をシステム情報から取得できます。  
  
-   ドライバーマネージャーは、対応するデータソースの仕様を見つけられない場合、既定のデータソースの仕様を検索し、関連付けられているドライバー DLL を読み込みます。ドライバーは、システム情報から既定のデータソースに関する情報を取得できます。 "DEFAULT" は、DSN のドライバーに渡されます。  
  
-   ドライバーマネージャーが対応するデータソースの仕様を見つけられず、既定のデータソースの仕様がない場合は、SQLSTATE IM002 (データソースが見つからず、既定のドライバーが指定されていない) で SQL_ERROR が返されます。  
  
 参照要求の接続文字列に **driver** キーワードが含まれている場合、ドライバーマネージャーは、指定されたドライバーを読み込みます。システム情報にデータソースを配置しようとすることはありません。 **Driver キーワードは**システム情報の情報を使用しないため、ドライバーは、参照要求接続文字列の情報のみを使用してデータソースに接続できるように、十分なキーワードを定義する必要があります。  
  
 **SQLBrowseConnect**を呼び出すたびに、アプリケーションは参照要求の接続文字列で接続属性の値を指定します。 ドライバーは、参照結果の接続文字列で、一連の属性と属性値を返します。参照要求の接続文字列にまだ列挙されていない接続属性がある限り、SQL_NEED_DATA を返します。 アプリケーションでは、参照結果の接続文字列の内容を使用して、次に **SQLBrowseConnect**を呼び出すための参照要求接続文字列を作成します。 次の**SQLBrowseConnect**の呼び出しには、すべての必須属性 ( *outconnectionstring*引数の前にアスタリスクが付いていない属性) を含める必要があります。 現在の参照要求の接続文字列を作成するときに、アプリケーションは以前の参照結果の接続文字列の内容を使用できないことに注意してください。つまり、以前のレベルで設定された属性に対して異なる値を指定することはできません。  
  
 すべてのレベルの接続とそれに関連付けられている属性が列挙されると、ドライバーは SQL_SUCCESS を返し、データソースへの接続が完了すると、アプリケーションに完全な接続文字列が返されます。 接続文字列は、 **SQLDriverConnect**と組み合わせて使用する場合に適しています。また、SQL_DRIVER_NOPROMPT オプションを使用して別の接続を確立することもできます。 ただし、 **SQLBrowseConnect**への別の呼び出しでは、完全な接続文字列を使用できません。 **SQLBrowseConnect** が再度呼び出された場合は、呼び出しのシーケンス全体を繰り返す必要があります。  
  
 **SQLBrowseConnect** は、参照プロセス中に回復可能な致命的でないエラーが発生した場合にも SQL_NEED_DATA を返します。たとえば、アプリケーションによって指定された無効なパスワードまたは属性キーワードです。 SQL_NEED_DATA が返され、参照結果の接続文字列が変更されていない場合、エラーが発生し、アプリケーションは **SQLGetDiagRec** を呼び出して、参照時エラーの SQLSTATE を返すことができます。 これにより、アプリケーションは属性を修正して参照を続行できます。  
  
 アプリケーションでは、 **Sqldisconnect**を呼び出すことで、いつでも参照プロセスを終了できます。 ドライバーは、未処理の接続を終了し、接続を切断された状態に戻します。  
  
 接続ハンドルで非同期操作が有効になっている場合、 **SQLBrowseConnect** も SQL_STILL_EXECUTING を返すことがあります。 SQL_NEED_DATA が返された場合、アプリケーションは **Sqldisconnect** を使用して参照プロセスを取り消す必要があります。 **SQLBrowseConnect**が SQL_STILL_EXECUTING を返す場合、アプリケーションは**sqlcancelhandle**を使用して、処理中の操作を取り消す必要があります。 関数がを返した後に **Sqlcancelhandle** を呼び出すと SQL_NEED_DATA は無効になります。  
  
 詳細については、「 [SQLBrowseConnect を使用した接続](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)」を参照してください。  
  
 ドライバーが **SQLBrowseConnect**をサポートしている場合、ドライバーのシステム情報の driver キーワードセクションには、3番目の文字が "Y" に設定された **connectfunctions** キーワードが含まれている必要があります。  
  
## <a name="code-example"></a>コード例  
  
> [!NOTE]  
>  Windows 認証をサポートするデータソースプロバイダーに接続する場合は、 `Trusted_Connection=yes` 接続文字列にユーザー ID とパスワードの情報ではなくを指定する必要があります。  
  
 次の例では、アプリケーションは **SQLBrowseConnect** を繰り返し呼び出します。 **SQLBrowseConnect**が SQL_NEED_DATA 返すたびに、outconnectionstring で必要なデータに関する情報が返さ \* *OutConnectionString*れます。 アプリケーションは、そのルーチンの**Getuserinput**に*outconnectionstring*を渡します (表示されません)。 **Getuserinput**情報を解析し、ダイアログボックスを構築して表示し、inconnectionstring にユーザーが入力した情報を返し \* *InConnectionString*ます。 アプリケーションは、次に **SQLBrowseConnect**を呼び出すときに、ユーザーの情報をドライバーに渡します。 アプリケーションがデータソースに接続するために必要なすべての情報を提供した後、 **SQLBrowseConnect** は SQL_SUCCESS を返し、アプリケーションは処理を続行します。  
  
 **SQLBrowseConnect**を呼び出して SQL Server ドライバーに接続する詳細な例については、「 [SQL Server の参照の例](../../../odbc/reference/develop-app/sql-server-browsing-example.md)」を参照してください。  
  
 たとえば、データソース Sales に接続するために、次のアクションが発生する可能性があります。 まず、アプリケーションが次の文字列を **SQLBrowseConnect**に渡します。  
  
```  
"DSN=Sales"  
```  
  
 ドライバーマネージャーは、データソース Sales に関連付けられているドライバーを読み込みます。 次に、アプリケーションから受け取ったのと同じ引数を使用して、ドライバーの **SQLBrowseConnect** 関数を呼び出します。 ドライバーは、**Outconnectionstring*に次の文字列を返します。  
  
```  
"HOST:Server={red,blue,green};UID:ID=?;PWD:Password=?"  
```  
  
 アプリケーションはこの文字列を **Getuserinput** ルーチンに渡します。これにより、ユーザーに対して、赤、青、または緑のサーバーを選択し、ユーザー ID とパスワードを入力するよう求めるダイアログボックスが作成されます。 ルーチンは、次のユーザー指定情報を \* *inconnectionstring*に渡して、アプリケーションが**SQLBrowseConnect**に渡します。  
  
```  
"HOST=red;UID=Smith;PWD=Sesame"  
```  
  
 **SQLBrowseConnect** はこの情報を使用して、パスワード Sesame を持つ Smith として red server に接続し、**outconnectionstring*で次の文字列を返します。  
  
```  
"*DATABASE:Database={SalesEmployees,SalesGoals,SalesOrders}"  
```  
  
 アプリケーションはこの文字列を **Getuserinput** ルーチンに渡します。これにより、ユーザーにデータベースを選択するよう求めるダイアログボックスが作成されます。 ユーザーが empdata を選択すると、アプリケーションは次の文字列を使用して最終的な **SQLBrowseConnect** を呼び出します。  
  
```  
"DATABASE=SalesOrders"  
```  
  
 これは、ドライバーがデータソースに接続するために必要な情報の最後の部分です。 **SQLBrowseConnect** は SQL_SUCCESS を返し、**outconnectionstring* には完了した接続文字列が含まれます。  
  
```cpp  
// SQLBrowseConnect_Function.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <sqltypes.h>  
#include <sqlext.h>  
  
#define BRWS_LEN 100  
SQLHENV henv;  
SQLHDBC hdbc;  
SQLHSTMT hstmt;  
SQLRETURN retcode;  
SQLCHAR szConnStrIn[BRWS_LEN], szConnStrOut[BRWS_LEN];  
SQLSMALLINT cbConnStrOut;  
  
void GetUserInput(SQLCHAR * szConnStrOut, SQLCHAR * szConnStrIn) {}  
  
int main() {  
   // Allocate the environment handle.  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);        
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
      // Set the version environment attribute.  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
         // Allocate the connection handle.  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            // Call SQLBrowseConnect until it returns a value other than SQL_NEED_DATA   
            // (pass data source name the first time).  If SQL_NEED_DATA is returned, call GetUserInput   
            // (not shown) to build a dialog from the values in szConnStrOut.  The user-supplied values   
            // are returned in szConnStrIn, which is passed in the next call to SQLBrowseConnect.  
  
            strcpy_s((char*)szConnStrIn, _countof(szConnStrIn), "DSN=Sales");  
            do {  
               retcode = SQLBrowseConnect(hdbc, szConnStrIn, SQL_NTS,  
                  szConnStrOut, BRWS_LEN, &cbConnStrOut);  
               if (retcode == SQL_NEED_DATA)  
                  GetUserInput(szConnStrOut, szConnStrIn);  
            } while (retcode == SQL_NEED_DATA);  
  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO){  
  
               // Allocate the statement handle.  
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
                  // Process data after successful connection  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               SQLDisconnect(hdbc);  
            }  
         }  
         SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
      }  
   }  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|接続ハンドルの割り当て|[SQLAllocHandle 関数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|データ ソースに接続する|[SQLConnect 関数](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|データソースからの切断|[SQLDisconnect 関数](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|接続文字列またはダイアログボックスを使用したデータソースへの接続|[SQLDriverConnect 関数](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|ドライバーの説明と属性を返す|[SQLDrivers 関数](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|接続ハンドルの解放|[SQLFreeHandle 関数](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
