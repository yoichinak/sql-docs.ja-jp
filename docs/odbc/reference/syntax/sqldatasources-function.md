---
description: SQLDataSources 関数
title: SQLDataSources ソース関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDataSources
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDataSources
helpviewer_keywords:
- SQLDataSources function [ODBC]
ms.assetid: 3f63b1b4-e70e-44cd-96c6-6878d50d0117
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bcf57779916b7a9d3189a5ce37b8603e5da5cb74
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461184"
---
# <a name="sqldatasources-function"></a>SQLDataSources 関数
**互換性**  
 導入されたバージョン: ODBC 1.0 標準準拠: ISO 92  
  
 **まとめ**  
 **Sqldatasources** ソースは、データソースに関する情報を返します。 この関数は、ドライバーマネージャーによってのみ実装されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLDataSources(  
     SQLHENV          EnvironmentHandle,  
     SQLUSMALLINT     Direction,  
     SQLCHAR *        ServerName,  
     SQLSMALLINT      BufferLength1,  
     SQLSMALLINT *    NameLength1Ptr,  
     SQLCHAR *        Description,  
     SQLSMALLINT      BufferLength2,  
     SQLSMALLINT *    NameLength2Ptr);  
```  
  
## <a name="arguments"></a>引数  
 *EnvironmentHandle*  
 代入環境ハンドル。  
  
 *方向*  
 代入ドライバーマネージャーが情報を返すデータソースを決定します。 次の値をとります。  
  
 SQL_FETCH_NEXT (一覧内の次のデータソース名を取得するため)、SQL_FETCH_FIRST (リストの先頭からフェッチ)、SQL_FETCH_FIRST_USER (最初のユーザー DSN をフェッチする場合)、または SQL_FETCH_FIRST_SYSTEM (最初のシステム DSN をフェッチする場合) です。  
  
 *Direction*が SQL_FETCH_FIRST に設定されている場合、その後、 *direction*をに設定して**sqldatasources ソース**を呼び出すと、ユーザーとシステムの両方の dsn が返さ SQL_FETCH_NEXT 返されます。 *Direction*が SQL_FETCH_FIRST_USER に設定されている場合、後続の**sqldatasources ソース**への呼び出しでは、*方向*がに設定され SQL_FETCH_NEXT ユーザー dsn のみが返されます。 *Direction*が SQL_FETCH_FIRST_SYSTEM に設定されている場合、後続の**sqldatasources ソース**への呼び出しでは、*方向*がに設定され SQL_FETCH_NEXT はシステム dsn のみを返します。  
  
 *ServerName*  
 Outputデータソース名を返すバッファーへのポインター。  
  
 *Servername*が NULL の場合でも、 *NameLength1Ptr*は、 *servername*が指すバッファー内で返すことができる文字の合計数 (文字データの null 終端文字を除く) を返します。  
  
 *BufferLength1*  
 代入**ServerName* バッファーの長さ (文字数)これは SQL_MAX_DSN_LENGTH より長く、null 終了文字を加えたものである必要はありません。  
  
 *NameLength1Ptr*  
 OutputServerName で返すことができる合計文字数 (null 終端文字を除く) を返すバッファーへのポインター \* *ServerName*。 戻り値として使用できる文字数が*BufferLength1*以上の場合、ServerName のデータソース名は \* *ServerName* *BufferLength1*に切り捨てられ、null 終了文字の長さを引いたものになります。  
  
 *説明*  
 Outputデータソースに関連付けられているドライバーの説明を返すバッファーへのポインター。 たとえば、dBASE や SQL Server などです。  
  
 *Description*が NULL の場合、 *NameLength2Ptr*は、*説明*に示されているバッファー内で返すことができる文字の合計数 (文字データの null 終端文字を除く) を返します。  
  
 *BufferLength2*  
 代入**Description* バッファーの長さ (文字数)。  
  
 *NameLength2Ptr*  
 Output説明で返すことができる文字の合計数 (null 終了文字を除く) を返すバッファーへのポインター \* *Description*。 戻り値として使用できる文字数が*BufferLength2*以上の場合は、[説明] に記載されているドライバーの説明 \* *Description*が、 *BufferLength2*から null 終了文字の長さを引いた値に切り捨てられます。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **Sqldatasources**が SQL_ERROR または SQL_SUCCESS_WITH_INFO のいずれかを返す場合、関連付けられた SQLSTATE 値を取得するには、 *Handletype* SQL_HANDLE_ENV と*EnvironmentHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出します。 次の表に、 **Sqldatasources ソース** によって通常返される SQLSTATE 値の一覧を示し、この関数のコンテキストでそれぞれについて説明します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|(DM) Driver Manager 固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データ、右側が切り捨てられました|(DM) バッファー \* *ServerName*は、完全なデータソース名を返すのに十分な大きさではありませんでした。 そのため、名前が切り詰められました。 データソース名全体の長さは、NameLength1Ptr で返され \* *NameLength1Ptr*ます。 (関数は SQL_SUCCESS_WITH_INFO を返します)。<br /><br /> (DM) バッファーの \* *説明*が完全なドライバーの説明を返すのに十分な大きさではありませんでした。 このため、説明は切り捨てられました。 切り捨てられていないデータソースの説明の長さは、**NameLength2Ptr*で返されます。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|HY000|一般的なエラー|(DM) 特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * \* Messagetext*バッファーの**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|(DM) ドライバーマネージャーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY010|関数のシーケンスエラー|(DM) **Sqlexecute**、 **SQLExecDirect**、または **Sqlmoreresults** が *StatementHandle* に対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY090|文字列またはバッファーの長さが無効です|(DM) 引数 *BufferLength1* に指定された値が0未満でした。<br /><br /> (DM) 引数 *BufferLength2* に指定された値が0未満でした。|  
|HY103|無効な取得コード|(DM) 引数の *方向* に指定された値が、SQL_FETCH_FIRST、SQL_FETCH_FIRST_USER、SQL_FETCH_FIRST_SYSTEM、または SQL_FETCH_NEXT と等しくありません。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
  
## <a name="comments"></a>コメント  
 **Sqldatasources ソース**は driver Manager に実装されているため、特定のドライバーの標準に準拠しているかどうかに関係なく、すべてのドライバーでサポートされます。  
  
 アプリケーションで **sqldatasources** ソースを複数回呼び出して、すべてのデータソース名を取得できます。 ドライバーマネージャーは、この情報をシステム情報から取得します。 データソース名が存在しない場合、ドライバーマネージャーは SQL_NO_DATA を返します。 **Sqldatasources**ソースが SQL_NO_DATA を返した直後に SQL_FETCH_NEXT で呼び出された場合は、最初のデータソース名が返されます。 アプリケーションが **Sqldatasources**ソースによって返された情報を使用する方法については、「 [データソースまたはドライバーの選択](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)」を参照してください。  
  
 SQL_FETCH_NEXT が初めて呼び出されたときに **Sqldatasources** ソースに渡されると、最初のデータソース名が返されます。  
  
 ドライバーは、データソース名を実際のデータソースにマップする方法を決定します。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|データソースへの接続に必要な値を検出して一覧表示する|[SQLBrowseConnect 関数](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|データ ソースに接続する|[SQLConnect 関数](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|接続文字列またはダイアログボックスを使用したデータソースへの接続|[SQLDriverConnect 関数](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|ドライバーの説明と属性を返す|[SQLDrivers 関数](../../../odbc/reference/syntax/sqldrivers-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
