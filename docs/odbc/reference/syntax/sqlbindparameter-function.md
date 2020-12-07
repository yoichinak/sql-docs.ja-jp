---
description: SQLBindParameter 関数
title: SQLBindParameter 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBindParameter
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBindParameter
helpviewer_keywords:
- SQLBindParameter function [ODBC]
ms.assetid: 38349d4b-be03-46f9-9d6a-e50dd144e225
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a7fa603edac9ede641697ba139670a2cae2e1e6e
ms.sourcegitcommit: 80701484b8f404316d934ad2a85fd773e26ca30c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93243551"
---
# <a name="sqlbindparameter-function"></a>SQLBindParameter 関数

**互換性**  
 導入されたバージョン: ODBC 2.0 標準準拠: ODBC  
  
 **まとめ**  
 **SQLBindParameter** は、SQL ステートメントのパラメーターマーカーにバッファーをバインドします。 **SQLBindParameter** は、基になるドライバーが unicode データをサポートしていない場合でも、unicode C データ型へのバインドをサポートします。  
  
> [!NOTE]  
>  この関数は、ODBC 1.0 関数 **SQLSetParam** を置き換えます。 詳細については、「コメント」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```cpp
  
SQLRETURN SQLBindParameter(  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ParameterNumber,  
      SQLSMALLINT     InputOutputType,  
      SQLSMALLINT     ValueType,  
      SQLSMALLINT     ParameterType,  
      SQLULEN         ColumnSize,  
      SQLSMALLINT     DecimalDigits,  
      SQLPOINTER      ParameterValuePtr,  
      SQLLEN          BufferLength,  
      SQLLEN *        StrLen_or_IndPtr);  
```
  
## <a name="arguments"></a>引数

 *StatementHandle*  
 代入ステートメントハンドル。  
  
 *ParameterNumber*  
 代入パラメーターの数を昇順に並べ替え、1から開始します。  
  
 *InputOutputType*  
 代入パラメーターの型。 詳細については、「コメント」の「 *Inputoutputtype* 引数」を参照してください。  
  
 *ValueType*  
 代入パラメーターの C データ型。 詳細については、「コメント」の「 *ValueType* 引数」を参照してください。  
  
 *ParameterType*  
 代入パラメーターの SQL データ型。 詳細については、「コメント」の「 *ParameterType* 引数」を参照してください。  
  
 *ColumnSize*  
 代入対応するパラメーターマーカーの列または式のサイズ。 詳細については、「コメント」の「 *Columnsize* 引数」を参照してください。  
  
 アプリケーションを64ビットの Windows オペレーティングシステムで実行する場合は、「 [ODBC 64 ビット情報](../../../odbc/reference/odbc-64-bit-information.md)」を参照してください。  
  
 *DecimalDigits*  
 代入対応するパラメーターマーカーの列または式の小数点以下の桁数。 列のサイズの詳細については、「 [列のサイズ、10進数、転送オクテットの長さ、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)」を参照してください。  
  
 *ParameterValuePtr*  
 [遅延入力]パラメーターのデータのバッファーを指すポインター。 詳細については、「コメント」の「 *Parametervalueptr* 引数」を参照してください。  
  
 *BufferLength*  
 [入力/出力] *Parametervalueptr* バッファーの長さ (バイト単位)。 詳細については、「コメント」の「 *Bufferlength* 引数」を参照してください。  
  
 アプリケーションが64ビットのオペレーティングシステムで実行される場合は、「 [ODBC 64 ビット情報](../../../odbc/reference/odbc-64-bit-information.md)」を参照してください。  
  
 *StrLen_or_IndPtr*  
 [遅延入力]パラメーターの長さのバッファーへのポインター。 詳細については、「コメント」の「 *StrLen_or_IndPtr* の引数」を参照してください。  
  
## <a name="returns"></a>戻り値

 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断

 **SQLBindParameter** が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合、関連付けられた SQLSTATE 値を取得するには、 *Handletype* SQL_HANDLE_STMT と *StatementHandle* の *ハンドル* を指定して **SQLGetDiagRec** を呼び出します。 次の表に、 **SQLBindParameter** によって通常返される SQLSTATE 値と、この関数のコンテキストでのそれぞれについて説明します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR ます。  

|SQLSTATE|エラー|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|07006|制限されたデータ型の属性違反|*ValueType* 引数によって識別されるデータ型は、 *ParameterType* 引数によって識別されるデータ型に変換できません。 このエラーは、 **SQLBindParameter** ではなく、実行時に **SQLExecDirect** 、 **Sqlexecute** 、または **sqlputdata** によって返される可能性があります。|  
|07009|無効な記述子のインデックス|(DM) 引数 *Parameternumber* に指定された値が1未満でした。|  
|HY000|一般的なエラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 * *Messagetext* バッファーの **SQLGetDiagRec** によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY003|アプリケーションバッファーの種類が無効です|引数 *ValueType* によって指定された値が、有効な C データ型または SQL_C_DEFAULT ではありませんでした。|  
|HY004|SQL データ型が無効です|引数 *ParameterType* に指定された値は、有効な ODBC SQL データ型識別子でも、ドライバーでサポートされているドライバー固有の sql データ型識別子でもありませんでした。|  
|HY009|引数の値が無効です|(DM) 引数 *Parametervalueptr* は null ポインターで、引数 *StrLen_or_IndPtr* が null ポインターであり、引数 *inputoutputtype* が SQL_PARAM_OUTPUT いませんでした。<br /><br /> (DM) SQL_PARAM_OUTPUT。引数 *Parametervalueptr* が null ポインター、C 型が char または Binary、Bufferlength ( *cbValueMax* ) が0を超えています。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *StatementHandle* に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、 **SQLBindParameter** が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute** 、 **SQLExecDirect** 、または **Sqlmoreresults** が *StatementHandle* に対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。<br /><br /> (DM) 非同期的に実行する関数が *StatementHandle* に対して呼び出されましたが、この関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute** 、 **SQLExecDirect** 、 **Sqlbulkoperations** 、 **SQLSetPos** が *StatementHandle* に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY021|不整合な記述子情報|整合性チェック中にチェックされた記述子情報が一致しませんでした。 ( **SQLSetDescField** の「整合性チェック」セクションを参照してください)。<br /><br /> 引数 *DecimalDigits* に指定された値が、 *ParameterType* 引数で指定された SQL データ型の列のデータソースでサポートされている値の範囲外でした。|  
|HY090|文字列またはバッファーの長さが無効です|(DM) *Bufferlength* の値が0未満でした。 ( **SQLSetDescField** の [SQL_DESC_DATA_PTR] フィールドの説明を参照してください)。|  
|HY104|有効桁数または小数点以下桁数の値が無効です|引数 *Columnsize* または *DecimalDigits* に指定された値が、 *ParameterType* 引数で指定された SQL データ型の列のデータソースでサポートされている値の範囲外でした。|  
|HY105|パラメーターの型が無効です|(DM) 引数 *Inputoutputtype* に指定された値が無効でした。 (「コメント」を参照してください)。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYC00|省略可能な機能は実装されていません|ドライバーまたはデータソースが、引数 *ValueType* に指定された値と、引数 *ParameterType* に指定されたドライバー固有の値の組み合わせによって指定された変換をサポートしていません。<br /><br /> 引数 *ParameterType* に指定された値は、ドライバーでサポートされている odbc のバージョンの有効な odbc SQL データ型識別子でしたが、ドライバーまたはデータソースではサポートされていませんでした。<br /><br /> ドライバーは ODBC 2 だけをサポートします。 *x* と引数 *ValueType* は次のいずれかでした。<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> すべての interval C データ型は、「付録 D: データ型」の [c データ型](../../../odbc/reference/appendixes/c-data-types.md) に記載されています。<br /><br /> ドライバーがサポートしているのは3.50 より前のバージョンの ODBC のみで、引数 *ValueType* は SQL_C_GUID です。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr** 、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle* に関連付けられているドライバーでは、関数はサポートされていません。|  
  
## <a name="comments"></a>コメント

 アプリケーションは **SQLBindParameter** を呼び出して、SQL ステートメント内の各パラメーターマーカーをバインドします。 バインドは、アプリケーションが **SQLBindParameter** を再度呼び出すか、または **SQLSetDescField** を呼び出し SQL_RESET_PARAMS て APD の SQL_DESC_COUNT header フィールドを0に設定するまで、 **有効なまま** になります。  
  
 パラメーターの詳細については、「 [ステートメントパラメーター](../../../odbc/reference/develop-app/statement-parameters.md)」を参照してください。 パラメーターのデータ型とパラメーターマーカーの詳細については、「付録 C: SQL 文法」の「 [パラメーターのデータ型](../../../odbc/reference/appendixes/parameter-data-types.md) と [パラメーターマーカー](../../../odbc/reference/appendixes/parameter-markers.md) 」を参照してください。  
  
