---
title: "FIRST_VALUE (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 11/10/2016
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
- FIRST_VALUE_TSQL
- FIRST_VALUE
dev_langs: TSQL
helpviewer_keywords:
- FIRST_VALUE function
- analytic functions, FIRST_VALUE
ms.assetid: 1990c3c7-dad2-48db-b2cd-3e8bd2c49d17
caps.latest.revision: "15"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 57c3f22adbc1073fc15e72e3228c1b65101bdbbc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="firstvalue-transact-sql"></a>FIRST_VALUE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の順序付けられた値のセットにある最初の値を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
FIRST_VALUE ( [scalar_expression ] )   
    OVER ( [ partition_by_clause ] order_by_clause [ rows_range_clause ] )  
  
```  
  
## <a name="arguments"></a>引数  
 *scalar_expression*  
 返される値。 *scalar_expression*列、サブクエリ、またはその他の任意の式を結果が 1 つの値を指定できます。 他の分析関数は指定できません。  
  
 OVER **(** [ *partition_by_clause* ] *order_by_clause* [ *rows_range_clause* ] **)**  
 *partition_by_clause* は、FROM 句で生成された結果セットをパーティションに分割します。このパーティションに関数が適用されます。 指定しない場合、関数ではクエリ結果セットのすべての行を 1 つのグループとして扱います。 *order_by_clause* は、演算が実行される論理的順序を指定します。 *order_by_clause* は必須です。 *rows_range_clause* はさらに、開始点と終了点を指定してパーティション内の行を制限します。 詳細については、「[OVER 句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)」を参照してください。  
  
## <a name="return-types"></a>戻り値の型  
 *scalar_expression* と同じ型です。  
  
## <a name="general-remarks"></a>全般的な解説  
 FIRST_VALUE は非決定的です。 詳細については、「 [決定的関数と非決定的関数](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-firstvalue-over-a-query-result-set"></a>A. クエリ結果セットで FIRST_VALUE を使用する  
 次の例では、FIRST_VALUE を使用して、指定された製品カテゴリ内で最も安価な製品の名前を返します。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Name, ListPrice,   
       FIRST_VALUE(Name) OVER (ORDER BY ListPrice ASC) AS LeastExpensive   
FROM Production.Product  
WHERE ProductSubcategoryID = 37;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
Name                    ListPrice             LeastExpensive  
----------------------- --------------------- --------------------  
Patch Kit/8 Patches     2.29                  Patch Kit/8 Patches  
Road Tire Tube          3.99                  Patch Kit/8 Patches  
Touring Tire Tube       4.99                  Patch Kit/8 Patches  
Mountain Tire Tube      4.99                  Patch Kit/8 Patches  
LL Road Tire            21.49                 Patch Kit/8 Patches  
ML Road Tire            24.99                 Patch Kit/8 Patches  
LL Mountain Tire        24.99                 Patch Kit/8 Patches  
Touring Tire            28.99                 Patch Kit/8 Patches  
ML Mountain Tire        29.99                 Patch Kit/8 Patches  
HL Road Tire            32.60                 Patch Kit/8 Patches  
HL Mountain Tire        35.00                 Patch Kit/8 Patches  
  
```  
  
### <a name="b-using-firstvalue-over-partitions"></a>B. パーティションで FIRST_VALUE を使用する  
 次の例では、FIRST_VALUE を使用して、同じ役職に付いている他の従業員と比べて、最も休暇時間数が少ない従業員を返します。 PARTITION BY 句によって役職ごとに従業員がパーティションに分割され、各パーティションに個別に FIRST_VALUE 関数が適用されます。 OVER 句に指定された ORDER BY 句は、各パーティション内の行に FIRST_VALUE 関数が適用される論理的な順序を決定します。 ROWS UNBOUNDED PRECEDING 句は、ウィンドウの開始位置が各パーティションの最初の行であることを指定します。  
  
```  
USE AdventureWorks2012;   
GO  
SELECT JobTitle, LastName, VacationHours,   
       FIRST_VALUE(LastName) OVER (PARTITION BY JobTitle   
                                   ORDER BY VacationHours ASC  
                                   ROWS UNBOUNDED PRECEDING  
                                  ) AS FewestVacationHours  
FROM HumanResources.Employee AS e  
INNER JOIN Person.Person AS p   
    ON e.BusinessEntityID = p.BusinessEntityID  
ORDER BY JobTitle;  
```  
  
 部分的な結果セットを次に示します。  
  
```  
  
JobTitle                            LastName                  VacationHours FewestVacationHours  
----------------------------------- ------------------------- ------------- -------------------  
Accountant                          Moreland                  58            Moreland  
Accountant                          Seamans                   59            Moreland  
Accounts Manager                    Liu                       57            Liu  
Accounts Payable Specialist         Tomic                     63            Tomic  
Accounts Payable Specialist         Sheperdigian              64            Tomic  
Accounts Receivable Specialist      Poe                       60            Poe  
Accounts Receivable Specialist      Spoon                     61            Poe  
Accounts Receivable Specialist      Walton                    62            Poe  
```  
  
## <a name="see-also"></a>参照  
 [OVER 句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)  
  
  
