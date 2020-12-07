---
description: SQLGetDiagField 関数
title: SQLGetDiagField 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDiagField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDiagField
helpviewer_keywords:
- SQLGetDiagField function [ODBC]
ms.assetid: 1dbc4398-97a8-4585-bb77-1f7ea75e24c4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 92043f5deb505d60ebe168a9c219c4d37a304ed5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461027"
---
# <a name="sqlgetdiagfield-function"></a>SQLGetDiagField 関数

**互換性**  
 導入されたバージョン: ODBC 3.0 標準準拠: ISO 92  
  
 **まとめ**  
 **SQLGetDiagField** は、エラー、警告、および状態の情報を含む診断データ構造 (指定されたハンドルに関連付けられている) のレコードの現在の値を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp

SQLRETURN SQLGetDiagField(  
     SQLSMALLINT     HandleType,  
     SQLHANDLE       Handle,  
     SQLSMALLINT     RecNumber,  
     SQLSMALLINT     DiagIdentifier,  
     SQLPOINTER      DiagInfoPtr,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLengthPtr);  
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
 代入アプリケーションが情報を検索するときに使用するステータスレコードを示します。 ステータスレコードには1から番号が付けられます。 *DiagIdentifier*引数が診断ヘッダーのフィールドを示している場合、 *recnumber*は無視されます。 そうでない場合は、0よりも大きくする必要があります。  
  
 *DiagIdentifier*  
 代入値が返される診断のフィールドを示します。 詳細については、「コメント」の「*DiagIdentifier* 引数」セクションを参照してください。  
  
 *DiagInfoPtr*  
 Output診断情報を返すバッファーへのポインター。 データ型は、 *DiagIdentifier*の値によって異なります。 *DiagInfoPtr*が整数型の場合、アプリケーションは SQLULEN のバッファーを使用し、この関数を呼び出す前に値を0に初期化する必要があります。一部のドライバーでは、バッファーの下位の32ビットまたは16ビットのみが書き込まれ、上位ビットは変更されないためです。  
  
 *DiagInfoPtr*が NULL の場合でも、 *stringlength Ptr*は、 *DiagInfoPtr*によってポイントされたバッファー内で返すことができる合計バイト数 (文字データの場合は、NULL 終端文字を除く) を返します。  
  
 *BufferLength*  
 代入*DiagIdentifier*が ODBC で定義された診断で、 *DiagInfoPtr*が文字列またはバイナリバッファーを指している場合、この引数は DiagInfoPtr の長さである必要があり \* *DiagInfoPtr*ます。 *DiagIdentifier*が ODBC で定義されたフィールドで、 \* *DiagInfoPtr*が整数である場合、 *bufferlength*は無視されます。 * \* DiagInfoPtr*の値が Unicode 文字列の場合 ( **SQLGetDiagFieldW**を呼び出した場合)、 *bufferlength*引数は偶数である必要があります。  
  
 *DiagIdentifier*がドライバーによって定義されたフィールドである場合、アプリケーションは、 *bufferlength*引数を設定することによって、ドライバーマネージャーに対してフィールドの性質を示します。 *Bufferlength* には次の値を指定できます。  
  
-   *DiagInfoPtr*が文字列へのポインターである場合、 *bufferlength*は文字列または SQL_NTS の長さを示します。  
  
-   *DiagInfoPtr*がバイナリバッファーへのポインターである場合、アプリケーションは*bufferlength*に SQL_LEN_BINARY_ATTR (*長さ*) マクロの結果を格納します。 これにより、 *Bufferlength*に負の値が挿入されます。  
  
-   *DiagInfoPtr*が文字列またはバイナリ文字列以外の値へのポインターである場合、 *bufferlength*には SQL_IS_POINTER 値を指定する必要があります。  
  
-   * \* DiagInfoPtr*に固定長データ型が含まれている場合は、必要に応じて、 *bufferlength*が SQL_IS_INTEGER、SQL_IS_UINTEGER、SQL_IS_SMALLINT、または SQL_IS_USMALLINT になります。  
  
 *Stringlength Ptr*  
 Output\*文字データに対して*DiagInfoPtr*で返すことができるバイト数の合計 (null 終端文字に必要なバイト数を除く) を返すバッファーへのポインター。 返すことのできるバイト数が*Bufferlength*以上の場合、DiagInfoPtr 内のテキストは \* *DiagInfoPtr* *bufferlength*に切り捨てられ、null 終端文字の長さを超えます。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE、または SQL_NO_DATA。  
  
