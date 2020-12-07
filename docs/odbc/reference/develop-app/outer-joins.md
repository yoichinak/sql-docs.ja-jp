---
description: 外部結合
title: 外部結合 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- outer join escape sequences [ODBC]
- escape sequences [ODBC], outer join
ms.assetid: be1a0203-5da9-4871-9566-4bd3fbc0895c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a9be14c2b7c0dd6cdebc458fd22dc090862eb9dc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429124"
---
# <a name="outer-joins"></a>外部結合
ODBC では、SQL-92 の left、right、および full outer join 構文がサポートされています。 外部結合のエスケープシーケンスは、  
  
 **{oj** _外部結合_**}**  
  
 *外部結合*の場合  
  
 *テーブル参照* {**左 &#124; 右 &#124; 完全} 外部結合** {*テーブル参照* &#124; *外部結合* **}** _検索条件_  
  
 テーブル*参照*はテーブル名を指定し、*検索条件*では*テーブル参照*間の結合条件を指定します。  
  
 外部結合要求は、 **FROM** キーワードの後、 **WHERE** 句 (存在する場合) の前に記述する必要があります。 構文の詳細については、「付録 C: SQL 文法」の「 [外部結合のエスケープシーケンス](../../../odbc/reference/appendixes/outer-join-escape-sequence.md) 」を参照してください。  
  
 たとえば、次の SQL ステートメントでは、すべての顧客を一覧表示し、開いている注文があることを示す同じ結果セットが作成されます。 最初のステートメントでは、エスケープシーケンス構文を使用します。 2番目のステートメントでは、Oracle のネイティブ構文を使用し、相互運用できません。  
  
```  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM {oj Customers LEFT OUTER JOIN Orders ON Customers.CustID=Orders.CustID}  
   WHERE Orders.Status='OPEN'  
  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM Customers, Orders  
   WHERE (Orders.Status='OPEN') AND (Customers.CustID= Orders.CustID(+))  
```  
  
 アプリケーションでは、データソースとドライバーがサポートする外部結合の種類を特定するために、SQL_OJ_CAPABILITIES フラグを使用して **SQLGetInfo** を呼び出します。 サポートされる可能性のある外部結合の種類は、left、right、full、または nested outer join です。外部結合。 **ON** 句の列名の順序は、 **外部結合** 句でのそれぞれのテーブル名と同じではありません。外部結合と組み合わせた内部結合。また、外部結合では、任意の ODBC 比較演算子を使用します。 SQL_OJ_CAPABILITIES 情報の種類が0を返す場合、外部結合句はサポートされません。
