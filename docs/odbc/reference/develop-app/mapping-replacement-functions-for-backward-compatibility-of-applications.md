---
description: アプリケーションの旧バージョンとの互換性のためのマッピング置換関数
title: アプリの互換性のための置換関数のマッピング-ODBC |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping replacement functions [ODBC]
- upgrading applications [ODBC], mapping replacement functions
- compatibility [ODBC], mapping replacement functions
- ODBC drivers [ODBC], backward compatibility
- functions [ODBC], mapping replacement functions
- application upgrades [ODBC], mapping replacement functions
- backward compatibility [ODBC], mapping replacement functions
ms.assetid: f5e6d9da-76ef-42cb-b3f5-f640857df732
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7cba29b0dda2b0d4533444fd3fa8b83eaaeae7a9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461414"
---
# <a name="mapping-replacement-functions-for-backward-compatibility-of-applications"></a>アプリケーションの旧バージョンとの互換性のためのマッピング置換関数
*Odbc 3.X ドライバーマネージャー*を使用して動作する odbc 3.x アプリケーションは、新しい機能が使用されていない限り *、odbc 2.x*ドライバーに対して動作*します。* ただし、重複した機能と動作の変更の両方が、odbc 2.x*ドライバーで odbc* *3.x アプリケーションを*動作させる方法に影響します。 ODBC 2.x ドライバーを使用する場合、ドライバーマネージャーは、1つ以上*の odbc 2.x 関数を*、対応*する odbc 2.x 関数に*置き換えた次の odbc *3 .x*関数をマップ*します。*  
  
|ODBC *3.x* 関数|ODBC *2.x* 関数|  
|-------------------------|-------------------------|  
|**SQLAllocHandle**|**Sqlallocenv**、 **sqlallocenv**、または **sqlallocenv**|  
|**SQLBulkOperations**|**SQLSetPos**|  
|**SQLColAttribute**|**SQLColAttributes**|  
|**SQLEndTran**|**SQLTransact**|  
|**SQLFetch**|**SQLExtendedFetch**|  
|**SQLFetchScroll**|**SQLExtendedFetch**|  
|**SQLFreeHandle**|**Sqlfreeenv**、 **SQLFreeConnect**、または **SQLFreeStmt**|  
|**SQLGetConnectAttr**|**SQLGetConnectOption**|  
|**SQLGetDiagRec**|**SQLError**|  
|**SQLGetStmtAttr**|**SQLGetStmtOption**[1]|  
|**SQLSetConnectAttr**|**SQLSetConnectOption**|  
|**SQLSetStmtAttr**|**SQLSetStmtOption**[1]|  
  
 [1] その他のアクションは、要求された属性によっても実行される可能性があります。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
 ドライバーマネージャーは、必要に応じて、これを **Sqlallocenv**、 **sqlallocenv**、または **sqlallocenv**にマップします。 **SQLAllocHandle**への次の呼び出し。  
  
```  
SQLAllocHandle(HandleType, InputHandle, OutputHandlePtr);  
```  
  
 ドライバーマネージャーは、次のようなマッピングを実行します (概念、エラーチェックなし)。  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLAllocEnv(OutputHandlePtr));  
   case SQL_HANDLE_DBC: return (SQLAllocConnect (InputHandle, OutputHandlePtr));  
   case SQL_HANDLE_STMT: return (SQLAllocStmt (InputHandle, OutputHandlePtr));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlbulkoperations"></a>SQLBulkOperations  
 ドライバーマネージャーはこれを **SQLSetPos**にマップします。 **Sqlbulkoperations**の次の呼び出し:  
  
```  
SQLBulkOperations(hstmt, Operation);  
```  
  
 では、次の一連の手順が実行されます。  
  
1.  Operation 引数が SQL_ADD の場合、ドライバーマネージャーは次のように **SQLSetPos** を呼び出します。  
  
    ```  
    SQLSetPos (hstmt, 0, SQL_ADD, SQL_LOCK_NO_CHANGE);  
    ```  
  
2.  操作の引数が SQL_ADD ない場合、ドライバーは SQLSTATE HY092 (無効な属性/オプション識別子) を返します。  
  
3.  アプリケーションが **Sqlfetch** 操作または **Sqlfetchscroll** 操作または **sqlbulkscroll 操作**の呼び出しの間の SQL_ATTR_ROW_STATUS_PTR を変更しようとした場合、ドライバーマネージャーは SQLSTATE HY011 を返します (属性を設定することはできません)。  
  