## <a name="diagnostics"></a>診断  
 **SQLGetDiagField** は自身の診断レコードを通知しません。 次の戻り値を使用して、独自の実行結果を報告します。  
  
-   SQL_SUCCESS: 関数は正常に診断情報を返しました。  
  
-   SQL_SUCCESS_WITH_INFO: \* *DiagInfoPtr*が小さすぎて、要求された診断フィールドを保持できませんでした。 そのため、診断フィールドのデータが切り捨てられました。 切り捨てが発生したことを確認するには、アプリケーションで *Bufferlength* と実際に使用可能なバイト数を比較する必要があります。これは **stringlength ptr*に書き込まれます。  
  
-   SQL_INVALID_HANDLE: *Handletype* と *handle* によって示されたハンドルが有効なハンドルではありませんでした。  
  
-   SQL_ERROR: 次のいずれかが発生しました。  
  
    -   *DiagIdentifier* 引数が有効な値ではありませんでした。  
  
    -   *DiagIdentifier* 引数が SQL_DIAG_CURSOR_ROW_COUNT、SQL_DIAG_DYNAMIC_FUNCTION、SQL_DIAG_DYNAMIC_FUNCTION_CODE、または SQL_DIAG_ROW_COUNT ですが、 *Handle* がステートメントハンドルではありませんでした。 (ドライバーマネージャーはこの診断を返します)。  
  
    -   *DiagIdentifier*が診断レコードのフィールドを指定した場合 *、recnumber*引数は負の値または0でした。 ヘッダーフィールドでは、 *Recnumber*は無視されます。  
  
    -   要求された値は文字列であり、 *Bufferlength* が0未満でした。  
  
    -   非同期通知を使用すると、ハンドルの非同期操作が完了しませんでした。  
  
-   SQL_NO_DATA: *recnumber* が、handle に指定されたハンドルに存在する診断レコードの数を超えてい *ます。* また、*ハンドル*の診断レコードが存在しない場合は、正の*値*に対しても SQL_NO_DATA が返されます。  
  
## <a name="comments"></a>コメント  
 アプリケーションは通常、次の3つの目標のいずれかを達成するために **SQLGetDiagField** を呼び出します。  
  
1.  関数呼び出しが返されたときに特定のエラーまたは警告情報を取得するには SQL_ERROR または SQL_SUCCESS_WITH_INFO ( **SQLBrowseConnect** 関数の場合は SQL_NEED_DATA) を返します。  
  
2.  挿入、削除、または更新操作が **Sqlexecute**、 **SQLExecDirect**、 **Sqlbulkoperations**、または **SQLSetPos** (SQL_DIAG_ROW_COUNT ヘッダーフィールドから) を呼び出して実行されたときに影響を受けたデータソース内の行の数を特定するには、ドライバーがこの情報を提供できる場合は (SQL_DIAG_CURSOR_ROW_COUNT ヘッダーフィールドから)、  
  
