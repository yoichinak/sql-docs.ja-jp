---
description: SQL ステートメントのバッチ
title: SQL ステートメントのバッチ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- batches [ODBC]
- SQL statements [ODBC], batches
- batches [ODBC], about batches
ms.assetid: 766488cc-450c-434c-9c88-467f6c57e17c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e342fd7eaef721f8fb0033a5ae022ca8de74cda1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465934"
---
# <a name="batches-of-sql-statements"></a>SQL ステートメントのバッチ
SQL ステートメントのバッチは、2つ以上の sql ステートメントのグループ、または2つ以上の SQL ステートメントのグループと同じ効果を持つ1つの SQL ステートメントです。 一部の実装では、結果が使用可能になる前にバッチステートメント全体が実行されます。 多くの場合、ネットワークトラフィックが減少し、データソースによって SQL ステートメントのバッチの実行が最適化される可能性があるため、ステートメントを個別に送信するよりも効率的です。 その他の実装では、 **Sqlmoreresults** を呼び出すと、バッチ内の次のステートメントの実行がトリガーされます。 ODBC では、次の種類のバッチがサポートされています。  
  
-   **明示的なバッチ***明示的なバッチ*は、セミコロン (;) で区切られた2つ以上の SQL ステートメントです。 たとえば、次の SQL ステートメントのバッチでは、新しい販売注文が開きます。 これには、Orders テーブルと Lines テーブルの両方に行を挿入する必要があります。 最後のステートメントの後にセミコロンがないことに注意してください。  
  
    ```  
    INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
       VALUES (2002, 1001, {fn CURDATE()}, 'Garcia', 'OPEN');  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 1, 1234, 10);  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 2, 987, 8);  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 3, 566, 17);  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 4, 412, 500)  
    ```  
  
-   **プロシージャ** プロシージャに複数の SQL ステートメントが含まれている場合は、SQL ステートメントのバッチと見なされます。 たとえば、次の SQL Server 固有のステートメントでは、顧客に関する情報を含む結果セットを返すプロシージャが作成され、その顧客のすべての開いている販売注文が一覧表示されます。  
  
    ```  
    CREATE PROCEDURE GetCustInfo (@CustomerID INT) AS  
       SELECT * FROM Customers WHERE CustID = @CustomerID  
       SELECT OrderID FROM Orders  
          WHERE CustID = @CustomerID AND Status = 'OPEN'  
    ```  
  
     **CREATE PROCEDURE**ステートメント自体は、SQL ステートメントのバッチではありません。 ただし、作成されるプロシージャは、SQL ステートメントのバッチです。 **CREATE procedure**ステートメントは SQL Server に固有であり、SQL Server では、 **create procedure**ステートメントで複数のステートメントを区切るためにセミコロンを必要としないため、2つの**SELECT**ステートメントはセミコロンで区切りません。  
  
-   **パラメーターの配列** パラメーターの配列は、一括操作を実行する効果的な方法として、パラメーター化された SQL ステートメントで使用できます。 たとえば、次の **insert** ステートメントでパラメーターの配列を使用すると、1つの SQL ステートメントのみを実行しながら、複数の行を行テーブルに挿入できます。  
  
    ```  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (?, ?, ?, ?)  
    ```  
  
     データソースがパラメーターの配列をサポートしていない場合、ドライバーは、パラメーターの各セットに対して SQL ステートメントを1回実行することで、それらをエミュレートできます。 詳細については、このセクションで後述する「 [ステートメントパラメーター](../../../odbc/reference/develop-app/statement-parameters.md) と [パラメーター値の配列](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)」を参照してください。  
  
 さまざまな種類のバッチを相互運用可能な方法で混在させることはできません。 つまり、プロシージャ呼び出し、パラメーターの配列を使用する明示的なバッチ、およびパラメーターの配列を使用するプロシージャコールを含む明示的なバッチの実行結果をアプリケーションが決定する方法は、ドライバーによって異なります。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [結果生成および結果解放ステートメント](../../../odbc/reference/develop-app/result-generating-and-result-free-statements.md)  
  
-   [バッチの実行](../../../odbc/reference/develop-app/executing-batches.md)  
  
-   [エラーおよびバッチ](../../../odbc/reference/develop-app/errors-and-batches.md)
