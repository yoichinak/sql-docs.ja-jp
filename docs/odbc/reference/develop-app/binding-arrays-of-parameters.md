---
description: パラメーターのバインディング配列
title: パラメーターの配列のバインド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- binding parameter arrays [ODBC]
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 037afe23-052d-4f3a-8aa7-45302b199ad0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 529ea49d2697ffcf7b89217746420ab5cb298890
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429484"
---
# <a name="binding-arrays-of-parameters"></a>パラメーターのバインディング配列
パラメーターの配列を使用するアプリケーションは、SQL ステートメントのパラメーターに配列をバインドします。 バインドスタイルには次の2つがあります。  
  
-   配列を各パラメーターにバインドします。 各データ構造 (配列) には、1つのパラメーターのすべてのデータが含まれています。 これは、単一のパラメーターの値の列をバインドするため、 *列方向のバインド* と呼ばれます。  
  
-   パラメーターのセット全体のパラメーターデータを保持する構造体を定義し、これらの構造体の配列をバインドします。 各データ構造には、1つの SQL ステートメントのデータが含まれています。 これは、パラメーターの行をバインドするため、 *行方向のバインド* と呼ばれます。  
  
 アプリケーションが1つの変数をパラメーターにバインドするときに、 **SQLBindParameter** を呼び出して配列をパラメーターにバインドします。 唯一の違いは、渡されるアドレスが単一変数のアドレスではなく配列アドレスであることです。 アプリケーションでは、列方向のバインド (既定値) または行方向のバインドのどちらを使用しているのかを指定するために、SQL_ATTR_PARAM_BIND_TYPE statement 属性を設定します。 列方向のバインドと行方向のバインドのどちらを使用するかは、主にアプリケーションの設定に関係しています。 プロセッサがメモリにアクセスする方法によっては、行方向のバインドが高速になる場合があります。 ただし、パラメーターの行数が非常に多い場合を除き、違いはほとんどありません。  
  