3.  **SQLExecDirect**または**sqlexecute** (SQL_DIAG_DYNAMIC_FUNCTION と SQL_DIAG_DYNAMIC_FUNCTION_CODE のヘッダーフィールドから) の呼び出しによって実行された関数を確認するには  
  
 ODBC 関数は、呼び出されるたびに0個以上の診断レコードをポストできます。そのため、任意の ODBC 関数呼び出しの後で、アプリケーションから **SQLGetDiagField** を呼び出すことができます。 一度に保存できる診断レコードの数に制限はありません。 **SQLGetDiagField** は、 *Handle* 引数で指定された診断データ構造に最後に関連付けられた診断情報のみを取得します。 アプリケーションが **SQLGetDiagField** または **SQLGETDIAGREC**以外の ODBC 関数を呼び出す場合、同じハンドルを使用した前回の呼び出しの診断情報は失われます。  
  
 アプリケーションでは、 **SQLGetDiagField**が SQL_SUCCESS を返す限り、 *recnumber*を増やすことですべての診断レコードをスキャンできます。 状態レコードの数は、SQL_DIAG_NUMBER ヘッダーフィールドに示されます。 **SQLGetDiagField**への呼び出しは、ヘッダーフィールドとレコードフィールドに対して非破壊です。 アプリケーションでは、診断関数以外の関数が中間で呼び出されていない限り、後で **SQLGetDiagField** を呼び出してレコードからフィールドを取得することができます。この場合、レコードは同じハンドルにポストされます。  
  
 アプリケーションでは、 **SQLGetDiagField** を呼び出して、任意の時点で任意の診断フィールドを返すことができます。ただし、 *ハンドル* がステートメントハンドルでない場合は SQL_ERROR が返される SQL_DIAG_CURSOR_ROW_COUNT や SQL_DIAG_ROW_COUNT は除きます。 他の診断フィールドが定義されていない場合、 **SQLGetDiagField** を呼び出すと (他の診断が検出されない場合) SQL_SUCCESS が返され、そのフィールドに対して未定義の値が返されます。  
  
 詳細については、「 [SQLGetDiagRec と SQLGetDiagField の使用](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) 」および「 [SQLGetDiagRec と SQLGetDiagField の実装](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)」を参照してください。  
  
 非同期に実行されている API 以外の API を呼び出すと、HY010 "関数シーケンスエラー" が生成されます。 ただし、非同期操作が完了する前にエラーレコードを取得することはできません。  
  
## <a name="handletype-argument"></a>HandleType 引数  
 各ハンドルの種類には、関連付けられた診断情報を含めることができます。 *Handletype*引数は*ハンドルのハンドル型を示し*ます。  
  
 環境、接続、ステートメント、記述子ハンドルに対して、一部のヘッダーフィールドとレコードフィールドを返すことはできません。 フィールドが適用されないハンドルは、次の「ヘッダーフィールド」セクションと「レコードフィールド」セクションで示されています。  
  
 *Handletype*が SQL_HANDLE_ENV の場合、*ハンドル*は、共有または非共有の環境ハンドルのいずれかになります。  
  
 ドライバー固有のヘッダー診断フィールドを環境ハンドルに関連付けることはできません。  
  
 記述子ハンドルに対して定義されている診断ヘッダーフィールドは、SQL_DIAG_NUMBER と SQL_DIAG_RETURNCODE のみです。  
  
## <a name="diagidentifier-argument"></a>DiagIdentifier 引数  
 この引数は、診断データ構造に必要なフィールドの識別子を示します。 *Recnumber*が1以上の場合、フィールドのデータは、関数によって返される診断情報を示します。 *Recnumber*が0の場合、フィールドは診断データ構造のヘッダーに含まれるため、特定の情報ではなく、診断情報を返した関数呼び出しに関連するデータが含まれます。  
  
 ドライバーでは、ドライバー固有のヘッダーフィールドとレコードフィールドを診断データ構造に定義できます。  
  
 Odbc*2.x アプリケーションは*、odbc*2.x ドライバーを*操作するときに、SQL_DIAG_CLASS_ORIGIN、SQL_DIAG_CLASS_SUBCLASS_ORIGIN、SQL_DIAG_CONNECTION_NAME、SQL_DIAG_MESSAGE_TEXT、SQL_DIAG_NATIVE、SQL_DIAG_NUMBER、SQL_DIAG_RETURNCODE、SQL_DIAG_SERVER_NAME、SQL_DIAG_SQLSTATE の*DiagIdentifier*引数を使用してのみ**SQLGetDiagField**を呼び出すことができます。 その他のすべての診断フィールドは SQL_ERROR を返します。  
  
## <a name="header-fields"></a>ヘッダーフィールド  
 *DiagIdentifier*引数には、次の表に示すヘッダーフィールドを含めることができます。  
  
