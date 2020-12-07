---
description: SQLGetData を使用した出力パラメーターの取得
title: SQLGetData | を使用した出力パラメーターの取得Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetData function [ODBC], retrieving output parameters
- output parameters [ODBC]
- retrieving output parameters [ODBC]
ms.assetid: 7a8c298a-2160-491d-a300-d36f45568d9c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a31cb6baa015e2a90977d0112e770ce66fa8e62f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461384"
---
# <a name="retrieving-output-parameters-using-sqlgetdata"></a>SQLGetData を使用した出力パラメーターの取得
ODBC 3.8 より前のアプリケーションでは、バインドされた出力バッファーを持つクエリの出力パラメーターのみを取得できました。 ただし、パラメーター値のサイズが非常に大きい場合 (たとえば、大きなイメージ)、非常に大きなバッファーを割り当てることは困難です。 ODBC 3.8 では、部分的に出力パラメーターを取得する新しい方法が導入されています。 アプリケーションでは、小さなバッファーを使用して **SQLGetData** を複数回呼び出して、大きなパラメーター値を取得できるようになりました。 これは、大きな列データを取得する場合と似ています。  
  
 出力パラメーターまたは入力/出力パラメーターをバインドしてパーツで取得するには、 *Inputoutputtype*引数を SQL_PARAM_OUTPUT_STREAM または SQL_PARAM_INPUT_OUTPUT_STREAM に設定して**SQLBindParameter**を呼び出します。 SQL_PARAM_INPUT_OUTPUT_STREAM では、アプリケーションは **Sqlputdata** を使用してパラメーターにデータを入力し、 **SQLGetData** を使用して出力パラメーターを取得できます。 入力データは、事前に割り当てられたバッファーにバインドするのではなく、 **Sqlputdata** を使用して、実行時データ (DAE) 形式である必要があります。  
  
 この機能は、odbc 3.8 アプリケーションで使用することも、odbc 3.x および ODBC 2.x アプリケーションを再コンパイルすることもできます。また、これらのアプリケーションには、 **SQLGetData** および Odbc 3.8 driver Manager を使用した出力パラメーターの取得をサポートする odbc 3.8 ドライバーが必要です。 古いアプリケーションで新しい ODBC 機能を使用できるようにする方法については、「 [互換性マトリックス](../../../odbc/reference/develop-app/compatibility-matrix.md)」を参照してください。  
  
## <a name="usage-example"></a>使用例  
 たとえば、ストアドプロシージャ **{CALL sp_f (?,?)}** を実行すると、両方のパラメーターが SQL_PARAM_OUTPUT_STREAM としてバインドされ、ストアドプロシージャから結果セットが返されなくなります (このトピックの後半では、より複雑なシナリオについて説明します)。  
  
1.  各パラメーターに対して、 *Inputoutputtype*を SQL_PARAM_OUTPUT_STREAM に設定し、 *parametervalueptr*をトークンに設定して、パラメーター番号、データへのポインター、またはアプリケーションが入力パラメーターをバインドするために使用する構造体へのポインターなどを指定して、 **SQLBindParameter**を呼び出します。 この例では、パラメーター序数をトークンとして使用します。  
  
2.  **SQLExecDirect**または**sqlexecute**を使用してクエリを実行します。 SQL_PARAM_DATA_AVAILABLE が返されます。これは、取得できるストリーム出力パラメーターがあることを示します。  
  
3.  **Sqlparamdata**を呼び出して、取得に使用できるパラメーターを取得します。 **Sqlparamdata** は、 **SQLBindParameter** (ステップ 1) で設定されている最初の使用可能なパラメーターのトークンを使用して SQL_PARAM_DATA_AVAILABLE を返します。 このトークンは、 *Valueptrptr* が指すバッファーで返されます。  
  
4.  引数*Col*_or を指定して**SQLGetData**を呼び出し、 \_ 使用可能な最初のパラメーターのデータを取得するためにパラメーター序数に設定*Param_Num*ます。 **SQLGetData**が SQL_SUCCESS_WITH_INFO と SQLState 01004 (データが切り捨てられました) を返し、型がクライアントとサーバーの両方で可変長の場合は、使用可能な最初のパラメーターからより多くのデータを取得します。 SQL_SUCCESS が返されるまで、または別の**SQLState**で SQL_SUCCESS_WITH_INFO **SQLGetData**を呼び出すことができます。  
  
