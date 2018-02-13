---
title: "CUME_DIST (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 07/24/2017
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
- CUME_DIST
- CUME_DIST_TSQL
dev_langs: TSQL
helpviewer_keywords:
- CUME_DIST function
- analytic functions, CUME_DIST
ms.assetid: 491b07f3-9ffd-4cdd-93e5-5abb636fc5ef
caps.latest.revision: "19"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: dadae05fa8556b403c6cba436647203b30452559
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="cumedist-transact-sql"></a>CUME_DIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にある値のグループ内の値の累積分布を計算します。 つまり、CUME_DIST は、値のグループにおける指定された値の相対位置を計算します。 行 *r* の場合、昇順と仮定して、*r* の CUME_DIST は *r* の値以下の値を持つ行の数を、パーティションまたはクエリ結果セット内で評価された行の数で割った値になります。 CUME_DIST は、PERCENT_RANK 関数に似ています。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
CUME_DIST( )  
    OVER ( [ partition_by_clause ] order_by_clause )  
  
```  
  
## <a name="arguments"></a>引数  
OVER **(** [ *partition_by_clause* ] *order_by_clause* **)**  
*partition_by_clause* は、FROM 句で生成された結果セットをパーティションに分割します。このパーティションに関数が適用されます。 指定しない場合、関数ではクエリ結果セットのすべての行を 1 つのグループとして扱います。 *order_by_clause* は、演算が実行される論理的順序を指定します。 *order_by_clause* は必須です。 OVER 構文の \<rows or range clause> は、CUME_DIST 関数では指定できません。 詳細については、「[OVER 句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)」を参照してください。
  
## <a name="return-types"></a>戻り値の型
**float(53)**
  
## <a name="remarks"></a>解説  
CUME_DIST によって返される値の範囲は、0 より大きく、1 以下になります。  同順位の値は常に、同じ累積分布の値に評価されます。 NULL 値は既定で含まれており、最小値として扱われます。
  
CUME_DIST は非決定的です。 詳細については、「 [決定的関数と非決定的関数](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)」を参照してください。
  
## <a name="examples"></a>使用例  
次の例では、CUME_DIST 関数を使用して、特定の部門の各従業員の給与を百分位数で計算します。  CUME_DIST 関数によって返される値は、同じ部門の現在の従業員の給与以下の従業員が部門に占める割合を表します。 PERCENT_RANK 関数は、部門における従業員の給与の割合の順位を計算します。 PARTITION BY 句を指定して、部門別に結果セットの行をパーティションに分割します。 OVER 句に指定された ORDER BY 句によって、各パーティション内の行が論理的に順序付けられます。 SELECT ステートメントの ORDER BY 句によって、結果セットの表示順序が決定されます。
  
```sql
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
  
```sql
  
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
[PERCENT_RANK &#40;Transact-SQL&#41;](../../t-sql/functions/percent-rank-transact-sql.md)
  
  
