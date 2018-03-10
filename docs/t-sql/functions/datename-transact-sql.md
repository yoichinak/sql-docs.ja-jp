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

指定された *date* について、特定の *datepart* を表す文字列を返します。
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] の日付と時刻のデータ型および関数の概要については、「[日付と時刻のデータ型および関数 &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)」を参照してください。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
DATENAME ( datepart , date )  
```  
  
## <a name="arguments"></a>引数  
*datepart*  
取得する *date* の要素を指定します。 次の表は、*datepart* 引数に有効なすべての値の一覧です。 ユーザー定義変数に相当するものは無効です。
  
|*datepart*|省略形|  
|---|---|
|**year**|**yy, yyyy**|  
|**quarter**|**qq, q**|  
|**month**|**mm, m**|  
|**dayofyear**|**dy, y**|  
|**day**|**dd, d**|  
|**week**|**wk, ww**|  
|**weekday**|**dw, w**|  
|**hour**|**mm**|  
|**minute**|**mi, n**|  
|**second**|**ss, s**|  
|**millisecond**|**ms**|  
|**microsecond**|**mcs**|  
|**nanosecond**|**ns**|  
|**TZoffset**|**tz**|  
|**ISO_WEEK**|**ISOWK, ISOWW**|  
  
*date*  
**time** 、**date**、**smalldatetime**、**datetime**、**datetime2**、**datetimeoffset** のいずれかの値に解決可能な式を指定します。 *date* には、式、列式、ユーザー定義変数、または文字列リテラルを指定できます。  
こうしたあいまいさを排除するため、4 桁の西暦を使用してください。 2 桁の年の詳細については、「[two digit year cutoff サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)」を参照してください。
  
## <a name="return-type"></a>戻り値の型  
**nvarchar**
  
## <a name="return-value"></a>戻り値  
  
-   いずれの *datepart* も、対応する省略形を指定すると、同じ値が返されます。  
  
戻り値は、[SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) およびログインの「[default language サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md)」で設定した言語環境に依存します。 *date* がなんらかの形式の文字列リテラルである場合、戻り値は SET DATEFORMAT に依存します。 date が日付データ型や時刻データ型の列式である場合、SET DATEFORMAT は戻り値に影響しません。
  
*date* パラメーターに **date** データ型の引数を指定した場合、戻り値は、[SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md) で指定された設定に依存します。
  
## <a name="tzoffset-datepart-argument"></a>TZoffset (datepart 引数)  
*datepart* 引数に **TZoffset** (**tz**) を指定し、*date* 引数にタイム ゾーン オフセットを指定しなかった場合は、0 が返されます。
  
## <a name="smalldatetime-date-argument"></a>smalldatetime (date 引数)  
*date* に [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) を指定した場合、秒要素は 00 として返されます。
  
## <a name="default-returned-for-a-datepart-that-is-not-in-the-date-argument"></a>date 引数に存在しない datepart を指定した場合に返される既定値  
*date* 引数のデータ型に、指定された *datepart* が存在しない場合、*date* にリテラルが指定されるときだけ、その *datepart* の既定値が返されます。
  
たとえば、**date** データ型の既定の年月日は 1900-01-01 です。 次のステートメントでは、*datepart* 引数と *date* 引数に、それぞれ日付部分と時刻を表す値が指定されています。この場合、戻り値は `1900, January, 1, 1, Monday` になります。
  
```sql
SELECT DATENAME(year, '12:10:30.123')  
    ,DATENAME(month, '12:10:30.123')  
    ,DATENAME(day, '12:10:30.123')  
    ,DATENAME(dayofyear, '12:10:30.123')  
    ,DATENAME(weekday, '12:10:30.123');  
```  
  
*date* が変数またはテーブル列として指定され、その変数または列のデータ型に、指定された *datepart* が存在しない場合は、エラー 9810 が返されます。 次のコード例は、変数 *@t* に対して宣言されている *time* データ型では日付部分の年が無効なため、失敗します。
  
```sql
DECLARE @t time = '12:10:30.123';   
SELECT DATENAME(year, @t);  
```  
  
## <a name="remarks"></a>解説  
DATENAME は、選択リストのほか、WHERE 句、HAVING 句、GROUP BY 句、および ORDER BY 句で使用できます。
  
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、DATENAME は、文字列リテラルを暗黙的に **datetime2** 型にキャストします。 つまり、DATENAME では、日付が文字列として渡される場合、YDM 形式をサポートしません。 YDM 形式を使用するには、文字列を **datetime** 型または **smalldatetime** 型に明示的にキャストする必要があります。
  
## <a name="examples"></a>使用例  
次の例は、指定された日付の日付部分を返します。
  
`SELECT DATENAME(datepart,'2007-10-30 12:15:32.1234567 +05:10');`
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|*datepart*|戻り値|  
|---|---|
|**year, yyyy, yy**|2007|  
|**quarter, qq, q**|4|  
|**month, mm, m**|10 月|  
|**dayofyear, dy, y**|303|  
|**day, dd, d**|30|  
|**week, wk, ww**|44|  
|**weekday, dw**|火曜日|  
|**hour, hh**|12|  
|**minute, n**|15|  
|**second, ss, s**|32|  
|**millisecond, ms**|123|  
|**microsecond, mcs**|123456|  
|**nanosecond, ns**|123456700|  
|**TZoffset, tz**|310|  
|**ISO_WEEK ISOWK, ISOWW**|44|  
  
[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]と[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

次の例は、指定された日付の日付部分を返します。
  
```sql
SELECT DATENAME(datepart,'2007-10-30 12:15:32.1234567 +05:10');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|*datepart*|戻り値|  
|---|---|
|**year, yyyy, yy**|2007|  
|**quarter, qq, q**|4|  
|**month, mm, m**|10 月|  
|**dayofyear, dy, y**|303|  
|**day, dd, d**|30|  
|**week, wk, ww**|44|  
|**weekday, dw**|火曜日|  
|**hour, hh**|12|  
|**minute, n**|15|  
|**second, ss, s**|32|  
|**millisecond, ms**|123|  
|**microsecond, mcs**|123456|  
|**nanosecond, ns**|123456700|  
|**TZoffset, tz**|310|  
|**ISO_WEEK ISOWK, ISOWW**|44|  
  
## <a name="see-also"></a>参照
[CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  

