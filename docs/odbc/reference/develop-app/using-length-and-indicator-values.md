---
description: 長さとインジケーターの値の使用
title: 長さとインジケーターの値を使用する |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- length/indicator buffers [ODBC]
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 849792f1-cb1e-4bc2-b568-c0aff0b66199
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7e9c7feb463b2a92d716be24c76d00b64c69a860
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424404"
---
# <a name="using-length-and-indicator-values"></a>長さとインジケーターの値の使用
長さ/インジケーターバッファーは、データバッファー内のデータのバイト長、またはデータが NULL であることを示す SQL_NULL_DATA などの特別なインジケーターを渡すために使用されます。 使用される関数に応じて、長さ/インジケーターバッファーは SQLINTEGER または SQLSMALLINT として定義されます。 したがって、これを記述するには1つの引数が必要です。 データバッファーが遅延なしの入力バッファーである場合、この引数にはデータ自体のバイト長またはインジケーター値が含まれます。 多くの場合、 *StrLen_or_Ind* または類似した名前として名前が付けられます。 たとえば、次のコードでは、 **Sqlputdata** を呼び出して、データがいっぱいになったバッファーを渡します。バイト長 (*Valuelen*) は、データバッファー (*valueptr*) が入力バッファーであるため、直接渡されます。  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLen;  
  
// Call local function to place data in ValuePtr. In ValueLen, return the  
// number of bytes of data placed in ValuePtr. If there is not enough  
// data, this will be less than 50.  
FillBuffer(ValuePtr, sizeof(ValuePtr), &ValueLen);  
  
// Call SQLPutData to send the data to the driver.  
SQLPutData(hstmt, ValuePtr, ValueLen);  
```  
  
 データバッファーが遅延入力バッファー、遅延なしの出力バッファー、または出力バッファーの場合、引数には長さ/インジケーターバッファーのアドレスが含まれます。 多くの場合、 *StrLen_or_IndPtr* または類似した名前として名前が付けられます。 たとえば、次のコードでは、 **SQLGetData**を呼び出して、データがいっぱいになったバッファーを取得します。バイト長は、対応するデータバッファー (*Valueptr*) が遅延なしの出力バッファーであるために、アドレスが**SQLGetData**に渡される長さ/インジケーターバッファー (*valuelenorind*) でアプリケーションに返されます。  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLGetData(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 長さ/インジケーターバッファー引数は、特に禁止されていない限り、0 (遅延入力以外の場合) または null ポインター (出力または遅延入力の場合) のいずれかになります。 入力バッファーの場合、ドライバーはデータのバイト長を無視します。 この場合、可変長データを渡すときにエラーが返されますが、長さとインジケーターの値がどちらも必要ないので、null 以外の固定長データを渡すときには、このエラーが発生します。 出力バッファーの場合、ドライバーはデータのバイト長またはインジケーター値を返しません。 これは、ドライバーによって返されるデータが NULL であっても、長さとインジケーターの値がどちらも必要ないために、固定長の非 null 許容データを取得するときに共通である場合に、エラーになります。  
  
 遅延されたデータバッファーのアドレスがドライバーに渡されるとき、遅延長/インジケーターバッファーのアドレスは、バッファーがバインド解除されるまで有効なままにしておく必要があります。  
  
 長さ/インジケーターの値として有効な長さは次のとおりです。  
  
-   *n*( *n* > 0)。  
  
-   0.  
  
-   SQL_NTS。 対応するデータバッファーのドライバーに送信された文字列が null で終了しています。これは、C プログラマがバイト長を計算せずに文字列を渡すための便利な方法です。 この値は、アプリケーションがデータをドライバーに送信する場合にのみ有効です。 ドライバーは、アプリケーションにデータを返すとき、常にデータの実際のバイト長を返します。  
  
 次の値は、長さ/インジケーターの値として有効です。 SQL_NULL_DATA は SQL_DESC_INDICATOR_PTR 記述子フィールドに格納されます。その他の値はすべて SQL_DESC_OCTET_LENGTH_PTR 記述子フィールドに格納されます。  
  
-   SQL_NULL_DATA。 データは NULL データ値であり、対応するデータバッファー内の値は無視されます。 この値は、ドライバーとの間で送受信される SQL データに対してのみ有効です。  
  
-   SQL_DATA_AT_EXEC。 データバッファーにデータが含まれていません。 代わりに、ステートメントが実行されたとき、または**Sqlputdata**または**SQLSetPos**が呼び出されたときに、 **sqlputdata**と共にデータが送信されます。 この値は、ドライバーに送信された SQL データに対してのみ有効です。 詳細については、「 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)、 [sqlbulkoperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)、 [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)」を参照してください。  
  
-   SQL_LEN_DATA_AT_EXEC (*長さ*) マクロの結果。 この値は SQL_DATA_AT_EXEC に似ています。 詳細については、「 [長いデータの送信](../../../odbc/reference/develop-app/sending-long-data.md)」を参照してください。  
  
-   SQL_NO_TOTAL。 ドライバーでは、出力バッファーで返すことができる長いデータのバイト数を特定できません。 この値は、ドライバーから取得された SQL データに対してのみ有効です。  
  
-   SQL_DEFAULT_PARAM。 プロシージャでは、対応するデータバッファーの値の代わりに、プロシージャで入力パラメーターの既定値を使用します。  
  
-   SQL_COLUMN_IGNORE。 **Sqlbulkoperations** または **SQLSetPos** は、データバッファー内の値を無視します。 **Sqlbulkoperations**または SQLSetPos の呼び出しによってデータの行を更新する場合 **、** 列の値は変更されません。 **Sqlbulkoperations**を呼び出すことによってデータの新しい行を挿入する場合、列の値が既定値に設定されるか、列に既定値がない場合は NULL に設定されます。
