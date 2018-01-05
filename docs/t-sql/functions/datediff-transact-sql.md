---
title: "DATEDIFF (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 07/29/2017
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
- DATEDIFF_TSQL
- DATEDIFF
dev_langs: TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- DATEDIFF function [SQL Server]
- time [SQL Server], crossed boundaries
- differences in date and time [SQL Server]
- counting crossed date time boundaries [SQL Server]
- date and time [SQL Server], DATEDIFF
- dates [SQL Server], crossed boundaries
- boundary differences date and time [SQL Server]
- functions [SQL Server], time
- functions [SQL Server], date and time
- interval dates [SQL Server]
- time [SQL Server], functions
- crossing date time boundaries [SQL Server]
- calculating dates times [SQL Server]
ms.assetid: eba979f2-1a8d-4cce-9d75-b74f9b519b37
caps.latest.revision: "52"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: cbbe6e93122cb69253b960afe067635ee0a852d8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="datediff-transact-sql"></a>DATEDIFF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

指定された数 (符号付き整数) を返します*datepart* 、指定された間の差*startdate*と*enddate*です。
  
大きな違いは、次を参照してください。 [DATEDIFF_BIG &#40;です。TRANSACT-SQL と #41 です。](../../t-sql/functions/datediff-big-transact-sql.md). すべての概要については[!INCLUDE[tsql](../../includes/tsql-md.md)]日付と時刻のデータ型および関数を参照してください[日付と時刻のデータ型および関数 &#40;TRANSACT-SQL と #41 です。](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
DATEDIFF ( datepart , startdate , enddate )  
```  
  
## <a name="arguments"></a>引数  
*datepart*  
一部である*startdate*と*enddate*を超えました。 境界の種類を指定します。 次の表にリストのすべての有効な*datepart*引数。 ユーザー定義変数に相当するものは無効です。
  
|*datepart*|省略形|  
|---|---|
|**year**|**yy、yyyy**|  
|**quarter**|**qq、q**|  
|**month**|**mm、m**|  
|**dayofyear**|**dy、y**|  
|**day**|**dd、d**|  
|**week**|**wk、ww**|  
|**hour**|**mm**|  
|**minute**|**mi、n**|  
|**second**|**ss、s**|  
|**millisecond**|**ms**|  
|**microsecond**|**mcs**|  
|**nanosecond**|**ns**|  
  
*startdate*  
式に解決されることができるは、**時間**、**日付**、 **smalldatetime**、 **datetime**、 **datetime2**、または**datetimeoffset**値。 *日付*できる式、列式、ユーザー定義変数または文字列リテラルです。 *startdate*から差し引かれます*enddate*です。
  
こうしたあいまいさを排除するため、4 桁の西暦を使用してください。 2 桁の年の詳細については、次を参照してください。[構成 two digit year cutoff Server Configuration Option](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)です。
  
*終了日*  
参照してください*startdate*です。
  
## <a name="return-type"></a>戻り値の型  
 **int**  
  
## <a name="return-value"></a>戻り値  
  
-   各*datepart*とその省略形は、同じ値を返します。  
  
戻り値が範囲外の場合**int** (-2,147, 483,648 ~ +2,147, 483,647)、エラーが返されます。 **ミリ秒**、最大時間差*startdate*と*enddate*は、24 日 20 時間 31 分 23.647 秒です。 **2 番目**、差の最大値は 68 年です。
  
場合*startdate*と*enddate*が両方割り当てられている時間の値のみ、 *datepart*時刻ではありません*datepart*0 が返されます。
  
タイム ゾーン オフセットのコンポーネント*startdate*または*endate*戻り値の計算では使用されません。
  
[Smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)が 1 分間にのみが正確なときに、 **smalldatetime**の値が使用*startdate*または*enddate*秒ミリ秒は常に、戻り値で 0 に設定します。
  
日付データ型の変数に時刻値だけが割り当てられた場合、欠落している日付要素の値は既定値である 1900-01-01 に設定されます。 時刻データ型または日付データ型の変数に日付値だけが割り当てられた場合、欠落している時刻要素の値は既定値である 00:00:00 に設定されます。 いずれか*startdate*または*enddate*ある時刻部分のみおよびその他ののみ、日付部分、欠落している時刻および日付の部分は、既定値に設定されます。
  
場合*startdate*と*enddate*の別の日付データ型は、1 つ以上の時刻の部分または秒の小数部の有効桁数よりも、他には、他の欠落している要素が 0 に設定されます。
  
## <a name="datepart-boundaries"></a>datepart 境界  
次のステートメントが同じである*startdate*と同じ*endate*です。 2 つの日付は隣接しており、時間的な差は .0000001 秒です。 間の違い、 *startdate*と*endate*の各ステートメント内の 1 つのカレンダーまたは時刻の境界を越えるその*datepart*です。 いずれのステートメントも戻り値は 1 です。 この例で異なる年を使用し、両方*startdate*と*endate*同じカレンダーの週の戻り値では、**週**0 になります。
  
```sql
SELECT DATEDIFF(year, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(quarter, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(month, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(dayofyear, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(day, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(week, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(hour, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(minute, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(second, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(millisecond, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
```
  
## <a name="remarks"></a>解説  
DATEDIFF は、選択リストのほか、WHERE 句、HAVING 句、GROUP BY 句、および ORDER BY 句で使用できます。
  
DATEDIFF は、文字列リテラルを暗黙的にキャスト、 **datetime2**型です。 つまり、DATEDIFF では、日付が文字列として渡される場合、YDM 形式をサポートしません。 文字列を明示的にキャストする必要があります、 **datetime**または**smalldatetime** YDM 形式を使用する型。
  
SET DATEFIRST を指定しても DATEDIFF に影響はありません。 DATEDIFF では、週の最初の曜日として常に日曜日を使用し、関数が決定的であることを確認します。
  
## <a name="examples"></a>使用例  
次の例の引数としてさまざまな種類の式を使用して、 *startdate*と*enddate*パラメーター。
  
### <a name="a-specifying-columns-for-startdate-and-enddate"></a>A. startdate と enddate に列を指定する  
次の例では、テーブルの 2 つの列に日付を格納し、両者の差を日単位で計算しています。
  
```sql
CREATE TABLE dbo.Duration  
    (  
    startDate datetime2  
    ,endDate datetime2  
    );  
INSERT INTO dbo.Duration(startDate,endDate)  
    VALUES('2007-05-06 12:10:09','2007-05-07 12:10:09');  
SELECT DATEDIFF(day,startDate,endDate) AS 'Duration'  
FROM dbo.Duration;  
-- Returns: 1  
```  
  
### <a name="b-specifying-user-defined-variables-for-startdate-and-enddate"></a>B. startdate と enddate にユーザー定義変数を指定する  
次の例の引数としてユーザー定義変数を使用して*startdate*と*enddate*です。
  
```sql
DECLARE @startdate datetime2 = '2007-05-05 12:10:09.3312722';  
DECLARE @enddate datetime2 = '2007-05-04 12:10:09.3312722';   
SELECT DATEDIFF(day, @startdate, @enddate);  
```  
  
### <a name="c-specifying-scalar-system-functions-for-startdate-and-enddate"></a>C. startdate と enddate にスカラー システム関数を指定する  
次の例の引数としてスカラー システム関数を使用して*startdate*と*enddate*です。
  
```sql
SELECT DATEDIFF(millisecond, GETDATE(), SYSDATETIME());  
```  
  
### <a name="d-specifying-scalar-subqueries-and-scalar-functions-for-startdate-and-enddate"></a>D. startdate と enddate にスカラー サブクエリおよびスカラー関数を指定する  
次の例の引数としてスカラー サブクエリおよびスカラー関数を使用して*startdate*と*enddate*です。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT DATEDIFF(day,(SELECT MIN(OrderDate) FROM Sales.SalesOrderHeader),  
    (SELECT MAX(OrderDate) FROM Sales.SalesOrderHeader));  
```  
  
### <a name="e-specifying-constants-for-startdate-and-enddate"></a>E. startdate と enddate に定数を指定する  
次の例の引数として文字定数を使用して*startdate*と*enddate*です。
  
```sql
SELECT DATEDIFF(day, '2007-05-07 09:53:01.0376635'  
    , '2007-05-08 09:53:01.0376635');  
```  
  
### <a name="f-specifying-numeric-expressions-and-scalar-system-functions-for-enddate"></a>F. enddate に数値式およびスカラー システム関数を指定する  
次の例では、数値式を`(GETDATE ()+ 1)`、およびスカラー システム関数、`GETDATE`と`SYSDATETIME`、引数として*enddate*です。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT DATEDIFF(day, '2007-05-07 09:53:01.0376635', GETDATE()+ 1)   
    AS NumberOfDays  
FROM Sales.SalesOrderHeader;  
GO  
USE AdventureWorks2012;  
GO  
SELECT DATEDIFF(day, '2007-05-07 09:53:01.0376635', DATEADD(day,1,SYSDATETIME())) AS NumberOfDays  
FROM Sales.SalesOrderHeader;  
GO  
```  
  
### <a name="g-specifying-ranking-functions-for-startdate"></a>G. startdate に順位付け関数を指定する  
次の例の引数として順位付け関数を使用して*startdate*です。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT p.FirstName, p.LastName  
    ,DATEDIFF(day,ROW_NUMBER() OVER (ORDER BY   
        a.PostalCode),SYSDATETIME()) AS 'Row Number'  
FROM Sales.SalesPerson s   
    INNER JOIN Person.Person p   
        ON s.BusinessEntityID = p.BusinessEntityID  
    INNER JOIN Person.Address a   
        ON a.AddressID = p.BusinessEntityID  
WHERE TerritoryID IS NOT NULL   
    AND SalesYTD <> 0;  
```  
  
### <a name="h-specifying-an-aggregate-window-function-for-startdate"></a>H. startdate に集計関数を指定する  
次の例に集計関数の引数として*startdate*です。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT soh.SalesOrderID, sod.ProductID, sod.OrderQty,soh.OrderDate  
    ,DATEDIFF(day,MIN(soh.OrderDate)   
        OVER(PARTITION BY soh.SalesOrderID),SYSDATETIME() ) AS 'Total'  
FROM Sales.SalesOrderDetail sod  
    INNER JOIN Sales.SalesOrderHeader soh  
        ON sod.SalesOrderID = soh.SalesOrderID  
WHERE soh.SalesOrderID IN(43659,58918);  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例:[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]と[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
次の例の引数としてさまざまな種類の式を使用して、 *startdate*と*enddate*パラメーター。
  
### <a name="i-specifying-columns-for-startdate-and-enddate"></a>I. startdate と enddate に列を指定する  
次の例では、テーブルの 2 つの列に日付を格納し、両者の差を日単位で計算しています。
  
```sql
CREATE TABLE dbo.Duration (  
    startDate datetime2  
    ,endDate datetime2  
    );  
INSERT INTO dbo.Duration(startDate,endDate)  
    VALUES('2007-05-06 12:10:09','2007-05-07 12:10:09');  
SELECT TOP(1) DATEDIFF(day,startDate,endDate) AS Duration  
FROM dbo.Duration;  
-- Returns: 1  
```  
  
### <a name="j-specifying-scalar-subqueries-and-scalar-functions-for-startdate-and-enddate"></a>J. startdate と enddate にスカラー サブクエリおよびスカラー関数を指定する  
次の例の引数としてスカラー サブクエリおよびスカラー関数を使用して*startdate*と*enddate*です。
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEDIFF(day,(SELECT MIN(HireDate) FROM dbo.DimEmployee),  
    (SELECT MAX(HireDate) FROM dbo.DimEmployee))   
FROM dbo.DimEmployee;  
  
```  
  
### <a name="k-specifying-constants-for-startdate-and-enddate"></a>K. startdate と enddate に定数を指定する  
次の例の引数として文字定数を使用して*startdate*と*enddate*です。
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEDIFF(day, '2007-05-07 09:53:01.0376635'  
    , '2007-05-08 09:53:01.0376635') FROM DimCustomer;  
```  
  
### <a name="l-specifying-ranking-functions-for-startdate"></a>L. startdate に順位付け関数を指定する  
次の例の引数として順位付け関数を使用して*startdate*です。
  
```sql
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
,DATEDIFF(day,ROW_NUMBER() OVER (ORDER BY   
        DepartmentName),SYSDATETIME()) AS RowNumber  
FROM dbo.DimEmployee;  
```  
  
### <a name="m-specifying-an-aggregate-window-function-for-startdate"></a>M. startdate に集計関数を指定する  
次の例に集計関数の引数として*startdate*です。
  
```sql
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, DepartmentName  
    ,DATEDIFF(year,MAX(HireDate)  
             OVER (PARTITION BY DepartmentName),SYSDATETIME()) AS SomeValue  
FROM dbo.DimEmployee  
```  
  
## <a name="see-also"></a>参照
[DATEDIFF_BIG &#40;です。TRANSACT-SQL と #41 です。](../../t-sql/functions/datediff-big-transact-sql.md)  
[CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  


