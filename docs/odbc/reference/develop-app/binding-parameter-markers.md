---
description: バインディング パラメーター マーカー
title: パラメーターマーカーのバインド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- parameter markers [ODBC]
- binding parameter markers [ODBC]
ms.assetid: fe88c1c2-4ee4-45e0-8500-b8c25c047815
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 259faf84e0388f74662471583657da1fd95bb007
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476854"
---
# <a name="binding-parameter-markers"></a>バインディング パラメーター マーカー
アプリケーションは、 **SQLBindParameter**を呼び出すことによってパラメーターをバインドします。 **SQLBindParameter** は、一度に1つのパラメーターをバインドします。 このアプリケーションでは、次のように指定します。  
  
-   パラメーターの数。 パラメーターには、SQL ステートメント内のパラメーターの順序が増加します。番号は1から始まります。 SQL ステートメントのパラメーター数よりも大きいパラメーター番号を指定することはできますが、ステートメントの実行時にパラメーター値は無視されます。  
  
-   パラメーターの型 (入力、入出力、または出力)。 プロシージャ呼び出しのパラメーターを除き、すべてのパラメーターは入力パラメーターです。 詳細については、このセクションで後述する「 [プロシージャのパラメーター](../../../odbc/reference/develop-app/procedure-parameters.md)」を参照してください。  
  
-   パラメーターにバインドされた変数の C データ型、アドレス、およびバイト長。 ドライバーは、データを C データ型から SQL データ型に変換できる必要があり、エラーが返されます。 サポートされている変換の一覧については、「付録 D: データ型」の「 [C から SQL データ型へのデータの変換](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) 」を参照してください。  
  
-   パラメーター自体の SQL データ型、有効桁数、および小数点以下桁数。  
  
-   長さ/インジケーターバッファーのアドレス。 バイナリまたは文字データのバイト長を提供したり、データが NULL であることを指定したり、データが **Sqlputdata**と共に送信されるように指定したりします。 詳細については、「 [長さとインジケーターの値の使用](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)」を参照してください。  
  
 たとえば、次のコードでは、販売員と*CustID*を、販売員と CustID の列のパラメーター*にバインドし*ます。 *販売員*には可変長の文字データが含まれているため、このコードで*は販売員*(11) のバイト長を指定し、 *SalesPersonLenOrInd*をバインドして、*販売員*のデータのバイト長を格納します。 この情報は、固定長の整数データを含むため、 *CustID* には必要ありません。  
  
```  
SQLCHAR       SalesPerson[11];  
SQLINTEGER    SalesPersonLenOrInd, CustIDInd;  
SQLUINTEGER   CustID;  
  
// Bind SalesPerson to the parameter for the SalesPerson column and  
// CustID to the parameter for the CustID column.  
SQLBindParameter(hstmt1, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 10, 0,  
                  SalesPerson, sizeof(SalesPerson), &SalesPersonLenOrInd);  
SQLBindParameter(hstmt1, 2, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 10, 0,  
                  &CustID, 0, &CustIDInd);  
  
// Set values of salesperson and customer ID and length/indicators.  
strcpy_s((char*)SalesPerson, _countof(SalesPerson), "Garcia");  
SalesPersonLenOrInd = SQL_NTS;  
CustID = 1331;  
CustIDInd = 0;  
  
// Execute a statement to get data for all orders made to the specified  
// customer by the specified salesperson.  
SQLExecDirect(hstmt1,"SELECT * FROM Orders WHERE SalesPerson=? AND CustID=?",SQL_NTS);  
```  
  
 **SQLBindParameter**が呼び出されると、ドライバーはこの情報をステートメントの構造体に格納します。 ステートメントを実行すると、この情報を使用してパラメーターデータが取得され、データソースに送信されます。  
  
> [!NOTE]  
>  ODBC 1.0 では、パラメーターは **SQLSetParam**にバインドされました。 ドライバーマネージャーは、アプリケーションとドライバーによって使用される ODBC のバージョンに応じて、 **SQLSetParam** と **SQLBindParameter**の間の呼び出しをマップします。
