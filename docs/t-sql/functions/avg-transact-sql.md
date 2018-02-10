---
title: "AVG (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 07/24/2017
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
- AVG_TSQL
- AVG
dev_langs: TSQL
helpviewer_keywords:
- AVG function [Transact-SQL]
- GROUP BY clause, AVG function
- DISTINCT keyword
- values [SQL Server], average
- average values
ms.assetid: 4534b705-d946-441b-9b5d-5fbe561c9131
caps.latest.revision: "52"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 40240e2c06055d61eb047c319349f4869b9979df
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="avg-transact-sql"></a>AVG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

グループ内の値の平均を返します。 NULL 値は無視されます。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
AVG ( [ ALL | DISTINCT ] expression )  
   OVER ( [ partition_by_clause ] order_by_clause )    
```  
  
## <a name="arguments"></a>引数  
ALL  
すべての値にこの集計関数を適用します。 ALL が既定値です。
  
DISTINCT  
値の出現回数にかかわらず、各値の一意なインスタンスだけに AVG を適用することを指定します。
  
*expression*  
真数型または概数型の[式](../../t-sql/language-elements/expressions-transact-sql.md)です。ただし、**bit** 型は除きます。 集計関数とサブクエリは使用できません。
  
OVER **(** [ *partition_by_clause* ] *order_by_clause* **)**  
*partition_by_clause*は FROM 句で生成される結果セットを関数が適用されるパーティションに分割します。 指定しない場合、関数ではクエリ結果セットのすべての行を 1 つのグループとして扱います。 *order_by_clause*は操作が実行される論理的順序を決定します。 *order_by_clause*は必須です。 詳細については、「[OVER 句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)を参照してください。 
  
## <a name="return-types"></a>戻り値の型
戻り値の型は、の評価結果の種類によって決まります*式*です。
  
|式の結果|戻り値の型|  
|---|---|
|**tinyint**|**int**|  
|**smallint**|**int**|  
|**int**|**int**|  
|**bigint**|**bigint**|  
|**decimal**型 (p, s)|**decimal (38、s)** を **decimal (10, 0)** で割ったもの |  
|**money**と**smallmoney**カテゴリ|**money**|  
|**float**と**real**カテゴリ|**float**|  
  
## <a name="remarks"></a>解説  
*expression* のデータ型が別名データ型の場合、戻り値の型も別名データ型になります。 ただし、**tinyint** から **int** への変換など、別名データ型の基本データ型が昇格する場合、戻り値は別名データ型ではなく昇格したデータ型になります。
  
AVG () は、値セットの合計を NULL 以外の値の数で除算することによって、これらの値の平均を計算します。 合計が戻り値のデータ型の最大値を超える場合は、エラーが返されます。
  
AVG は、OVER 句や ORDER BY 句なしで使用される場合は決定的関数です。 OVER 句や ORDER BY 句と共に使用される場合は、非決定的関数です。 詳細については、「 [決定的関数と非決定的関数](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)」を参照してください。
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-the-sum-and-avg-functions-for-calculations"></a>A. SUM 関数と AVG 関数を使用して計算する  
次の例では、[!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] の副社長が利用した休暇時間の平均および病気休暇時間の合計が計算されます。 これらの集計関数は、それぞれ取得されたすべての行の値の集計値を 1 つ返します。 この例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]データベースを使います。
  
```sql
SELECT AVG(VacationHours)AS 'Average vacation hours',   
    SUM(SickLeaveHours) AS 'Total sick leave hours'  
FROM HumanResources.Employee  
WHERE JobTitle LIKE 'Vice President%';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Average vacation hours       Total sick leave hours
 ----------------------       ----------------------
25                           97
  
(1 row(s) affected)
```
  
### <a name="b-using-the-sum-and-avg-functions-with-a-group-by-clause"></a>B. GROUP BY 句を伴う SUM 関数と AVG 関数を使用する  
各集計関数を `GROUP BY` 句と共に使用した場合、テーブル全体ではなく、グループごとに 1 つの値が返されます。 次の例は、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]データベースの販売区域ごとの集計の値を返します。 このサマリーでは、各区域の販売員が受け取ったボーナスの平均額と、各区域ごとの今年度の売上累計額が一覧表示されます。
  
```sql
SELECT TerritoryID, AVG(Bonus)as 'Average bonus', SUM(SalesYTD) as 'YTD sales'  
FROM Sales.SalesPerson  
GROUP BY TerritoryID;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
TerritoryID Average Bonus         YTD Sales  
----------- --------------------- ---------------------  
NULL        0.00                  1252127.9471  
1           4133.3333             4502152.2674  
2           4100.00               3763178.1787  
3           2500.00               3189418.3662  
4           2775.00               6709904.1666  
5           6700.00               2315185.611  
6           2750.00               4058260.1825  
7           985.00                3121616.3202  
8           75.00                 1827066.7118  
9           5650.00               1421810.9242  
10          5150.00               4116871.2277  
  
(11 row(s) affected)  
```  
  
### <a name="c-using-avg-with-distinct"></a>C. DISTINCT を伴う AVG を使用する  
次のステートメントは、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]データベース内の製品の平均表示価格を返します。 DISTINCT を指定すると、一意の値だけが計算で考慮されます。
  
```sql
SELECT AVG(DISTINCT ListPrice)  
FROM Production.Product;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
------------------------------
437.4042
  