## <a name="parameternumber-argument"></a>ParameterNumber 引数  
 **SQLBindParameter** の呼び出しの *parameternumber* が SQL_DESC_COUNT の値より大きい場合は、 **SQLSetDescField** が呼び出され、 *parameternumber* に対して SQL_DESC_COUNT の値が増加します。  
  
## <a name="inputoutputtype-argument"></a>InputOutputType 引数  
 *Inputoutputtype* 引数は、パラメーターの型を指定します。 この引数は、IPD の SQL_DESC_PARAMETER_TYPE フィールドを設定します。 **INSERT** ステートメントなど、プロシージャを呼び出さない SQL ステートメントのすべてのパラメーターは、 *入力 * * パラメーター* です。 プロシージャ呼び出しのパラメーターには、入力、入力、出力、または出力パラメーターを指定できます。 (アプリケーションは **SQLProcedureColumns** を呼び出して、プロシージャ呼び出しのパラメーターの型を決定します。型を特定できないパラメーターは入力パラメーターと見なされます)。  
  
 *InputOutputType* 引数は、次にいずれかの値になります。  
  
-   SQL_PARAM_INPUT。 パラメーターは、 **INSERT** ステートメントなどのプロシージャを呼び出さない SQL ステートメントのパラメーター、またはプロシージャの入力パラメーターとしてマークするパラメーターをマークします。 たとえば、 **INSERT INTO EMPLOYEE VALUES (?,?,?)** のパラメーターは入力パラメーターですが、 **{Call addemp (?,?,?)}** のパラメーターは、必ずしも入力パラメーターであるとは限りません。  
  
     ステートメントが実行されると、ドライバーはパラメーターのデータをデータソースに送信します。\* *parametervalueptr* バッファーには有効な入力値を含める必要があります。または、* *StrLen_or_IndPtr* バッファーには、SQL_NULL_DATA、SQL_DATA_AT_EXEC、または SQL_LEN_DATA_AT_EXEC マクロの結果が含まれている必要があります。  
  
     アプリケーションがプロシージャ呼び出しでパラメーターの型を判断できない場合は、 *Inputoutputtype* を SQL_PARAM_INPUT に設定します。データソースからパラメーターの値が返された場合、ドライバーはその値を破棄します。  
  
-   SQL_PARAM_INPUT_OUTPUT。 パラメーターは、プロシージャの入力/出力パラメーターをマークします。 たとえば、 **{Call GetEmpDept (?)}** のパラメーターは、従業員の名前を受け取り、従業員の部署名を返す入力/出力パラメーターです。  
  
     ステートメントが実行されると、ドライバーはパラメーターのデータをデータソースに送信します。\* *parametervalueptr* バッファーには有効な入力値を含める必要があります。または、 \* *StrLen_or_IndPtr* バッファーには、SQL_NULL_DATA、SQL_DATA_AT_EXEC、または SQL_LEN_DATA_AT_EXEC マクロの結果が含まれている必要があります。 ステートメントが実行されると、ドライバーはパラメーターのデータをアプリケーションに返します。データソースが入力/出力パラメーターの値を返さない場合、ドライバーは * *StrLen_or_IndPtr* バッファーを SQL_NULL_DATA に設定します。  
  
    > [!NOTE]  
    >  ODBC 1.0 アプリケーションが ODBC 2.0 ドライバーで **SQLSetParam** を呼び出すと、ドライバーマネージャーはこれを **SQLBindParameter** への呼び出しに変換します。この呼び出しで、 *inputoutputtype* 引数が SQL_PARAM_INPUT_OUTPUT に設定されています。  
  
-   SQL_PARAM_OUTPUT。 プロシージャ内のプロシージャまたは出力パラメーターの戻り値は、パラメーターによってマークされます。どちらの場合も、 *出力パラメーター* と呼ばれます。 たとえば、 **{? = Call GetNextEmpID}** のパラメーターは、次の employee ID を返す出力パラメーターです。  
  
     ステートメントが実行された後は、パラメーターのデータがドライバーによってアプリケーションに返されます。ただし、 *Parametervalueptr* 引数と *StrLen_or_IndPtr* 引数が両方とも null ポインターの場合、ドライバーは出力値を破棄します。 データソースが出力パラメーターの値を返さない場合、ドライバーは * *StrLen_or_IndPtr* バッファーを SQL_NULL_DATA に設定します。  
  
-   SQL_PARAM_INPUT_OUTPUT_STREAM。 入力/出力パラメーターをストリームする必要があることを示します。 **SQLGetData** は、部分のパラメーター値を読み取ることができます。 バッファー長は **SQLGetData** の呼び出しで決定されるため、 *bufferlength* は無視されます。 *StrLen_or_IndPtr* バッファーの値には、SQL_NULL_DATA、SQL_DEFAULT_PARAM、SQL_DATA_AT_EXEC、または SQL_LEN_DATA_AT_EXEC マクロの結果が含まれている必要があります。 パラメーターは、出力時にストリームされる場合、入力時に実行時データ (DAE) パラメーターとしてバインドされている必要があります。 *Parametervalueptr* は、入力と出力の両方に *parametervalueptr* を使用して渡された値を持つユーザー定義トークンとして **sqlparamdata** によって返される、null 以外のポインター値にすることができます。 詳細については、「 [SQLGetData を使用した出力パラメーターの取得](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)」を参照してください。  
  
-   SQL_PARAM_OUTPUT_STREAM。 出力パラメーターの SQL_PARAM_INPUT_OUTPUT_STREAM と同じです。 **StrLen_or_IndPtr* は入力時に無視されます。  
  
 次の表に、 *Inputoutputtype* と * *StrLen_or_IndPtr* のさまざまな組み合わせを示します。  
  
|*InputOutputType*|**StrLen_or_IndPtr*|結果|ParameterValuePtr の注釈|  
|-----------------------|----------------------------|-------------|---------------------------------|  
|SQL_PARAM_INPUT|SQL_LEN_DATA_AT_EXEC ( *LEN* ) または SQL_DATA_AT_EXEC|パーツでの入力|*Parametervalueptr* には、 *parametervalueptr* で値が渡されたユーザー定義トークンとして **sqlparamdata** によって返されるポインター値を指定できます。|  
|SQL_PARAM_INPUT|Not SQL_LEN_DATA_AT_EXEC ( *LEN* ) または SQL_DATA_AT_EXEC|入力バインドバッファー|*Parametervalueptr* は、入力バッファーのアドレスです。|  
|SQL_PARAM_OUTPUT|入力時には無視されます。|出力バインドバッファー|*Parametervalueptr* は出力バッファーのアドレスです。|  
|SQL_PARAM_OUTPUT_STREAM|入力時には無視されます。|ストリーム出力|*Parametervalueptr* には任意のポインター値を指定できます。この値は、 *parametervalueptr* で渡された値を持つユーザー定義トークンとして **sqlparamdata** によって返されます。|  
|SQL_PARAM_INPUT_OUTPUT|SQL_LEN_DATA_AT_EXEC ( *LEN* ) または SQL_DATA_AT_EXEC|部分および出力バインドバッファーでの入力|*Parametervalueptr* は出力バッファーのアドレスです。これは、 *parametervalueptr* で値が渡されたユーザー定義トークンとして **sqlparamdata** によっても返されます。|  
|SQL_PARAM_INPUT_OUTPUT|Not SQL_LEN_DATA_AT_EXEC ( *LEN* ) または SQL_DATA_AT_EXEC|入力バインドバッファーと出力バインドバッファー|*Parametervalueptr* は、共有入出力バッファーのアドレスです。|
|SQL_PARAM_INPUT_OUTPUT_STREAM|SQL_LEN_DATA_AT_EXEC ( *LEN* ) または SQL_DATA_AT_EXEC|部分およびストリーム出力の入力|*Parametervalueptr* には、null 以外のポインター値を指定できます。この値は、入力と出力の両方に *parametervalueptr* を使用して渡された値を持つユーザー定義トークンとして **sqlparamdata** によって返されます。|  
  
> [!NOTE]  
>  ドライバーでは、アプリケーションが出力パラメーターまたは入出力パラメーターをストリームとしてバインドするときに許可される SQL 型を決定する必要があります。 ドライバーマネージャーでは、無効な SQL の種類に対してエラーは生成されません。  
  
