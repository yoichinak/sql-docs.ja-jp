---
description: SQLColAttribute 関数
title: SQLColAttribute 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLColAttribute
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLColAttribute
helpviewer_keywords:
- SQLColAttribute function [ODBC]
ms.assetid: 8c45c598-cb01-4789-a571-e93619a18ed9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d5cc7020300fd9099b70ed6f33716f343d47d571
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448817"
---
# <a name="sqlcolattribute-function"></a>SQLColAttribute 関数
**互換性**  
 導入されたバージョン: ODBC 3.0 標準準拠: ISO 92  
  
 **まとめ**  
 **Sqlcolattribute** は、結果セット内の列の記述子情報を返します。 記述子情報は、文字列、記述子に依存する値、または整数値として返されます。  
  
> [!NOTE]  
>  ドライバーマネージャーが ODBC 3 でこの関数をマップする方法の詳細については、「」を参照してください。*x* アプリケーションは ODBC 2 で動作しています。*x* ドライバー、「 [アプリケーションの旧バージョンとの互換性のための置換関数のマッピング](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLColAttribute (  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ColumnNumber,  
      SQLUSMALLINT    FieldIdentifier,  
      SQLPOINTER      CharacterAttributePtr,  
      SQLSMALLINT     BufferLength,  
      SQLSMALLINT *   StringLengthPtr,  
      SQLLEN *        NumericAttributePtr);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル。  
  
 *ColumnNumber*  
 代入フィールド値の取得元となる、IRD 内のレコードの番号。 この引数は、結果データの列数に対応します。列の順序は、1から順に昇順に並べ替えられます。 列は任意の順序で記述できます。  
  
 この引数には列0を指定できますが、SQL_DESC_TYPE と SQL_DESC_OCTET_LENGTH を除くすべての値は、未定義の値を返します。  
  
 *FieldIdentifier*  
 代入記述子ハンドル。 このハンドルは、IRD 内のどのフィールドを照会する必要があるかを定義します (SQL_COLUMN_TABLE_NAME など)。  
  
 *CharacterAttributePtr*  
 Outputフィールドが文字列である場合に、IRD の*Columnnumber*行の*FieldIdentifier*フィールドの値を返すバッファーへのポインターです。 それ以外の場合、フィールドは使用されません。  
  
 文字 *attributeptr* が NULL の場合でも、 *stringlength ptr* は、文字 *attributeptr*によってポイントされたバッファー内で返されるバイトの合計数 (文字データの NULL 終端文字を除く) を返します。  
  
 *BufferLength*  
 代入*FieldIdentifier*が ODBC で定義されたフィールドであり、文字*attributeptr*が文字列またはバイナリバッファーを指している場合、この引数は文字 attributeptr の長さである必要があり \* *CharacterAttributePtr*ます。 *FieldIdentifier*が ODBC で定義されたフィールドであり、文字 \* *属性*Ptr が整数である場合、このフィールドは無視されます。 文字* \* Attributeptr*が Unicode 文字列の場合 ( **sqlcolattributew**を呼び出すとき)、 *bufferlength*引数は偶数である必要があります。 *FieldIdentifier*がドライバーによって定義されたフィールドである場合、アプリケーションは、 *bufferlength*引数を設定することによって、ドライバーマネージャーに対してフィールドの性質を示します。 *Bufferlength* には次の値を指定できます。  
  
-   文字 *Attributeptr* がポインターへのポインターである場合、 *bufferlength* には SQL_IS_POINTER 値を指定する必要があります。  
  
-   文字 *Attributeptr* が文字列へのポインターである場合、 *bufferlength* はバッファーの長さです。  
  
-   文字 *Attributeptr* がバイナリバッファーへのポインターである場合、アプリケーションは、SQL_LEN_BINARY_ATTR (*長さ*) マクロの結果を *bufferlength*に配置します。 これにより、 *Bufferlength*に負の値が挿入されます。  
  
-   文字 *Attributeptr* が固定長データ型へのポインターである場合、 *bufferlength* には次のいずれかを指定する必要があります: SQL_IS_INTEGER、SQL_IS_UNINTEGER、SQL_SMALLINT、または sqlus悪意。  
  
 *Stringlength Ptr*  
 Output* 文字*Attributeptr*で返すことができるバイト数の合計 (文字データの null 終端バイトを除く) を返すバッファーへのポインター。  
  
 文字データの場合、返される使用可能なバイト数が*Bufferlength*以上の場合、文字 \* *attributeptr*内の記述子情報は*bufferlength*の長さから null 終端文字の長さを引いた値に切り捨てられ、ドライバーによって null で終了されます。  
  
 他のすべての種類のデータについては、 *Bufferlength* の値は無視され、ドライバーは * 文字*attributeptr* のサイズが32ビットであることを前提としています。  
  
 *NumericAttributePtr*  
 Outputフィールドが SQL_DESC_COLUMN_LENGTH などの数値記述子の型である場合、IRD の*Columnnumber*行の*FieldIdentifier*フィールドの値を返す整数バッファーへのポインターです。 それ以外の場合、フィールドは使用されません。 一部のドライバーでは、バッファーの下位の32ビットまたは16ビットのみが書き込まれ、上位ビットは変更されないことに注意してください。 したがって、この関数を呼び出す前に、アプリケーションは値を0に初期化する必要があります。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **Sqlcolattribute**が SQL_ERROR または SQL_SUCCESS_WITH_INFO のいずれかを返す場合、SQL_HANDLE_STMT の*Handletype*と*StatementHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出すことによって、関連付けられた SQLSTATE 値を取得できます。 次の表に、 **Sqlcolattribute** によって一般的に返される SQLSTATE 値の一覧を示し、この関数のコンテキストでそれぞれについて説明します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  
  
|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データ、右側が切り捨てられました|バッファー文字 \* *attributeptr*が文字列値全体を返すのに十分な大きさではないため、文字列値が切り捨てられました。 切り捨てられていない文字列値の長さは、**Stringlength ptr*で返されます。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|07005|準備されたステートメントが*カーソル指定*ではありません|*StatementHandle*に関連付けられたステートメントで結果セットが返されませんでした。 *FieldIdentifier*は SQL_DESC_COUNT ませんでした。 説明する列がありませんでした。|  
|07009|無効な記述子のインデックス|(DM) *Columnnumber* に指定された値が0で、SQL_ATTR_USE_BOOKMARKS statement 属性が SQL_UB_OFF でした。<br /><br /> 引数 *Columnnumber* に指定された値が、結果セット内の列数を超えています。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 診断データ構造から **SQLGetDiagField** によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|*StatementHandle*に対して非同期処理が有効になりました。 関数が呼び出され、実行が完了する前に、 **SQLCancel** または **Sqlcancelhandle** が *StatementHandle*で呼び出されました。 次に、 *StatementHandle*で関数が再度呼び出されました。<br /><br /> 関数が呼び出され、実行が完了する前に、マルチスレッドアプリケーションの別のスレッドの*StatementHandle*で**SQLCancel**または**sqlcancelhandle**が呼び出されました。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この aynchronous 関数は、SQLColAttribute が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または **Sqlmoreresults** が *StatementHandle* に対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。<br /><br /> (DM) 関数は、 **SQLPrepare**、 **SQLExecDirect**、または *StatementHandle*のカタログ関数を呼び出す前に呼び出されました。<br /><br /> (DM) 非同期的に実行されている関数 (この1つではない) が *StatementHandle* に対して呼び出され、この関数が呼び出されたときにまだ実行されています。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **Sqlbulkoperations**、 **SQLSetPos** が *StatementHandle* に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY090|文字列またはバッファーの長さが無効です|(DM) 文字* \* attributeptr*は文字列であり、 *bufferlength*は0未満ですが SQL_NTS と等しくありません。|  
|HY091|無効な記述子フィールド識別子|引数 *FieldIdentifier* に指定された値が、定義された値の1つではなく、実装定義の値ではありませんでした。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYC00|ドライバーに対応していません|引数 *FieldIdentifier* に指定された値は、ドライバーでサポートされていませんでした。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle* に関連付けられているドライバーでは、関数はサポートされていません。|  
|IM017|非同期通知モードでは、ポーリングは無効になっています|通知モデルが使用されるたびに、ポーリングは無効になります。|  
|IM018|**Sqlcompleteasync** は、このハンドルで前の非同期操作を完了するために呼び出されていません。|ハンドルに対する前の関数呼び出しが SQL_STILL_EXECUTING を返し、通知モードが有効になっている場合は、処理を完了するために、ハンドルに対して **Sqlcompleteasync** を呼び出す必要があります。|  
  
 **SQLPrepare**の後、 **sqlexecute**の前に呼び出された場合、データソースが*StatementHandle*に関連付けられている SQL ステートメントを評価するタイミングに応じて、 **Sqlcolattribute**は**SQLPrepare**または**sqlexecute**によって返される SQLSTATE を返すことができます。  
  
 パフォーマンス上の理由から、アプリケーションでは、ステートメントを実行する前に **Sqlcolattribute** を呼び出さないでください。  
  
## <a name="comments"></a>コメント  
 **Sqlcolattribute**によって返される情報をアプリケーションで使用する方法の詳細については、「[結果セットのメタデータ](../../../odbc/reference/develop-app/result-set-metadata.md)」を参照してください。  
  
 **Sqlcolattribute**は、 \* *numericattributeptr*または文字 \* *attributeptr*の情報を返します。 整数情報は \* 、SQLLEN 値として*numericattributeptr*に返されます。その他のすべての形式の情報は、文字 \* *attributeptr*で返されます。 Numericattributeptr で情報が返されると、 \* *NumericAttributePtr*ドライバーは、文字*attributeptr*、 *Bufferlength*、および*stringlength ptr*を無視します。 文字 attributeptr で情報が返された場合 \* *CharacterAttributePtr*、ドライバーは*numericattributeptr*を無視します。  
  
 **Sqlcolattribute** は、IRD の記述子フィールドから値を返します。 関数は、記述子ハンドルではなく、ステートメントハンドルで呼び出されます。 このセクションで後述する*FieldIdentifier*値の**sqlcolattribute**によって返される値は、適切な IRD ハンドルを指定して**SQLGetDescField**を呼び出すことによって取得することもできます。  
  
 このセクションでは、現在定義されている記述子フィールド、ODBC のバージョン、および情報が返される引数を後で示します。ドライバーでは、さまざまなデータソースを利用するために、より多くの記述子の種類を定義できます。  
  
 ODBC 3.*x* ドライバーは、各記述子フィールドに対して値を返す必要があります。 記述子フィールドがドライバーまたはデータソースに適用されない場合、特に明記されていない場合、ドライバーは \* *stringlength ptr*または空の文字列 (* 文字*attributeptr*) で0を返します。  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 ODBC 3.*x* 関数 **sqlcolattribute** は、非推奨の ODBC 2 を置き換えます。*x* 関数 **sqlcolattributes**。 **Sqlcolattributes**を**sqlcolattributes**にマップする場合 (ODBC 2 の場合)。*x*アプリケーションは ODBC 3 を使用して動作しています。*x*ドライバー)、または**sqlcolattribute**を**sqlcolattribute** (ODBC 3 の場合) にマッピングします。*x*アプリケーションは ODBC 2 で動作しています。*x*ドライバー) の場合、ドライバーマネージャーは*FieldIdentifier*の値をから渡すか、新しい値にマップするか、次のようにエラーを返します。  
  