|DiagIdentifier|の戻り値の型 :|戻り値|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CURSOR_ROW_COUNT|SQLLEN|このフィールドには、カーソル内の行の数が含まれます。 このセマンティクスは、SQL_DYNAMIC_CURSOR_ATTRIBUTES2、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2、SQL_KEYSET_CURSOR_ATTRIBUTES2、および SQL_STATIC_CURSOR_ATTRIBUTES2 の **SQLGetInfo** 情報の種類によって異なります。これは、各カーソルの種類 (SQL_CA2_CRC_EXACT と SQL_CA2_CRC_APPROXIMATE ビット) で使用できる行数を示します。<br /><br /> このフィールドの内容は、ステートメントハンドルに対してのみ定義され、 **Sqlexecute**、 **SQLExecDirect**、または **sqlmoreresults** が呼び出された後にのみ定義されます。 ステートメントハンドル以外の SQL_DIAG_CURSOR_ROW_COUNT の*DiagIdentifier*を使用して**SQLGetDiagField**を呼び出すと、SQL_ERROR が返されます。|  
|SQL_DIAG_DYNAMIC_FUNCTION|SQLCHAR|これは、基になる関数が実行した SQL ステートメントを記述する文字列です。 (特定の値については、このセクションで後述する「動的関数フィールドの値」を参照してください)。このフィールドの内容は、ステートメントハンドルだけでは、 **Sqlexecute**、 **SQLExecDirect**、または **sqlmoreresults**の呼び出しの後にのみ定義されます。 ステートメントハンドル以外の SQL_DIAG_DYNAMIC_FUNCTION の*DiagIdentifier*を使用して**SQLGetDiagField**を呼び出すと、SQL_ERROR が返されます。 このフィールドの値は、 **Sqlexecute** または **SQLExecDirect**の呼び出しの前に定義されていません。|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|SQLINTEGER|これは、基になる関数によって実行された SQL ステートメントを記述する数値コードです。 (特定の値については、このセクションで後述する「動的関数フィールドの値」を参照してください)。このフィールドの内容は、ステートメントハンドルだけでは、 **Sqlexecute**、 **SQLExecDirect**、または **sqlmoreresults**の呼び出しの後にのみ定義されます。 ステートメントハンドル以外の SQL_DIAG_DYNAMIC_FUNCTION_CODE の*DiagIdentifier*を使用して**SQLGetDiagField**を呼び出すと、SQL_ERROR が返されます。 このフィールドの値は、 **Sqlexecute** または **SQLExecDirect**の呼び出しの前に定義されていません。|  
|SQL_DIAG_NUMBER|SQLINTEGER|指定されたハンドルで使用可能な状態レコードの数。|  
|SQL_DIAG_RETURNCODE|SQLRETURN|関数によって返されるコードを返します。 リターンコードの一覧については、「 [リターンコード](../../../odbc/reference/develop-app/return-codes-odbc.md)」を参照してください。 ドライバーは SQL_DIAG_RETURNCODE を実装する必要はありません。これは常にドライバーマネージャーによって実装されます。 *ハンドル*で関数がまだ呼び出されていない場合は、SQL_DIAG_RETURNCODE に対して SQL_SUCCESS が返されます。|  
|SQL_DIAG_ROW_COUNT|SQLLEN|**Sqlexecute**、 **SQLExecDirect**、 **Sqlbulkoperations**、または**SQLSetPos**によって実行される挿入、削除、または更新の影響を受ける行の数。 これは、 *カーソル指定* が実行された後のドライバーによって定義されます。 このフィールドの内容は、ステートメントハンドルに対してのみ定義されます。 ステートメントハンドル以外の SQL_DIAG_ROW_COUNT の*DiagIdentifier*を使用して**SQLGetDiagField**を呼び出すと、SQL_ERROR が返されます。 このフィールドのデータは、 **SQLRowCount**の*rowcountptr*引数でも返されます。 このフィールドのデータは、非診断関数呼び出しが行われるたびにリセットされます。一方、 **SQLRowCount** によって返される行数は、ステートメントが準備済みまたは割り当て済みの状態に戻るまで同じままです。|  
  
## <a name="record-fields"></a>レコードフィールド  
 次の表に示すレコードフィールドは、 *DiagIdentifier* 引数に含めることができます。  
  