## <a name="column-wise-binding"></a>列方向のバインド  
 列方向のバインドを使用する場合、アプリケーションは、データを提供する各パラメーターに1つまたは2つの配列をバインドします。 最初の配列はデータ値を保持し、2番目の配列は長さ/インジケーターバッファーを保持します。 各配列には、パラメーターの値と同じ数の要素が含まれています。  
  
 列方向のバインドが既定値です。 また、アプリケーションは、SQL_ATTR_PARAM_BIND_TYPE statement 属性を設定することによって、行方向のバインドから列方向のバインドに変更することもできます。 次の図は、列方向のバインドのしくみを示しています。  
  
 ![列&#45;のバインドのしくみを示します](../../../odbc/reference/develop-app/media/pr31.gif "pr31")  
  
 たとえば、次のコードでは、10要素の配列を、PartID、Description、および Price 列のパラメーターにバインドし、10行を挿入するステートメントを実行します。 列方向のバインドを使用します。  
  
```  
#define DESC_LEN 51  
#define ARRAY_SIZE 10  
  
SQLCHAR *      Statement = "INSERT INTO Parts (PartID, Description,  Price) "  
                                                "VALUES (?, ?, ?)";  
SQLUINTEGER    PartIDArray[ARRAY_SIZE];  
SQLCHAR        DescArray[ARRAY_SIZE][DESC_LEN];  
SQLREAL        PriceArray[ARRAY_SIZE];  
SQLINTEGER     PartIDIndArray[ARRAY_SIZE], DescLenOrIndArray[ARRAY_SIZE],  
               PriceIndArray[ARRAY_SIZE];  
SQLUSMALLINT   i, ParamStatusArray[ARRAY_SIZE];  
SQLULEN ParamsProcessed;  
  
memset(DescLenOrIndArray, 0, sizeof(DescLenOrIndArray));  
memset(PartIDIndArray, 0, sizeof(PartIDIndArray));  
memset(PriceIndArray, 0, sizeof(PriceIndArray));  
  
// Set the SQL_ATTR_PARAM_BIND_TYPE statement attribute to use  
// column-wise binding.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_BIND_TYPE, SQL_PARAM_BIND_BY_COLUMN, 0);  
  
// Specify the number of elements in each parameter array.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMSET_SIZE, ARRAY_SIZE, 0);  
  
// Specify an array in which to return the status of each set of  
// parameters.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_STATUS_PTR, ParamStatusArray, 0);  
  
// Specify an SQLUINTEGER value in which to return the number of sets of  
// parameters processed.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMS_PROCESSED_PTR, &ParamsProcessed, 0);  
  
// Bind the parameters in column-wise fashion.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  PartIDArray, 0, PartIDIndArray);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,  
                  DescArray, DESC_LEN, DescLenOrIndArray);  
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  PriceArray, 0, PriceIndArray);  
  
// Set part ID, description, and price.  
for (i = 0; i < ARRAY_SIZE; i++) {  
   GetNewValues(&PartIDArray[i], DescArray[i], &PriceArray[i]);  
   PartIDIndArray[i] = 0;  
   DescLenOrIndArray[i] = SQL_NTS;  
   PriceIndArray[i] = 0;  
}  
  
// Execute the statement.  
SQLExecDirect(hstmt, Statement, SQL_NTS);  
  
// Check to see which sets of parameters were processed successfully.  
for (i = 0; i < ParamsProcessed; i++) {  
   printf("Parameter Set  Status\n");  
   printf("-------------  -------------\n");  
   switch (ParamStatusArray[i]) {  
      case SQL_PARAM_SUCCESS:  
      case SQL_PARAM_SUCCESS_WITH_INFO:  
         printf("%13d  Success\n", i);  
         break;  
  
      case SQL_PARAM_ERROR:  
         printf("%13d  Error\n", i);  
         break;  
  
      case SQL_PARAM_UNUSED:  
         printf("%13d  Not processed\n", i);  
         break;  
  
      case SQL_PARAM_DIAG_UNAVAILABLE:  
         printf("%13d  Unknown\n", i);  
         break;  
  
   }  
}  
```  
  
## <a name="row-wise-binding"></a>行方向のバインド  
 行方向のバインドを使用する場合、アプリケーションでは、パラメーターの各セットの構造を定義します。 構造体には、パラメーターごとに1つまたは2つの要素が含まれます。 最初の要素はパラメーター値を保持し、2番目の要素は長さ/インジケーターバッファーを保持します。 次に、アプリケーションはこれらの構造体の配列を割り当てます。これには、各パラメーターの値と同じ数の要素が含まれます。  
  
 アプリケーションは、SQL_ATTR_PARAM_BIND_TYPE statement 属性を使用して、構造体のサイズをドライバーに宣言します。 アプリケーションは、配列の最初の構造内のパラメーターのアドレスをバインドします。 このため、ドライバーでは、特定の行と列のデータのアドレスを  
  
```  
Address = Bound Address + ((Row Number - 1) * Structure Size) + Offset  
```  
  
 行には、1からパラメーターセットのサイズまでの番号が付けられます。 オフセット (定義されている場合) は、SQL_ATTR_PARAM_BIND_OFFSET_PTR statement 属性が指す値です。 次の図は、行方向のバインドのしくみを示しています。 パラメーターは任意の順序で構造体に配置できますが、わかりやすくするために順番に表示されます。  
  
 ![行&#45;方向のバインドのしくみを示します](../../../odbc/reference/develop-app/media/pr32.gif "pr32")  
  
 次のコードでは、PartID、Description、および Price 列に格納する値の要素を含む構造体を作成します。 次に、これらの構造体の10要素配列を割り当て、行方向のバインドを使用して、PartID、Description、および Price 列のパラメーターにバインドします。 次に、10行を挿入するステートメントを実行します。  
  
```  
#define DESC_LEN 51  
#define ARRAY_SIZE 10  
  
typedef tagPartStruct {  
   SQLREAL       Price;  
   SQLUINTEGER   PartID;  
   SQLCHAR       Desc[DESC_LEN];  
   SQLINTEGER    PriceInd;  
   SQLINTEGER    PartIDInd;  
   SQLINTEGER    DescLenOrInd;  
} PartStruct;  
  
PartStruct PartArray[ARRAY_SIZE];  
SQLCHAR *      Statement = "INSERT INTO Parts (PartID, Description,  
                Price) "  
               "VALUES (?, ?, ?)";  
SQLUSMALLINT   i, ParamStatusArray[ARRAY_SIZE];  
SQLULEN ParamsProcessed;  
  
// Set the SQL_ATTR_PARAM_BIND_TYPE statement attribute to use  
// column-wise binding.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_BIND_TYPE, sizeof(PartStruct), 0);  
  
// Specify the number of elements in each parameter array.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMSET_SIZE, ARRAY_SIZE, 0);  
  
// Specify an array in which to return the status of each set of  
// parameters.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_STATUS_PTR, ParamStatusArray, 0);  
  
// Specify an SQLUINTEGER value in which to return the number of sets of  
// parameters processed.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMS_PROCESSED_PTR, &ParamsProcessed, 0);  
  
// Bind the parameters in row-wise fashion.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &PartArray[0].PartID, 0, &PartArray[0].PartIDInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,  
                  PartArray[0].Desc, DESC_LEN, &PartArray[0].DescLenOrInd);  
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &PartArray[0].Price, 0, &PartArray[0].PriceInd);  
  
// Set part ID, description, and price.  
for (i = 0; i < ARRAY_SIZE; i++) {  
   GetNewValues(&PartArray[i].PartID, PartArray[i].Desc, &PartArray[i].Price);  
   PartArray[0].PartIDInd = 0;  
   PartArray[0].DescLenOrInd = SQL_NTS;  
   PartArray[0].PriceInd = 0;  
}  
  
// Execute the statement.  
SQLExecDirect(hstmt, Statement, SQL_NTS);  
  
// Check to see which sets of parameters were processed successfully.  
for (i = 0; i < ParamsProcessed; i++) {  
   printf("Parameter Set  Status\n");  
   printf("-------------  -------------\n");  
   switch (ParamStatusArray[i]) {  
      case SQL_PARAM_SUCCESS:  
      case SQL_PARAM_SUCCESS_WITH_INFO:  
         printf("%13d  Success\n", i);  
         break;  
  
      case SQL_PARAM_ERROR:  
         printf("%13d  Error\n", i);  
         break;  
  
      case SQL_PARAM_UNUSED:  
         printf("%13d  Not processed\n", i);  
         break;  
  
      case SQL_PARAM_DIAG_UNAVAILABLE:  
         printf("%13d  Unknown\n", i);  
         break;  
  
   }  
```
