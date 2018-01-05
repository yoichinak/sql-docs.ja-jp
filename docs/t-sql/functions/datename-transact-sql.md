---
title: "DATENAME (TRANSACT-SQL) |Microsoft ドキュメント"
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
- DATENAME_TSQL
- DATENAME
dev_langs: TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- DATENAME function [SQL Server
- functions [SQL Server], time
- functions [SQL Server], date and time
- dateparts [SQL Server], datename
- date and time [SQL Server], DATENAME
- comparing dates times [SQL Server]
- dates [SQL Server], dateparts
ms.assetid: 11855b56-c554-495d-aad4-ba446990153b
caps.latest.revision: "59"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 22dc10851e3185512527f82f593fdc2cdb2b765f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="datename-transact-sql"></a>DATENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

表す、指定した文字列を返します*datepart*の指定した*日付*
  
すべての概要については[!INCLUDE[tsql](../../includes/tsql-md.md)]日付と時刻のデータ型および関数を参照してください[日付と時刻のデータ型および関数 &#40;TRANSACT-SQL と #41 です。](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
DATENAME ( datepart , date )  
```  
  
## <a name="arguments"></a>引数  
*datepart*  
一部である、*日付*を返します。 次の表にリストのすべての有効な*datepart*引数。 ユーザー定義変数に相当するものは無効です。
  
|*datepart*|省略形|  
|---|---|
|**year**|**yy、yyyy**|  
|**quarter**|**qq、q**|  
|**month**|**mm、m**|  
|**dayofyear**|**dy、y**|  
|**day**|**dd、d**|  
|**week**|**wk、ww**|  
|**weekday**|**dw、w**|  
|**hour**|**mm**|  
|**minute**|**mi、n**|  
|**second**|**ss、s**|  
|**millisecond**|**ms**|  
|**microsecond**|**mcs**|  
|**nanosecond**|**ns**|  
|**TZoffset**|**tz**|  
|**ISO_WEEK**|**ISOWK、ISOWW**|  
  
*date*  
式に解決されることができるは、**時間**、**日付**、 **smalldatetime**、 **datetime**、 **datetime2**、または**datetimeoffset**値。 *日付*できる、式、列式、ユーザー定義変数、または文字列リテラルです。  
こうしたあいまいさを排除するため、4 桁の西暦を使用してください。 については 2 桁の年を参照してください[構成 two digit year cutoff Server Configuration Option](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)です。
  
## <a name="return-type"></a>戻り値の型  
**nvarchar**
  
## <a name="return-value"></a>戻り値  
  
-   各*datepart*とその省略形は、同じ値を返します。  
  
戻り値を使用して設定した言語環境に依存[SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md)および、 [default language サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md)ログインします。 戻り値が依存している[SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md)場合*日付*文字列は、いくつかの形式のリテラルです。 date が日付データ型や時刻データ型の列式である場合、SET DATEFORMAT は戻り値に影響しません。
  
ときに、*日付*パラメーターには、**日付**データ型の引数、戻り値を使用して指定された設定によって異なります。 [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md)です。
  
## <a name="tzoffset-datepart-argument"></a>TZoffset (datepart 引数)  
場合*datepart*引数は**TZoffset** (**tz**) および*日付*引数は、タイム ゾーン オフセットを持たない、0 が返されます。
  
## <a name="smalldatetime-date-argument"></a>smalldatetime (date 引数)  
ときに*日付*は[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)秒は 00 として返されます。
  
## <a name="default-returned-for-a-datepart-that-is-not-in-the-date-argument"></a>date 引数に存在しない datepart を指定した場合に返される既定値  
データ型の場合、*日付*引数が、指定がありません*datepart*、既定値が*datepart* のリテラルを指定した場合にのみが返されます*日付*です。
  
たとえば、既定の年-月-日のいずれか**日付**データ型は 1900-01-01 です。 次のステートメントは、日付部分の引数を持つ*datepart*、引数の*日付*、し、返します`1900, January, 1, 1, Monday`です。
  
```sql
SELECT DATENAME(year, '12:10:30.123')  
    ,DATENAME(month, '12:10:30.123')  
    ,DATENAME(day, '12:10:30.123')  
    ,DATENAME(dayofyear, '12:10:30.123')  
    ,DATENAME(weekday, '12:10:30.123');  
```  
  
場合*日付*が指定されているは、変数またはテーブルの列と、データ、変数または列がないこと、指定の型。 として*datepart*、エラー 9810 が返されます。 日付部分の年が無効のため、次のコード例が失敗した、**時間**変数の宣言されているデータ型 *@t*です。
  
```sql
DECLARE @t time = '12:10:30.123';   
SELECT DATENAME(year, @t);  
```  
  
## <a name="remarks"></a>解説  
DATENAME は、選択リストのほか、WHERE 句、HAVING 句、GROUP BY 句、および ORDER BY 句で使用できます。
  
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、DATENAME は、文字列リテラルを暗黙的にキャスト、 **datetime2**型です。 つまり、DATENAME では、日付が文字列として渡される場合、YDM 形式をサポートしません。 文字列を明示的にキャストする必要があります、 **datetime**または**smalldatetime** YDM 形式を使用する型。
  
## <a name="examples"></a>使用例  
次の例は、指定された日付の日付部分を返します。
  
`SELECT DATENAME(datepart,'2007-10-30 12:15:32.1234567 +05:10');`
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|*datepart*|戻り値|  
|---|---|
|**year、yyyy, yy**|2007|  
|**四半期、qq、q**|4|  
|**月、mm、m**|10 月|  
|**dayofyear、dy、y**|303|  
|**日、dd、d**|30|  
|**week、wk、ww**|44|  
|**平日、dw**|火曜日|  
|**hour、hh**|12|  
|**1 分、n**|15|  
|**2 番目、ss、s**|32|  
|**millisecond、ms**|123|  
|**マイクロ秒、mcs**|123456|  
|**(ナノ秒)、ns**|123456700|  
|**TZoffset、tz**|310|  
|**ISO_WEEK ISOWK、ISOWW**|44|  
  
[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]そして[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

次の例は、指定された日付の日付部分を返します。
  
```sql
SELECT DATENAME(datepart,'2007-10-30 12:15:32.1234567 +05:10');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|*datepart*|戻り値|  
|---|---|
|**year、yyyy, yy**|2007|  
|**四半期、qq、q**|4|  
|**月、mm、m**|10 月|  
|**dayofyear、dy、y**|303|  
|**日、dd、d**|30|  
|**week、wk、ww**|44|  
|**平日、dw**|火曜日|  
|**hour、hh**|12|  
|**1 分、n**|15|  
|**2 番目、ss、s**|32|  
|**millisecond、ms**|123|  
|**マイクロ秒、mcs**|123456|  
|**(ナノ秒)、ns**|123456700|  
|**TZoffset、tz**|310|  
|**ISO_WEEK ISOWK、ISOWW**|44|  
  
## <a name="see-also"></a>参照
[CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  