5.  現在のパラメーターを取得するには、手順 3. と手順 4. を繰り返します。  
  
6.  **Sqlparamdata**を再度呼び出します。 SQL_PARAM_DATA_AVAILABLE 以外のものが返された場合は、取得するストリームパラメーターデータがなく、リターンコードは次に実行されるステートメントのリターンコードになります。  
  
7.  **Sqlmoreresults**を呼び出して、SQL_NO_DATA が返されるまで、次の一連のパラメーターを処理します。 ステートメント属性 SQL_ATTR_PARAMSET_SIZE が1に設定されている場合、 **Sqlmoreresults**はこの例の SQL_NO_DATA を返します。 それ以外の場合は、 **Sqlmoreresults** は SQL_PARAM_DATA_AVAILABLE を返して、取得するパラメーターの次のセットに対して使用できるストリーム出力パラメーターがあることを示します。  
  
 DAE 入力パラメーターと同様に、 **SQLBindParameter** (ステップ 1) の引数*parametervalueptr*で使用されるトークンは、アプリケーションのデータ構造を指すポインターにすることができます。これには、パラメーターの序数と、必要に応じてアプリケーション固有の情報が含まれます。  
  
 返されたストリーム出力または入出力パラメーターの順序はドライバーに固有であり、クエリで指定された順序と常に同じであるとは限りません。  
  
 手順 4. でアプリケーションが **SQLGetData** を呼び出さない場合、パラメーター値は破棄されます。 同様に、すべてのパラメーター値が**SQLGetData**に読み取られる前にアプリケーションが**sqlparamdata**を呼び出すと、値の残りの部分は破棄され、アプリケーションは次のパラメーターを処理できます。  
  
 すべてのストリーム出力パラメーターが処理される前にアプリケーションが **Sqlmoreresults** を呼び出す場合 (**sqlparamdata** は引き続き SQL_PARAM_DATA_AVAILABLE を返します)、残りのすべてのパラメーターは破棄されます。 同様に、すべてのパラメーター値が**SQLGetData**によって読み取られる前にアプリケーションが**Sqlmoreresults**を呼び出すと、残りの値と残りのすべてのパラメーターが破棄され、アプリケーションは次のパラメーターセットの処理を続行できます。  
  
 アプリケーションでは、 **SQLBindParameter** と **SQLGetData**の両方で C データ型を指定できます。 **SQLGetData**で指定された c データ型は、 **SQLGetData**に指定された c データ型が SQL_APD_TYPE でない限り、 **SQLBindParameter**で指定された c データ型よりも優先されます。  
  
 ストリーム出力パラメーターは、出力パラメーターのデータ型が BLOB の場合に便利ですが、この機能は任意のデータ型でも使用できます。 ストリーム出力パラメーターでサポートされるデータ型は、ドライバーで指定されます。  
  
 処理する SQL_PARAM_INPUT_OUTPUT_STREAM パラメーターがある場合は、 **Sqlexecute** または **SQLExecDirect** が最初に SQL_NEED_DATA を返します。 アプリケーションでは、 **Sqlparamdata** と **sqlparamdata** を呼び出して、DAE パラメーターデータを送信できます。 すべての DAE 入力パラメーターが処理されると、 **Sqlparamdata** は、ストリーミングされた出力パラメーターが使用可能であることを示す SQL_PARAM_DATA_AVAILABLE を返します。  
  
 ストリーム出力パラメーターとバインドされた出力パラメーターが処理されると、ドライバーは出力パラメーターの処理順序を決定します。 したがって、出力パラメーターがバッファーにバインドされている場合 ( **SQLBindParameter** パラメーター *inputoutputtype* が SQL_PARAM_INPUT_OUTPUT または SQL_PARAM_OUTPUT に設定されている場合)、 **sqlparamdata** が SQL_SUCCESS または SQL_SUCCESS_WITH_INFO を返すまで、バッファーが設定されない可能性があります。 アプリケーションは、 **Sqlparamdata** が SQL_SUCCESS を返すか、すべてのストリーム出力パラメーターが処理された後である SQL_SUCCESS_WITH_INFO した後にのみ、バインドされたバッファーを読み取る必要があります。  
  
 データソースは、ストリーミングされた出力パラメーターに加えて、警告と結果セットを返すことができます。 一般に、警告と結果セットは、 **Sqlmoreresults**を呼び出すことによって、ストリーミングされた出力パラメーターとは別に処理されます。 ストリーミングされた出力パラメーターを処理する前に、警告と結果セットを処理します。  
  
 次の表では、サーバーに送信される1つのコマンドのさまざまなシナリオと、アプリケーションの動作について説明します。  
  