4.  操作引数が SQL_ADD 場合、アプリケーションは、挿入するデータをバインドするために **SQLBindCol** を呼び出す必要があります。 **SQLSetDescField**または**SQLSetDescRec**を呼び出して、挿入するデータをバインドすることはできません。  
  
5.  操作の引数が SQL_ADD で、挿入する行の数が現在の行セットのサイズと同じでない場合は、 **Sqlbulkoperations**を呼び出す前に、 **SQLSetStmtAttr**を呼び出して、SQL_ATTR_ROW_ARRAY_SIZE statement 属性に挿入する行の数を設定する必要があります。 前の行セットサイズに戻すには、アプリケーションで **Sqlfetch**、 **Sqlfetchscroll**、 **SQLSetPos** が呼び出される前に、SQL_ATTR_ROW_ARRAY_SIZE statement 属性を設定する必要があります。  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
 ドライバーマネージャーはこれを **Sqlcolattributes**にマップします。 **Sqlcolattribute**の次の呼び出し:  
  
```  
SQLColAttribute(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
```  
  
 では、次の一連の手順が実行されます。  
  
1.  *FieldIdentifier*が次のいずれかの場合:  
  
     SQL_DESC_PRECISION、SQL_DESC_SCALE、SQL_DESC_LENGTH、SQL_DESC_OCTET_LENGTH、SQL_DESC_UNNAMED、SQL_DESC_BASE_COLUMN_NAME、SQL_DESC_LITERAL_PREFIX、SQL_DESC_LITERAL_SUFFIX、または SQL_DESC_LOCAL_TYPE_NAME  
  
     ドライバーマネージャーは、SQLSTATE HY091 (無効な記述子フィールド識別子) を使用して SQL_ERROR を返します。 このセクションの他のルールは適用されません。  
  
2.  ドライバーマネージャーは、SQL_COLUMN_COUNT、SQL_COLUMN_NAME、または SQL_COLUMN_NULLABLE をそれぞれ SQL_DESC_COUNT、SQL_DESC_NAME、または SQL_DESC_NULLABLE にマップします。 (ODBC 2.x *ドライバーで* は、SQL_DESC_COUNT、SQL_DESC_NAME、SQL_DESC_NULLABLE ではなく、SQL_COLUMN_COUNT、SQL_COLUMN_NAME、および SQL_COLUMN_NULLABLE のみがサポートされています。)SQLColAttribute の呼び出しは、次のようにマップされます。  
  
    ```  
    SQLColAttributes(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
    ```  
  
3.  他のすべての *FieldIdentifier* 値はドライバーに渡され、 **sqlcolattribute** は前に示したように **sqlcolattribute** にマップされます。  
  
4.  *Bufferlength*が0未満の場合、ドライバーマネージャーは SQLSTATE HY090 (無効な文字列またはバッファー長) の SQL_ERROR を返します。 このセクションの他のルールは適用されません。  
  
5.  *FieldIdentifier*が SQL_DESC_CONCISE_TYPE、戻り値の型が簡潔な datetime データ型である場合、ドライバーマネージャーは日付、時刻、およびタイムスタンプのコードの戻り値をマップします。  
  
6.  ドライバーマネージャーは、SQLSTATE HY010 (関数シーケンスエラー) を発生させる必要があるかどうかを確認するために必要なチェックを実行します。 その場合、ドライバーマネージャーは SQL_ERROR と SQLSTATE HY010 (関数シーケンスエラー) を返します。 このセクションの他のルールは適用されません。  
  
## <a name="sqlendtran"></a>SQLEndTran  
 ドライバーマネージャーはこれを **Sqltransact**にマップします。 **SQLEndTran**への次の呼び出し。  
  