> [!NOTE]  
>  ODBC 3 の *FieldIdentifier* 値で使用されるプレフィックス。*x* は、ODBC 2 で使用されているものから変更されています。*x*。 新しいプレフィックスは "SQL_DESC" です。古いプレフィックスは "SQL_COLUMN" でした。  
  
-   ODBC 2 の **#define** 値の場合は。*x* *FIELDIDENTIFIER* は、ODBC 3 の **#define** 値と同じです。*x* *FieldIdentifier*の場合、関数呼び出しの値が渡されるだけです。  
  
-   ODBC 2 の **#define** 値です。*x* *FieldIdentifiers* SQL_COLUMN_LENGTH、SQL_COLUMN_PRECISION、および SQL_COLUMN_SCALE は、ODBC 3 の **#define** 値とは異なります。*x* *FieldIdentifiers* SQL_DESC_PRECISION、SQL_DESC_SCALE、および SQL_DESC_LENGTH。 ODBC 2。*x* ドライバーは ODBC 2 だけをサポートする必要があります。*x* 値。 ODBC 3.*x* ドライバーは、これら3つの *FieldIdentifiers*の "SQL_COLUMN" と "SQL_DESC" の両方の値をサポートする必要があります。 有効桁数、小数点以下桁数、および長さは ODBC 3 では異なるため、これらの値は異なります。*x* は ODBC 2 ではありませんでした。*x*。 詳細については、「 [列のサイズ、10進数、転送オクテットの長さ、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)」を参照してください。  
  
