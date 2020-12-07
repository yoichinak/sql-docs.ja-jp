---
description: SQLDrivers 関数
title: SQLDrivers 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDrivers
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDrivers
helpviewer_keywords:
- SQLDrivers function [ODBC]
ms.assetid: 6b5b7514-e9cb-4cfd-8b7a-ab51dfab9efa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9abe7502b7efcfba695bd58081752342504378ab
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461164"
---
# <a name="sqldrivers-function"></a>SQLDrivers 関数
**互換性**  
 導入されたバージョン: ODBC 2.0 標準準拠: ODBC  
  
 **まとめ**  
 **Sqldrivers** には、ドライバーの説明とドライバーの属性キーワードが一覧表示されます。 この関数は、ドライバーマネージャーによってのみ実装されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLDrivers(  
     SQLHENV         EnvironmentHandle,  
     SQLUSMALLINT    Direction,  
     SQLCHAR *       DriverDescription,  
     SQLSMALLINT     BufferLength1,  
     SQLSMALLINT *   DescriptionLengthPtr,  
     SQLCHAR *       DriverAttributes,  
     SQLSMALLINT     BufferLength2,  
     SQLSMALLINT *   AttributesLengthPtr);  
```  
  
## <a name="arguments"></a>引数  
 *EnvironmentHandle*  
 代入環境ハンドル。  
  
 *方向*  
 代入ドライバーマネージャーが一覧内の次のドライバーの説明をフェッチするか (SQL_FETCH_NEXT)、検索をリストの先頭から開始するか (SQL_FETCH_FIRST) を決定します。  
  
 *DriverDescription*  
 Outputドライバーの説明を返すバッファーへのポインター。  
  
 *Driverdescription*が NULL の場合でも、 *descriptionlength Ptr*は、 *driverdescription*が指すバッファーで返すことができる文字の合計数 (文字データの NULL 終端文字を除く) を返します。  
  
 *BufferLength1*  
 代入**Driverdescription* バッファーの長さ (文字数)。  
  
 *説明の長さの Ptr*  
 OutputDriverdescription で返すことができる文字の合計数 (null 終了文字を除く) を返すバッファーへのポインター \* *DriverDescription*。 戻り値として使用できる文字数が*BufferLength1*以上の場合、driverdescription のドライバーの説明 \* *DriverDescription*は*BufferLength1*に切り捨てられ、null 終了文字の長さを引いたものになります。  
  
 *DriverAttributes*  
 Outputドライバーの属性値のペアの一覧を返すバッファーへのポインター (「コメント」を参照)。  
  
 *Driverattributes*が NULL の場合でも、 *attributes length Ptr*は、 *driverattributes*が指すバッファー内で返すことができる合計バイト数 (文字データの NULL 終端文字を除く) を返します。  
  
 *BufferLength2*  
 代入\* *Driverattributes*バッファーの長さ (文字数)。 * \* Driverdescription*値が Unicode 文字列の場合 ( **sqldriversw**を呼び出すとき)、 *bufferlength*引数は偶数である必要があります。  
  
 *属性の長さの Ptr*  
 OutputDriverattributes で返すことができる合計バイト数 (null 終端バイトを除く) を返すバッファーへのポインター \* *DriverAttributes*。 返すことのできるバイト数が*BufferLength2*以上の場合、driverattributes 内の属性値のペアのリストが \* *DriverAttributes* *BufferLength2*に切り捨てられ、null 終了文字の長さを引いたものになります。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **Sqldrivers**が SQL_ERROR または SQL_SUCCESS_WITH_INFO のいずれかを返す場合、関連付けられた SQLSTATE 値を取得するには、 *handletype*を SQL_HANDLE_ENV、 *EnvironmentHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出します。 次の表に、 **Sqldrivers** によって通常返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|(DM) Driver Manager 固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データ、右側が切り捨てられました|(DM) バッファー \* *driverdescription*が完全なドライバーの説明を返すのに十分な大きさではありませんでした。 このため、説明は切り捨てられました。 完全なドライバーの説明の長さは、 \* *descriptionlength ptr*で返されます。 (関数は SQL_SUCCESS_WITH_INFO を返します)。<br /><br /> (DM) バッファー \* *Driverattributes*が、属性値のペアの完全な一覧を返すのに十分な大きさではありませんでした。 そのため、リストは切り捨てられました。 属性値のペアの切り捨てられていないリストの長さは、* 属性の長さの*ptr*で返されます。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * \* Messagetext*バッファーの**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|(DM) ドライバーマネージャーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY010|関数のシーケンスエラー|(DM) **Sqlexecute**、 **SQLExecDirect**、または **Sqlmoreresults** が *StatementHandle* に対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY090|文字列またはバッファーの長さが無効です|(DM) 引数 *BufferLength1* に指定された値が0未満でした。<br /><br /> (DM) 引数 *BufferLength2* に指定された値が0未満であるか1に等しい。|  
|HY103|無効な取得コード|(DM) 引数の *方向* に指定された値が SQL_FETCH_FIRST または SQL_FETCH_NEXT と等しくありません。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
  
## <a name="comments"></a>コメント  
 **Sqldrivers**はドライバーの説明を \* *driverdescription*バッファーに返します。 このメソッドは、ドライバーに関する追加情報を \* *driverattributes*バッファーからキーワードと値のペアの一覧として返します。 システム情報に記載されているドライバーのすべてのキーワードがすべてのドライバーに対して返されます。ただし、 **Createdsn**は、データソースの作成を要求するために使用されるものであり、省略可能です。 各ペアは null バイトで終了し、完全なリストは null バイトで終了します (つまり、2つの null バイトがリストの末尾にマークされます)。 たとえば、C 構文を使用するファイルベースのドライバーでは、次の属性の一覧が返される場合があります ("\ 0" は null 文字を表します)。  
  
```  
FileUsage=1\0FileExtns=*.dbf\0\0  
```  
  
 \* *Driverattributes*がリスト全体を保持するのに十分な大きさではない場合、リストは切り捨てられ、 **sqldrivers**は SQLSTATE 01004 (データが切り捨てられました) を返します。また、リストの長さ (最終的な null 終了バイトを除く) が **attributes length ptr*に返されます。  
  
 ドライバー属性キーワードは、ドライバーのインストール時にシステム情報から追加されます。 詳細については、「 [ODBC コンポーネントのインストール](../../../odbc/reference/install/installing-odbc-components.md)」を参照してください。  
  
 アプリケーションは **Sqldrivers** を複数回呼び出して、すべてのドライバーの説明を取得できます。 ドライバーマネージャーは、この情報をシステム情報から取得します。 ドライバーの説明がこれ以上ない場合、 **Sqldrivers** は SQL_NO_DATA を返します。 **Sqldrivers**が SQL_NO_DATA を返した直後に SQL_FETCH_NEXT で呼び出された場合は、最初のドライバーの説明が返されます。 アプリケーションが **Sqldrivers**によって返される情報を使用する方法については、「 [データソースまたはドライバーの選択](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)」を参照してください。  
  
 初回呼び出し時に **sqldrivers** に SQL_FETCH_NEXT が渡された場合、 **sqldrivers** は最初のデータソース名を返します。  
  
 **Sqldrivers**は driver Manager に実装されているため、特定のドライバーの標準に準拠しているかどうかに関係なく、すべてのドライバーでサポートされます。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|データソースへの接続に必要な値を検出して一覧表示する|[SQLBrowseConnect 関数](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|データ ソースに接続する|[SQLConnect 関数](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|データソース名を返す|[SQLDataSources 関数](../../../odbc/reference/syntax/sqldatasources-function.md)|  
|接続文字列またはダイアログボックスを使用したデータソースへの接続|[SQLDriverConnect 関数](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
