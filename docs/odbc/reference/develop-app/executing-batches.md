---
description: バッチの実行
title: バッチの実行 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- batches [ODBC], executing
- SQL statements [ODBC], batches
ms.assetid: f082c717-4f82-4820-a2fa-ba607d8fd872
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b3bb923f95dfcfb731d472aad8ead7ff35053171
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424644"
---
# <a name="executing-batches"></a>バッチの実行
アプリケーションでは、ステートメントのバッチを実行する前に、ステートメントがサポートされているかどうかを確認する必要があります。 これを行うには、アプリケーションは、SQL_BATCH_SUPPORT、SQL_PARAM_ARRAY_ROW_COUNTS、および SQL_PARAM_ARRAY_SELECTS オプションを使用して **SQLGetInfo** を呼び出します。 最初のオプションは、行カウント生成ステートメントと結果セット生成ステートメントが明示的なバッチおよびプロシージャでサポートされているかどうかを返します。後者の2つのオプションは、パラメーター化された実行での行数と結果セットの可用性に関する情報を返します。  
  
 ステートメントのバッチは、 **Sqlexecute** または **SQLExecDirect**を使用して実行されます。 たとえば、次の呼び出しでは、ステートメントの明示的なバッチが実行され、新しい販売注文が開かれます。  
  
```  
SQLCHAR *BatchStmt =  
   "INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)"  
      "VALUES (2002, 1001, {fn CURDATE()}, 'Garcia', 'OPEN');"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 1, 1234, 10);"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 2, 987, 8);"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 3, 566, 17);"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 4, 412, 500)";  
  
SQLExecDirect(hstmt, BatchStmt, SQL_NTS);  
```  
  
 結果生成ステートメントのバッチが実行されると、1つ以上の行カウントまたは結果セットが返されます。 これらを取得する方法の詳細については、「 [複数の結果](../../../odbc/reference/develop-app/multiple-results.md)」を参照してください。  
  
 ステートメントのバッチにパラメーターマーカーが含まれている場合は、他のステートメントのように、パラメーターの順序が増加します。 たとえば、次のバッチステートメントには、1 ~ 21 のパラメーター番号が付いています。最初の **insert** ステートメントでは、1 ~ 5 の番号が付けられています。最後の **insert** ステートメントには、18 ~ 21 の番号が付けられています。  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
```  
  
 パラメーターの詳細については、このセクションで後述する「 [ステートメントパラメーター](../../../odbc/reference/develop-app/statement-parameters.md)」を参照してください。