-   ODBC 2 の **#define** 値の場合は。*x* *FIELDIDENTIFIER* は、ODBC 3 の **#define** 値とは異なります。*x* *FIELDIDENTIFIER*は、COUNT、NAME、および NULLABLE 値と共に発生するため、関数呼び出しの値は対応する値にマップされます。 たとえば、SQL_COLUMN_COUNT は SQL_DESC_COUNT にマップされ、SQL_DESC_COUNT はマッピングの方向に応じて SQL_COLUMN_COUNT にマップされます。  
  
-   *FieldIdentifier*が ODBC 3 の新しい値の場合。*x*。 ODBC 2 では、対応する値がありませんでした。*x*は、ODBC 3 ではマップされません。*x*アプリケーションは、ODBC 2 の**sqlcolattribute**の呼び出しでそれを使用します。*x*ドライバーを呼び出したときに、SQLSTATE HY091 (無効な記述子フィールド識別子) が返されます。  
  
 次の表に、 **Sqlcolattribute**によって返される記述子の種類を示します。 *Numericattributeptr*値の型は** \* sqllen**です。  
  
|*FieldIdentifier*|Information<br /><br /> 返される値|説明|  
|-----------------------|---------------------------------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE (ODBC 1.0)|*NumericAttributePtr*|列が自動増分列である場合は SQL_TRUE します。<br /><br /> 列が自動増分列ではないか、または数値でない場合に SQL_FALSE します。<br /><br /> このフィールドは、数値データ型の列に対してのみ有効です。 アプリケーションでは、自動インクリメント列を含む行に値を挿入できますが、通常、列の値を更新することはできません。<br /><br /> 自動インクリメント列に挿入が行われると、挿入時に一意の値が列に挿入されます。 インクリメントは定義されていませんが、データソース固有です。 アプリケーションでは、autoincrement 列が特定のポイントで開始されるか、特定の値によってインクリメントされると想定しないでください。|  
|SQL_DESC_BASE_COLUMN_NAME (ODBC 3.0)|*CharacterAttributePtr*|結果セット列の基本列名。 ベース列名が存在しない場合 (式である列の場合と同様)、この変数には空の文字列が含まれます。<br /><br /> この情報は、読み取り専用フィールドである IRD の SQL_DESC_BASE_COLUMN_NAME レコードフィールドから返されます。|  
|SQL_DESC_BASE_TABLE_NAME (ODBC 3.0)|*CharacterAttributePtr*|列を含むベーステーブルの名前。 ベーステーブル名を定義できない場合、または適用できない場合、この変数には空の文字列が含まれます。<br /><br /> この情報は、読み取り専用フィールドである IRD の SQL_DESC_BASE_TABLE_NAME レコードフィールドから返されます。|  
|SQL_DESC_CASE_SENSITIVE (ODBC 1.0)|*NumericAttributePtr*|列が照合順序と比較で大文字と小文字を区別して扱うかどうかを SQL_TRUE します。<br /><br /> 列が照合順序と比較で大文字と小文字を区別せずに処理されるかどうか、または非文字であるかどうかを SQL_FALSE します。|  
|SQL_DESC_CATALOG_NAME (ODBC 2.0)|*CharacterAttributePtr*|列を含むテーブルのカタログです。 列が式である場合、または列がビューの一部である場合、戻り値は実装によって定義されます。 データソースでカタログがサポートされていない場合、またはカタログ名を特定できない場合は、空の文字列が返されます。 この VARCHAR レコードフィールドは、128文字に制限されていません。|  
|SQL_DESC_CONCISE_TYPE (ODBC 1.0)|*NumericAttributePtr*|簡潔なデータ型。<br /><br /> Datetime および interval データ型の場合、このフィールドは簡潔なデータ型を返します。たとえば、SQL_TYPE_TIME や SQL_INTERVAL_YEAR のようになります。 (詳細については、「付録 D: データ型」の「 [データ型の識別子と記述子](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) 」を参照してください)。<br /><br /> この情報は、IRD の SQL_DESC_CONCISE_TYPE レコードフィールドから返されます。|  
|SQL_DESC_COUNT (ODBC 1.0)|*NumericAttributePtr*|結果セットで使用できる列の数。 結果セットに列がない場合は、0が返されます。 *Columnnumber*引数の値は無視されます。<br /><br /> この情報は、IRD の SQL_DESC_COUNT header フィールドから返されます。|  
|SQL_DESC_DISPLAY_SIZE (ODBC 1.0)|*NumericAttributePtr*|列のデータを表示するために必要な最大文字数。 表示サイズの詳細については、「付録 D: データ型」の「 [列サイズ、10進数、転送オクテット長、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 」を参照してください。|  
|SQL_DESC_FIXED_PREC_SCALE (ODBC 1.0)|*NumericAttributePtr*|列の有効桁数が固定され、データソース固有の小数点以下桁数が0以外の場合に SQL_TRUE します。<br /><br /> 列の有効桁数が固定されておらず、データソース固有の小数点以下桁数が0以外の場合に SQL_FALSE します。|  
|SQL_DESC_LABEL (ODBC 2.0)|*CharacterAttributePtr*|列のラベルまたはタイトル。 たとえば、EmpName という名前の列は、Employee Name というラベルが付けられているか、別名でラベル付けされている可能性があります。<br /><br /> 列にラベルがない場合は、列名が返されます。 列にラベルが付けられていない場合は、空の文字列が返されます。|  
|SQL_DESC_LENGTH (ODBC 3.0)|*NumericAttributePtr*|文字列またはバイナリデータ型の最大文字長または実際の文字長の数値。 固定長データ型の場合は最大文字長、可変長データ型の場合は実際の文字長です。 この値は、文字列を終了する null 終了バイトを常に除外します。<br /><br /> この情報は、IRD の SQL_DESC_LENGTH レコードフィールドから返されます。<br /><br /> 長さの詳細については、「付録 D: データ型」の「 [列のサイズ、10進数、転送オクテットの長さ、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 」を参照してください。|  
|SQL_DESC_LITERAL_PREFIX (ODBC 3.0)|*CharacterAttributePtr*|この VARCHAR (128) レコードフィールドには、ドライバーがこのデータ型のリテラルのプレフィックスとして認識する文字または文字が含まれています。 このフィールドには、リテラルプレフィックスが適用されないデータ型の空の文字列が含まれています。 詳細については、「 [リテラルプレフィックスとサフィックス](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)」を参照してください。|  
|SQL_DESC_LITERAL_SUFFIX (ODBC 3.0)|*CharacterAttributePtr*|この VARCHAR (128) レコードフィールドには、ドライバーがこのデータ型のリテラルのサフィックスとして認識する文字または文字が含まれています。 このフィールドには、リテラルサフィックスが適用されないデータ型の空の文字列が含まれています。 詳細については、「 [リテラルプレフィックスとサフィックス](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)」を参照してください。|  
|SQL_DESC_LOCAL_TYPE_NAME (ODBC 3.0)|*CharacterAttributePtr*|この VARCHAR (128) レコードフィールドには、データ型の標準名とは異なる可能性がある、ローカライズされた (ネイティブ言語) 名が含まれています。 ローカライズされた名前がない場合は、空の文字列が返されます。 このフィールドは、表示のみを目的としています。 文字列の文字セットはロケールに依存し、通常はサーバーの既定の文字セットです。|  
|SQL_DESC_NAME (ODBC 3.0)|*CharacterAttributePtr*|列の別名 (適用される場合)。 列の別名が適用されない場合は、列名が返されます。 どちらの場合も、SQL_DESC_UNNAMED は SQL_NAMED に設定されます。 列名または列の別名がない場合は、空の文字列が返され、SQL_DESC_UNNAMED が SQL_UNNAMED に設定されます。<br /><br /> この情報は、IRD の SQL_DESC_NAME レコードフィールドから返されます。|  
|SQL_DESC_NULLABLE (ODBC 3.0)|*NumericAttributePtr*|列が NULL 値を持つことができるかどうかを SQL_ null 値を許容します。列に NULL 値が含まれていない場合は SQL_NO_NULLS します。列が NULL 値を許容するかどうかが不明な場合は、SQL_NULLABLE_UNKNOWN ます。<br /><br /> この情報は、IRD の SQL_DESC_NULLABLE レコードフィールドから返されます。|  
|SQL_DESC_NUM_PREC_RADIX (ODBC 3.0)|*NumericAttributePtr*|SQL_DESC_TYPE フィールドのデータ型が概数データ型の場合、この SQLINTEGER フィールドには値2が格納されます。これは、SQL_DESC_PRECISION フィールドにビット数が含まれているためです。 SQL_DESC_TYPE フィールドのデータ型が正確な数値データ型である場合、このフィールドには10の値が格納されます。これは、SQL_DESC_PRECISION フィールドに小数点以下の桁数が含まれているためです。 数値以外のすべてのデータ型では、このフィールドは0に設定されます。|  
|SQL_DESC_OCTET_LENGTH (ODBC 3.0)|*NumericAttributePtr*|文字列またはバイナリデータ型の長さ (バイト単位)。 固定長の文字型またはバイナリ型の場合、実際のバイト数です。 可変長の文字型またはバイナリ型の場合は、バイト単位の最大長です。 この値には、null 終端文字は含まれません。<br /><br /> この情報は、IRD の SQL_DESC_OCTET_LENGTH レコードフィールドから返されます。<br /><br /> 長さの詳細については、「付録 D: データ型」の「 [列のサイズ、10進数、転送オクテットの長さ、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 」を参照してください。|  
|SQL_DESC_PRECISION (ODBC 3.0)|*NumericAttributePtr*|数値データ型の数値は、適用可能な有効桁数を表します。 データ型 SQL_TYPE_TIME、SQL_TYPE_TIMESTAMP、および時間間隔を表すすべての interval データ型の場合、その値は秒の小数部の適用可能な有効桁数になります。<br /><br /> この情報は、IRD の SQL_DESC_PRECISION レコードフィールドから返されます。|  
|SQL_DESC_SCALE (ODBC 3.0)|*NumericAttributePtr*|数値データ型に適用できる小数点以下桁数を表す数値です。 DECIMAL データ型と NUMERIC データ型の場合、これは定義されたスケールです。 他のすべてのデータ型では定義されていません。<br /><br /> この情報は、IRD の [スケールレコード] フィールドから返されます。|  
|SQL_DESC_SCHEMA_NAME (ODBC 2.0)|*CharacterAttributePtr*|列を含むテーブルのスキーマです。 列が式である場合、または列がビューの一部である場合、戻り値は実装によって定義されます。 データソースでスキーマがサポートされていない場合、またはスキーマ名を特定できない場合は、空の文字列が返されます。 この VARCHAR レコードフィールドは、128文字に制限されていません。|  
|SQL_DESC_SEARCHABLE (ODBC 1.0)|*NumericAttributePtr*|WHERE 句で列を使用できない場合は SQL_PRED_NONE します。 (これは、ODBC 2 の SQL_UNSEARCHABLE 値と同じです。*x*)<br /><br /> WHERE 句で列を使用できるが、LIKE 述語でのみ使用できる場合は SQL_PRED_CHAR します。 (これは、ODBC 2 の SQL_LIKE_ONLY 値と同じです。*x*)<br /><br /> WHERE 句で列を使用できるかどうかを SQL_PRED_BASIC します。ただし、のようにすべての比較演算子を使用できます。 (これは、ODBC 2 の SQL_EXCEPT_LIKE 値と同じです。*x*)<br /><br /> 任意の比較演算子を持つ WHERE 句で列を使用できるかどうかを SQL_PRED_SEARCHABLE します。<br /><br /> SQL_LONGVARCHAR 型の列と SQL_LONGVARBINARY は通常 SQL_PRED_CHAR を返します。|  
|SQL_DESC_TABLE_NAME (ODBC 2.0)|*CharacterAttributePtr*|列を含むテーブルの名前です。 列が式である場合、または列がビューの一部である場合、戻り値は実装によって定義されます。<br /><br /> テーブル名を特定できない場合は、空の文字列が返されます。|  
|SQL_DESC_TYPE (ODBC 3.0)|*NumericAttributePtr*|SQL データ型を示す数値です。<br /><br /> *Columnnumber*が0の場合、可変長のブックマークに対して SQL_BINARY が返され、固定長のブックマークに対して SQL_INTEGER が返されます。<br /><br /> Datetime および interval データ型の場合、このフィールドには、SQL_DATETIME または SQL_INTERVAL の詳細データ型が返されます。 (詳細については、「付録 D: データ型」の「 [データ型の識別子と記述子](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) 」を参照してください。<br /><br /> この情報は、IRD の SQL_DESC_TYPE レコードフィールドから返されます。 **注:**  ODBC 2 に対して機能します。*x* ドライバーでは、代わりに SQL_DESC_CONCISE_TYPE を使用します。|  
|SQL_DESC_TYPE_NAME (ODBC 1.0)|*CharacterAttributePtr*|データソースに依存するデータ型の名前。たとえば、"CHAR"、"VARCHAR"、"MONEY"、"LONG VARBINARY"、"CHAR () FOR BIT DATA" などです。<br /><br /> 型が不明な場合は、空の文字列が返されます。|  
|SQL_DESC_UNNAMED (ODBC 3.0)|*NumericAttributePtr*|SQL_NAMED または SQL_UNNAMED。 IRD の SQL_DESC_NAME フィールドに列の別名または列の名前が含まれている場合は SQL_NAMED が返されます。 列名または列の別名がない場合は、SQL_UNNAMED が返されます。<br /><br /> この情報は、IRD の SQL_DESC_UNNAMED レコードフィールドから返されます。|  
|SQL_DESC_UNSIGNED (ODBC 1.0)|*NumericAttributePtr*|列が符号なし (または数値ではない) の場合に SQL_TRUE します。<br /><br /> 列が署名されている場合は SQL_FALSE します。|  
|SQL_DESC_UPDATABLE (ODBC 1.0)|*NumericAttributePtr*|列は、定義されている定数の値によって記述されます。<br /><br /> SQL_ATTR_READONLY SQL_ATTR_WRITE SQL_ATTR_READWRITE_UNKNOWN<br /><br /> SQL_DESC_UPDATABLE は、ベーステーブルの列ではなく、結果セットの列の更新可能性について説明します。 結果セットの列の基になるベース列の更新可能性は、このフィールドの値と異なる場合があります。 列を更新できるかどうかは、データ型、ユーザー権限、および結果セット自体の定義に基づいて決まります。 列が更新可能かどうかが不明な場合は、SQL_ATTR_READWRITE_UNKNOWN が返されます。|  
  
 **Sqlcolattribute** は、 **SQLDescribeCol**の拡張可能な代替手段です。 **SQLDescribeCol** は、ANSI-89 SQL に基づいて固定された記述子情報のセットを返します。 **Sqlcolattribute** を使用すると、ANSI SQL-92 および DBMS ベンダーの拡張機能で利用可能な、より広範な記述子情報セットにアクセスできます。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|結果セット内の列へのバッファーのバインド|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|ステートメント処理の取り消し|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|結果セットの列に関する情報を返す|[SQLDescribeCol 関数](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|データのブロックのフェッチまたは結果セットのスクロール|[SQLFetchScroll 関数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|複数行のデータのフェッチ|[SQLFetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
  
## <a name="example"></a>例  
 次のサンプルコードでは、ハンドルと接続は解放されません。 ハンドルとステートメントを解放するコードサンプルについては、「 [Sqlfreehandle 関数](../../../odbc/reference/syntax/sqlfreehandle-function.md)」、「 [サンプル ODBC プログラム](../../../odbc/reference/sample-odbc-program.md)」、および「 [SQLFreeStmt 関数](../../../odbc/reference/syntax/sqlfreestmt-function.md) 」を参照してください。  
  
```cpp  
// SQLColAttibute.cpp  
// compile with: user32.lib odbc32.lib  
  
#define UNICODE  
  
#include <windows.h>  
#include <sqlext.h>  
#include <strsafe.h>  
  
struct DataBinding {  
   SQLSMALLINT TargetType;  
   SQLPOINTER TargetValuePtr;  
   SQLINTEGER BufferLength;  
   SQLLEN StrLen_or_Ind;  
};  
  
void printStatementResult(SQLHSTMT hstmt) {  
   int bufferSize = 1024, i;  
   SQLRETURN retCode;  
   SQLSMALLINT numColumn = 0, bufferLenUsed;
   
   retCode = SQLNumResultCols(hstmt, &numColumn);  
   
   SQLPOINTER* columnLabels = (SQLPOINTER *)malloc( numColumn * sizeof(SQLPOINTER*) );  
   struct DataBinding* columnData = (struct DataBinding*)malloc( numColumn * sizeof(struct DataBinding) );  
  
   printf( "Columns from that table:\n" );  
   for ( i = 0 ; i < numColumn ; i++ ) {  
      columnLabels[i] = (SQLPOINTER)malloc( bufferSize*sizeof(char) );  
  
      retCode = SQLColAttribute(hstmt, (SQLUSMALLINT)i + 1, SQL_DESC_LABEL, columnLabels[i], (SQLSMALLINT)bufferSize, &bufferLenUsed, NULL);  
      wprintf( L"Column %d: %s\n", i, (wchar_t*)columnLabels[i] );  
   }  
  
   // allocate memory for the binding  
   for ( i = 0 ; i < numColumn ; i++ ) {  
      columnData[i].TargetType = SQL_C_CHAR;  
      columnData[i].BufferLength = (bufferSize+1);  
      columnData[i].TargetValuePtr = malloc( sizeof(unsigned char)*columnData[i].BufferLength );  
   }  
  
   // setup the binding   
   for ( i = 0 ; i < numColumn ; i++ ) {  
      retCode = SQLBindCol(hstmt, (SQLUSMALLINT)i + 1, columnData[i].TargetType,   
         columnData[i].TargetValuePtr, columnData[i].BufferLength, &(columnData[i].StrLen_or_Ind));  
   }  
  
   printf( "Data from that table:\n" );  
   // fetch the data and print out the data  
   for ( retCode = SQLFetch(hstmt) ; retCode == SQL_SUCCESS || retCode == SQL_SUCCESS_WITH_INFO ; retCode = SQLFetch(hstmt) ) {  
      int j;  
      for ( j = 0 ; j < numColumn ; j++ )  
         wprintf( L"%s: %hs\n", columnLabels[j], columnData[j].TargetValuePtr );  
      printf( "\n" );  
   }  
   printf( "\n" );   
}  
  
int main() {  
   int bufferSize = 1024, i, count = 1, numCols = 5;  
   wchar_t firstTableName[1024], * dbName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize ), * userName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize );  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLWCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen, bufferLen;  
   SQLRETURN retCode;  
  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   struct DataBinding* catalogResult = (struct DataBinding*) malloc( numCols * sizeof(struct DataBinding) );  
   SQLWCHAR* selectAllQuery = (SQLWCHAR *)malloc( sizeof(SQLWCHAR) * bufferSize );  
  
   // connect to database  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLCHAR *)(void*)SQL_OV_ODBC3, -1);  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
   retCode = SQLDriverConnect(hdbc, desktopHandle, L"Driver={SQL Server}", SQL_NTS, connStrbuffer, 1025, &connStrBufferLen, SQL_DRIVER_PROMPT);  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   // display the database information  
   retCode = SQLGetInfo(hdbc, SQL_DATABASE_NAME, dbName, (SQLSMALLINT)bufferSize, (SQLSMALLINT *)&bufferLen);  
   retCode = SQLGetInfo(hdbc, SQL_USER_NAME, userName, (SQLSMALLINT)bufferSize, &bufferLen);  
  
   for ( i = 0 ; i < numCols ; i++ ) {  
      catalogResult[i].TargetType = SQL_C_CHAR;  
      catalogResult[i].BufferLength = (bufferSize + 1);  
      catalogResult[i].TargetValuePtr = malloc( sizeof(unsigned char)*catalogResult[i].BufferLength );  
   }  
  
   // Set up the binding. This can be used even if the statement is closed by closeStatementHandle  
   for ( i = 0 ; i < numCols ; i++ )  
      retCode = SQLBindCol(hstmt, (SQLUSMALLINT)i + 1, catalogResult[i].TargetType, catalogResult[i].TargetValuePtr, catalogResult[i].BufferLength, &(catalogResult[i].StrLen_or_Ind));  
  
   retCode = SQLTables( hstmt, (SQLWCHAR*)SQL_ALL_CATALOGS, SQL_NTS, L"", SQL_NTS, L"", SQL_NTS, L"", SQL_NTS );  
   retCode = SQLFreeStmt(hstmt, SQL_CLOSE);  
  
   retCode = SQLTables( hstmt, dbName, SQL_NTS, userName, SQL_NTS, L"%", SQL_NTS, L"TABLE", SQL_NTS );  
  
   for ( retCode = SQLFetch(hstmt) ; retCode == SQL_SUCCESS || retCode == SQL_SUCCESS_WITH_INFO ; retCode = SQLFetch(hstmt), ++count )  
      if ( count == 1 )  
         StringCchPrintfW( firstTableName, 1024, L"%hs", catalogResult[2].TargetValuePtr );  
   retCode = SQLFreeStmt(hstmt, SQL_CLOSE);  
  
   wprintf( L"Select all data from the first table (%s)\n", firstTableName );  
   StringCchPrintfW( selectAllQuery, bufferSize, L"SELECT * FROM %s", firstTableName );  
  
   retCode = SQLExecDirect(hstmt, selectAllQuery, SQL_NTS);  
   printStatementResult(hstmt);  
}  
```  
  
## <a name="see-also"></a>関連項目  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダーファイル](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC のサンプル プログラム](../../../odbc/reference/sample-odbc-program.md)