## <a name="valuetype-argument"></a>ValueType 引数

 *ValueType* 引数は、パラメーターの C データ型を指定します。 この引数は、APD の SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE、および SQL_DESC_DATETIME_INTERVAL_CODE フィールドを設定します。 これは、「付録 D: データ型」の「 [C データ型](../../../odbc/reference/appendixes/c-data-types.md) 」セクションの値のいずれかである必要があります。  
  
 *ValueType* 引数が interval データ型の1つである場合、APD の *parameternumber* レコードの SQL_DESC_TYPE フィールドは SQL_INTERVAL に設定されます。また、APD の SQL_DESC_CONCISE_TYPE フィールドは、簡潔な interval データ型に設定され、 *parameternumber* レコードの SQL_DESC_DATETIME_INTERVAL_CODE フィールドは、特定の interval データ型のサブコードに設定されます。 (「 [付録 D: データ型](../../../odbc/reference/appendixes/appendix-d-data-types.md)」を参照してください)。SQL_DESC_PRECISION SQL_DESC_DATETIME_INTERVAL_PRECISION に設定された既定の間隔 (2) と既定の間隔 (秒) の有効桁数 (6) は、それぞれ APD のフィールドに設定されています。 既定の有効桁数が適切でない場合、アプリケーションでは、 **SQLSetDescField** または **SQLSetDescRec** の呼び出しによって記述子フィールドを明示的に設定する必要があります。  
  
 *ValueType* 引数が datetime データ型の1つである場合、APD の *parameternumber* レコードの SQL_DESC_TYPE フィールドは SQL_DATETIME に設定されます。また、APD の *parameternumber* レコードの SQL_DESC_CONCISE_TYPE フィールドは、簡潔な datetime C データ型に設定され、 *parameternumber* レコードの SQL_DESC_DATETIME_INTERVAL_CODE フィールドは特定の datetime データ型のサブコードに設定されます。 (「 [付録 D: データ型](../../../odbc/reference/appendixes/appendix-d-data-types.md)」を参照してください)。  
  
 *ValueType* 引数が SQL_C_NUMERIC のデータ型の場合、既定の有効桁数 (ドライバー定義) と、APD の SQL_DESC_PRECISION と SQL_DESC_SCALE のフィールドに設定されている既定の小数点以下桁数 (0) がデータに使用されます。 既定の有効桁数または小数点以下桁数が適切でない場合は、アプリケーションで明示的に記述子フィールドを **SQLSetDescField** または **SQLSetDescRec** の呼び出しによって設定する必要があります。  
  
 SQL_C_DEFAULT は、 *ParameterType* で指定された SQL データ型の既定の C データ型からパラメーター値が転送されることを指定します。  
  
 拡張 C データ型を指定することもできます。 詳細については、「 [ODBC の C データ型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)」を参照してください。  
  
 詳細については、「付録 D: データ型」の「 [既定の c データ型](../../../odbc/reference/appendixes/default-c-data-types.md)」、「 [データを c から sql データ型に変換する](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)」、および「 [データを sql から c データ型に変換](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) する」を参照してください。  
  
## <a name="parametertype-argument"></a>ParameterType 引数

 これは、「付録 D: データ型」の「 [SQL データ型](../../../odbc/reference/appendixes/sql-data-types.md) 」セクションに記載されている値のいずれかであるか、またはドライバー固有の値である必要があります。 この引数は、IPD の SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE、および SQL_DESC_DATETIME_INTERVAL_CODE フィールドを設定します。  
  
 *ParameterType* 引数が datetime 識別子の1つである場合、IPD の SQL_DESC_TYPE フィールドは SQL_DATETIME に設定され、IPD の SQL_DESC_CONCISE_TYPE フィールドは簡潔な datetime SQL データ型に設定され、SQL_DESC_DATETIME_INTERVAL_CODE フィールドは適切な datetime サブコード値に設定されます。  
  
 *ParameterType* が間隔識別子の1つである場合、IPD の SQL_DESC_TYPE フィールドは SQL_INTERVAL に設定され、IPD の SQL_DESC_CONCISE_TYPE フィールドは簡潔な SQL interval データ型に設定され、IPD の SQL_DESC_DATETIME_INTERVAL_CODE フィールドは適切な間隔サブコードに設定されます。 IPD の [SQL_DESC_DATETIME_INTERVAL_PRECISION] フィールドは、間隔の先頭の有効桁数に設定され、[SQL_DESC_PRECISION] フィールドは [間隔 (秒)] の有効桁数 (該当する場合) に設定されます。 SQL_DESC_DATETIME_INTERVAL_PRECISION または SQL_DESC_PRECISION の既定値が適切でない場合は、 **SQLSetDescField** を呼び出すことによって、アプリケーションで明示的に設定する必要があります。 これらのフィールドの詳細については、「 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)」を参照してください。  
  
 *ValueType* 引数が SQL_NUMERIC のデータ型の場合、既定の有効桁数 (ドライバー定義) と、IPD の SQL_DESC_PRECISION と SQL_DESC_SCALE のフィールドに設定されている既定の小数点以下桁数 (0) がデータに使用されます。 既定の有効桁数または小数点以下桁数が適切でない場合は、アプリケーションで明示的に記述子フィールドを **SQLSetDescField** または **SQLSetDescRec** の呼び出しによって設定する必要があります。  
  
 データの変換方法の詳細については、「付録 D: データ型」の「データを [c から Sql データ型に](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) 変換する」および「 [データを Sql から C データ型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) に変換する」を参照してください。  
  
## <a name="columnsize-argument"></a>ColumnSize 引数

 *Columnsize* 引数は、パラメーターマーカー、そのデータの長さ、またはその両方に対応する列または式のサイズを指定します。 この引数は、SQL データ型 ( *ParameterType* 引数) に応じて、IPD のさまざまなフィールドを設定します。 このマッピングには、次の規則が適用されます。  
  
-   *ParameterType* が SQL_CHAR、SQL_VARCHAR、SQL_LONGVARCHAR、SQL_BINARY、SQL_VARBINARY、SQL_LONGVARBINARY、または簡潔な SQL datetime データ型または interval データ型の1つである場合、IPD の SQL_DESC_LENGTH フィールドは *columnsize* の値に設定されます。 (詳細については、「付録 D: データ型」の [列のサイズ、10進数、転送オクテットの長さ、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) に関するセクションを参照してください)。  
  
-   *ParameterType* が SQL_DECIMAL、SQL_NUMERIC、SQL_FLOAT、SQL_REAL、または SQL_DOUBLE の場合、IPD の SQL_DESC_PRECISION フィールドは *columnsize* の値に設定されます。  
  
-   その他のデータ型の場合、 *Columnsize* 引数は無視されます。  
  
 詳細については、「パラメーター値の引き渡し」と「 *StrLen_or_IndPtr* 引数」の SQL_DATA_AT_EXEC を参照してください。  
  
## <a name="decimaldigits-argument"></a>DecimalDigits 引数

 *ParameterType* が SQL_TYPE_TIME、SQL_TYPE_TIMESTAMP、SQL_INTERVAL_SECOND、SQL_INTERVAL_DAY_TO_SECOND、SQL_INTERVAL_HOUR_TO_SECOND、または SQL_INTERVAL_MINUTE_TO_SECOND の場合、IPD の SQL_DESC_PRECISION フィールドは *DecimalDigits* に設定されます。 *ParameterType* が SQL_NUMERIC または SQL_DECIMAL の場合、IPD の SQL_DESC_SCALE フィールドは *DecimalDigits* に設定されます。 その他のすべてのデータ型では、 *DecimalDigits* 引数は無視されます。  
  
