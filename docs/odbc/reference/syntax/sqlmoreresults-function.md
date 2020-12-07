---
description: SQLMoreResults 関数
title: SQLMoreResults 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLMoreResults
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLMoreResults
helpviewer_keywords:
- SQLMoreResults function [ODBC]
ms.assetid: bf169ed5-4d55-412c-b184-12065a726e89
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4a23d806c1367636bc92a4a36b271d8d231070a7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428934"
---
# <a name="sqlmoreresults-function"></a>SQLMoreResults 関数
**互換性**  
 導入されたバージョン: ODBC 1.0 標準準拠: ODBC  
  
 **まとめ**  
 **Sqlmoreresults** は、 **select**、 **UPDATE**、 **INSERT**、または **DELETE** ステートメントを含むステートメントでより多くの結果が得られるかどうかを判断し、存在する場合は、それらの結果の処理を初期化します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLMoreResults(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_NO_DATA、SQL_ERROR、SQL_INVALID_HANDLE、SQL_PARAM_DATA_AVAILABLE。  
  
## <a name="diagnostics"></a>診断  
 **Sqlmoreresults**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合、関連付けられた SQLSTATE 値を取得するには、 *handletype*を SQL_HANDLE_STMT、 *StatementHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出します。 次の表は、 **Sqlmoreresults** によって一般的に返される SQLSTATE 値の一覧を示しています。この関数のコンテキストでは、それぞれについて説明しています。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01S02|オプションの値が変更されました|バッチ処理中に、ステートメント属性の値が変更されました。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続されていたデータソースとの間の通信リンクが失敗しました。|  
|40001|シリアル化エラー|リソースが別のトランザクションでデッドロックしているため、トランザクションがロールバックされました。|  
|40003|ステートメントの完了が不明です|この関数の実行中に関連付けられた接続が失敗したため、トランザクションの状態を確認できません。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * \* Messagetext*バッファーの**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|*StatementHandle*に対して非同期処理が有効になりました。 **Sqlmoreresults**関数が呼び出され、実行が完了する前に、 **SQLCancel**または**sqlcancelhandle**が*StatementHandle*で呼び出されました。 その後、 *StatementHandle*で**Sqlmoreresults**関数が再度呼び出されました。<br /><br /> **Sqlmoreresults**関数が呼び出され、実行が完了する前に、マルチスレッドアプリケーションの別のスレッドの*StatementHandle*で**SQLCancel**または**sqlcancelhandle**が呼び出されました。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、 **Sqlmoreresults** 関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) 非同期的に実行されている関数 (この1つではない) が *StatementHandle* に対して呼び出され、この関数が呼び出されたときにまだ実行されています。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **Sqlbulkoperations**、 **SQLSetPos** が *StatementHandle* に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle* に関連付けられているドライバーでは、関数はサポートされていません。|  
|IM017|非同期通知モードでは、ポーリングは無効になっています|通知モデルが使用されるたびに、ポーリングは無効になります。|  
|IM018|**Sqlcompleteasync** は、このハンドルで前の非同期操作を完了するために呼び出されていません。|ハンドルに対する前の関数呼び出しが SQL_STILL_EXECUTING を返し、通知モードが有効になっている場合は、処理を完了するために、ハンドルに対して **Sqlcompleteasync** を呼び出す必要があります。|  
  