```  
SQLEndTran(HandleType, Handle, CompletionType);  
```  
  
 ドライバーマネージャーは、次のようなマッピングを実行します (概念、エラーチェックなし)。  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV:return(SQLTransact(Handle, SQL_NULL_HDBC, CompletionType));  
   case SQL_HANDLE_DBC:return(SQLTransact(SQL_NULL_HENV, Handle, CompletionType);  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlfetch"></a>SQLFetch  
 ドライバーマネージャーは、SQL_FETCH_NEXT の*Fetchorientation*引数を使用して、これを**SQLExtendedFetch**にマップします。 **Sqlfetch**の次の呼び出し:  
  
```  
SQLFetch (StatementHandle);  
```  
  
 次のように、ドライバーマネージャーによって **SQLExtendedFetch**が呼び出されます。  
  
```  
rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, &RowCount, RowStatusArray);  
```  
  
 この呼び出しでは、 *Pcrow* 引数は、 **SQLSetStmtAttr**を呼び出すことによって、アプリケーションが SQL_ATTR_ROWS_FETCHED_PTR statement 属性を設定する値に設定されます。  
  
> [!NOTE]  
>  アプリケーションが **SQLSetStmtAttr** を呼び出して、ステータス配列を指すように SQL_ATTR_ROW_STATUS_PTR を設定すると、ドライバーマネージャーはポインターをキャッシュします。 *Rowstatusarray* は null ポインターと同じにすることができます。  
  
 ドライバーが **SQLExtendedFetch** をサポートしておらず、カーソルライブラリが読み込まれている場合、ドライバーマネージャーはカーソルライブラリの **SQLExtendedFetch** を使用して **sqlfetch** を **SQLExtendedFetch**にマップします。 ドライバーが **SQLExtendedFetch** をサポートしておらず、カーソルライブラリが読み込まれていない場合は、ドライバーマネージャーによって **sqlfetch** の呼び出しがドライバーに渡されます。 アプリケーションが SQL_ATTR_ROW_STATUS_PTR を設定するために **SQLSetStmtAttr** を呼び出すと、ドライバーマネージャーによって配列が確実に設定されます。 アプリケーションが SQL_ATTR_ROWS_FETCHED_PTR を設定するために **SQLSetStmtAttr** を呼び出す場合、このフィールドは1に設定されます。  
  
## <a name="sqlfetchscroll"></a>SQLFetchScroll  
 ドライバーマネージャーはこれを **SQLExtendedFetch**にマップします。 **Sqlfetchscroll**の次の呼び出し:  
  
```  
SQLFetchScroll(StatementHandle, FetchOrientation, FetchOffset);  
```  
  
 では、次の一連の手順が実行されます。  
  
1.  アプリケーションが **SQLSetStmtAttr** を呼び出して、ステータス配列を指すように SQL_ATTR_ROW_STATUS_PTR (IRD の SQL_DESC_ARRAY_STATUS_PTR フィールドを設定する) を設定すると、ドライバーマネージャーはこのポインターをキャッシュします。 このポインターを *Rowstatusarray*; にします。それ以外の場合は、 *Rowstatusarray* を null ポインターと同じにします。 *Rowstatusarray*引数が null ポインターに設定されている場合は、ドライバーマネージャーによって行ステータス配列が生成されます。  
  
2.  *Fetchorientation*が SQL_FETCH_NEXT、SQL_FETCH_PRIOR、SQL_FETCH_ABSOLUTE、SQL_FETCH_RELATIVE、SQL_FETCH_FIRST、SQL_FETCH_LAST、SQL_FETCH_BOOKMARK のいずれでもない場合、Driver Manager は SQL_ERROR と SQLSTATE HY106 (範囲外のフェッチの種類) を返します。 このセクションの他のルールは適用されません。  
  
3.  大文字と小文字の区別:  
  
-   *Fetchorientation*が SQL_FETCH_BOOKMARK と等しい場合は、次のようになります。  
  
    -   SQL_ATTR_FETCH_BOOKMARK_PTR の値を設定するために前に **SQLSetStmtAttr** が呼び出された場合は、ポインター SQL_DESC_FETCH_BOOKMARK_PTR を逆参照して取得した値を *bmk* にします。  
  
    -   それ以外の場合は、SQLSTATE HY111 (無効なブックマーク値) を使用して SQL_ERROR を返します。 このセクションの他のルールは適用されません。  
  
     ドライバーマネージャーは、次のように **SQLExtendedFetch**を呼び出すようになりました。  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, Bmk, pcRow, RowStatusArray);  
    ```  
  
-   それ以外の場合、ドライバーマネージャーは次のように **SQLExtendedFetch**を呼び出します。  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, pcRow, RowStatusArray);  
    ```  
  
     これらの呼び出しでは、 *Pcrow* 引数は、 **SQLSetStmtAttr**の呼び出しによって、アプリケーションが SQL_ATTR_ROWS_FETCHED_PTR ステートメント属性を設定する値に設定されます。  
  