|DiagIdentifier|の戻り値の型 :|戻り値|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CLASS_ORIGIN|SQLCHAR|このレコードの SQLSTATE 値のクラス部分を定義するドキュメントを示す文字列。 Open Group と ISO 呼び出しレベルのインターフェイスで定義されているすべての SQLSTATEs の値は "ISO 9075" です。 ODBC 固有の SQLSTATEs (SQLSTATE クラスが "IM" であるすべてのもの) の場合、その値は "ODBC 3.0" です。|  
|SQL_DIAG_COLUMN_NUMBER|SQLINTEGER|SQL_DIAG_ROW_NUMBER フィールドが行セット内の有効な行番号または一連のパラメーターである場合、このフィールドには、結果セットの列番号を表す値、またはパラメーターのセットのパラメーター番号が格納されます。 結果セットの列番号は常に1から始まります。この状態レコードがブックマーク列に関連している場合は、フィールドを0にすることができます。 パラメーター番号は1から始まります。 状態レコードが列番号またはパラメーター番号に関連付けられていない場合は、SQL_NO_COLUMN_NUMBER 値が使用されます。 このレコードが関連付けられている列番号またはパラメーター番号をドライバーが特定できない場合、このフィールドには SQL_COLUMN_NUMBER_UNKNOWN 値が割り当てられます。<br /><br /> このフィールドの内容は、ステートメントハンドルに対してのみ定義されます。|  
|SQL_DIAG_CONNECTION_NAME|SQLCHAR|診断レコードが関連付けられている接続の名前を示す文字列。 このフィールドはドライバーで定義されています。 環境ハンドルに関連付けられている診断データ構造と、接続に関係のない診断の場合、このフィールドは長さが0の文字列になります。|  
|SQL_DIAG_MESSAGE_TEXT|SQLCHAR|エラーまたは警告に関する情報メッセージ。 このフィールドは、「 [診断メッセージ](../../../odbc/reference/develop-app/diagnostic-messages.md)」で説明されているように書式設定されます。 診断メッセージテキストの最大長はありません。|  
|SQL_DIAG_NATIVE|SQLINTEGER|ドライバー/データソース固有のネイティブエラーコード。 ネイティブエラーコードがない場合、ドライバーは0を返します。|  
|SQL_DIAG_ROW_NUMBER|SQLLEN|このフィールドには、行セット内の行番号、または状態レコードが関連付けられているパラメーターのセットのパラメーター番号が格納されます。 行番号とパラメーター番号は1から始まります。 この状態レコードが行番号またはパラメーター番号に関連付けられていない場合、このフィールドには SQL_NO_ROW_NUMBER 値が含まれます。 このレコードが関連付けられている行番号またはパラメーター番号をドライバーが特定できない場合、このフィールドには SQL_ROW_NUMBER_UNKNOWN 値が割り当てられます。<br /><br /> このフィールドの内容は、ステートメントハンドルに対してのみ定義されます。|  
|SQL_DIAG_SERVER_NAME|SQLCHAR|診断レコードが関連付けられているサーバー名を示す文字列。 これは、SQL_DATA_SOURCE_NAME オプションを指定して **SQLGetInfo** を呼び出す場合に返される値と同じです。 環境ハンドルに関連付けられている診断データ構造と、どのサーバーにも関係のない診断の場合、このフィールドは長さが0の文字列になります。|  
|SQL_DIAG_SQLSTATE|SQLCHAR|5文字の SQLSTATE 診断コード。 詳細については、「 [Sqlstates](../../../odbc/reference/develop-app/sqlstates.md)」を参照してください。|  
|SQL_DIAG_SUBCLASS_ORIGIN|SQLCHAR|SQLSTATE コードのサブクラス部分の定義部分を識別する、SQL_DIAG_CLASS_ORIGIN と同じ形式および有効な値を持つ文字列。 "ODBC 3.0" が返される ODBC 固有の SQLSTATES には、次のようなものがあります。<br /><br /> 01S00、01S01、01S02、01S06、01S07、07S01、08S01、21S01、21S02、25S01、25S02、25S03、42 S01、42 S02、42 S11、42 S12、42 S21、42 S22、HY095、HY097、HY098、HY099、HY100、HY101、HY105、HY107、HY109、HY110、HY111、HYT00、HYT01、IM001、IM002、IM003、IM004、IM005、IM006、IM007、IM008、IM010、IM011、IM012。|  
  
