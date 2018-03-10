---
title: "DATEADD (TRANSACT-SQL) |Microsoft ドキュメント"
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
- DATEADD
- DATEADD_TSQL
dev_langs: TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- add interval to date or time [SQL Server]
- subtract interval from date or time [SQL Server]
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
- dates [SQL Server], intervals
- date and time [SQL Server], DATEADD
- DATEADD function [SQL Server]
ms.assetid: 89c5ae32-89c6-47e1-979e-15d97908b9f1
caps.latest.revision: "71"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: db5499d73b4eab7ff4ba3079469412cc30a111a3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="dateadd-transact-sql"></a>DATEADD (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

*number* に指定された間隔 (符号付き整数) を加算した *date* を返します。この間隔は、指定した *date* の *datepart* に加算されます。
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] の日付と時刻のデータ型および関数の概要については、「[日付と時刻のデータ型および関数 &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)」を参照してください。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
DATEADD (datepart , number , date )  
```  
  
## <a name="arguments"></a>引数  
*datepart*  
**integer** 型の *number* を、*date* のどの構成要素に加算するかを指定します。 次の表は、*datepart* 引数に有効なすべての値の一覧です。 ユーザー定義変数に相当するものは無効です。
  
|*datepart*|省略形|  
|---|---|
|**year**|**yy**, **yyyy**|  
|**quarter**|**qq**, **q**|  
|**month**|**mm**, **m**|  
|**dayofyear**|**dy**, **y**|  
|**day**|**dd**, **d**|  
|**week**|**wk**, **ww**|  
|**weekday**|**dw**, **w**|  
|**hour**|**mm**|  
|**minute**|**mi**, **n**|  
|**second**|**ss**, **s**|  
|**millisecond**|**ms**|  
|**microsecond**|**mcs**|  
|**nanosecond**|**ns**|  
  
*number*  
*date* の *datepart* に加算する値として、[int](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md) 型に解決可能な式を指定します。 ユーザー定義型の変数は有効です。  
小数を含む値を指定した場合、小数部は丸められずに切り捨てられます。
  
*date*  
**time** 、**date**、**smalldatetime**、**datetime**、**datetime2**、**datetimeoffset** のいずれかの値に解決可能な式を指定します。 *date* には、式、列式、ユーザー定義変数、または文字列リテラルを指定できます。 式が文字列リテラルの場合は、**datetime** に解決する必要があります。 このあいまいな状態を避けるためには、4 桁の西暦を使用して表記します。 2 桁の年の詳細については、「[two digit year cutoff サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)」を参照してください。
  
## <a name="return-types"></a>戻り値の型
文字列リテラルを除き、戻り値のデータ型は、*date* 引数のデータ型になります。
文字列リテラルの戻り値のデータ型は **datetime** です。 文字列リテラルの秒の小数点以下桁数が 3 桁 (. nnn) を超えた場合またはタイム ゾーン オフセット部分を含んでいた場合、エラーが発生します。
  
## <a name="return-value"></a>戻り値  
  
## <a name="datepart-argument"></a>datepart 引数  
**dayofyear**、**day**、および**weekday**は同じ値を返します。
  
各*datepart*とその省略形は、同じ値を返します。
  
*datepart*が**month**で、*date*の月が戻り値の月より多くの日を持ち、*date*の日が戻り値の月に存在しない場合、戻り値の月の最終日が返されます。 たとえば、9 月の日数は 30 日であるので、次の 2 つのステートメントは、2006-09-30 00:00:00.000 を返します。
  
```sql
SELECT DATEADD(month, 1, '2006-08-30');
SELECT DATEADD(month, 1, '2006-08-31');
```
  
## <a name="number-argument"></a>number 引数  
*number* 引数に、**int** の範囲を超える値は指定できません。 次のステートメントでは、*number* 引数が **int** の範囲を 1 つ超えています。 "`Msg 8115, Level 16, State 2, Line 1. Arithmetic overflow error converting expression to data type int.`"というエラー メッセージが返されます。
  
```sql
SELECT DATEADD(year,2147483648, '2006-07-31');  
SELECT DATEADD(year,-2147483649, '2006-07-31');  
```  
  
## <a name="date-argument"></a>date 引数  
*date* 引数を、そのデータ型の範囲外の値に増やすことはできません。 次のステートメントでは、*date* 値に加算される *number* 値が、*date* データ型の範囲を超えています。 "`Msg 517, Level 16, State 1, Line 1 Adding a value to a 'datetime' column caused overflow.`" というエラー メッセージが返されます。
  
```sql
SELECT DATEADD(year,2147483647, '2006-07-31');  
SELECT DATEADD(year,-2147483647, '2006-07-31');  
```  
  
## <a name="return-values-for-a-smalldatetime-date-and-a-second-or-fractional-seconds-datepart"></a>smalldatetime に対する戻り値 (秒または 1 秒未満の秒)  
[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) 値の秒要素は常に 00 になります。 *date* が **smalldatetime** の場合、次の規則が適用されます。
- *datepart*が**second**で*number*が -30 ～ +29 である場合、加算処理は実行されません。
- *datepart*が**second**で*number*が -30 より小さいか +29 より大きい場合、加算処理は 1 分から実行されます。
- *datepart*が**millisecond**で*number*が -30001 ～ +29998 である場合、加算処理は実行されません。
- *datepart*が**millisecond**で*number*が -30001 より小さいか +29998 より大きい場合、加算処理は 1 分から実行されます。
  
## <a name="remarks"></a>解説  
DATEADD は、SELECT \<list> のほか、WHERE 句、HAVING 句、GROUP BY 句、および ORDER BY 句で使用できます。
  
## <a name="fractional-seconds-precision"></a>秒の小数部の有効桁数
*date*のデータ型が**smalldatetime**、**date**、**datetime**のいずれかである場合、*datepart*を**microsecond**や**nanosecond**にして加算処理を行うことはできません。

ミリ秒の小数点以下桁数は 3 (.123) です。マイクロ秒の小数点以下桁数は 6 (.123456) です。ナノ秒の小数点以下桁数は 9 (.123456789) です。 **time**、 **datetime2**、および**datetimeoffset**データ型がある最大小数点以下桁数は 7 (. 1234567)。*datepart*が**nanosecond**である場合、*date*の秒の小数部を増やす前に、*number*を 100 にする必要があります。1 ～ 49 の*number*は 0 に切り捨てられ、50 ～ 99 は 100 に切り上げられます。
  
次のステートメントでは、**millisecond**、**microsecond**、または**nanosecond**の*datepart*を加算します。
  
```sql
DECLARE @datetime2 datetime2 = '2007-01-01 13:10:10.1111111';  
SELECT '1 millisecond', DATEADD(millisecond,1,@datetime2)  
UNION ALL  
SELECT '2 milliseconds', DATEADD(millisecond,2,@datetime2)  
UNION ALL  
SELECT '1 microsecond', DATEADD(microsecond,1,@datetime2)  
UNION ALL  
SELECT '2 microseconds', DATEADD(microsecond,2,@datetime2)  
UNION ALL  
SELECT '49 nanoseconds', DATEADD(nanosecond,49,@datetime2)  
UNION ALL  
SELECT '50 nanoseconds', DATEADD(nanosecond,50,@datetime2)  
UNION ALL  
SELECT '150 nanoseconds', DATEADD(nanosecond,150,@datetime2);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
1 millisecond     2007-01-01 13:10:10.1121111  
2 milliseconds    2007-01-01 13:10:10.1131111  
1 microsecond     2007-01-01 13:10:10.1111121  
2 microseconds    2007-01-01 13:10:10.1111131  
49 nanoseconds    2007-01-01 13:10:10.1111111  
50 nanoseconds    2007-01-01 13:10:10.1111112  
150 nanoseconds   2007-01-01 13:10:10.1111113  
```  
  
## <a name="time-zone-offset"></a>タイム ゾーン オフセット
タイム ゾーン オフセットの加算は許可されません。
  
## <a name="examples"></a>使用例  

### <a name="a-incrementing-datepart-by-an-interval-of-1"></a>A. datepart を 1 単位増やす  
次の各ステートメントでは、*datepart* を 1 単位増やしています。
  
```sql
DECLARE @datetime2 datetime2 = '2007-01-01 13:10:10.1111111';  
SELECT 'year', DATEADD(year,1,@datetime2)  
UNION ALL  
SELECT 'quarter',DATEADD(quarter,1,@datetime2)  
UNION ALL  
SELECT 'month',DATEADD(month,1,@datetime2)  
UNION ALL  
SELECT 'dayofyear',DATEADD(dayofyear,1,@datetime2)  
UNION ALL  
SELECT 'day',DATEADD(day,1,@datetime2)  
UNION ALL  
SELECT 'week',DATEADD(week,1,@datetime2)  
UNION ALL  
SELECT 'weekday',DATEADD(weekday,1,@datetime2)  
UNION ALL  
SELECT 'hour',DATEADD(hour,1,@datetime2)  
UNION ALL  
SELECT 'minute',DATEADD(minute,1,@datetime2)  
UNION ALL  
SELECT 'second',DATEADD(second,1,@datetime2)  
UNION ALL  
SELECT 'millisecond',DATEADD(millisecond,1,@datetime2)  
UNION ALL  
SELECT 'microsecond',DATEADD(microsecond,1,@datetime2)  
UNION ALL  
SELECT 'nanosecond',DATEADD(nanosecond,1,@datetime2);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Year         2008-01-01 13:10:10.1111111  
quarter      2007-04-01 13:10:10.1111111  
month        2007-02-01 13:10:10.1111111  
dayofyear    2007-01-02 13:10:10.1111111  
day          2007-01-02 13:10:10.1111111  
week         2007-01-08 13:10:10.1111111  
weekday      2007-01-02 13:10:10.1111111  
hour         2007-01-01 14:10:10.1111111  
minute       2007-01-01 13:11:10.1111111  
second       2007-01-01 13:10:11.1111111  
millisecond  2007-01-01 13:10:10.1121111  
microsecond  2007-01-01 13:10:10.1111121  
nanosecond   2007-01-01 13:10:10.1111111  
```  
  
### <a name="b-incrementing-more-than-one-level-of-datepart-in-one-statement"></a>B. 単一のステートメントで datepart を複数単位増やす  
次の各ステートメントでは、*number* を、上位の *datepart* への繰り上がりが生じる程度に大きくとって、*date* の *datepart* を増やしています。
  
```sql
DECLARE @datetime2 datetime2;  
SET @datetime2 = '2007-01-01 01:01:01.1111111';  
--Statement                                 Result     
-------------------------------------------------------------------   
SELECT DATEADD(quarter,4,@datetime2);     --2008-01-01 01:01:01.110  
SELECT DATEADD(month,13,@datetime2);      --2008-02-01 01:01:01.110  
SELECT DATEADD(dayofyear,365,@datetime2); --2008-01-01 01:01:01.110  
SELECT DATEADD(day,365,@datetime2);       --2008-01-01 01:01:01.110  
SELECT DATEADD(week,5,@datetime2);        --2007-02-05 01:01:01.110  
SELECT DATEADD(weekday,31,@datetime2);    --2007-02-01 01:01:01.110  
SELECT DATEADD(hour,23,@datetime2);       --2007-01-02 00:01:01.110  
SELECT DATEADD(minute,59,@datetime2);     --2007-01-01 02:00:01.110  
SELECT DATEADD(second,59,@datetime2);     --2007-01-01 01:02:00.110  
SELECT DATEADD(millisecond,1,@datetime2); --2007-01-01 01:01:01.110  
```  
  
### <a name="c-using-expressions-as-arguments-for-the-number-and-date-parameters"></a>C. number パラメーターと date パラメーターの引数として式を使用する  
次の例では、*number* パラメーターと *date* パラメーターの引数としてさまざまな種類の式を使用しています。 例では、AdventureWorks データベースを使用します。
  
#### <a name="specifying-a-column-as-date"></a>列を date として指定する  
次の例では、`OrderDate` 列の各値に `2` 日を加算し、`PromisedShipDate` という名前の新しい列を作成します。
  
```sql
SELECT SalesOrderID  
    ,OrderDate   
    ,DATEADD(day,2,OrderDate) AS PromisedShipDate  