|シナリオ|SQLExecute または SQLExecDirect からの戻り値|次の作業|  
|--------------|---------------------------------------------------|---------------------|  
|データにはストリーム出力パラメーターのみが含まれます|SQL_PARAM_DATA_AVAILABLE|**Sqlparamdata**と**SQLGetData**を使用して、ストリーム出力パラメーターを取得します。|  
|データには、結果セットとストリーム出力パラメーターが含まれます。|SQL_SUCCESS|**SQLBindCol**と**SQLGetData**を使用して結果セットを取得します。<br /><br /> **Sqlmoreresults**を呼び出して、ストリーミングされた出力パラメーターの処理を開始します。 SQL_PARAM_DATA_AVAILABLE が返されます。<br /><br /> **Sqlparamdata**と**SQLGetData**を使用して、ストリーム出力パラメーターを取得します。|  
|データには、警告メッセージとストリーム出力パラメーターが含まれます。|SQL_SUCCESS_WITH_INFO|警告メッセージを処理するには、 **SQLGetDiagRec** と **SQLGetDiagField** を使用します。<br /><br /> **Sqlmoreresults**を呼び出して、ストリーミングされた出力パラメーターの処理を開始します。 SQL_PARAM_DATA_AVAILABLE が返されます。<br /><br /> **Sqlparamdata**と**SQLGetData**を使用して、ストリーム出力パラメーターを取得します。|  
|データには、警告メッセージ、結果セット、およびストリーム出力パラメーターが含まれます。|SQL_SUCCESS_WITH_INFO|警告メッセージを処理するには、 **SQLGetDiagRec** と **SQLGetDiagField** を使用します。 次に、 **Sqlmoreresults** を呼び出して、結果セットの処理を開始します。<br /><br /> **SQLBindCol**と**SQLGetData**を使用して結果セットを取得します。<br /><br /> **Sqlmoreresults**を呼び出して、ストリーミングされた出力パラメーターの処理を開始します。 **Sqlmoreresults** は SQL_PARAM_DATA_AVAILABLE を返す必要があります。<br /><br /> **Sqlparamdata**と**SQLGetData**を使用して、ストリーム出力パラメーターを取得します。|  
|DAE 入力パラメーターを使用したクエリ (ストリーム入力/出力 (DAE) パラメーターなど)|SQL NEED_DATA|**Sqlparamdata**と**sqlparamdata**を呼び出して、DAE の入力パラメーターデータを送信します。<br /><br /> すべての DAE 入力パラメーターが処理された後、 **Sqlparamdata** は、 **Sqlexecute** および **SQLExecDirect** が返すことができるリターンコードを返すことができます。 その後、このテーブル内のケースを適用できます。<br /><br /> リターンコードが SQL_PARAM_DATA_AVAILABLE 場合は、ストリーミングされた出力パラメーターを使用できます。 アプリケーションは、この表の最初の行で説明されているように、ストリーム出力パラメーターのトークンを取得するために、 **Sqlparamdata** を再度呼び出す必要があります。<br /><br /> リターンコードが SQL_SUCCESS 場合は、処理する結果セットがあるか、処理が完了しています。<br /><br /> リターンコードが SQL_SUCCESS_WITH_INFO 場合は、警告メッセージが処理されます。|  
  
 **Sqlexecute**、 **SQLExecDirect**、または**sqlmoreresults**によって SQL_PARAM_DATA_AVAILABLE が返された後、アプリケーションが次の一覧にない関数を呼び出すと、関数シーケンスエラーが発生します。  
  
-   **SQLAllocHandle**  / **SQLAllocHandleStd**  
  
-   **Sqldatasources ソース**  / **Sqldrivers**  
  
-   **SQLGetInfo**  / **Sqlgetfunctions**  
  
-   **Sqlgetconnectattr**  / **SQLGetEnvAttr**  / **SQLGetDescField**  / **Sqlgetdescrec**  
  