## <a name="parametervalueptr-argument"></a>ParameterValuePtr 引数

 *Parametervalueptr* 引数は、 **Sqlexecute** または **SQLExecDirect** が呼び出されたときにパラメーターの実際のデータを格納するバッファーを指します。 データは、 *ValueType* 引数で指定された形式である必要があります。 この引数は、APD の SQL_DESC_DATA_PTR フィールドを設定します。 アプリケーションでは、 *\* StrLen_or_IndPtr* が SQL_NULL_DATA または SQL_DATA_AT_EXEC である限り、 *parametervalueptr* 引数を null ポインターに設定できます。 (これは、入力パラメーターまたは入出力パラメーターにのみ適用されます)。  
  
 \* *StrLen_or_IndPtr* が SQL_LEN_DATA_AT_EXEC ( *長さ* ) マクロまたは SQL_DATA_AT_EXEC の結果である場合、 *parametervalueptr* は、パラメーターに関連付けられたアプリケーション定義のポインター値です。 **Sqlparamdata** を使用してアプリケーションに返されます。 たとえば、 *Parametervalueptr* は、パラメーター番号、データへのポインター、またはアプリケーションが入力パラメーターをバインドするために使用する構造体へのポインターなど、0以外のトークンである場合があります。 ただし、パラメーターが入力/出力パラメーターの場合、 *Parametervalueptr* は出力値が格納されるバッファーへのポインターである必要があることに注意してください。 SQL_ATTR_PARAMSET_SIZE statement 属性の値が1より大きい場合、アプリケーションは、 *Parametervalueptr* 引数と共に、SQL_ATTR_PARAMS_PROCESSED_PTR statement 属性が指す値を使用できます。 たとえば、 *Parametervalueptr* は値の配列を指す場合があり、アプリケーションは SQL_ATTR_PARAMS_PROCESSED_PTR が指す値を使用して、配列から正しい値を取得することがあります。 詳細については、このセクションで後述する「パラメーター値の引き渡し」を参照してください。  
  
 *Inputoutputtype* 引数が SQL_PARAM_INPUT_OUTPUT または SQL_PARAM_OUTPUT の場合、 *parametervalueptr* は、ドライバーが出力値を返すバッファーをポイントします。 プロシージャが1つ以上の結果セットを返す場合、 \* *parametervalueptr* バッファーは、すべての結果セット/行カウントが処理されるまで設定されることは保証されません。 処理が完了するまでバッファーが設定されていない場合は、 **Sqlmoreresults** が SQL_NO_DATA を返すまで、出力パラメーターと戻り値は使用できません。 SQL_CLOSE オプションを指定して **SqlcloSQLFreeStmt** または **SQLFreeStmt** を呼び出すと、これらの値が破棄されます。  
  
 SQL_ATTR_PARAMSET_SIZE statement 属性の値が1より大きい場合、 *Parametervalueptr* は配列を指します。 1つの SQL ステートメントは、入力パラメーターまたは入出力パラメーターの入力値の配列全体を処理し、入力/出力パラメーターまたは出力パラメーターの出力値の配列を返します。  
  
## <a name="bufferlength-argument"></a>BufferLength 引数

 文字およびバイナリ C データの場合、 *Bufferlength* 引数は \* *parametervalueptr* バッファーの長さ (1 つの要素の場合) または \* *parametervalueptr* 配列内の要素の長さ (SQL_ATTR_PARAMSET_SIZE statement 属性の値が1より大きい場合) を指定します。 この引数は、APD の SQL_DESC_OCTET_LENGTH レコードフィールドを設定します。 アプリケーションで複数の値が指定されている場合は、入力時と出力時の両方で、* *Parametervalueptr* 配列内の値の場所を決定するために *bufferlength* が使用されます。 入力/出力パラメーターおよび出力パラメーターの場合は、出力時に文字とバイナリ C データを切り捨てるかどうかを決定するために使用されます。  
  
-   文字 C データの場合、返される使用可能なバイト数が *Bufferlength* 以上の場合、 \* *parametervalueptr* 内のデータは、null 終端文字の長さを下回る *bufferlength* に切り捨てられ、ドライバーによって null で終了されます。  
  
-   バイナリ C データの場合、返すことのできるバイト数が *bufferlength* よりも大きい場合、 \* *parametervalueptr* 内のデータは *bufferlength* バイトに切り捨てられます。  
  
 その他すべての種類の C データでは、 *Bufferlength* 引数は無視されます。 \* *Parametervalueptr* バッファーの長さ (1 つの要素の場合) または \* *parametervalueptr* 配列内の要素の長さ (アプリケーションが、各パラメーターに複数の値を指定するために SQL_ATTR_PARAMSET_SIZE の *属性* 引数を使用して **SQLSetStmtAttr** を呼び出す場合) は、C データ型の長さであると想定されます。  
  
 ストリーム出力またはストリーム入出力パラメーターでは、バッファー長が **SQLGetData** で指定されているため、 *bufferlength* 引数は無視されます。  
  
> [!NOTE]  
>  ODBC 1.0 アプリケーションが ODBC 3 で **SQLSetParam** を呼び出す場合。 *x* ドライバーは、ドライバーマネージャーがこれを **SQLBindParameter** への呼び出しに変換します。この呼び出しで、 *bufferlength* 引数は常に SQL_SETPARAM_VALUE_MAX ます。 ODBC 3 の場合、ドライバーマネージャーはエラーを返します。 *x* アプリケーションは、 *bufferlength* を SQL_SETPARAM_VALUE_MAX (ODBC 3) に設定します。 *x* ドライバーはこれを使用して、ODBC 1.0 アプリケーションによっていつ呼び出されるかを判断できます。  
  
> [!NOTE]  
>  **SQLSetParam** では、アプリケーションが * *parametervalueptr* バッファーの長さを指定して、ドライバーが文字またはバイナリデータを返すことができるようにします。また、アプリケーションが文字またはバイナリのパラメーター値の配列をドライバーに送信する方法は、ドライバーによって定義されます。  
  
## <a name="strlen_or_indptr-argument"></a>StrLen_or_IndPtr 引数

 *StrLen_or_IndPtr* 引数は、 **Sqlexecute** または **SQLExecDirect** が呼び出されたときに、次のいずれかが含まれているバッファーを指します。 (この引数は、アプリケーションパラメーターポインターの SQL_DESC_OCTET_LENGTH_PTR および SQL_DESC_INDICATOR_PTR レコードフィールドを設定します)。  
  
-   * *Parametervalueptr* に格納されているパラメーター値の長さ。 これは、文字またはバイナリ C データを除いて無視されます。  
  
-   SQL_NTS。 パラメーター値は、null で終わる文字列です。  
  
-   SQL_NULL_DATA。 パラメーター値が NULL です。  
  
-   SQL_DEFAULT_PARAM。 プロシージャは、アプリケーションから取得した値の代わりに、パラメーターの既定値を使用します。 この値は、ODBC 正規表現で呼び出されたプロシージャ内でのみ有効で、 *Inputoutputtype* 引数が SQL_PARAM_INPUT、SQL_PARAM_INPUT_OUTPUT、または SQL_PARAM_INPUT_OUTPUT_STREAM の場合にのみ有効です。 \* *StrLen_or_IndPtr* が SQL_DEFAULT_PARAM 場合、入力パラメーターの *ValueType* 、 *ParameterType* 、 *Columnsize* 、 *DecimalDigits* 、 *bufferlength* 、 *parametervalueptr* の各引数は無視され、入力パラメーターと出力パラメーターの出力パラメーター値を定義するためにのみ使用されます。  
  
-   SQL_LEN_DATA_AT_EXEC ( *長さ* ) マクロの結果。 パラメーターのデータは **Sqlputdata** と共に送信されます。 *ParameterType* 引数が SQL_LONGVARBINARY、SQL_LONGVARCHAR、または長いデータソース固有のデータ型で、ドライバーが **SQLGetInfo** の SQL_NEED_LONG_DATA_LEN 情報型に対して "Y" を返す場合、 *length* は、パラメーターに送信されるデータのバイト数です。それ以外の場合、 *長さ* は負でない値である必要があり、無視されます。 詳細については、このセクションの後の「パラメーター値の引き渡し」を参照してください。  
  
     たとえば、1つまたは複数の SQL_LONGVARCHAR 呼び出しで **Sqlputdata** と共に1万バイトのデータを送信するように指定するには、アプリケーションで * *StrLen_or_IndPtr* を SQL_LEN_DATA_AT_EXEC (10000) に設定します。  
  
-   SQL_DATA_AT_EXEC。 パラメーターのデータは **Sqlputdata** と共に送信されます。 この値は、odbc 1.0 アプリケーションが ODBC 3 を呼び出すときに使用されます。 *x* ドライバー。 詳細については、このセクションの後の「パラメーター値の引き渡し」を参照してください。  
  
 *StrLen_or_IndPtr* が null ポインターの場合、ドライバーは、すべての入力パラメーター値が null ではなく、文字とバイナリデータが null で終わることを前提としています。 *Inputoutputtype* が SQL_PARAM_OUTPUT または SQL_PARAM_OUTPUT_STREAM と *parametervalueptr* と *StrLen_or_IndPtr* が両方とも null ポインターの場合、ドライバーは出力値を破棄します。  
  
> [!NOTE]  
>  アプリケーション開発者は、パラメーターのデータ型が SQL_C_BINARY 場合に *StrLen_or_IndPtr* に null ポインターを指定しないことを強くお勧めします。 ドライバーによって SQL_C_BINARY データが予期せず切り捨てられないようにするには、 *StrLen_or_IndPtr* に有効な長さの値へのポインターが含まれている必要があります。  
  
 *Inputoutputtype* 引数が SQL_PARAM_INPUT_OUTPUT、SQL_PARAM_OUTPUT、SQL_PARAM_INPUT_OUTPUT_STREAM、または SQL_PARAM_OUTPUT_STREAM の場合、 *StrLen_or_IndPtr* は、ドライバーが返すバッファー、parametervalueptr で返すことができるバイト数 \* *ParameterValuePtr* (文字データの NULL 終端バイトを除く)、または SQL_NULL_DATA (返されるバイト数を決定できない場合) を指します。 プロシージャが1つ以上の結果セットを返す場合、* *StrLen_or_IndPtr* バッファーは、すべての結果がフェッチされるまで設定されることは保証されません。  
  
 SQL_ATTR_PARAMSET_SIZE statement 属性の値が1より大きい場合、 *StrLen_or_IndPtr* は SQLLEN 値の配列を指します。 これらは、このセクションで前に示したいずれかの値にすることができ、1つの SQL ステートメントで処理されます。  
  