-   SQL_ATTR_ROW_ARRAY_SIZE は SQL_ROWSET_SIZE にマップされます。  
  
-   *Rc*が SQL_SUCCESS または SQL_SUCCESS_WITH_INFO に等しい場合、 *fetchorientation*が SQL_FETCH_BOOKMARK と等しく、 *fetchorientation*が0でない場合、ドライバーマネージャーは警告 SQLSTATE 01S10 (ブックマークオフセットによってフェッチを試行し、オフセット値は無視) をポストして SQL_SUCCESS_WITH_INFO を返します。  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 ドライバーマネージャーは、必要に応じてこれを **Sqlfreeenv**、 **SQLFreeConnect**、または **SQLFreeStmt** にマップします。 **Sqlfreehandle**への次の呼び出し:  
  
```  
SQLFreeHandle(HandleType, Handle);  
```  
  
 ドライバーマネージャーは、次のようなマッピングを実行します (概念、エラーチェックなし)。  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLFreeEnv(Handle));  
   case SQL_HANDLE_DBC: return (SQLFreeConnect(Handle));  
   case SQL_HANDLE_STMT: return (SQLFreeStmt(Handle, SQL_DROP));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
 ドライバーマネージャーはこれを **SQLGetConnectOption**にマップします。 **Sqlgetconnectattr**の次の呼び出し:  
  
```  
SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 では、次の一連の手順が実行されます。  
  
1.  *属性*がドライバー定義の接続またはステートメント属性ではなく、ODBC 2.x で定義されている*属性では*ない場合、ドライバーマネージャーは SQLSTATE HY092 (無効な属性/オプション識別子) を使用して SQL_ERROR を返します。 このセクションのその他のルールは適用されません。  
  
2.  *属性*が SQL_ATTR_AUTO_IPD または SQL_ATTR_METADATA_ID と等しい場合、ドライバーマネージャーは SQLSTATE HY092 (無効な属性/オプション識別子) を使用して SQL_ERROR を返します。  
  
3.  ドライバーマネージャーは、SQLSTATE 08003 (接続が開いていません) または SQLSTATE HY010 (関数シーケンスエラー) が発生する必要があるかどうかを確認するために必要なチェックを実行します。 その場合、ドライバーマネージャーは SQL_ERROR を返し、適切なエラーメッセージを投稿します。 このセクションの他のルールは適用されません。  
  
4.  ドライバーマネージャーは、次のように **SQLGetConnectOption** を呼び出します。  
  
    ```  
    SQLGetConnectOption (ConnectionHandle, Attribute, ValuePtr);  
    ```  
  
     *Bufferlength*および*stringlength ptr*は無視されることに注意してください。  
  
## <a name="sqlgetdata"></a>SQLGetData  
 *Odbc 2.x アプリケーションが*odbc 2.x ドライバーを操作するときに、 *columnnumber*引数が0に設定されている**SQLGetData**を呼び出すと、Odbc *3.x ドライバーマネージャー*は、 *Option*属性が SQL_GET_BOOKMARK に設定された**SQLGetStmtOption**への呼び出しにこれをマップ*します。*  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
 ドライバーマネージャーはこれを **SQLGetStmtOption**にマップします。 **SQLGetStmtAttr**への次の呼び出し。  
  
```  
SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 では、次の一連の手順が実行されます。  
  
1.  *属性*がドライバー定義の接続またはステートメント属性ではなく、ODBC 2.x で定義されている*属性では*ない場合、ドライバーマネージャーは SQLSTATE HY092 (無効な属性/オプション識別子) を使用して SQL_ERROR を返します。 このセクションのその他のルールは適用されません。  
  
2.  *属性*が次のいずれかの場合:  
  
     SQL_ATTR_APP_ROW_DESC  
  
     SQL_ATTR_APP_PARAM_DESC  
  
     SQL_ATTR_AUTO_IPD  
  
     SQL_ATTR_ROW_BIND_TYPE  
  
     SQL_ATTR_IMP_ROW_DESC  
  
     SQL_ATTR_IMP_PARAM_DESC  
  
     SQL_ATTR_METADATA_ID  
  
     SQL_ATTR_PARAM_BIND_TYPE  
  
     SQL_ATTR_PREDICATE_PTR  
  
     SQL_ATTR_PREDICATE_OCTET_LENGTH_PTR  
  
     SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_OPERATION_PTR  
  
     SQL_ATTR_PARAM_OPERATION_PTR  
  
     ドライバーマネージャーは、SQLSTATE HY092 (無効な属性/オプション識別子) を使用して SQL_ERROR を返します。 このセクションの他のルールは適用されません。  
  