-   **SQLNumParams**  
  
-   **SQLDescribeParam**  
  
-   **SQLNativeSql**  
  
-   **SQLParamData**  
  
-   **SQLMoreResults**  
  
-   **SQLGetDiagField**  / **SQLGetDiagRec**  
  
-   **SQLCancel**  
  
-   **Sqlcancelhandle** (ステートメントハンドルを含む)  
  
-   **SQLFreeStmt** (オプション = SQL_CLOSE、SQL_DROP または SQL_UNBIND)  
  
-   **SQLCloseCursor**  
  
-   **SQLDisconnect**  
  
-   **Sqlfreehandle** (handletype = SQL_HANDLE_STMT)  
  
-   **SQLGetStmtAttr**  
  
 アプリケーションは引き続き **SQLSetDescField** または **SQLSetDescRec** を使用して、バインド情報を設定できます。 フィールドマッピングは変更されません。 ただし、記述子内のフィールドは、新しい値を返す場合があります。 たとえば、SQL_DESC_PARAMETER_TYPE は SQL_PARAM_INPUT_OUTPUT_STREAM または SQL_PARAM_OUTPUT_STREAM を返す場合があります。  
  
## <a name="usage-scenario-retrieve-an-image-in-parts-from-a-result-set"></a>使用シナリオ: 結果セットからパーツ内のイメージを取得する  
 **SQLGetData** を使用すると、ストアドプロシージャから、イメージに関する1行のメタデータを含む結果セットが返され、そのイメージが大きな出力パラメーターで返された場合に、データを部分的に取得できます。  
  
```  
// CREATE PROCEDURE SP_TestOutputPara  
//      @ID_of_picture   as int,  
//      @Picture         as varbinary(max) out  
// AS  
//     output the image data through streamed output parameter  
// GO  
BOOL displayPicture(SQLUINTEGER idOfPicture, SQLHSTMT hstmt) {  
   SQLLEN      lengthOfPicture;    // The actual length of the picture.  
   BYTE        smallBuffer[100];   // A very small buffer.  
   SQLRETURN   retcode, retcode2;  
  
   // Bind the first parameter (input parameter)  
   SQLBindParameter(  
         hstmt,  
         1,                         // The first parameter.   
         SQL_PARAM_INPUT,           // Input parameter: The ID_of_picture.  
         SQL_C_ULONG,               // The C Data Type.  
         SQL_INTEGER,               // The SQL Data Type.  
         0,                         // ColumnSize is ignored for integer.  
         0,                         // DecimalDigits is ignored for integer.  
         &idOfPicture,              // The Address of the buffer for the input parameter.  
         0,                         // BufferLength is ignored for integer.  
         NULL);                     // This is ignored for integer.  
  
   // Bind the streamed output parameter.  
   SQLBindParameter(  
         hstmt,   
         2,                         // The second parameter.  
         SQL_PARAM_OUTPUT_STREAM,   // A streamed output parameter.   
         SQL_C_BINARY,              // The C Data Type.    
         SQL_VARBINARY,             // The SQL Data Type.  
         0,                         // ColumnSize: The maximum size of varbinary(max).  
         0,                         // DecimalDigits is ignored for binary type.  
         (SQLPOINTER)2,             // ParameterValuePtr: An application-defined  
                                    // token (this will be returned from SQLParamData).  
                                    // In this example, we used the ordinal   
                                    // of the parameter.  
         0,                         // BufferLength is ignored for streamed output parameters.  
         &lengthOfPicture);         // StrLen_or_IndPtr: The status variable returned.   
  
   retcode = SQLPrepare(hstmt, L"{call SP_TestOutputPara(?, ?)}", SQL_NTS);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   retcode = SQLExecute(hstmt);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   // Assume that the retrieved picture exists.  Use SQLBindCol or SQLGetData to retrieve the result-set.  
  
   // Process the result set and move to the streamed output parameters.  
   retcode = SQLMoreResults( hstmt );  
  
   // SQLGetData retrieves and displays the picture in parts.  
   // The streamed output parameter is available.  
   while (retcode == SQL_PARAM_DATA_AVAILABLE) {  
      SQLPOINTER token;   // Output by SQLParamData.  
      SQLLEN cbLeft;      // #bytes remained  
      retcode = SQLParamData(hstmt, &token);   // returned token is 2 (according to the binding)  
      if ( retcode == SQL_PARAM_DATA_AVAILABLE ) {  
         // A do-while loop retrieves the picture in parts.  
         do {  
            retcode2 = SQLGetData(   
               hstmt,   
               (UWORD) token,          // the value of the token is the ordinal.   
               SQL_C_BINARY,           // The C-type.  
               smallBuffer,            // A small buffer.   
               sizeof(smallBuffer),    // The size of the buffer.  
               &cbLeft);               // How much data we can get.  
         }  
         while ( retcode2 == SQL_SUCCESS_WITH_INFO );  
      }  
   }  
  
   return TRUE;  
}  
```  
  