## <a name="passing-parameter-values"></a>パラメーター値の引き渡し

 アプリケーションは、 \* *parametervalueptr* バッファーまたは **sqlputdata** への1回以上の呼び出しでパラメーターの値を渡すことができます。 データが **Sqlputdata** と共に渡されるパラメーターは、 *実行時データ* パラメーターと呼ばれます。 これらは通常、SQL_LONGVARBINARY および SQL_LONGVARCHAR パラメーターのデータを送信するために使用され、他のパラメーターと組み合わせることができます。  
  
 パラメーター値を渡すために、アプリケーションは次の一連の手順を実行します。  
  
1.  各パラメーターの **SQLBindParameter** を呼び出して、パラメーターの値 ( *parametervalueptr* 引数) と長さ/インジケーター ( *StrLen_or_IndPtr* 引数) のバッファーをバインドします。 実行時データパラメーターでは、 *Parametervalueptr* は、パラメーター番号やデータへのポインターなどのアプリケーション定義のポインター値です。 値は後で返され、パラメーターを識別するために使用できます。  
  
2.  入力パラメーターと入出力パラメーターの値を \* *parametervalueptr* および * *StrLen_or_IndPtr* バッファーに配置します。  
  
    -   通常のパラメーターの場合、アプリケーションはパラメーター値を \* *parametervalueptr* バッファーに、その値の長さを * *StrLen_or_IndPtr* バッファーに配置します。 詳細については、「 [パラメーター値の設定](../../../odbc/reference/develop-app/setting-parameter-values.md)」を参照してください。  
  
    -   実行時データパラメーターの場合、アプリケーションは * *StrLen_or_IndPtr* バッファー内の SQL_LEN_DATA_AT_EXEC ( *長さ* ) マクロ (ODBC 2.0 ドライバーを呼び出すとき) の結果を格納します。  
  
3.  SQL ステートメントを実行するには、 **Sqlexecute** または **SQLExecDirect** を呼び出します。  
  
    -   実行時データパラメーターがない場合、プロセスは完了です。  
  
    -   実行時データパラメーターがある場合、関数は SQL_NEED_DATA を返します。  
  
4.  **Sqlparamdata** を呼び出して、 **SQLBindParameter** の *parametervalueptr* 引数で指定されたアプリケーション定義の値を取得し、最初の実行時データパラメーターを処理します。 **Sqlparamdata** は SQL_NEED_DATA を返します。  
  
    > [!NOTE]  
    >  実行時データパラメーターは実行時データ列に似ていますが、 **Sqlparamdata** によって返される値はそれぞれ異なっています。 実行時データパラメーターは、 **SQLExecDirect** または **sqlexecute** を使用してステートメントを実行するときに、 **sqlputdata** を使用してデータを送信する SQL ステートメントのパラメーターです。 これらは **SQLBindParameter** にバインドされています。 **Sqlparamdata** によって返される値は、 *Parametervalueptr* 引数の **SQLBindParameter** に渡されるポインター値です。 実行時データ列とは、行が更新されたとき、または **Sqlputdata** で更新されたとき、または **SQLSetPos** で更新されたときに、データが **sqlputdata** と共に送信される行セット内の列です。 これらは **SQLBindCol** にバインドされています。 **Sqlparamdata** によって返される値は、処理される * *targetvalueptr* バッファー ( **SQLBindCol** の呼び出しで設定される) の行のアドレスです。  
  
5.  **Sqlputdata** を1回以上呼び出して、パラメーターのデータを送信します。 データ値が \* **sqlputdata** に指定されている *parametervalueptr* バッファーより大きい場合は、複数の呼び出しが必要です。文字、バイナリ、またはデータソース固有のデータ型の列に文字 c データを送信する場合、または文字、バイナリ、またはデータソース固有のデータ型を持つ列にバイナリ c データを送信する場合に限り、同じパラメーターに対して **sqlputdata** を複数回呼び出すことができます。  
  
6.  **Sqlparamdata** を再度呼び出して、すべてのデータがパラメーターとして送信されたことを通知します。  
  
    -   実行時データパラメーターが多くなると、 **Sqlparamdata** は SQL_NEED_DATA を返し、次に実行時データパラメーターのアプリケーション定義値を処理します。 アプリケーションは、手順4と5を繰り返します。  
  
    -   実行時データパラメーターがこれ以上ない場合は、プロセスが完了します。 ステートメントが正常に実行された場合、 **Sqlparamdata** は SQL_SUCCESS または SQL_SUCCESS_WITH_INFO を返します。実行が失敗した場合は SQL_ERROR を返します。 この時点で、 **Sqlparamdata** は、ステートメントの実行に使用される関数 ( **SQLExecDirect** または **sqlexecute** ) によって返されるすべての SQLSTATE を返すことができます。  
  
         入力/出力パラメーターまたは出力パラメーターの出力値は、 \* アプリケーションがステートメントによって生成されたすべての結果セットを取得した後に、 *parametervalueptr* および * *StrLen_or_IndPtr* バッファーで使用できます。  
  
 **Sqlexecute** または **SQLExecDirect** を呼び出すと、ステートメントが SQL_NEED_DATA 状態になります。 この時点で、アプリケーションは、ステートメントまたはステートメントに関連付けられている *接続ハンドル* を使用して、 **SQLCancel** 、 **SQLGetDiagField** 、 **SQLGetDiagRec** 、 **Sqlgetfunctions** 、 **sqlgetfunctions** 、または **sqlgetfunctions** だけを呼び出すことができます。 ステートメントまたはステートメントに関連付けられた接続を使用して他の関数を呼び出す場合、関数は SQLSTATE HY010 (関数シーケンスエラー) を返します。 **Sqlparamdata** または **sqlparamdata** からエラーが返された場合、 **sqlparamdata** が SQL_SUCCESS または SQL_SUCCESS_WITH_INFO を返した場合、またはステートメントが取り消された場合、ステートメントは SQL_NEED_DATA 状態を保持します。  
  
 アプリケーションが **SQLCancel** を呼び出しても、ドライバーが実行時データパラメーターのデータを必要としている場合、ドライバーはステートメントの実行を取り消します。その後、アプリケーションは **Sqlexecute** または **SQLExecDirect** を再度呼び出すことができます。  
  
## <a name="retrieving-streamed-output-parameters"></a>ストリーム出力パラメーターの取得

 アプリケーションが *Inputoutputtype* を SQL_PARAM_INPUT_OUTPUT_STREAM または SQL_PARAM_OUTPUT_STREAM に設定する場合は、 **SQLGetData** の1回以上の呼び出しによって出力パラメーターの値を取得する必要があります。 ドライバーがストリーム出力パラメーターの値を保持してアプリケーションに戻ると、 **Sqlmoreresults** 、 **Sqlexecute** 、 **SQLExecDirect** の各関数の呼び出しに応答して SQL_PARAM_DATA_AVAILABLE が返されます。 アプリケーションは **Sqlparamdata** を呼び出して、使用可能なパラメーター値を判別します。  
  
 SQL_PARAM_DATA_AVAILABLE およびストリーム出力パラメーターの詳細については、「 [SQLGetData を使用した出力パラメーターの取得](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)」を参照してください。  
  