3.  ドライバーマネージャーは、SQLSTATE HY010 (関数シーケンスエラー) を発生させる必要があるかどうかを確認するために必要なチェックを実行します。 その場合、ドライバーマネージャーは SQL_ERROR と SQLSTATE HY010 (関数シーケンスエラー) を返します。 このセクションの他のルールは適用されません。  
  
4.  *属性*が SQL_ATTR_ROWS_FETCHED_PTR と等しい場合、ドライバーマネージャーは、内部ドライバー*マネージャー変数に*対するポインターを返します。この変数は、 **SQLExtendedFetch**の呼び出しで使用または使用されます。 このセクションの他のルールは適用されません。  
  
5.  *属性*が SQL_DESC_FETCH_BOOKMARK_PTR と等しい場合、ドライバーマネージャーは**SQLSetStmtAttr**の呼び出し中にキャッシュされた適切なポインターを返します。  
  
6.  *属性*が SQL_ATTR_ROW_STATUS_PTR と等しい場合、ドライバーマネージャーは**SQLSetStmtAttr**の呼び出し中にキャッシュされた適切なポインターを返します。  
  
7.  ドライバーマネージャーは、次のように **SQLGetStmtOption** を呼び出します。  
  
    ```  
    SQLGetStmtOption (hstmt, fOption, pvParam);  
    ```  
  
     ここで、 *hstmt*、 *Foption*、および *Pvparam* は、それぞれ *StatementHandle*、 *Attribute*、および *valueptr*の値に設定されます。 *Bufferlength*および*stringlength ptr*は無視されます。  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
 ドライバーマネージャーはこれを **SQLSetConnectOption**にマップします。 **SQLSetConnectAttr**への次の呼び出し。  
  
```  
SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, StringLength);  
```  
  
 では、次の一連の手順が実行されます。  
  
1.  *属性*がドライバー定義の接続またはステートメント属性ではなく、ODBC 2.x で定義されている*属性では*ない場合、ドライバーマネージャーは SQLSTATE HY092 (無効な属性/オプション識別子) を使用して SQL_ERROR を返します。 このセクションのその他のルールは適用されません。  
  
2.  *属性*が SQL_ATTR_AUTO_IPD と等しい場合、ドライバーマネージャーは SQLSTATE HY092 (無効な属性/オプション識別子) を使用して SQL_ERROR を返します。  
  
3.  ドライバーマネージャーは、SQLSTATE 08003 (接続が開いていません) または SQLSTATE HY010 (関数シーケンスエラー) が発生する必要があるかどうかを確認するために必要なチェックを実行します。 これらのエラーのいずれかを発生させる必要がある場合、ドライバーマネージャーは SQL_ERROR を返し、適切なエラーメッセージを投稿します。 このセクションの他のルールは適用されません。  
  
4.  ドライバーマネージャーは、次のように **SQLSetConnectOption** を呼び出します。  
  
    ```  
    SQLSetConnectOption (hdbc, fOption, vParam);  
    ```  
  
     ここで、 *hdbc*、 *Foption*、および *Vparam* は、それぞれ *Connectionhandle*、 *Attribute*、および *valueptr*の値に設定されます。 *Stringlength ptr* は無視されます。  
  
> [!NOTE]  
>  接続レベルのステートメント属性を設定する機能は非推奨とされました。 ODBC 3.x アプリケーションでは、ステートメント属性を接続レベルで設定しないで*ください。*  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 ドライバーマネージャーはこれを **SQLSetStmtOption**にマップします。 **SQLSetStmtAttr**への次の呼び出し。  
  
```  
SQLSetStmtAttr(StatementHandle, Attribute, ValuePtr, StringLength);  
```  
  
 では、次の一連の手順が実行されます。  
  
1.  *属性*がドライバー定義の接続またはステートメント属性ではなく、ODBC 2.x で定義されている*属性では*ない場合、ドライバーマネージャーは SQLSTATE HY092 (無効な属性/オプション識別子) を使用して SQL_ERROR を返します。 このセクションのその他のルールは適用されません。  
  