FROM Sales.SalesOrderHeader;  
```  
  
部分的な結果セットを次に示します。
  
```sql
SalesOrderID OrderDate               PromisedShipDate  
------------ ----------------------- -----------------------  
43659        2005-07-01 00:00:00.000 2005-07-03 00:00:00.000  
43660        2005-07-01 00:00:00.000 2005-07-03 00:00:00.000  
43661        2005-07-01 00:00:00.000 2005-07-03 00:00:00.000  
...  
43702        2005-07-02 00:00:00.000 2005-07-04 00:00:00.000  
43703        2005-07-02 00:00:00.000 2005-07-04 00:00:00.000  
43704        2005-07-02 00:00:00.000 2005-07-04 00:00:00.000  
43705        2005-07-02 00:00:00.000 2005-07-04 00:00:00.000  
43706        2005-07-03 00:00:00.000 2005-07-05 00:00:00.000  
...  
43711        2005-07-04 00:00:00.000 2005-07-06 00:00:00.000  
43712        2005-07-04 00:00:00.000 2005-07-06 00:00:00.000  
...  
43740        2005-07-11 00:00:00.000 2005-07-13 00:00:00.000  
43741        2005-07-12 00:00:00.000 2005-07-14 00:00:00.000  
  
```  
  
#### <a name="specifying-user-defined-variables-as-number-and-date"></a>number および date にユーザー定義変数を指定する  
次の例では、*number* と *date* の引数としてユーザー定義変数を指定しています。
  
```sql
DECLARE @days int = 365,   
        @datetime datetime = '2000-01-01 01:01:01.111'; /* 2000 was a leap year */;  