## <a name="using-arrays-of-parameters"></a>パラメーターの配列の使用

 アプリケーションでパラメーターマーカーを含むステートメントを準備し、パラメーターの配列を渡すと、2つの異なる方法で実行できます。 1つの方法は、ドライバーがバックエンドの配列処理機能に依存している場合です。この場合、パラメーターの配列を持つステートメント全体が1つのアトミック単位として扱われます。 Oracle は、配列処理機能をサポートするデータソースの一例です。 この機能を実装するもう1つの方法は、ドライバーが SQL ステートメントのバッチを生成し、パラメーター配列内のパラメーターのセットごとに1つの SQL ステートメントを生成し、バッチを実行することです。 パラメーターの配列は、 **UPDATE WHERE CURRENT** ステートメントと共に使用することはできません。  
  
 パラメーターの配列が処理されると、個々の結果セット/行数 (パラメーターセットごとに1つ) を使用できるようになります。また、結果セット/行数を1つにロールアップできます。 **SQLGetInfo** の SQL_PARAM_ARRAY_ROW_COUNTS オプションは、各パラメーターセット (SQL_PARC_BATCH) に対して行数が使用可能かどうか、または1つの行カウントしか使用できない (SQL_PARC_NO_BATCH) かどうかを示します。  
  
 **SQLGetInfo** の SQL_PARAM_ARRAY_SELECTS オプションは、一連のパラメーター (SQL_PAS_BATCH) に対して結果セットが使用可能かどうか、または1つの結果セットのみが使用可能である (SQL_PAS_NO_BATCH) かどうかを示します。 パラメーターの配列を使用して結果セット生成ステートメントを実行することがドライバーで許可されていない場合、SQL_PARAM_ARRAY_SELECTS は SQL_PAS_NO_SELECT を返します。  
  
 詳細については、「 [SQLGetInfo 関数](../../../odbc/reference/syntax/sqlgetinfo-function.md)」を参照してください。  
  
 パラメーターの配列をサポートするには、各パラメーターの値の数を指定するように SQL_ATTR_PARAMSET_SIZE statement 属性を設定します。 フィールドが1より大きい場合は、APD の SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、および SQL_DESC_OCTET_LENGTH_PTR フィールドが配列を指す必要があります。 各配列のカーディナリティは、SQL_ATTR_PARAMSET_SIZE の値と同じです。  
  
 APD の [SQL_DESC_ROWS_PROCESSED_PTR] フィールドは、エラーセットを含む、処理されたパラメーターのセットの数を含むバッファーを指します。 各パラメーターのセットが処理されると、ドライバーは新しい値をバッファーに格納します。 Null ポインターの場合、数値は返されません。 パラメーターの配列を使用すると、設定関数によって SQL_ERROR が返された場合でも、APD の SQL_DESC_ROWS_PROCESSED_PTR フィールドが指す値が設定されます。 SQL_NEED_DATA が返された場合、APD の SQL_DESC_ROWS_PROCESSED_PTR フィールドが指す値は、処理されるパラメーターのセットに設定されます。  
  
 パラメーターの配列がバインドされ、現在のステートメントが実行されて **いる更新プログラム** がドライバーによって定義されている場合はどうなりますか。  
  
## <a name="column-wise-parameter-binding"></a>Column-Wise パラメーターのバインド

 列方向のバインドでは、アプリケーションによって、個別のパラメーターと長さ/インジケーター配列が各パラメーターにバインドされます。  
  
 列方向のバインドを使用するには、まず、アプリケーションで SQL_ATTR_PARAM_BIND_TYPE statement 属性を SQL_PARAM_BIND_BY_COLUMN に設定します。 (これが既定値です)。バインドされる各列に対して、アプリケーションは次の手順を実行します。  
  
1.  パラメーターバッファー配列を割り当てます。  
  
2.  長さ/インジケーターバッファーの配列を割り当てます。  
  
    > [!NOTE]  
    >  列方向のバインドを使用するときにアプリケーションが記述子に直接書き込む場合は、長さとインジケーターデータに個別の配列を使用できます。  
  
3.  次の引数を使用して **SQLBindParameter** を呼び出します。  
  
    -   *ValueType* は、パラメーターバッファー配列内の1つの要素の C 型です。  
  
    -   *ParameterType* は、パラメーターの SQL 型です。  
  
    -   *Parametervalueptr* は、パラメーターバッファー配列のアドレスです。  
  
    -   *Bufferlength* は、パラメーターバッファー配列内の1つの要素のサイズです。 *Bufferlength* 引数は、データが固定長データの場合は無視されます。  
  
    -   *StrLen_or_IndPtr* は、長さ/インジケーター配列のアドレスです。  
  
 この情報の使用方法の詳細については、このセクションで後述する「コメント」の「ParameterValuePtr 引数」を参照してください。 パラメーターの列方向のバインドの詳細については、「 [パラメーターの配列のバインド](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)」を参照してください。  
  
## <a name="row-wise-parameter-binding"></a>Row-Wise パラメーターのバインド

 行方向のバインドでは、アプリケーションは、バインドされる各パラメーターのパラメーターと長さ/インジケーターバッファーを含む構造体を定義します。  
  
 行方向のバインドを使用するために、アプリケーションは次の手順を実行します。  
  
1.  パラメーターの1つのセット (パラメーターと長さ/インジケーターバッファーを含む) を保持する構造体を定義し、これらの構造体の配列を割り当てます。  
  
    > [!NOTE]  
    >  行方向のバインドを使用するときにアプリケーションが記述子に直接書き込む場合は、長さとインジケーターデータに個別のフィールドを使用できます。  
  
2.  SQL_ATTR_PARAM_BIND_TYPE ステートメントの属性を、パラメーターの1つのセットを含む構造体のサイズ、またはパラメーターがバインドされるバッファーのインスタンスのサイズに設定します。 長さには、バインドされているすべてのパラメーターの領域と、構造体またはバッファーの埋め込みを含める必要があります。バインドされたパラメーターのアドレスが指定された長さでインクリメントされると、結果は次の行の同じパラメーターの先頭を指します。 ANSI C で *sizeof* 演算子を使用すると、この動作は保証されます。  
  
3.  は、バインドされる各パラメーターに対して次の引数を指定して **SQLBindParameter** を呼び出します。  
  
    -   *ValueType* は、列にバインドされるパラメーターバッファーメンバーの種類です。  
  
    -   *ParameterType* は、パラメーターの SQL 型です。  
  
    -   *Parametervalueptr* は、最初の配列要素内のパラメーターバッファーメンバーのアドレスです。  
  
    -   *Bufferlength* は、パラメーターバッファーメンバーのサイズです。  
  
    -   *StrLen_or_IndPtr* は、バインドされる長さ/インジケーターメンバーのアドレスです。  
  
 この情報の使用方法の詳細については、このセクションで後述する「 *Parametervalueptr* 引数」を参照してください。 パラメーターの行方向のバインドの詳細については、「 [パラメーターのバインド配列](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)」を参照してください。  
  
## <a name="error-information"></a>エラー情報

 ドライバーがパラメーター配列をバッチとして実装していない場合 (SQL_PARAM_ARRAY_ROW_COUNTS オプションは SQL_PARC_NO_BATCH)、1つのステートメントが実行されたかのようにエラー状況が処理されます。 ドライバーがパラメーター配列をバッチとして実装している場合、アプリケーションでは、IPD の SQL_DESC_ARRAY_STATUS_PTR ヘッダーフィールドを使用して、SQL ステートメントのパラメーターまたはパラメーターの配列内のパラメーターによって、 **SQLExecDirect** または **sqlexecute** がエラーを返す原因を特定できます。 このフィールドには、パラメーター値の各行の状態情報が含まれます。 フィールドがエラーが発生したことを示している場合、診断データ構造内のフィールドは、失敗したパラメーターの行とパラメーター番号を示します。 配列内の要素の数は、APD の SQL_DESC_ARRAY_SIZE header フィールドによって定義されます。このフィールドは、SQL_ATTR_PARAMSET_SIZE statement 属性で設定できます。  
  
> [!NOTE]  
>  APD の SQL_DESC_ARRAY_STATUS_PTR header フィールドは、パラメーターを無視するために使用されます。 パラメーターを無視する方法の詳細については、次の「パラメーターのセットを無視する」を参照してください。  
  
 **Sqlexecute** または **SQLExecDirect** が SQL_ERROR を返すと、IPD の SQL_DESC_ARRAY_STATUS_PTR フィールドが指す配列内の要素には、SQL_PARAM_ERROR、SQL_PARAM_SUCCESS、SQL_PARAM_SUCCESS_WITH_INFO、SQL_PARAM_UNUSED、または SQL_PARAM_DIAG_UNAVAILABLE が格納されます。  
  
 この配列内の各要素について、診断データ構造に1つ以上の状態レコードが含まれています。 構造体の SQL_DIAG_ROW_NUMBER フィールドは、エラーの原因となったパラメーター値の行番号を示します。 エラーの原因となったパラメーターの行で特定のパラメーターを特定できる場合は、[SQL_DIAG_COLUMN_NUMBER] フィールドにパラメーター番号が入力されます。  
  
 パラメーターが使用されていないときに SQL_PARAM_UNUSED が入力されます。これは、 **Sqlexecute** または **SQLExecDirect** を強制的に中止する前のパラメーターでエラーが発生したためです。 たとえば、50パラメーターがあり、 **Sqlexecute** または **SQLExecDirect** の中止の原因となったパラメーターの fortieth セットの実行中にエラーが発生した場合、SQL_PARAM_UNUSED は、パラメーター 41 ~ 50 の状態配列に入力されます。  
  
 ドライバーがパラメーターの配列をモノリシック単位として処理するときに SQL_PARAM_DIAG_UNAVAILABLE が入力されるため、この個別のパラメーターレベルのエラー情報は生成されません。  
  
 パラメーターの1つのセットの処理中にエラーが発生すると、配列内の後続のパラメーターセットの処理が停止します。 その他のエラーは、後続のパラメーターの処理には影響しません。 処理を停止するエラーはドライバーで定義されています。 処理が停止されていない場合は、配列内のすべてのパラメーターが処理され、エラーの結果として返さ SQL_SUCCESS_WITH_INFO が返されます。 SQL_ATTR_PARAMS_PROCESSED_PTR によって定義されるバッファーは、エラーセットを含む、SQL_ATTR_PARAMSET_SIZE statement 属性で定義されているように処理されたパラメーターのセットの合計数に設定されます。  
  