2.  *属性*が次のいずれかの場合:  
  
     SQL_ATTR_APP_ROW_DESC  
  
     SQL_ATTR_APP_PARAM_DESC  
  
     SQL_ATTR_AUTO_IPD  
  
     SQL_ATTR_ROW_BIND_TYPE  
  
     SQL_ATTR_IMP_ROW_DESC  
  
     SQL_ATTR_IMP_PARAM_DESC  
  
     SQL_ATTR_METADATA_ID  
  
     SQL_ATTR_PARAM_BIND_TYPE  
  
     SQL_ATTR_PREDICATE_PTR  
  
     SQL_ATTR_PREDICATE_OCTET_LENGTH_PTR  
  
     SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_OPERATION_PTR  
  
     SQL_ATTR_PARAM_OPERATION_PTR  
  
     ドライバーマネージャーは、SQLSTATE HY092 (無効な属性/オプション識別子) を使用して SQL_ERROR を返します。 このセクションの他のルールは適用されません。  
  
3.  ドライバーマネージャーは、SQLSTATE HY010 (関数シーケンスエラー) を発生させる必要があるかどうかを確認するために必要なチェックを実行します。 その場合、ドライバーマネージャーは SQL_ERROR と SQLSTATE HY010 (関数シーケンスエラー) を返します。 このセクションの他のルールは適用されません。  
  
4.  *属性*が SQL_ATTR_PARAMSET_SIZE または SQL_ATTR_PARAMS_PROCESSED_PTR と等しい場合は、このトピックで後述する「パラメーター配列を処理するためのマッピング」を参照してください。 このセクションの他のルールは適用されません。  
  
5.  *属性*が SQL_ATTR_ROWS_FETCHED_PTR と等しい場合、ドライバーマネージャーは、後で**sqlfetchscroll**を使用するためにポインター値をキャッシュします。  
  
6.  *属性*が SQL_ATTR_ROW_STATUS_PTR と等しい場合、ドライバーマネージャーは、後で**sqlfetchscroll**または**SQLSetPos**と共に使用するためにポインター値をキャッシュします。 このセクションの他のルールは適用されません。  
  
7.  *属性*が SQL_ATTR_FETCH_BOOKMARK_PTR と等しい場合、ドライバーマネージャーは*valueptr*をキャッシュし、後で**sqlfetchscroll**の呼び出しでキャッシュされた値を使用します。 このセクションの他のルールは適用されません。  
  
8.  ドライバーマネージャーは、次のように **SQLSetStmtOption** を呼び出します。  
  
    ```  
    SQLSetStmtOption (hstmt, fOption, vParam);  
    ```  
  
     ここで、 *hstmt*、 *Foption*、および *Vparam* は、それぞれ *StatementHandle*、 *Attribute*、および *valueptr*の値に設定されます。 *Stringlength*引数は無視されます。  
  
     ODBC 2.x ドライバーで、文字文字列、ドライバー固有のステートメントオプションがサポート *されて* いる場合は、odbc *3. x* アプリケーションで **SQLSetStmtOption** を呼び出してこれらのオプションを設定する必要があります。  
  
## <a name="mappings-for-handling-parameter-arrays"></a>パラメーター配列を処理するためのマッピング  
 アプリケーションが次を呼び出すとき:  
  
```  
SQLSetStmtAttr (StatementHandle, SQL_ATTR_PARAMSET_SIZE, Size, StringLength);  
```  
  
 ドライバーマネージャーは、次のものを呼び出します。  
  
