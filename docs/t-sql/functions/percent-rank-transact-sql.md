---
title: "PERCENT_RANK (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 10/20/2015
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PERCENT_RANK_TSQL
- PERCENT_RANK
dev_langs: TSQL
helpviewer_keywords:
- PERCENT_RANK function
- analytic functions, PERCENT_RANK
ms.assetid: e361c2d4-c01f-4da4-8e89-1ddc724a2629
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f506b8f3007157f9e1757da76442af848d023494
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="percentrank-transact-sql"></a>PERCENT_RANK (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の行のグループ内の行の相対的な順位を計算します。 PERCENT_RANK を使用すると、クエリ結果またはパーティション内の値の相対的な順位を評価できます。 PERCENT_RANK は CUME_DIST 関数に似ています。  
  
## <a name="syntax"></a>構文  
  
```  
PERCENT_RANK( )  
    OVER ( [ partition_by_clause ] order_by_clause )  
  
```  
  
## <a name="arguments"></a>引数  
 OVER **(** [ *partition_by_clause* ] *order_by_clause* **)**  
 *partition_by_clause* は、FROM 句で生成された結果セットをパーティションに分割します。このパーティションに関数が適用されます。 指定しない場合、関数ではクエリ結果セットのすべての行を 1 つのグループとして扱います。 *order_by_clause* は、演算が実行される論理的順序を指定します。 *order_by_clause* は必須です。 OVER 構文の \<rows or range clause> は、PERCENT_RANK 関数では指定できません。 詳細については、「[OVER 句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)」を参照してください。  
  
## <a name="return-types"></a>戻り値の型  
 **float(53)**  
  
## <a name="general-remarks"></a>全般的な解説  
 PERCENT_RANK によって返される値の範囲は、0 より大きく、1 以下になります。  セットの最初の行では PERCENT_RANK は 0 です。 NULL 値は既定で含まれており、最小値として扱われます。  
  
 PERCENT_RANK は非決定的です。 詳細については、「 [決定的関数と非決定的関数](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
 次の例では、CUME_DIST 関数を使用して、特定の部門の各従業員の給与を百分位数で計算します。  CUME_DIST 関数によって返される値は、同じ部門の現在の従業員の給与以下の従業員が部門に占める割合を表します。 PERCENT_RANK 関数は、部門内の従業員の給与のランクが部門に占める割合を計算します。 PARTITION BY 句を指定して、部門別に結果セットの行をパーティションに分割します。 OVER 句で指定した ORDER BY 句によって、各パーティション内の行の順序が決められます。 SELECT ステートメントの ORDER BY 句によって、結果セット全体で行の並べ替えが行われます。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Department, LastName, Rate,   
       CUME_DIST () OVER (PARTITION BY Department ORDER BY Rate) AS CumeDist,   
       PERCENT_RANK() OVER (PARTITION BY Department ORDER BY Rate ) AS PctRank  
FROM HumanResources.vEmployeeDepartmentHistory AS edh  
    INNER JOIN HumanResources.EmployeePayHistory AS e    
    ON e.BusinessEntityID = edh.BusinessEntityID  
WHERE Department IN (N'Information Services',N'Document Control')   
ORDER BY Department, Rate DESC;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
Department             LastName               Rate                  CumeDist               PctRank  
---------------------- ---------------------- --------------------- ---------------------- ----------------------  
Document Control       Arifin                 17.7885               1                      1  
Document Control       Norred                 16.8269               0.8                    0.5  
Document Control       Kharatishvili          16.8269               0.8                    0.5  
Document Control       Chai                   10.25                 0.4                    0  
Document Control       Berge                  10.25                 0.4                    0  
Information Services   Trenary                50.4808               1                      1  
Information Services   Conroy                 39.6635               0.9                    0.888888888888889  
Information Services   Ajenstat               38.4615               0.8                    0.666666666666667  
Information Services   Wilson                 38.4615               0.8                    0.666666666666667  
Information Services   Sharma                 32.4519               0.6                    0.444444444444444  
Information Services   Connelly               32.4519               0.6                    0.444444444444444  
Information Services   Berg                   27.4038               0.4                    0  
Information Services   Meyyappan              27.4038               0.4                    0  
Information Services   Bacon                  27.4038               0.4                    0  
Information Services   Bueno                  27.4038               0.4                    0  
(15 row(s) affected)  
```  
  
## <a name="see-also"></a>参照  
 [CUME_DIST &#40;Transact-SQL&#41;](../../t-sql/functions/cume-dist-transact-sql.md)  
  
  