SELECT DATEADD(day, @days, @datetime);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
-----------------------  
2000-12-31 01:01:01.110  
  
(1 row(s) affected)  
```  
  
#### <a name="specifying-scalar-system-function-as-date"></a>スカラー システム関数を date として指定する  
次の例では、*date* に対して `SYSDATETIME` を指定しています。
  
```sql
SELECT DATEADD(month, 1, SYSDATETIME());  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
---------------------------  
2013-02-06 14:29:59.6727944  
  
(1 row(s) affected)  
```  
  
#### <a name="specifying-scalar-subqueries-and-scalar-functions-as-number-and-date"></a>number および date にスカラー サブクエリやスカラー関数を指定する  
次の例では、*number* と *date* の引数として、スカラー サブクエリ `MAX(ModifiedDate)` を使用しています。 `(SELECT TOP 1 BusinessEntityID FROM Person.Person)` は、値リストから *number* 引数を選択する方法を紹介するために用意した架空の引数です。
  
```sql
SELECT DATEADD(month,(SELECT TOP 1 BusinessEntityID FROM Person.Person),  
    (SELECT MAX(ModifiedDate) FROM Person.Person));  
```  
  
#### <a name="specifying-numeric-expressions-and-scalar-system-functions-as-number-and-date"></a>number および date として数値式やスカラー システム関数を指定する  
次の例では、*number* および *date* の引数として、数値式 (`-(10/2)`)、[単項演算子](../../mdx/unary-operators.md) (`-`)、[算術演算子](../../mdx/arithmetic-operators.md) (`/`)、およびスカラー システム関数 (`SYSDATETIME`) を使用しています。
  
```sql
SELECT DATEADD(month,-(10/2), SYSDATETIME());  
```  
  
#### <a name="specifying-ranking-functions-as-number"></a>number として順位付け関数を指定する  
次の例では、*number* の引数として順位付け関数を使用しています。
  
```sql
SELECT p.FirstName, p.LastName  
    ,DATEADD(day,ROW_NUMBER() OVER (ORDER BY  
        a.PostalCode),SYSDATETIME()) AS 'Row Number'  
FROM Sales.SalesPerson AS s   
    INNER JOIN Person.Person AS p   
        ON s.BusinessEntityID = p.BusinessEntityID  
    INNER JOIN Person.Address AS a   
        ON a.AddressID = p.BusinessEntityID  
WHERE TerritoryID IS NOT NULL   
    AND SalesYTD <> 0;  
```  
  
#### <a name="specifying-an-aggregate-window-function-as-number"></a>number として集計関数を指定する  
次の例では、*number* の引数として集計関数を使用しています。
  
```sql
SELECT SalesOrderID, ProductID, OrderQty  
    ,DATEADD(day,SUM(OrderQty)   
        OVER(PARTITION BY SalesOrderID),SYSDATETIME()) AS 'Total'  
FROM Sales.SalesOrderDetail   
WHERE SalesOrderID IN(43659,43664);  
GO  
```  
  
  
## <a name="see-also"></a>参照
[CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  

