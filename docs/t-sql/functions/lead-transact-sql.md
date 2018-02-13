---
title: "LEAD (Transact-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 11/09/2017
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
- LEAD_TSQL
- LEAD
dev_langs: TSQL
helpviewer_keywords:
- LEAD function
- analytic functions, LEAD
ms.assetid: 21f66bbf-d1ea-4f75-a3c4-20dc7fc1c69e
caps.latest.revision: "22"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 67b5d9300d4be84d16b2a650265e812eba1988a9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="lead-transact-sql"></a>LEAD (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] の自己結合を使用せずに同じ結果セットの後続の行からデータにアクセスします。 LEAD によって、現在の行の後に続く指定された物理的なオフセットの行にアクセスできます。 SELECT ステートメントでこの分析関数を使用して、現在の行の値と後続の行の値を比較します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
LEAD ( scalar_expression [ ,offset ] , [ default ] )   
    OVER ( [ partition_by_clause ] order_by_clause )  
```  
  
## <a name="arguments"></a>引数  
 *scalar_expression*  
 指定されたオフセットに基づいて返される値。 単一の (スカラー) 値を返す任意の型の式です。 *scalar_expression* は分析関数にはなりません。  
  
 *offset*  
 値を取得する現在の行よりも前にある行の数。 指定しない場合は、1 が既定値です。 *offset* は、列、サブクエリ、または正の整数と評価されたり、暗黙的に **bigint** に変換される可能性があるその他の式です。 *offset* は、負の値または分析関数にはなりません。  
  
 *default*  
 *offset* の *scalar_expression* が NULL の場合に返される値。 既定値を指定しない場合、NULL が返されます。 *default* には、列、サブクエリ、または式を指定できますが、分析関数は指定できません。 *default* には、*scalar_expression* の型との互換性が必要です。  
  
 OVER **(** [ *partition_by_clause* ] *order_by_clause* **)**  
 *partition_by_clause* は、FROM 句で生成された結果セットをパーティションに分割します。このパーティションに関数が適用されます。 指定しない場合、関数ではクエリ結果セットのすべての行を 1 つのグループとして扱います。 *order_by_clause* は、関数を適用する前にデータの順序を決定します。 *partition_by_clause* が指定されると、各パーティションのデータの順序が決まります。 *order_by_clause* は必須です。 詳細については、「[OVER 句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)」を参照してください。  
  
## <a name="return-types"></a>戻り値の型  
 指定した *scalar_expression* のデータ型。 *scalar_expression* で NULL 値が許可されているか *default* が NULL に設定されていると、NULL が返されます。  
  
 LEAD は非決定的です。 詳細については、「 [決定的関数と非決定的関数](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-compare-values-between-years"></a>A. 年間の値を比較します。  
 クエリでは、LEAD 関数を使用して後の数年間にわたる特定従業員の販売ノルマの差が返されます。 最後の行に使用できるリード値がないため、既定のゼロ (0) が返されることに注意してください。  
  
```t-sql  
USE AdventureWorks2012;  
GO  
SELECT BusinessEntityID, YEAR(QuotaDate) AS SalesYear, SalesQuota AS CurrentQuota,   
    LEAD(SalesQuota, 1,0) OVER (ORDER BY YEAR(QuotaDate)) AS NextQuota  