> [!CAUTION]  
>  Odbc 3 では、パラメーターの配列の処理でエラーが発生した場合の ODBC 動作が異なります。 *x* は ODBC 2 ではありませんでした。 *x* 。 ODBC 2 の場合。 *x* 関数は SQL_ERROR を返し、なったを処理します。 **Sqlparamoptions** の *pirow* 引数によってポイントされたバッファーには、エラー行の番号が含まれていました。 ODBC 3 の場合。 *x* 関数は、SQL_SUCCESS_WITH_INFO を返し、処理を停止するか続行するかを指定します。 続行すると、SQL_ATTR_PARAMS_PROCESSED_PTR によって指定されたバッファーは、エラーの原因となったすべてのパラメーターを含む、処理されたすべてのパラメーターの値に設定されます。 この動作の変更により、既存のアプリケーションで問題が発生する可能性があります。  
  
 SQL_ERROR や SQL_NEED_DATA が返されたときなど、パラメーター配列内のすべてのパラメーターセットの処理が完了する前に **Sqlexecute** または **SQLExecDirect** が返された場合、状態配列には既に処理されているパラメーターの状態が含まれます。 IPD の SQL_DESC_ROWS_PROCESSED_PTR フィールドが指す位置には、SQL_ERROR または SQL_NEED_DATA エラーコードの原因となったパラメーター配列内の行番号が含まれています。 パラメーターの配列が SELECT ステートメントに送信されると、状態配列値の可用性はドライバーで定義されます。ステートメントが実行された後、または結果セットがフェッチされた後に使用できる場合があります。  
  
## <a name="ignoring-a-set-of-parameters"></a>パラメーターのセットを無視します。

 (SQL_ATTR_PARAM_STATUS_PTR statement 属性によって設定された) APD の SQL_DESC_ARRAY_STATUS_PTR フィールドを使用すると、SQL ステートメント内のバインドされたパラメーターのセットを無視するように指定できます。 実行中にドライバーが1つ以上のパラメーターを無視するように指定するには、アプリケーションで次の手順を実行する必要があります。  
  
1.  **SQLSetDescField** を呼び出して、APD の SQL_DESC_ARRAY_STATUS_PTR ヘッダーフィールドを、ステータス情報を含む SQLUS悪意のある値の配列を指すように設定します。 このフィールドは、SQL_ATTR_PARAM_OPERATION_PTR の *属性* を指定して **SQLSetStmtAttr** を呼び出すことによって設定することもできます。これにより、アプリケーションは記述子ハンドルを取得せずにフィールドを設定できます。  
  
2.  APD の [SQL_DESC_ARRAY_STATUS_PTR] フィールドによって定義された配列の各要素を、次の2つの値のいずれかに設定します。  
  
    -   SQL_PARAM_IGNORE、行がステートメントの実行から除外されることを示します。  
  
    -   SQL_PARAM_PROCEED、行がステートメントの実行に含まれることを示します。  
  
3.  **SQLExecDirect** または **sqlexecute** を呼び出して、準備されたステートメントを実行します。  
  
 APD の SQL_DESC_ARRAY_STATUS_PTR フィールドで定義されている配列には、次の規則が適用されます。  
  
-   既定では、ポインターは null に設定されています。  
  
-   ポインターが null の場合は、すべての要素が SQL_ROW_PROCEED に設定されているかのように、すべてのパラメーターセットが使用されます。  
  
-   要素を SQL_PARAM_PROCEED に設定しても、その特定のパラメーターセットを操作で使用することは保証されません。  
  
-   ヘッダーファイルでは、SQL_PARAM_PROCEED は0として定義されます。  
  
 アプリケーションでは、APD の SQL_DESC_ARRAY_STATUS_PTR フィールドを、IRD の SQL_DESC_ARRAY_STATUS_PTR フィールドが指すものと同じ配列を指すように設定できます。 これは、パラメーターを行データにバインドするときに便利です。 その後、行データの状態に応じて、パラメーターを無視できます。 SQL_PARAM_IGNORE に加えて、次のコードを使用すると、SQL ステートメントのパラメーターが無視されます: SQL_ROW_DELETED、SQL_ROW_UPDATED、および SQL_ROW_ERROR。 SQL_PARAM_PROCEED に加えて、次のコードを実行すると、SQL ステートメントが実行されます。 SQL_ROW_SUCCESS、SQL_ROW_SUCCESS_WITH_INFO、および SQL_ROW_ADDED です。  
  
## <a name="rebinding-parameters"></a>再バインド (パラメーターを)

 アプリケーションでは、次の2つの操作のいずれかを実行して、バインドを変更できます。  
  
-   **SQLBindParameter** を呼び出して、既にバインドされている列の新しいバインドを指定します。 ドライバーは、古いバインディングを新しいもので上書きします。  
  
-   **SQLBindParameter** へのバインド呼び出しで指定されたバッファーアドレスに追加するオフセットを指定します。 詳細については、次の「オフセットによる再バインド」を参照してください。  
  
## <a name="rebinding-with-offsets"></a>オフセットによる再バインド

 パラメーターの再バインドは、多くのパラメーターを含めることができても、 **SQLExecDirect** または **sqlexecute** への呼び出しで使用されるパラメーターの数が少ない場合に、アプリケーションにバッファー領域の設定がある場合に特に便利です。 バッファー領域の残りの領域は、既存のバインドをオフセットによって変更することによって、次のパラメーターのセットに使用できます。  
  
 APD の SQL_DESC_BIND_OFFSET_PTR header フィールドは、バインドオフセットを指します。 フィールドが null 以外の場合、ドライバーはポインターを逆参照し、SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、および SQL_DESC_OCTET_LENGTH_PTR の各フィールドの値が null ポインターでない場合は、実行時に記述子レコードのフィールドに逆参照された値を追加します。 新しいポインター値は、SQL ステートメントの実行時に使用されます。 オフセットは再バインド後も有効なままです。 SQL_DESC_BIND_OFFSET_PTR はオフセット自体ではなくオフセットへのポインターであるため、アプリケーションは [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) または [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md) を呼び出して記述子フィールドを変更することなく、直接オフセットを変更できます。 既定では、ポインターは null に設定されています。 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)の SQL_DESC_BIND_OFFSET_PTR フィールドを設定するには、SQLSetStmtAttr を呼び出します。または、 *fattribute* が SQL_ATTR_PARAM_BIND_OFFSET_PTR の [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)を呼び出します。  
  
 バインドオフセットは、常に、SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、および SQL_DESC_OCTET_LENGTH_PTR の各フィールドの値に直接追加されます。 オフセットが別の値に変更された場合でも、新しい値は各記述子フィールドの値に直接追加されます。 新しいオフセットは、フィールド値とそれ以前のオフセットの合計には追加されません。  
  
## <a name="descriptors"></a>記述子

 パラメーターのバインド方法は、APDs および IPDs のフィールドによって決まります。 **SQLBindParameter** の引数は、これらの記述子フィールドを設定するために使用されます。 また、 **SQLSetDescField** 関数によってフィールドを設定することもできます。ただし、 **SQLBindParameter** は **SQLBindParameter** を呼び出すための記述子ハンドルを取得する必要がないため、使用する方が効率的です。  
  
> [!CAUTION]  
>  あるステートメントに対して **SQLBindParameter** を呼び出すと、他のステートメントに影響を与える可能性があります。 このエラーは、ステートメントに関連付けられているが明示的に割り当てられ、他のステートメントにも関連付けられている場合に発生します。 **SQLBindParameter** は APD のフィールドを変更するため、この記述子が関連付けられているすべてのステートメントに変更が適用されます。 これが必要な動作でない場合、アプリケーションは、 **SQLBindParameter** を呼び出す前に、他のステートメントとこの記述子の関連付けを解除する必要があります。  
  
 概念的には、 **SQLBindParameter** は次の手順を順番に実行します。  
  
1.  [SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)を呼び出して、APD ハンドルを取得します。  
  
2.  [SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)を呼び出して APD の SQL_DESC_COUNT フィールドを取得します。 *columnnumber* 引数の値が SQL_DESC_COUNT の値を超える場合は、 **SQLSetDescField** を呼び出して、SQL_DESC_COUNT の値を *columnnumber* に増やします。  
  
