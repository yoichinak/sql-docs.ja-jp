---
title: "VARP (Transact-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- VARP_TSQL
- VARP
dev_langs: TSQL
helpviewer_keywords:
- statistical variances
- expressions [SQL Server], statistical variance
- VARP function [Transact-SQL]
ms.assetid: ce5d2e32-01da-4e18-b8ed-a08b61d84456
caps.latest.revision: "40"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1590c8faa87bbbfba3f752ff295712654174c6ba
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="varp-transact-sql"></a>VARP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指定した式のすべての値について、母集団に対する統計的変位を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
VARP ( [ ALL | DISTINCT ] expression )  
   OVER ( [ partition_by_clause ] order_by_clause )  nh  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
-- Aggregate Function Syntax   
VARP ( [ ALL | DISTINCT ] expression )  
  
-- Analytic Function Syntax  
VARP (expression) OVER ( [ partition_by_clause ] order_by_clause)  
```  
  
## <a name="arguments"></a>引数  
 **ALL**  
 すべての値にこの関数を適用します。 ALL が既定値です。  
  
 DISTINCT  
 重複する値は 1 つだけカウントします。  
  
 *expression*  
 **bit** データ型を除く、真数データ型または概数データ型の[式](../../t-sql/language-elements/expressions-transact-sql.md)を指定します。 集計関数とサブクエリは使用できません。  
  
 OVER **(** [ *partition_by_clause* ] *order_by_clause* **)**  
 *partition_by_clause* は、FROM 句で生成された結果セットをパーティションに分割します。このパーティションに関数が適用されます。 指定しない場合、関数ではクエリ結果セットのすべての行を 1 つのグループとして扱います。 *order_by_clause* は、演算が実行される論理的順序を指定します。 *order_by_clause* は必須です。 詳細については、「[OVER 句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)」を参照してください。  
  
## <a name="return-types"></a>戻り値の型  
 **float**  
  
## <a name="remarks"></a>解説  
 SELECT ステートメントのすべてのアイテムで VARP を使用すると、結果セットの各値が計算に含められます。 VARP は、数値型列に対して使用できます。 NULL 値は無視されます。  
  
 VARP は、OVER 句や ORDER BY 句なしで使用される場合は決定的関数です。 OVER 句や ORDER BY 句と共に使用される場合は、非決定的関数です。 詳細については、「 [決定的関数と非決定的関数](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-varp"></a>A: VARP を使用する  
 この例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースの `SalesPerson` テーブル内のすべてのボーナス額を母集団として偏差を返します。  
  
```  
SELECT VARP(Bonus)  
FROM Sales.SalesPerson;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例:[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]と[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-using-varp"></a>B: VARP を使用する  
 次の例では、 `dbo.FactSalesQuota` テーブルの販売ノルマの値の `VARP` を返します。 最初の列にすべての個別の値の分散が、 2 番目の列に重複値も含めてすべての値の分散が含まれています。  
  
```  
-- Uses AdventureWorks  
  
SELECT VARP(DISTINCT SalesAmountQuota)AS Distinct_Values, VARP(SalesAmountQuota) AS All_Values  
FROM dbo.FactSalesQuota;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Distinct_Values   All_Values
----------------  ----------------
158146830494.18   157788848582.94
```  
  
### <a name="c-using-varp-with-over"></a>C. OVER と共に VARP を使用する  
 次の例では、カレンダー年度の四半期ごとの販売ノルマの値の `VARP` を返します。 OVER 句内の ORDER BY で統計的変位を、 SELECT ステートメントの ORDER BY で結果セットを並べ替えることに注目してください。  
  
```  
-- Uses AdventureWorks  
  
SELECT CalendarYear AS Year, CalendarQuarter AS Quarter, SalesAmountQuota AS SalesQuota,  
       VARP(SalesAmountQuota) OVER (ORDER BY CalendarYear, CalendarQuarter) AS Variance  
FROM dbo.FactSalesQuota  
WHERE EmployeeKey = 272 AND CalendarYear = 2002  
ORDER BY CalendarQuarter;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Year  Quarter  SalesQuota              Variance
----  -------  ----------------------  -------------------
2002  1         91000.0000             0.00
2002  2        140000.0000             600250000.00
2002  3         70000.0000             860222222.22
2002  4        154000.0000             1185187500.00
```  
  
## <a name="see-also"></a>参照  
 [集計関数 &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)   
 [OVER 句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)  
  
  