```  
SQLParamOptions (StatementHandle, Size, &RowCount);  
```  
  
 アプリケーションが **SQLGetStmtAttr** を呼び出して SQL_ATTR_PARAMS_PROCESSED_PTR を取得すると、後でドライバーマネージャーがこの変数へのポインターを返します。 ドライバーマネージャーは、ステートメントハンドルが準備された状態または割り当て済みの状態に戻るまで、この内部変数を変更することはできません。  
  
 ODBC *3. x* アプリケーションは、 **SQLGetStmtAttr** を呼び出して、APD の SQL_DESC_ARRAY_SIZE フィールドが明示的に設定されていない場合でも、SQL_ATTR_PARAMS_PROCESSED_PTR の値を取得できます。 この状況は、たとえば、 **Sqlexecute** が SQL_NEED_DATA を返したときに処理されているパラメーターの現在の "row" を確認する汎用ルーチンがアプリケーションにある場合に発生する可能性があります。 このルーチンは、SQL_DESC_ARRAY_SIZE が1であるか、または1より大きいかどうかにかかわらず呼び出されます。 このことを考慮するために、ドライバーマネージャーは、アプリケーションが APD の SQL_DESC_ARRAY_SIZE フィールドを設定するために **SQLSetStmtAttr** を呼び出したかどうかにかかわらず、この内部変数を定義する必要があります。 SQL_DESC_ARRAY_SIZE が設定されていない場合、ドライバーマネージャーは、 **SQLExecDirect** または **sqlexecute**から戻る前に、この変数に値1が含まれていることを確認する必要があります。  
  
## <a name="error-handling"></a>エラー処理  
 *ODBC 3.x では、* **sqlfetch**または**sqlfetchscroll**を呼び出すと、IRD 内の SQL_DESC_ARRAY_STATUS_PTR が設定されます。また、特定の診断レコードの SQL_DIAG_ROW_NUMBER フィールドには、このレコードが関連する行セット内の行番号が含まれます。 これを使用すると、アプリケーションは、エラーメッセージと特定の行の位置を関連付けることができます。  
  
 ODBC 2.x ドライバーは、この機能を提供できませ*ん。* ただし、SQLSTATE 01S01 (行内のエラー) でエラーの境界が表示されます。 **Sqlfetch**または**sqlfetchscroll**を使用*する odbc* *2.x アプリケーションは*、この事実を認識している必要があります。 このようなアプリケーションは、実際に SQL_DIAG_ROW_NUMBER フィールドを取得するために **SQLGetDiagField** を呼び出すことができないことにも注意してください。 *Odbc 2.x アプリケーションは*、odbc 2.x ドライバーを操作するときに、SQL_DIAG_MESSAGE_TEXT、SQL_DIAG_NATIVE、SQL_DIAG_RETURNCODE、または SQL_DIAG_SQLSTATE の*DiagIdentifier*引数を使用してのみ**SQLGetDiagField**を呼び出すことが*できます。* *Odbc 2.x*ドライバーマネージャーは、odbc *2.x ドライバーを*使用する場合に診断データ構造を保持しますが *、odbc 2.x*ドライバーはこれら4つのフィールドのみを返します。  
  
 *Odbc 2.x アプリケーションが*odbc *2.x ドライバーを使用して*動作しているときに、1つの操作によってドライバーマネージャーによって複数のエラーが返される可能性がある場合は *、odbc 2.x*ドライバーマネージャーによって、odbc *3.x ドライバーマネージャー*によって異なるエラーが返されることがあります。  
  
## <a name="mappings-for-bookmark-operations"></a>ブックマーク操作のマッピング  
 Odbc 2.x *Driver Manager* では *、odbc 2.X アプリケーションが* odbc *2.x ドライバーを* 操作するときに、次のマッピングが実行されます。  
  
### <a name="sqlbindcol"></a>SQLBindCol  
 *Odbc 2.x アプリケーションが*odbc 2.x ドライバーを使用しているときに**SQLBindCol**を呼び出して、 *fctype*が SQL_C_VARBOOKMARK に等しい列0にバインドする場合 *、ODBC* *3.x ドライバーマネージャー*は、 *bufferlength*引数が4未満か4より大きいかどうかを確認し、存在する場合は SQLSTATE HY090 (無効な文字列またはバッファー長) を返します。 *Bufferlength*引数が4に等しい場合、ドライバーマネージャーは、 *fctype*を SQL_C_BOOKMARK に置き換えた後、ドライバーで**SQLBindCol**を呼び出します。  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 *Odbc 2.x アプリケーションで*odbc *2.x ドライバーを*使用する場合、 *columnnumber*引数を0に設定して**Sqlcolattribute**を呼び出すと、ドライバーマネージャーは、次の表に示す*FieldIdentifier*値を返します。  
  