## <a name="usage-scenario-send-and-receive-a-large-object-as-a-streamed-inputoutput-parameter"></a>使用シナリオ: ストリーム入力/出力パラメーターとしてラージオブジェクトを送信および受信する  
 **SQLGetData** を使用すると、ストアドプロシージャが大きなオブジェクトを入力/出力パラメーターとして渡し、データベースとの間で値をストリーミングするときに、パーツのデータを取得して送信することができます。 すべてのデータをメモリに保存する必要はありません。  
  
```  
// CREATE PROCEDURE SP_TestInOut  
//       @picture as varbinary(max) out  
// AS  
//    output the image data through output parameter   
// go  
  
BOOL displaySimilarPicture(BYTE* image, ULONG lengthOfImage, SQLHSTMT hstmt) {  
   BYTE smallBuffer[100];   // A very small buffer.  
   SQLRETURN retcode, retcode2;  
   SQLLEN statusOfPicture;  
  
   // First bind the parameters, before preparing the statement that binds the output streamed parameter.  
   SQLBindParameter(  
      hstmt,   
      1,                                 // The first parameter.  
      SQL_PARAM_INPUT_OUTPUT_STREAM,     // I/O-streamed parameter: The Picture.  
      SQL_C_BINARY,                      // The C Data Type.  
      SQL_VARBINARY,                     // The SQL Data Type.  
      0,                                 // ColumnSize: The maximum size of varbinary(max).  
      0,                                 // DecimalDigits is ignored.   
      (SQLPOINTER)1,                     // An application defined token.   
      0,                                 // BufferLength is ignored for streamed I/O parameters.  
      &statusOfPicture);                 // The status variable.  
  
   statusOfPicture = SQL_DATA_AT_EXEC;   // Input data in parts (DAE parameter at input).  
  
   retcode = SQLPrepare(hstmt, L"{call SP_TestInOut(?) }", SQL_NTS);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   // Execute the statement.  
   retcode = SQLExecute(hstmt);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   if ( retcode == SQL_NEED_DATA ) {  
      // Use SQLParamData to loop through DAE input parameters.  For  
      // each, use SQLPutData to send the data to database in parts.  
  
      // This example uses an I/O parameter with streamed output.  
      // Therefore, the last call to SQLParamData should return  
      // SQL_PARAM_DATA_AVAILABLE to indicate the end of the input phrase   
      // and report that a streamed output parameter is available.  
  
      // Assume retcode is set to the return value of the last call to  
      // SQLParamData, which is equal to SQL_PARAM_DATA_AVAILABLE.  
   }  
  
   // Start processing the streamed output parameters.  
   while ( retcode == SQL_PARAM_DATA_AVAILABLE ) {  
      SQLPOINTER token;   // Output by SQLParamData.  
      SQLLEN cbLeft;     // #bytes remained  
      retcode = SQLParamData(hstmt, &token);  
      if ( retcode == SQL_PARAM_DATA_AVAILABLE ) {  
         do {  
            retcode2 = SQLGetData(   
               hstmt,   
               (UWORD) token,          // the value of the token is the ordinal.   
               SQL_C_BINARY,           // The C-type.  
               smallBuffer,            // A small buffer.   
               sizeof(smallBuffer),    // The size of the buffer.  
               &cbLeft);               // How much data we can get.  
         }  
         while ( retcode2 == SQL_SUCCESS_WITH_INFO );  
      }  
   }   
  
   return TRUE;  
}  
```  
  
## <a name="see-also"></a>関連項目  
 [ステートメント パラメーター](../../../odbc/reference/develop-app/statement-parameters.md)
