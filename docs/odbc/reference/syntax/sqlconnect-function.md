---
description: SQLConnect 関数
title: SQLConnect 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLConnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLConnect
helpviewer_keywords:
- SQLConnect function [ODBC]
ms.assetid: 59075e46-a0ca-47bf-972a-367b08bb518d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 714bc6f69a72609ee266effff71f1898d62ec7d6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461204"
---
# <a name="sqlconnect-function"></a>SQLConnect 関数
**互換性**  
 導入されたバージョン: ODBC 1.0 標準準拠: ISO 92  
  
 **まとめ**  
 **SQLConnect** は、ドライバーとデータソースへの接続を確立します。 接続ハンドルは、データソースへの接続に関するすべての情報 (状態、トランザクション状態、エラー情報など) のストレージを参照します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLConnect(  
     SQLHDBC        ConnectionHandle,  
     SQLCHAR *      ServerName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      UserName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      Authentication,  
     SQLSMALLINT    NameLength3);  
```  
  
## <a name="arguments"></a>引数  
 *ConnectionHandle*  
 [入力] 接続ハンドル。  
  
 *ServerName*  
 代入データソース名。 データが、プログラムと同じコンピューター、またはネットワーク上の別のコンピューターに配置されている可能性があります。 アプリケーションでデータソースを選択する方法の詳細については、「 [データソースまたはドライバーの選択](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)」を参照してください。  
  
 *NameLength1*  
 代入**ServerName* の長さ (文字数)。  
  
 *UserName*  
 代入ユーザー識別子。  
  
 *NameLength2*  
 代入**ユーザー名* の長さ (文字数)。  
  
 *認証*  
 代入認証文字列 (通常はパスワード)。  
  
 *NameLength3*  
 代入文字での **認証* の長さ。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE、または SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>診断  
 **SQLConnect**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返した場合、関連付けられた SQLSTATE 値を取得するには、 *handletype* SQL_HANDLE_DBC および*connectionhandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出します。 次の表に、 **SQLConnect** によって通常返される SQLSTATE 値と、この関数のコンテキストでのそれぞれについて説明します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01S02|オプションの値が変更されました|ドライバーは、 **SQLSetConnectAttr**の*valueptr*引数に指定された値をサポートしておらず、同様の値に置き換えられました。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|08001|クライアントが接続を確立できません|ドライバーは、データソースとの接続を確立できませんでした。|  
|08002|使用中の接続名|(DM) 指定された *Connectionhandle* は、データソースとの接続を確立するために既に使用されていましたが、接続が開いているか、ユーザーが接続を参照していました。|  
|08004|サーバーが接続を拒否しました|データソースは、実装定義の理由により、接続の確立を拒否しました。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続しようとしているデータソースとの間の通信リンクが失敗しました。|  
|28000|認証の指定が無効です|引数の *ユーザー名* に指定された値、または引数 *認証* に指定された値が、データソースによって定義された制限に違反しました。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * \* Messagetext*バッファーの**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|(DM) ドライバーマネージャーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|*Connectionhandle*に対して非同期処理が有効になりました。 **SQLConnect**関数が呼び出され、実行が完了する前に、 [Sqlcancelhandle 関数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)が*connectionhandle*で呼び出されました。その後、 **SQLConnect**関数が*connectionhandle*で再度呼び出されました。<br /><br /> または、 **SQLConnect**関数が呼び出され、実行が完了する前に、マルチスレッドアプリケーションの別のスレッドからの*Connectionhandle*で**sqlcancelhandle**が呼び出されました。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数 (この1つではない) が *Connectionhandle* に対して呼び出されましたが、この関数が呼び出されたときにまだ実行されていました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY090|文字列またはバッファーの長さが無効です|(DM) 引数 *NameLength1*、 *NameLength2*、または *NameLength3* に指定された値が0未満ですが、SQL_NTS と等しくありません。<br /><br /> (DM) 引数 *NameLength1* に指定された値が、データソース名の最大長を超えました。|  
|HYT00|タイムアウトに達しました|データソースへの接続が完了する前に、クエリのタイムアウト期間が経過しました。 タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_LOGIN_TIMEOUT によって設定されます。|  
|HY114|ドライバーは、接続レベルの非同期関数の実行をサポートしていません|(DM) アプリケーションは、接続を確立する前に、接続ハンドルで非同期操作を有効にしました。 ただし、ドライバーは接続ハンドルに対する非同期操作をサポートしていません。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) データソース名で指定されたドライバーでは、関数はサポートされていません。|  
|IM002|データソースが見つからず、既定のドライバーが指定されていません|(DM) 引数 *ServerName* に指定されたデータソース名がシステム情報に見つからなかったか、既定のドライバー仕様がありませんでした。|  
|IM003|指定されたドライバーに接続できませんでした|(DM) システム情報のデータソースの仕様に記載されているドライバが見つからないか、何らかの理由で接続できませんでした。|  
|IM004|SQL_HANDLE_ENV のドライバーの SQLAllocHandle に失敗しました|(DM) **SQLConnect**中、ドライバーマネージャーは、 *handletype*が SQL_HANDLE_ENV のドライバーの**SQLAllocHandle**関数を呼び出しましたが、ドライバーはエラーを返しました。|  
|IM005|SQL_HANDLE_DBC のドライバーの SQLAllocHandle に失敗しました|(DM) **SQLConnect**中、ドライバーマネージャーは、 *handletype*が SQL_HANDLE_DBC のドライバーの**SQLAllocHandle**関数を呼び出しましたが、ドライバーはエラーを返しました。|  
|IM006|ドライバーの SQLSetConnectAttr に失敗しました|**SQLConnect**中に、ドライバーマネージャーがドライバーの**SQLSetConnectAttr**関数を呼び出し、ドライバーがエラーを返しました。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|IM009|Translation DLL に接続できません|ドライバーは、データソースに対して指定された変換 DLL に接続できませんでした。|  
|IM010|データソース名が長すぎます|(DM) * \* サーバー名*が SQL_MAX_DSN_LENGTH 文字を超えています。|  
|IM014|指定された DSN には、ドライバーとアプリケーションのアーキテクチャの不一致が含まれています|(DM) 32 ビットアプリケーションは、64ビットドライバーに接続する DSN を使用します。または、その逆も同様です。|  
|IM015|SQL_HANDLE_DBC_INFO_HANDLE のドライバーの SQLConnect に失敗しました|ドライバーが SQL_ERROR を返した場合、ドライバーマネージャーはアプリケーションに SQL_ERROR を返し、接続は失敗します。<br /><br /> SQL_HANDLE_DBC_INFO_TOKEN の詳細については、「 [ODBC ドライバーでの接続プールの認識の開発](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)」を参照してください。|  
|IM017|非同期通知モードでは、ポーリングは無効になっています|通知モデルが使用されるたびに、ポーリングは無効になります。|  
|IM018|**Sqlcompleteasync** は、このハンドルで前の非同期操作を完了するために呼び出されていません。|ハンドルに対する前の関数呼び出しが SQL_STILL_EXECUTING を返し、通知モードが有効になっている場合は、処理を完了するために、ハンドルに対して **Sqlcompleteasync** を呼び出す必要があります。|  
|S1118|ドライバーは非同期通知をサポートしていません|ドライバーが非同期通知をサポートしていない場合、SQL_ATTR_ASYNC_DBC_EVENT または SQL_ATTR_ASYNC_DBC_RETCODE_PTR を設定することはできません。|  
  
## <a name="comments"></a>コメント  
 アプリケーションで **SQLConnect**を使用する理由の詳細については、「 [SQLConnect を使用した接続](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)」を参照してください。  
  
 ドライバーマネージャーは、アプリケーションが関数 (**SQLConnect**、 **SQLDriverConnect**、または **SQLBrowseConnect**) を呼び出してドライバーに接続するまで、ドライバーに接続しません。 その時点までは、ドライバーマネージャーは独自のハンドルを使用し、接続情報を管理します。 アプリケーションが接続関数を呼び出すと、ドライバーマネージャーは、指定された *Connectionhandle*に対してドライバーが現在接続されているかどうかを確認します。  
  
-   ドライバーがに接続されていない場合、ドライバーマネージャーはドライバーに接続し、 *Handletype*が SQL_HANDLE_ENV、 **SQLAllocHandle**が*handletype* SQL_HANDLE_DBC、 **SQLSetConnectAttr** (アプリケーションで接続属性が指定されている場合)、およびドライバー内の接続関数を使用して**SQLAllocHandle**を呼び出します。 ドライバーマネージャーは SQLSTATE IM006 (ドライバーの **SQLSetConnectOption** failed) を返し、ドライバーが **SQLSetConnectAttr**に対してエラーを返した場合は、接続関数の SQL_SUCCESS_WITH_INFO します。 詳細については、「 [データソースまたはドライバーへの接続](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)」を参照してください。  
  
-   指定したドライバーが既に *Connectionhandle*でに接続されている場合、ドライバーマネージャーはドライバー内の接続関数だけを呼び出します。 この場合、ドライバーは、 *Connectionhandle* のすべての接続属性が現在の設定を維持していることを確認する必要があります。  
  
-   別のドライバーがに接続されている場合、ドライバーマネージャーは SQL_HANDLE_DBC の*Handletype*を使用して**sqlfreehandle**を呼び出し、その環境で他のドライバーがに接続されていない場合は、接続されたドライバーの SQL_HANDLE_ENV の*Handletype*を使用して**sqlfreehandle**を呼び出し、そのドライバーを切断します。 次に、ドライバーがに接続されていない場合と同じ操作を実行します。  
  
 次に、ドライバーによってハンドルが割り当てられ、それ自体が初期化されます。  
  
 アプリケーションが **sqldisconnect**を呼び出すと、ドライバーマネージャーはドライバーで **sqldisconnect** を呼び出します。 ただし、ドライバーは切断されません。 これにより、データソースに対して繰り返し接続および切断を行うアプリケーションに対して、ドライバーがメモリ内に保持されます。 アプリケーションが SQL_HANDLE_DBC の*Handletype*を使用して**sqlfreehandle**を呼び出すと、ドライバーマネージャーは、 *handletype が*SQL_HANDLE_DBC で sqlfreehandle を呼び出した後、ドライバーの SQL_HANDLE_ENV の*handletype*を使用して**sqlfreehandle** **を呼び出し、** ドライバーを切断します。  
  
 ODBC アプリケーションでは、複数の接続を確立できます。  
  
## <a name="driver-manager-guidelines"></a>ドライバーマネージャーのガイドライン  
 **ServerName* の内容は、ドライバーマネージャーとドライバーが連携してデータソースへの接続を確立する方法に影響します。  
  
-   \* *ServerName*に有効なデータソース名が含まれている場合、ドライバーマネージャーは対応するデータソースの仕様をシステム情報で検索し、関連付けられているドライバーに接続します。 ドライバーマネージャーは、各 **SQLConnect** 引数をドライバーに渡します。  
  
-   データソース名が見つからない場合、または *ServerName* が null ポインターの場合は、ドライバーマネージャーが既定のデータソースの仕様を特定し、関連付けられているドライバーに接続します。 ドライバーマネージャーは、 *ユーザー名* と *認証* の引数が変更されていないことをドライバーに渡し、 *ServerName* 引数の "DEFAULT" を渡します。  
  
-   *ServerName*引数が "default" の場合は、ドライバーマネージャーが既定のデータソースの仕様を特定し、関連付けられているドライバーに接続します。 ドライバーマネージャーは、各 **SQLConnect** 引数をドライバーに渡します。  
  
-   データソース名が見つからない場合、または *ServerName* が null ポインターであり、既定のデータソースの仕様が存在しない場合、ドライバーマネージャーは SQLSTATE IM002 (データソース名が見つからず、既定のドライバーが指定されていません) で SQL_ERROR を返します。  
  
 ドライバーマネージャーによって接続されると、ドライバーは、対応するデータソースの仕様をシステム情報で特定し、仕様のドライバー固有の情報を使用して必要な接続情報のセットを完成させることができます。  
  
 既定の変換ライブラリがデータソースのシステム情報に指定されている場合、ドライバーはそのライブラリに接続します。 SQL_ATTR_TRANSLATE_LIB 属性を使用して **SQLSetConnectAttr** を呼び出すことによって、別の変換ライブラリに接続できます。 SQL_ATTR_TRANSLATE_OPTION 属性を指定して **SQLSetConnectAttr** を呼び出すことによって、翻訳オプションを指定できます。  
  
 ドライバーが **SQLConnect**をサポートしている場合、ドライバーのシステム情報の driver キーワードセクションには、最初の文字が "Y" に設定された **connectfunctions** キーワードが含まれている必要があります。  
  
### <a name="connection-pooling"></a>接続プール  
 接続プールを使用すると、既に作成されている接続をアプリケーションで再利用できます。 接続プールが有効になっていて、 **SQLConnect** が呼び出されると、ドライバーマネージャーは、接続プール用に指定された環境内の接続のプールの一部である接続を使用して接続を試みます。 この環境は、プール内の接続を使用するすべてのアプリケーションで使用される共有環境です。  
  
 **SQLSetEnvAttr**を呼び出すことによって環境が割り当てられる前に、接続プールが有効になります。これにより SQL_ATTR_CONNECTION_POOLING が SQL_CP_ONE_PER_DRIVER に設定されます (ドライバーごとに最大1つのプールを指定)。または SQL_CP_ONE_PER_HENV (環境あたり最大1つのプールを指定)。 この場合、 **SQLSetEnvAttr**は、 *EnvironmentHandle*を null に設定して呼び出されます。これにより、属性がプロセスレベルの属性になります。 SQL_ATTR_CONNECTION_POOLING が SQL_CP_OFF に設定されている場合、接続プールは無効になります。  
  
 接続プールを有効にすると、SQL_HANDLE_ENV の*Handletype*を持つ**SQLAllocHandle**が呼び出され、環境が割り当てられます。 接続プールが有効になっているため、この呼び出しによって割り当てられる環境は共有環境です。 ただし、 **SQLAllocHandle** SQL_HANDLE_DBC の *handletype* が呼び出されるまで、使用される環境は決定されません。  
  
 SQL_HANDLE_DBC の*Handletype*を持つ**SQLAllocHandle**は、接続を割り当てるために呼び出されます。 ドライバーマネージャーは、アプリケーションによって設定された環境属性に一致する既存の共有環境の検索を試みます。 このような環境が存在しない場合は、暗黙的な *共有環境*として作成されます。 一致する共有環境が見つかった場合は、環境ハンドルがアプリケーションに返され、その参照カウントがインクリメントされます。  
  
 ただし、 **SQLConnect** が呼び出されるまで、使用される接続は決定されません。 その時点で、ドライバーマネージャーは、アプリケーションによって要求された条件に一致する接続プール内の既存の接続を見つけようとします。 これらの条件には、 **SQLConnect** の呼び出しで要求された接続オプション ( *ServerName*、 *UserName*、 *Authentication* キーワードの値) と、 **SQLAllocHandle** 以降に設定されたすべての接続属性 (SQL_HANDLE_DBC の *handletype* が呼び出された場合) が含まれます。 ドライバーマネージャーは、プール内の接続の対応する接続キーワードと属性に対して、これらの条件を確認します。 一致が見つかった場合は、プール内の接続が使用されます。 一致するものが見つからない場合は、新しい接続が作成されます。  
  
 SQL_ATTR_CP_MATCH 環境属性が SQL_CP_STRICT_MATCH に設定されている場合、使用するプール内の接続に対して一致する必要があります。 SQL_ATTR_CP_MATCH 環境属性が SQL_CP_RELAXED_MATCH に設定されている場合、 **SQLConnect** の呼び出しの接続オプションは一致している必要がありますが、すべての接続属性が一致している必要があります。  
  
 **SQLConnect**が呼び出される前にアプリケーションによって設定された接続属性がプール内の接続の接続属性と一致しない場合は、次の規則が適用されます。  
  
-   接続を確立する前に接続属性を設定する必要がある場合は、次のようにします。  
  
     SQL_ATTR_CP_MATCH が SQL_CP_STRICT_MATCH 場合、プールされた接続の SQL_ATTR_PACKET_SIZE は、アプリケーションによって設定された属性と同じである必要があります。 SQL_CP_RELAXED_MATCH 場合、SQL_ATTR_PACKET_SIZE の値は異なる場合があります。  
  
     SQL_ATTR_LOGIN_VALUE の値は一致には影響しません。  
  
-   接続の作成前または終了後に接続属性を設定できる場合は、次のように指定します。  
  
     接続属性がアプリケーションによって設定されておらず、プール内の接続に設定されていて、既定値がある場合は、プールされた接続の接続属性が既定値に戻り、一致が宣言されます。 既定値がない場合、プールされた接続は一致と見なされません。  
  
     接続属性がアプリケーションによって設定されていても、プール内の接続に対して設定されていない場合、プールの接続属性はアプリケーションによって設定されたものに変更され、一致が宣言されます。  
  
     接続属性がアプリケーションによって設定されており、プール内の接続にも設定されていても、値が異なる場合は、アプリケーションの接続属性の値が使用され、一致が宣言されます。  
  
-   ドライバー固有の接続属性の値が同一ではなく、SQL_ATTR_CP_MATCH が SQL_CP_STRICT_MATCH に設定されている場合、プール内の接続は使用されません。  
  
 アプリケーションが **Sqldisconnect** を呼び出して切断すると、接続が接続プールに返され、再利用できるようになります。  
  
### <a name="optimizing-connection-pooling-performance"></a>接続プールのパフォーマンスの最適化  
 分散トランザクションが関係している場合は、SQLUINTEGER ビットマスクである **SQL_DTC_TRANSITION_COST**を使用して、接続プールのパフォーマンスを最適化することができます。 参照される遷移は、値0から0以外の値に移動する SQL_ATTR_ENLIST_IN_DTC 接続属性の遷移であり、その逆も同様です。 これは、分散トランザクションに参加していない分散トランザクションに参加していない接続であり、その逆も同様です。 ドライバーが参加を実装した方法 (接続属性の設定 SQL_ATTR_ENLIST_IN_DTC) によっては、これらの移行に負荷がかかり、最適なパフォーマンスが得られないようにする必要があります。  
  
 ドライバーによって返される値には、次のビットの任意の組み合わせが含まれます。  
  
-   **SQL_DTC_ENLIST_EXPENSIVE**が設定されている場合、0以外の移行では、0以外の値から別の0以外の値への移行よりも大幅にコストが高くなります (次のトランザクションで、以前に参加した接続に参加します)。  
  
-   **SQL_DTC_UNENLIST_EXPENSIVE**が設定されている場合は、0以外の値を設定すると、SQL_ATTR_ENLIST_IN_DTC 属性が既に0に設定されている接続を使用する場合よりも大幅にコストが高くなります。  
  
 パフォーマンスと接続の使用のトレードオフがあります。 ドライバーが、これらの遷移のうち1つ以上が高コストであることを示している場合、ドライバーマネージャーの接続プーラーは、プール内の接続数を増やすことによってこれに応答します。 プール内の一部の接続は非トランザクション使用に適しており、トランザクション使用に適しています。 ただし、これらの遷移が高コストでないことがドライバーによって示されている場合は、使用できる接続の数を減らすことができます。  
  
 SQL_ATTR_ENLIST_IN_DTC をサポートしていないドライバーは、SQL_DTC_TRANSITION_COST をサポートする必要はありません。 SQL_DTC_TRANSITION_COST ではなく SQL_ATTR_ENLIST_IN_DTC をサポートするドライバーの場合、この値に対してドライバーが 0 (ビットセット) を返した場合と同じように、移行に負荷がかかることが想定されます。  
  
 SQL_DTC_TRANSITION_COST は odbc 3.5 (ODBC 2) で導入されました。ドライバーマネージャーは、ドライバーのバージョンに関係なく、この情報を照会するため、 *x* ドライバーでもサポートされます。  
  
### <a name="code-example"></a>コード例  
 次の例では、アプリケーションが環境ハンドルと接続ハンドルを割り当てます。 次に、ユーザー ID ジョンズとパスワード Sesame を使用して SalesOrders データソースに接続し、データを処理します。 データの処理が完了すると、データソースから切断され、ハンドルが解放されます。  
  
```cpp  
// SQLConnect_ref.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
  
   SQLCHAR * OutConnStr = (SQLCHAR * )malloc(255);  
   SQLSMALLINT * OutConnStrLen = (SQLSMALLINT *)malloc(255);  
  
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            // Connect to data source  
            retcode = SQLConnect(hdbc, (SQLCHAR*) "NorthWind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
  
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
  
### <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|ハンドルの割り当て|[SQLAllocHandle 関数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|データソースへの接続に必要な値の検出と列挙|[SQLBrowseConnect 関数](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|データソースからの切断|[SQLDisconnect 関数](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|接続文字列またはダイアログボックスを使用したデータソースへの接続|[SQLDriverConnect 関数](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|接続属性の設定を返す|[SQLGetConnectAttr 関数](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|接続属性の設定|[SQLSetConnectAttr 関数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
