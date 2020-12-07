---
description: ハンドル
title: Handle |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- handles [ODBC]
- driver handles [ODBC]
- driver manager [ODBC], handles
- handles [ODBC], about handles
ms.assetid: f663101e-a4cc-402b-b9d7-84d5e975be71
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6e9d2445dbbd676e8d48be519c1649d550fd89c5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465764"
---
# <a name="handles"></a>ハンドル
ハンドルは、特定の項目を識別する非透過の32ビット値です。ODBC では、このアイテムは環境、接続、ステートメント、または記述子にすることができます。 アプリケーションが **SQLAllocHandle**を呼び出すと、ドライバーマネージャーまたはドライバーは、指定された種類の新しい項目を作成し、そのハンドルをアプリケーションに返します。 後で、アプリケーションは、このハンドルを使用して、ODBC 関数を呼び出すときにその項目を識別します。 ドライバーマネージャーとドライバーは、ハンドルを使用して項目に関する情報を検索します。  
  
 たとえば、次のコードでは、2つのステートメントハンドル (*hstmtOrder* と *hstmtLine*) を使用して、販売注文と販売注文の行番号の結果セットを作成するステートメントを識別します。 後でこれらのハンドルを使用して、データのフェッチ元の結果セットを識別します。  
  
```  
SQLHSTMT      hstmtOrder, hstmtLine; // Statement handles.  
SQLUINTEGER   OrderID;  
SQLINTEGER    OrderIDInd = 0;  
SQLRETURN     rc;  
  
// Prepare the statement that retrieves line number information.  
SQLPrepare(hstmtLine, "SELECT * FROM Lines WHERE OrderID = ?", SQL_NTS);  
  
// Bind OrderID to the parameter in the preceding statement.  
SQLBindParameter(hstmtLine, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
               &OrderID, 0, &OrderIDInd);  
  
// Bind the result sets for the Order table and the Lines table. Bind  
// OrderID to the OrderID column in the Orders table. When each row is  
// fetched, OrderID will contain the current order ID, which will then be  
// passed as a parameter to the statement tofetch line number  
// information. Code not shown.  
  
// Create a result set of sales orders.  
SQLExecDirect(hstmtOrder, "SELECT * FROM Orders", SQL_NTS);  
  
// Fetch and display the sales order data. Code to check if rc equals  
// SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
while ((rc = SQLFetch(hstmtOrder)) != SQL_NO_DATA) {  
   // Display the sales order data. Code not shown.  
  
   // Create a result set of line numbers for the current sales order.  
   SQLExecute(hstmtLine);  
  
   // Fetch and display the sales order line number data. Code to check  
   // if rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
   while ((rc = SQLFetch(hstmtLine)) != SQL_NO_DATA) {  
      // Display the sales order line number data. Code not shown.  
   }  
  
   // Close the sales order line number result set.  
   SQLCloseCursor(hstmtLine);  
}  
  
// Close the sales order result set.  
SQLCloseCursor(hstmtOrder);  
```  
  
 ハンドルは、それを作成した ODBC コンポーネントに対してのみ意味があります。つまり、ドライバーマネージャーだけがドライバーマネージャーハンドルを解釈でき、ドライバーだけが独自のハンドルを解釈できます。  
  
 たとえば、前の例のドライバーでステートメントに関する情報を格納する構造体を割り当て、ステートメントハンドルとしてこの構造体へのポインターを返すとします。 アプリケーションが **SQLPrepare**を呼び出すと、SQL ステートメントと、販売注文の行番号に使用されるステートメントのハンドルが渡されます。 ドライバーは、データソースに SQL ステートメントを送信します。これにより、データソースが準備され、アクセスプラン識別子が返されます。 ドライバーは、ハンドルを使用して、この識別子を格納する構造体を検索します。  
  
 その後、アプリケーションが **Sqlexecute** を呼び出して、特定の販売注文の行番号の結果セットを生成すると、同じハンドルが渡されます。 ドライバーは、ハンドルを使用して、構造からアクセスプラン id を取得します。 この id をデータソースに送信して、実行するプランを指定します。  
  
 ODBC には、ドライバーマネージャーが処理するハンドルとドライバーハンドルの2つのレベルがあります。 アプリケーションは、ドライバーマネージャーでこれらの関数を呼び出すため、ODBC 関数を呼び出すときに Driver Manager ハンドルを使用します。 ドライバーマネージャーは、このハンドルを使用して対応するドライバーハンドルを検索し、ドライバーの関数を呼び出すときにドライバーハンドルを使用します。 ドライバーとドライバーマネージャーの処理を使用する方法の例については、「 [接続プロセスにおけるドライバーマネージャーの役割](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)」を参照してください。  
  
 ハンドルには、ODBC アーキテクチャの成果物の2つのレベルがあります。ほとんどの場合、アプリケーションとドライバーのどちらにも関係ありません。 通常、このような理由はありませんが、アプリケーションは **SQLGetInfo**を呼び出してドライバーハンドルを特定することができます。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [環境ハンドル](../../../odbc/reference/develop-app/environment-handles.md)  
  
-   [接続ハンドル](../../../odbc/reference/develop-app/connection-handles.md)  
  
-   [ステートメント ハンドル](../../../odbc/reference/develop-app/statement-handles.md)  
  
-   [記述子ハンドル](../../../odbc/reference/develop-app/descriptor-handles.md)  
  
-   [状態遷移](../../../odbc/reference/develop-app/state-transitions.md)