## <a name="comments"></a>コメント  
 **SELECT** ステートメントは結果セットを返します。 **UPDATE**、 **INSERT**、および **DELETE** ステートメントは、影響を受ける行の数を返します。 これらのステートメントのいずれかがバッチ処理されている場合、パラメーターの配列 (パラメーターの順序の昇順で番号が付けられているか、バッチに出現する順序で番号が付けられます) またはプロシージャで、複数の結果セットまたは行数を返すことができます。 ステートメントとパラメーターの配列のバッチについては、「SQL ステートメントと[パラメーター値の配列](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)[のバッチ](../../../odbc/reference/develop-app/batches-of-sql-statements.md)」を参照してください。  
  
 バッチを実行すると、アプリケーションは最初の結果セットに配置されます。 アプリケーションでは、1つの結果セットだけがある場合と同じように、最初または後続の結果セットで **SQLBindCol**、 **sqlbulkoperations**、 **sqlfetch**、 **SQLGetData**、 **sqlbulkoperations**、 **SQLSetPos**、およびすべてのメタデータ関数を呼び出すことができます。 最初の結果セットが完成すると、アプリケーションは **Sqlmoreresults** を呼び出して次の結果セットに移動します。 別の結果セットまたはカウントが使用可能な場合、 **Sqlmoreresults** は SQL_SUCCESS を返し、結果セットまたは追加処理のカウントを初期化します。 行カウント生成ステートメントが、結果セット生成ステートメントの間に出現する場合は、 **Sqlmoreresults**を呼び出すことによってステップオーバーできます。**UPDATE**、 **INSERT**、または**DELETE**ステートメントに対して**sqlmoreresults**を呼び出した後、アプリケーションは**SQLRowCount**を呼び出すことができます。  
  
 フェッチされた行のない現在の結果セットがある場合、 **Sqlmoreresults** はその結果セットを破棄し、次の結果セットまたはカウントを使用できるようにします。 すべての結果が処理されている場合は、 **Sqlmoreresults** によって SQL_NO_DATA が返されます。 一部のドライバーでは、すべての結果セットと行カウントが処理されるまで、出力パラメーターと戻り値は使用できません。 このようなドライバーでは、 **Sqlmoreresults** が SQL_NO_DATA を返すと、出力パラメーターと戻り値が使用できるようになります。  
  
 以前の結果セットに対して確立されたバインドは引き続き有効です。 列構造がこの結果セットと異なる場合は、 **Sqlfetch** または **sqlfetchscroll** を呼び出すと、エラーまたは切り捨てが発生する可能性があります。 これを回避するには、アプリケーションは **SQLBindCol** を呼び出して、必要に応じて明示的に再バインドする必要があります (または、記述子フィールドを設定します)。 また、アプリケーションは SQL_UNBIND の*オプション*を使用して**SQLFreeStmt**を呼び出し、すべての列バッファーのバインドを解除することもできます。  
  
 カーソルの種類、カーソルの同時実行、キーセットのサイズ、最大長などのステートメント属性の値は、アプリケーションが **Sqlmoreresults**を呼び出してバッチを移動するときに変更される可能性があります。 この場合、 **Sqlmoreresults** は SQL_SUCCESS_WITH_INFO と SQLSTATE 01S02 (オプション値が変更されました) を返します。  
  
 SQL_CLOSE の*オプション***を指定して** **sqlcloを**呼び出すと、バッチの実行結果として使用可能だったすべての結果セットと行数が破棄されます。 ステートメントハンドルは、割り当てられた状態または準備された状態に戻ります。 バッチが実行され、ステートメントハンドルが実行中、カーソル位置、または非同期状態にあるときに、非同期に実行する関数をキャンセルするために **SQLCancel** を呼び出すと、キャンセル呼び出しが成功した場合に、バッチによって生成されたすべての結果セットと行数が破棄されます。 ステートメントは、準備された状態または割り当てられた状態に戻ります。  
  
 ステートメントまたはプロシージャのバッチに、 **SELECT**、 **UPDATE**、 **INSERT**、および **DELETE** ステートメントを使用する他の SQL ステートメントが混在している場合、これらのステートメントは **sqlmoreresults**に影響しません。  
  
 詳細については、「 [複数の結果](../../../odbc/reference/develop-app/multiple-results.md)」を参照してください。  
  
 ステートメントのバッチで検索された update、insert、または delete ステートメントがデータソースの行に影響を与えない場合は、 **Sqlmoreresults** は SQL_SUCCESS を返します。 これは、 **SQLExecDirect**、 **sqlexecute**、または **sqlparamdata**を使用して実行される検索 update、insert、または delete ステートメントの場合とは異なり、データソースの行に影響を与えない場合は SQL_NO_DATA を返します。 アプリケーションが **SQLRowCount** を呼び出して、 **Sqlmoreresults** を呼び出した後に行数を取得した場合、 **SQLRowCount** は SQL_NO_DATA を返します。  
  
 結果処理関数の有効なシーケンス処理の詳細については、「 [付録 B: ODBC 状態遷移テーブル](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)」を参照してください。  
  
 SQL_PARAM_DATA_AVAILABLE およびストリーム出力パラメーターの詳細については、「 [SQLGetData を使用した出力パラメーターの取得](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)」を参照してください。  
  
## <a name="availability-of-row-counts"></a>行数の可用性  
 バッチに複数の連続した行カウント生成ステートメントが含まれている場合、これらの行カウントが1行のカウントにロールアップされる可能性があります。 たとえば、バッチに5つの insert ステートメントが含まれている場合、特定のデータソースは5つの個別の行カウントを返すことができます。 他の特定のデータソースは、5つの個別の行カウントの合計を表す行数を1つだけ返します。  
  
 バッチに結果セット生成と行数生成ステートメントの組み合わせが含まれている場合、行カウントがまったく使用できないか、または使用できない可能性があります。 行数の可用性に関するドライバーの動作は、 **SQLGetInfo**の呼び出しを通じて使用可能な SQL_BATCH_ROW_COUNT 情報の種類で列挙されます。 たとえば、バッチに **select**が含まれており、その後に2つの **INSERT**s と別の **select**が含まれているとします。 その場合、次のようなケースが考えられます。  
  
-   2つの **INSERT** ステートメントに対応する行カウントは、まったく使用できません。 **Sqlmoreresults**の最初の呼び出しでは、2番目の**SELECT**ステートメントの結果セットが配置されます。  
  
-   2つの **INSERT** ステートメントに対応する行カウントは、個別に使用できます。 ( **SQLGetInfo** を呼び出すと、SQL_BATCH_ROW_COUNT 情報型の SQL_BRC_ROLLED_UP ビットは返されません)。 **Sqlmoreresults** の最初の呼び出しでは、最初の **挿入**の行数が示されます。2回目の呼び出しでは、2番目の **insert**の行数が示されます。 **Sqlmoreresults**の3回目の呼び出しでは、2番目の**SELECT**ステートメントの結果セットが配置されます。  
  
-   2つの **挿入** に対応する行数が、1つの使用可能な行数にロールアップされます。 ( **SQLGetInfo** を呼び出すと、SQL_BATCH_ROW_COUNT 情報型の SQL_BRC_ROLLED_UP ビットが返されます)。 **Sqlmoreresults** の最初の呼び出しでは、ロールアップされた行数に移動し、2回目の **Sqlmoreresults** を呼び出すと、2番目の **SELECT**の結果セットが配置されます。  
  
 特定のドライバーでは、行の数を明示的なバッチに対してのみ使用でき、ストアドプロシージャでは使用できません。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|ステートメント処理の取り消し|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|データのブロックのフェッチまたは結果セットのスクロール|[SQLFetchScroll 関数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|1つの行またはデータのブロックを順方向専用にフェッチする|[SQLFetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|データ列の一部またはすべてをフェッチしています|[SQLGetData 関数](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダーファイル](../../../odbc/reference/install/odbc-header-files.md)   
 [SQLGetData を使用した出力パラメーターの取得](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