## <a name="values-of-the-dynamic-function-fields"></a>動的関数のフィールドの値  
 次の表では、 **Sqlexecute** または **SQLExecDirect**の呼び出しによって実行される SQL ステートメントの各種類に適用される SQL_DIAG_DYNAMIC_FUNCTION および SQL_DIAG_DYNAMIC_FUNCTION_CODE の値について説明します。 ドライバーでは、ドライバーによって定義された値を一覧に追加できます。  
  
|SQL ステートメント<br /><br /> れる| の値<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION| の値<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION_CODE|  
|--------------------------------|-----------------------------------------------|-----------------------------------------------------|  
|*alter-domain-ステートメント*|"ALTER DOMAIN"|SQL_DIAG_ALTER_DOMAIN|  
|*alter-table-ステートメント*|"ALTER TABLE"|SQL_DIAG_ALTER_TABLE|  
|*アサーション-定義*|"アサーションの作成"|SQL_DIAG_CREATE_ASSERTION|  
|*文字セットの定義*|"文字セットの作成"|SQL_DIAG_CREATE_CHARACTER_SET|  
|*照合順序-定義*|"照合順序の作成"|SQL_DIAG_CREATE_COLLATION|  
|*domainn-定義*|"ドメインの作成"|SQL_DIAG_CREATE_DOMAIN|
|*create-index-ステートメント*|"インデックスの作成"|SQL_DIAG_CREATE_INDEX|  
|*create-table-ステートメント*|"CREATE TABLE"|SQL_DIAG_CREATE_TABLE|  
|*create-view-ステートメント*|"ビューの作成"|SQL_DIAG_CREATE_VIEW|  
|*カーソル-指定*|"カーソルの選択"|SQL_DIAG_SELECT_CURSOR|  
|*delete ステートメントの位置指定*|"動的な DELETE カーソル"|SQL_DIAG_DYNAMIC_DELETE_CURSOR|  
|*delete ステートメント-検索*|"DELETE WHERE"|SQL_DIAG_DELETE_WHERE|  
|*drop-assertion ステートメント*|"DROP ASSERTION"|SQL_DIAG_DROP_ASSERTION|  
|*drop 文字セット-stmt*|"ドロップ文字セット"|SQL_DIAG_DROP_CHARACTER_SET|  
|*drop-collation ステートメント*|"DROP COLLATION"|SQL_DIAG_DROP_COLLATION|  
|*drop-ドメインステートメント*|"DROP DOMAIN"|SQL_DIAG_DROP_DOMAIN|  
|*drop-index-ステートメント*|"DROP INDEX"|SQL_DIAG_DROP_INDEX|  
|*drop-schema ステートメント*|"DROP SCHEMA"|SQL_DIAG_DROP_SCHEMA|  
|*drop-table-ステートメント*|"DROP TABLE"|SQL_DIAG_DROP_TABLE|  
|*drop-translation-ステートメント*|"DROP TRANSLATION"|SQL_DIAG_DROP_TRANSLATION|  
|*drop-view-ステートメント*|"ドロップビュー"|SQL_DIAG_DROP_VIEW|  
|*grantstatement*|許諾|SQL_DIAG_GRANT|
|*insert ステートメント*|INSERT|SQL_DIAG_INSERT|  
|*ODBC-プロシージャ-拡張機能*|発信|SQL_DIAG_ の呼び出し|  
|*revoke ステートメント*|B|SQL_DIAG_REVOKE|  
|*スキーマ定義*|"スキーマの作成"|SQL_DIAG_CREATE_SCHEMA|  
|*translation-定義*|"翻訳の作成"|SQL_DIAG_CREATE_TRANSLATION|  
|*update ステートメント-位置指定*|"動的な更新カーソル"|SQL_DIAG_DYNAMIC_UPDATE_CURSOR|  
|*update ステートメント-検索*|"WHERE WHERE"|SQL_DIAG_UPDATE_WHERE|  
|Unknown|*空の文字列*|SQL_DIAG_UNKNOWN_STATEMENT|  

<!--
These two malformed table rows were fixed by educated GUESS only.
Each pair starts with the original flawed row.
Flawed because treated as only two cells by HTML render,
and because missing info anyway.
Also, these flawed rows lacked '|' as their first nonWhitespace character (although markdown technically allows this omission, unfortunately).
Arguably the following SQL.H file shows the sequence of the flawed rows in the table was suboptimal also.