|*FieldIdentifier*|値|  
|-----------------------|-----------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_FALSE|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|  
|SQL_DESC_CATALOG_NAME|"" (空の文字列)|  
|SQL_DESC_CONCISE_TYPE|SQL_BINARY|  
|SQL_DESC_COUNT|**Sqlnumresultcols**によって返される同じ値|  
|SQL_DESC_DATETIME_INTERVAL_CODE|0|  
|SQL_DESC_DISPLAY_SIZE|8|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|  
|SQL_DESC_LABEL|"" (空の文字列)|  
|SQL_DESC_LENGTH|0|  
|SQL_DESC_LITERAL_PREFIX|"" (空の文字列)|  
|SQL_DESC_LITERAL_SUFFIX|"" (空の文字列)|  
|SQL_DESC_LOCAL_TYPE_NAME|"" (空の文字列)|  
|SQL_DESC_NAME|"" (空の文字列)|  
|SQL_DESC_NULLABLE|SQL_NO_NULLS|  
|SQL_DESC_OCTET_LENGTH|4|  
|SQL_DESC_PRECISION|4|  
|SQL_DESC_SCALE|0|  
|SQL_DESC_SCHEMA_NAME|"" (空の文字列)|  
|SQL_DESC_SEARCHABLE|SQL_PRED_NONE|  
|SQL_DESC_TABLE_NAME|"" (空の文字列)|  
|SQL_DESC_TYPE|SQL_BINARY|  
|SQL_DESC_TYPE_NAME|"" (空の文字列)|  
|SQL_DESC_UNNAMED|SQL_UNNAMED|  
|SQL_DESC_UNSIGNED|SQL_FALSE|  
|SQL_DESC_UPDATEABLE|SQL_ATTR_READ_ONLY|  
  
### <a name="sqldescribecol"></a>SQLDescribeCol  
 *Odbc 2.x アプリケーションが*odbc *2.x ドライバーを*操作するときに、 *columnnumber*引数を0に設定して**SQLDescribeCol**を呼び出すと、ドライバーマネージャーは次の表に示す値を返します。  
  
|バッファー|値|  
|------------|-----------|  
|ColumnName|"" (空の文字列)|  
|*NameLengthPtr|0|  
|*DataTypePtr|SQL_BINARY|  
|* ColumnSizePtr|4|  
|*DecimalDigitsPtr|0|  
|*NullablePtr|SQL_NO_NULLS|  
  
### <a name="sqlgetdata"></a>SQLGetData  
 *Odbc 2.x アプリケーションが*odbc 2.x ドライバーを操作するときに、ブックマークを取得するために次の**SQLGetData**の呼び出しを*行います。*  
  
```  
SQLGetData(StatementHandle, 0, SQL_C_VARBOOKMARK, TargetValuePtr, BufferLength, StrLen_or_IndPtr)  
```  
  
 この呼び出しは、次のように SQL_GET_BOOKMARK の*Foption*を指定して**SQLGetStmtOption**にマップされます。  
  
```  
SQLGetStmtOption(hstmt, SQL_GET_BOOKMARK, TargetValuePtr)  
```  
  
 ここで、 *hstmt* と *pvparam* は、それぞれ *StatementHandle* および *targetvalueptr*の値に設定されています。 このブックマークは、 *Pvparam* (*targetvalueptr*) 引数が指すバッファーに返されます。 **SQLGetData**への呼び出しで*StrLen_or_IndPtr*引数が指すバッファーの値が4に設定されています。  
  
 このマッピングは、 **SQLGetData**の呼び出しの前に**sqlfetch**が呼び出され、ODBC 2.x ドライバーが**SQLExtendedFetch**をサポートしていない場合に考慮する必要が*あります。* この場合、 **Sqlfetch** は ODBC 2.x ドライバーに渡さ *れます。* この場合、ブックマークの取得はサポートされていません。  
  
 **SQLGetData**を ODBC 2.x ドライバーで複数回呼び出すことはできません *。* そのため、 *bufferlength*引数を4未満の値に設定し、 *columnnumber*引数を0に設定して**SQLGetData**を呼び出すと、SQLSTATE HY090 (無効な文字列またはバッファー長) が返されます。 ただし、 **SQLGetData**は、同じブックマークを取得するために複数回呼び出すことができます。  
  
### <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 *Odbc 2.x アプリケーションが*odbc 2.x ドライバーを操作するときに**SQLSetStmtAttr**を呼び出して、SQL_ATTR_USE_BOOKMARKS 属性を SQL_UB_VARIABLE に設定すると、ドライバーマネージャーによって、基になる ODBC *2.x ドライバーの*属性が SQL_UB_ON に設定さ*れます。*