3.  [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)を複数回呼び出して、APD の次のフィールドに値を割り当てます。  
  
    -   SQL_DESC_TYPE と SQL_DESC_CONCISE_TYPE を *valuetype* の値に設定します。ただし、 *valuetype* が datetime または interval のサブタイプの簡潔な識別子の1つである場合、SQL_DESC_TYPE を SQL_DATETIME または SQL_INTERVAL に設定して、SQL_DESC_CONCISE_TYPE を簡潔な識別子に設定し、SQL_DESC_DATETIME_INTERVAL_CODE を対応する datetime または interval サブコードに設定します。  
  
    -   SQL_DESC_OCTET_LENGTH フィールドを *Bufferlength* の値に設定します。  
  
    -   SQL_DESC_DATA_PTR フィールドを *parametervalue* の値に設定します。  
  
    -   SQL_DESC_OCTET_LENGTH_PTR フィールドを *StrLen_or_Ind* の値に設定します。  
  
    -   SQL_DESC_INDICATOR_PTR フィールドを *StrLen_or_Ind* の値にも設定します。  
  
     *StrLen_or_Ind* パラメーターは、インジケーター情報とパラメーター値の長さの両方を指定します。  
  
4.  [SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)を呼び出して、IPD ハンドルを取得します。  
  
5.  [SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)を呼び出して IPD の SQL_DESC_COUNT フィールドを取得します。 *columnnumber* 引数の値が SQL_DESC_COUNT の値を超える場合は、 **SQLSetDescField** を呼び出して、SQL_DESC_COUNT の値を *columnnumber* に増やします。  
  
6.  [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)を複数回呼び出して、IPD の次のフィールドに値を割り当てます。  
  
    -   SQL_DESC_TYPE と SQL_DESC_CONCISE_TYPE を *ParameterType* の値に設定します。ただし、datetime または interval サブタイプの簡潔な識別子の1つで *ある場合、* SQL_DESC_TYPE を SQL_DATETIME または SQL_INTERVAL に設定し、SQL_DESC_CONCISE_TYPE を簡潔な識別子に設定し、SQL_DESC_DATETIME_INTERVAL_CODE を対応する datetime または interval サブコードに設定します。  
  
    -   *ParameterType* に応じて、SQL_DESC_LENGTH、SQL_DESC_PRECISION、および SQL_DESC_DATETIME_INTERVAL_PRECISION の1つ以上を設定します。  
  
    -   SQL_DESC_SCALE を *DecimalDigits* の値に設定します。  
  
 **SQLBindParameter** の呼び出しが失敗した場合、APD に設定されていた記述子フィールドの内容は未定義になり、APD の SQL_DESC_COUNT フィールドは変更されません。 また、IPD の適切なレコードの SQL_DESC_LENGTH、SQL_DESC_PRECISION、SQL_DESC_SCALE、および SQL_DESC_TYPE の各フィールドは定義されておらず、IPD の SQL_DESC_COUNT フィールドは変更されていません。  
  
## <a name="conversion-of-calls-to-and-from-sqlsetparam"></a>SQLSetParam との間の呼び出しの変換

 ODBC 1.0 アプリケーションが ODBC 3 で **SQLSetParam** を呼び出す場合。 *x* ドライバー (ODBC 3)。 *x* ドライバーマネージャーは、次の表に示すように呼び出しをマップします。  
  
|ODBC 1.0 アプリケーションによる呼び出し|ODBC 3 を呼び出します。 *x* ドライバー|  
|----------------------------------|-------------------------------|  
|SQLSetParam (StatementHandle, ParameterNumber, ValueType, ParameterType, Length Precision, Parameternumber, ParameterValuePtr, StrLen_or_IndPtr);|SQLBindParameter (StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType,      *Columnsize* ,      *DecimalDigits* , parametervalueptr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr);|  
  
## <a name="examples"></a>例  

### <a name="a-use-sqlbindparameter-function"></a>A. SQLBindParameter 関数を使用する

 次の例では、アプリケーションが ORDERS テーブルにデータを挿入するための SQL ステートメントを準備します。 アプリケーションは、ステートメント内のパラメーターごとに、 **SQLBindParameter** を呼び出して、ODBC C データ型とパラメーターの SQL データ型を指定し、バッファーを各パラメーターにバインドします。 アプリケーションは、データの行ごとに、データ値を各パラメーターに割り当て、 **Sqlexecute** を呼び出してステートメントを実行します。  
  
 次の例では、northwind データベースに関連付けられている Northwind という名前の ODBC データソースがコンピューターにあることを前提としています。  
  
 コード例の詳細については、「 [Sqlbulkoperations 関数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)」、「 [sqlprocedures 関数](../../../odbc/reference/syntax/sqlprocedures-function.md)」、「 [sqlbulkoperations 関数](../../../odbc/reference/syntax/sqlputdata-function.md)」、および「 [SQLSetPos 関数](../../../odbc/reference/syntax/sqlsetpos-function.md)」を参照してください。  
  
```cpp
// SQLBindParameter_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqltypes.h>  
#include <sqlext.h>  
  
#define EMPLOYEE_ID_LEN 10  
  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLRETURN retcode;  
SQLHSTMT hstmt = NULL;  
SQLSMALLINT sCustID;  
  
SQLCHAR szEmployeeID[EMPLOYEE_ID_LEN];  
SQL_DATE_STRUCT dsOrderDate;  
SQLINTEGER cbCustID = 0, cbOrderDate = 0, cbEmployeeID = SQL_NTS;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retcode = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, EMPLOYEE_ID_LEN, 0, szEmployeeID, 0, &cbEmployeeID);  
   retcode = SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_SSHORT, SQL_INTEGER, 0, 0, &sCustID, 0, &cbCustID);  
   retcode = SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TIMESTAMP, sizeof(dsOrderDate), 0, &dsOrderDate, 0, &cbOrderDate);  
  
   retcode = SQLPrepare(hstmt, (SQLCHAR*)"INSERT INTO Orders(CustomerID, EmployeeID, OrderDate) VALUES (?, ?, ?)", SQL_NTS);  
  
   strcpy_s((char*)szEmployeeID, _countof(szEmployeeID), "BERGS");  
   sCustID = 5;  
   dsOrderDate.year = 2006;  
   dsOrderDate.month = 3;  
   dsOrderDate.day = 17;  
  
   retcode = SQLExecute(hstmt);  
}  
```  
  
### <a name="b-execute-a-stored-procedure-using-a-named-parameter"></a>B. 名前付きパラメーターを使用してストアドプロシージャを実行する

 次の例では、アプリケーションは名前付きパラメーターを使用して SQL Server ストアドプロシージャを実行します。  
  
```cpp
// SQLBindParameter_Function_2.cpp  
// compile with: ODBC32.lib  
// sample assumes the following stored procedure:  
// use northwind  
// DROP PROCEDURE SQLBindParameter  
// GO  
//   
// CREATE PROCEDURE SQLBindParameter @quote int  
// AS  
// delete from orders where OrderID >= @quote  
// GO  
#include <windows.h>  
#include <sqltypes.h>  
#include <sqlext.h>  
  
SQLHDESC hIpd = NULL;  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLRETURN retcode;  
SQLHSTMT hstmt = NULL;  
SQLCHAR szQuote[50] = "100084";  
SQLINTEGER cbValue = SQL_NTS;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retcode = SQLPrepare(hstmt, (SQLCHAR*)"{call SQLBindParameter(?)}", SQL_NTS);  
   retcode = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 50, 0, szQuote, 0, &cbValue);  
   retcode = SQLGetStmtAttr(hstmt, SQL_ATTR_IMP_PARAM_DESC, &hIpd, 0, 0);  
   retcode = SQLSetDescField(hIpd, 1, SQL_DESC_NAME, "@quote", SQL_NTS);  
  
   retcode = SQLExecute(hstmt);  
}  
```  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|ステートメント内のパラメーターに関する情報を返す|[SQLDescribeParam 関数](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|SQL ステートメントの実行|[SQLExecDirect 関数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|準備された SQL ステートメントの実行|[SQLExecute 関数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|ステートメントのパラメーターバッファーを解放しています|[SQLFreeStmt 関数](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|ステートメントのパラメーターの数を返す|[SQLNumParams 関数](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|データを送信する次のパラメーターを返す|[SQLParamData 関数](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|複数のパラメーター値の指定|[SQLParamOptions 関数](../../../odbc/reference/syntax/sqlparamoptions-function.md)|  
|実行時にパラメーターデータを送信する|[SQLPutData 関数](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>参照

 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダーファイル](../../../odbc/reference/install/odbc-header-files.md)   
 [SQLGetData を使用した出力パラメーターの取得](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