(1 row(s) affected)
```
  
### <a name="d-using-avg-without-distinct"></a>D. DISTINCT を伴わない AVG を使用する  
DISTINCT がない場合、`AVG` 関数は、重複する値を含め、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースの `Product` テーブル内のすべての製品の平均表示価格を返します。
  
```sql
SELECT AVG(ListPrice)  
FROM Production.Product;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
------------------------------
438.6662
  
(1 row(s) affected)
```
  
### <a name="e-using-the-over-clause"></a>E. OVER 句を使用する  
次の例では、OVER 句を指定した AVG 関数を使用して、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]データベースの `Sales.SalesPerson` テーブルに各区域の年間売り上げの移動平均を入力します。 データは `TerritoryID` によってパーティションに分割され、`SalesYTD` によって論理的に順序付けされます。 つまり、AVG 関数は年を基にして区域ごとに計算されます。 `TerritoryID` 1 の 2005 年については、その年の 2 人の営業担当者を表す 2 行があります。 これら 2 行の平均売上が計算された後、2006 年の売上を表す 3 番目の行が計算に組み込まれます。
  
```sql
SELECT BusinessEntityID, TerritoryID   
   ,DATEPART(yy,ModifiedDate) AS SalesYear  
   ,CONVERT(varchar(20),SalesYTD,1) AS  SalesYTD  
   ,CONVERT(varchar(20),AVG(SalesYTD) OVER (PARTITION BY TerritoryID   
                                            ORDER BY DATEPART(yy,ModifiedDate)   
                                           ),1) AS MovingAvg  
   ,CONVERT(varchar(20),SUM(SalesYTD) OVER (PARTITION BY TerritoryID   
                                            ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS CumulativeTotal  
FROM Sales.SalesPerson  
WHERE TerritoryID IS NULL OR TerritoryID < 5  
ORDER BY TerritoryID,SalesYear;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
BusinessEntityID TerritoryID SalesYear   SalesYTD             MovingAvg            CumulativeTotal  
---------------- ----------- ----------- -------------------- -------------------- --------------------  
274              NULL        2005        559,697.56           559,697.56           559,697.56  
287              NULL        2006        519,905.93           539,801.75           1,079,603.50  
285              NULL        2007        172,524.45           417,375.98           1,252,127.95  
283              1           2005        1,573,012.94         1,462,795.04         2,925,590.07  
280              1           2005        1,352,577.13         1,462,795.04         2,925,590.07  
284              1           2006        1,576,562.20         1,500,717.42         4,502,152.27  
275              2           2005        3,763,178.18         3,763,178.18         3,763,178.18  
277              3           2005        3,189,418.37         3,189,418.37         3,189,418.37  
276              4           2005        4,251,368.55         3,354,952.08         6,709,904.17  
281              4           2005        2,458,535.62         3,354,952.08         6,709,904.17  
  
(10 row(s) affected)  
  
```  
  
この例では、OVER 句に PARTITION BY が含まれません。 これは、関数がクエリによって返されるすべての行に適用されることを意味します。 OVER 句で指定されている ORDER BY 句によって、AVG 関数が適用される論理的な順序が決まります。 このクエリは、WHERE 句で指定されているすべての販売区域について、年ごとの売上の移動平均を返します。 SELECT ステートメントで指定されている ORDER BY 句により、クエリの行が表示される順序が決まります。
  
```sql
SELECT BusinessEntityID, TerritoryID   
   ,DATEPART(yy,ModifiedDate) AS SalesYear  
   ,CONVERT(varchar(20),SalesYTD,1) AS  SalesYTD  
   ,CONVERT(varchar(20),AVG(SalesYTD) OVER (ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS MovingAvg  
   ,CONVERT(varchar(20),SUM(SalesYTD) OVER (ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS CumulativeTotal  
FROM Sales.SalesPerson  
WHERE TerritoryID IS NULL OR TerritoryID < 5  
ORDER BY SalesYear;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
BusinessEntityID TerritoryID SalesYear   SalesYTD             MovingAvg            CumulativeTotal  
---------------- ----------- ----------- -------------------- -------------------- --------------------  
274              NULL        2005        559,697.56           2,449,684.05         17,147,788.35  
275              2           2005        3,763,178.18         2,449,684.05         17,147,788.35  
276              4           2005        4,251,368.55         2,449,684.05         17,147,788.35  
277              3           2005        3,189,418.37         2,449,684.05         17,147,788.35  
280              1           2005        1,352,577.13         2,449,684.05         17,147,788.35  
281              4           2005        2,458,535.62         2,449,684.05         17,147,788.35  
283              1           2005        1,573,012.94         2,449,684.05         17,147,788.35  
284              1           2006        1,576,562.20         2,138,250.72         19,244,256.47  
287              NULL        2006        519,905.93           2,138,250.72         19,244,256.47  
285              NULL        2007        172,524.45           1,941,678.09         19,416,780.93  
(10 row(s) affected)  
```  
  
## <a name="see-also"></a>参照
[集計関数 &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[OVER 句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  