FROM Sales.SalesPersonQuotaHistory  
WHERE BusinessEntityID = 275 and YEAR(QuotaDate) IN ('2005','2006');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
BusinessEntityID SalesYear   CurrentQuota          NextQuota  
---------------- ----------- --------------------- ---------------------  
275              2005        367000.00             556000.00  
275              2005        556000.00             502000.00  
275              2006        502000.00             550000.00  
275              2006        550000.00             1429000.00  
275              2006        1429000.00            1324000.00  
275              2006        1324000.00            0.00  
```  
  
### <a name="b-compare-values-within-partitions"></a>B. パーティション内の値を比較します。  
 次の例では、LEAD 関数を使用して従業員間の今年に入ってからの売上高を比較します。 PARTITION BY 句を指定して、販売区域ごとに結果セットの行をパーティションに分割します。 LEAD 関数は各パーティションに対して個別に適用され、各パーティションで計算が新たに行われます。 OVER 句で指定した ORDER BY 句によって、関数が適用される前に各パーティションの行の順序が設定されます。 SELECT ステートメントの ORDER BY 句によって、結果セット全体で行の順序付けが行われます。 各パーティションの最後の行に使用できるリード値がないため、既定のゼロ (0) が返されることに注意してください。  
  
```t-sql  
USE AdventureWorks2012;  
GO  
SELECT TerritoryName, BusinessEntityID, SalesYTD,   
       LEAD (SalesYTD, 1, 0) OVER (PARTITION BY TerritoryName ORDER BY SalesYTD DESC) AS NextRepSales  
FROM Sales.vSalesPerson  
WHERE TerritoryName IN (N'Northwest', N'Canada')   
ORDER BY TerritoryName;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```   
TerritoryName            BusinessEntityID SalesYTD              NextRepSales  
-----------------------  ---------------- --------------------- ---------------------  
Canada                   282              2604540.7172          1453719.4653  
Canada                   278              1453719.4653          0.00  
Northwest                284              1576562.1966          1573012.9383  
Northwest                283              1573012.9383          1352577.1325  
Northwest                280              1352577.1325          0.00  
  
```  
  
### <a name="c-specifying-arbitrary-expressions"></a>C. 任意の式を指定する  
 次の例では、LEAD 関数の構文にさまざまな任意の式を指定する方法を示します。  
  
```t-sql  
CREATE TABLE T (a int, b int, c int);   
GO  
INSERT INTO T VALUES (1, 1, -3), (2, 2, 4), (3, 1, NULL), (4, 3, 1), (5, 2, NULL), (6, 1, 5);   
  
SELECT b, c,   
    LEAD(2*c, b*(SELECT MIN(b) FROM T), -c/2.0) OVER (ORDER BY a) AS i  
FROM T;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
b           c           i  
----------- ----------- -----------  
1           -3          8  
2           4           2  
1           NULL        2  
3           1           0  
2           NULL        NULL  
1           5           -2  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例:[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]と[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-compare-values-between-quarters"></a>D: 四半期間で値を比較します。  
 次の例では、LEAD 関数を示します。 クエリでは、後続のカレンダー四半期に、指定された従業員の販売ノルマの値の差を取得します。 ないためリード値使用可能な最後の行の後に、ゼロ (0) の既定値が使用されることに注意してください。  
  
```t-sql  
-- Uses AdventureWorks  
  
SELECT CalendarYear AS Year, CalendarQuarter AS Quarter, SalesAmountQuota AS SalesQuota,  
       LEAD(SalesAmountQuota,1,0) OVER (ORDER BY CalendarYear, CalendarQuarter) AS NextQuota,  
   SalesAmountQuota - LEAD(Sale sAmountQuota,1,0) OVER (ORDER BY CalendarYear, CalendarQuarter) AS Diff  
FROM dbo.FactSalesQuota  
WHERE EmployeeKey = 272 AND CalendarYear IN (2001,2002)  
ORDER BY CalendarYear, CalendarQuarter;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Year Quarter  SalesQuota  NextQuota  Diff  
---- -------  ----------  ---------  -------------  
2001 3        28000.0000   7000.0000   21000.0000 
2001 4         7000.0000  91000.0000  -84000.0000  
2001 1        91000.0000 140000.0000  -49000.0000  
2002 2       140000.0000   7000.0000    7000.0000  
2002 3         7000.0000 154000.0000   84000.0000  
2002 4       154000.0000      0.0000  154000.0000
```  
  
## <a name="see-also"></a>参照  
 [LAG &#40;Transact-SQL&#41;](../../t-sql/functions/lag-transact-sql.md)  
  
  