ftp://www.fpc.org/fpc32/VS6Disk1/VC98/INCLUDE/SQL.H

GeneMi , 2019/01/19
- - - - - - - - - - - - - -

n-definition*|"CREATE DOMAIN"|SQL_DIAG_CREATE_DOMAIN|  

|*domain-definition*|"CREATE DOMAIN"|SQL_DIAG_CREATE_DOMAIN|

-statement*|"GRANT"|SQL_DIAG_GRANT|  

|*grant-statement*|"GRANT"|SQL_DIAG_GRANT|

-->

## <a name="sequence-of-status-records"></a>状態レコードのシーケンス

 状態レコードは、行番号と診断の種類に基づいてシーケンスに配置されます。 ドライバーマネージャーは、生成された状態レコードを返す最終的な順序を決定します。 ドライバーは、生成された状態レコードを返す最終的な順序を決定します。  
  
 診断レコードがドライバーマネージャーとドライバーの両方によって送信されている場合は、ドライバーマネージャーによってそれらの順序が決定されます。  
  
 複数の状態レコードがある場合は、レコードのシーケンスが最初に行番号によって決定されます。 次の規則は、一連の診断レコードを行ごとに決定する場合に適用されます。  
  
-   行に対応していないレコードは、特定の行に対応するレコードの前に表示されます。これは SQL_NO_ROW_NUMBER が-1 に定義されているためです。  
  
-   SQL_ROW_NUMBER_UNKNOWN が-2 に定義されているため、行番号が不明なレコードは、他のすべてのレコードの前に表示されます。  
  
-   特定の行に関連するすべてのレコードについて、レコードは SQL_DIAG_ROW_NUMBER フィールドの値によって並べ替えられます。 影響を受けた最初の行のすべてのエラーと警告が表示され、その後、影響を受けた次の行のすべてのエラーと警告が表示されます。  
  
> [!NOTE]
>  Odbc*2.x ドライバーマネージャー*は、sqlstate 01S01 (行のエラー) が odbc*2.x ドライバーに*よって返された場合、または**SQLExtendedFetch**が呼び出されたとき、または**SQLExtendedFetch**が配置されているカーソルで**SQLSetPos**が呼び出された場合に、診断キューの状態レコードを注文しませ*ん。*  
  
 各行内、または行番号が不明なすべてのレコード、または行番号が SQL_NO_ROW_NUMBER であるすべてのレコードについては、一覧表示された最初のレコードが並べ替え規則のセットを使用して決定されます。 最初のレコードの後に、行に影響を与える他のレコードの順序は定義されていません。 アプリケーションでは、最初のレコードの後に、エラーが警告の前にあると想定できません。 アプリケーションは、完全な診断データ構造をスキャンして、関数への失敗した呼び出しに関する完全な情報を取得する必要があります。  
  
 次の規則は、行内の最初のレコードを決定するために使用されます。 ランクが最も高いレコードが最初のレコードになります。 レコードの順位付け時には、レコードのソース (ドライバーマネージャー、ドライバー、ゲートウェイなど) は考慮されません。  
  
-   **エラー** エラーを説明する状態レコードのランクが最も高くなります。 並べ替えエラーには、次の規則が適用されます。  
  
    -   トランザクションエラーまたは可能性のあるトランザクションエラーを示すレコードは、他のすべてのレコードを処理します。  
  
    -   2つ以上のレコードが同じエラー条件を記述している場合、Open Group CLI 仕様 (クラス 03 ~ HZ) によって SQLSTATEs が定義されます。  
  
-   **実装で定義されたデータ値がありません** ドライバーで定義されたデータ値がないことを示す状態レコード (クラス 02) には、2番目に高いランクが付けられます。  
  
-   **警告** 警告 (クラス 01) を説明する状態レコードのランクは最も低くなります。 2つ以上のレコードが同じ警告条件を記述している場合、Open Group CLI 仕様で定義されている警告 SQLSTATEs は、ODBC 定義の sqlstates とドライバーで定義された SQLSTATEs を指定します。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|診断データ構造の複数のフィールドの取得|[SQLGetDiagRec 関数](sqlgetdiagrec-function.md)|  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
