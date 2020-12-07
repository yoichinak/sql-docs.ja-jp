---
description: ステートメントの実行
title: ステートメント | を実行するMicrosoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], executing
ms.assetid: e5f0d2ee-0453-4faf-b007-12978dd300a1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4ce060c91e2500b016e824e733d8189c99334e1b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461474"
---
# <a name="executing-a-statement"></a>ステートメントの実行
ステートメントを実行するには、データベースエンジンによってコンパイル (準備) された日時に応じて、次の4つの方法を実行します。  
  
-   **直接実行** アプリケーションでは、SQL ステートメントを定義します。 これは、実行時に1回の手順で準備および実行されます。  
  
-   **準備実行** アプリケーションでは、SQL ステートメントを定義します。 実行時に個別のステップで準備および実行されます。 ステートメントを1回準備し、複数回実行することができます。  
  
-   **プロシージャ** アプリケーションでは、開発時に1つ以上の SQL ステートメントを定義してコンパイルし、これらのステートメントをデータソースにプロシージャとして格納できます。 実行時にプロシージャが1回以上実行されます。 アプリケーションでは、カタログ関数を使用して、使用可能なストアドプロシージャを列挙できます。  
  
-   **カタログ関数** ドライバーライターは、定義済みの結果セットを返す関数を作成します。 通常、この関数は、定義済みの SQL ステートメントを送信するか、この目的のために作成されたプロシージャを呼び出します。 関数は、実行時に1回以上実行されます。  
  
 特定のステートメント (ステートメントハンドルによって識別される) は、任意の回数実行できます。 ステートメントは、さまざまな SQL ステートメントを使用して実行できます。また、同じ SQL ステートメントを使用して繰り返し実行することもできます。 たとえば、次のコードでは、同じステートメントハンドル (*hstmt1*) を使用して、Sales データベース内のテーブルを取得し、表示します。 次に、このハンドルを再利用して、ユーザーが選択したテーブルの列を取得します。  
  
```  
SQLHSTMT    hstmt1;  
SQLCHAR *   Table;  
  
// Create a result set of all tables in the Sales database.  
SQLTables(hstmt1, "Sales", SQL_NTS, "sysadmin", SQL_NTS, NULL, 0, NULL, 0);  
  
// Fetch and display the table names; then close the cursor.  
// Code not shown.  
  
// Have the user select a particular table.  
SelectTable(Table);  
  
// Reuse hstmt1 to create a result set of all columns in Table.  
SQLColumns(hstmt1, "Sales", SQL_NTS, "sysadmin", SQL_NTS, Table, SQL_NTS, NULL, 0);  
  
// Fetch and display the column names in Table; then close the cursor.  
// Code not shown.  
```  
  
 次のコードは、1つのハンドルを使用して同じステートメントを繰り返し実行し、テーブルから行を削除する方法を示しています。  
  
```  
SQLHSTMT      hstmt1;  
SQLUINTEGER   OrderID;  
SQLINTEGER    OrderIDInd = 0;  
  
// Prepare a statement to delete orders from the Orders table.  
SQLPrepare(hstmt1, "DELETE FROM Orders WHERE OrderID = ?", SQL_NTS);  
  
// Bind OrderID to the parameter for the OrderID column.  
SQLBindParameter(hstmt1, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &OrderID, 0, &OrderIDInd);  
  
// Repeatedly execute hstmt1 with different values of OrderID.  
while ((OrderID = GetOrderID()) != 0) {  
   SQLExecute(hstmt1);  
}  
```  
  
 多くのドライバーでは、ステートメントの割り当てはコストの高いタスクであるため、通常は既存のステートメントを解放して新しいステートメントを割り当てるよりも、同じステートメントを再利用する方が効率的です。 ステートメントに結果セットを作成するアプリケーションでは、ステートメントを再実行する前に、結果セットの上にカーソルを閉じるように注意する必要があります。詳細については、「 [カーソルを閉じる](../../../odbc/reference/develop-app/closing-the-cursor.md)」を参照してください。  
  
 また、ステートメントを再利用することで、同時にアクティブにできるステートメントの数が一部のドライバーで制限されないようにすることもできます。 "Active" の正確な定義はドライバーに固有ですが、多くの場合、準備または実行され、結果が使用可能なステートメントを指します。 たとえば、 **INSERT** ステートメントの準備が完了すると、通常はアクティブと見なされます。 **SELECT** ステートメントが実行され、カーソルがまだ開いている場合、通常はアクティブと見なされます。 **CREATE TABLE** ステートメントの実行後は、通常、アクティブと見なされません。  
  
 アプリケーションは、SQL_MAX_CONCURRENT_ACTIVITIES オプションを指定して **SQLGetInfo** を呼び出すことによって、一度に1つの接続でアクティブにできるステートメントの数を決定します。 アプリケーションでは、データソースへの複数の接続を開くことで、この制限よりも多くのアクティブなステートメントを使用できます。ただし、接続には負荷がかかる場合があるため、パフォーマンスへの影響を考慮する必要があります。  
  
 アプリケーションでは、ステートメントが SQL_ATTR_QUERY_TIMEOUT statement 属性で実行されるために割り当てられる時間を制限できます。 データソースから結果セットが返される前にタイムアウト期間が経過すると、SQL ステートメントを実行している関数から SQLSTATE HYT00 (タイムアウト期限切れ) が返されます。 既定では、タイムアウトはありません。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [直接実行](../../../odbc/reference/develop-app/direct-execution-odbc.md)  
  
-   [準備実行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)  
  
-   [手順](../../../odbc/reference/develop-app/procedures-odbc.md)  
  
-   [SQL ステートメントのバッチ](../../../odbc/reference/develop-app/batches-of-sql-statements.md)  
  
-   [カタログ関数の実行](../../../odbc/reference/develop-app/executing-catalog-functions.md)
