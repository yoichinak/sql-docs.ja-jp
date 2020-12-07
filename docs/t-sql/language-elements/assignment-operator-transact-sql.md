---
description: = (代入演算子) (Transact-SQL)
title: = (代入演算子) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operators [Transact-SQL], assignment
- assignment operators [Transact-SQL]
- headings [SQL Server columns]
- relationships [SQL Server], assignment operators
- column headings [SQL Server]
ms.assetid: c3040db6-21d6-40ac-a783-82c98ec006cc
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9e7b83fe2e452d2f58f592d4af6958ce94786f13
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196848"
---
# <a name="-assignment-operator-transact-sql"></a>= (代入演算子) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)] の代入演算子は等号 (=) だけです。 次の例では、`@MyCounter` 変数を作成した後、代入演算子によって、`@MyCounter` を式で返される値に設定します。  
  
```sql  
DECLARE @MyCounter INT;  
SET @MyCounter = 1;  
```  
  
 代入演算子を使用すると、列見出しと、列の値を定義する式との関係を設定することもできます。 次の例では、列見出しの `FirstColumnHeading` と `SecondColumnHeading` を表示します。 ここでは、すべての行の `xyz` 列見出しに文字列 `FirstColumnHeading` が表示され、 続けて、`Product` テーブルの各製品 ID が `SecondColumnHeading` 列見出しに一覧表示されます。  
  
```sql  
-- Uses AdventureWorks  
  
SELECT FirstColumnHeading = 'xyz',  
       SecondColumnHeading = ProductID  
FROM Production.Product;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [演算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [複合演算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  
