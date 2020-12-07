---
description: 比較演算子 (Transact-SQL)
title: 比較演算子 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- expressions [SQL Server], testing
- operators [Transact-SQL], comparison
- testing expressions
- Boolean data type
- Boolean expressions
- comparing expressions
- comparison operators [SQL Server]
ms.assetid: b0cc68ef-3029-484c-a917-0c15dcbc230d
author: rothja
ms.author: jroth
ms.openlocfilehash: 34df520dcb0f193e2b548a909ea10cd4113995fc
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96124479"
---
# <a name="comparison-operators-transact-sql"></a>比較演算子 (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  比較演算子は、2 つの式が同じかどうかをテストします。 比較演算子は **text**、**ntext**、または **image** データ型の式を除くすべての式で使用できます。 次の表は、[!INCLUDE[tsql](../../includes/tsql-md.md)] の比較演算子の一覧です。  
  
|演算子|説明|  
|--------------|-------------|  
|[= (等しい)](../../t-sql/language-elements/equals-transact-sql.md)|等しい|  
|[> (より大きい)](../../t-sql/language-elements/greater-than-transact-sql.md)|より大きい|  
|[< (より小さい)](../../t-sql/language-elements/less-than-transact-sql.md)|より小さい|  
|[>= (以上)](../../t-sql/language-elements/greater-than-or-equal-to-transact-sql.md)|以上|  
|[<= (以下)](../../t-sql/language-elements/less-than-or-equal-to-transact-sql.md)|以下|  
|[<> (等しくない)](../../t-sql/language-elements/not-equal-to-transact-sql-traditional.md)|等しくない|  
|[\!= (等しくない)](../../t-sql/language-elements/not-equal-to-transact-sql-exclamation.md)|等しくない (ISO 標準外)|  
|[\!< (以上)](../../t-sql/language-elements/not-less-than-transact-sql.md)|より小さくない (ISO 標準外)|  
|[\!> (以下)](../../t-sql/language-elements/not-greater-than-transact-sql.md)|より大きくない (ISO 標準外)|  
  
## <a name="boolean-data-type"></a>Boolean データ型  
 比較演算子の結果は **ブール** データ型になります。 有効値には、TRUE、FALSE、UNKNOWN があります。 **ブール** データ型を返す式は、ブール式とも呼ばれます。  
  
 **ブール** データ型は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の他のデータ型と異なり、テーブルの列や変数のデータ型として指定することはできず、結果セットで返すこともできません。  
  
 SET ANSI_NULLS が ON の場合、1 つまたは 2 つの NULL 式が含まれる演算子では UNKNOWN が返されます。 SET ANSI_NULLS が OFF の場合、等号 (=) 演算子と不等号 (<>) 演算子を除き、同じ規則が適用されます。 SET ANSI_NULLS が OFF の場合、これらの演算子では、他の NULL と同等の、既知の値として NULL を処理し、TRUE または FALSE のみを返します (UNKNOWN を返すことはありません)。  
  
 **ブール** データ型の式は、検索条件を満たす行をフィルター選択するための WHERE 句、または IF や WHILE などのフロー制御言語ステートメントで使用します。たとえば次のようになります。  
  
```syntaxsql  
-- Uses AdventureWorks  
  
DECLARE @MyProduct INT;  
SET @MyProduct = 750;  
IF (@MyProduct <> 0)  
   SELECT ProductID, Name, ProductNumber  
   FROM Production.Product  
   WHERE ProductID = @MyProduct;  
```  
  
## <a name="see-also"></a>関連項目  
 [式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
 [演算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
