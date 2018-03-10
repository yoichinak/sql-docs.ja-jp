---
title: "DATEPART (TRANSACT-SQL) |Microsoft ドキュメント"
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
- DATEPART_TSQL
- DATEPART
dev_langs: TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- date and time [SQL Server], DATEPART
- dateparts [SQL Server]
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
- dateparts [SQL Server], datepart
- comparing dates times [SQL Server]
- DATEPART function [SQL Server]
- dates [SQL Server], dateparts
ms.assetid: 15f1a5bc-4c0c-4c48-848d-8ec03473e6c1
caps.latest.revision: "57"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: a972e0646d68620b915fe441e35ebfb617d06859
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="datepart-transact-sql"></a>DATEPART (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

指定された *date* の特定の *datepart* を表す整数を返します。
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] の日付と時刻のデータ型および関数の概要については、「[日付と時刻のデータ型および関数 &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)」を参照してください。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
DATEPART ( datepart , date )  
```  
  
## <a name="arguments"></a>引数  
*datepart*  
**integer** の取得対象となる、*date* の要素 (日付または時刻値) を指定します。 次の表は、*datepart* 引数に有効なすべての値の一覧です。 ユーザー定義変数に相当するものは無効です。
  
|*datepart*|省略形|  
|---|---|
|**year**|**yy**, **yyyy**|  
|**quarter**|**qq**, **q**|  
|**month**|**mm**, **m**|  
|**dayofyear**|**dy**, **y**|  
|**day**|**dd**, **d**|  
|**week**|**wk**, **ww**|  
|**weekday**|**dw**|  
|**hour**|**mm**|  
|**minute**|**mi,n**|  
|**second**|**ss**, **s**|  
|**millisecond**|**ms**|  
|**microsecond**|**mcs**|  
|**nanosecond**|**ns**|  
|**TZoffset**|**tz**|  
|**ISO_WEEK**|**isowk**, **isoww**|  
  
*date*  
**time** 、**date**、**smalldatetime**、**datetime**、**datetime2**、**datetimeoffset** のいずれかの値に解決可能な式を指定します。 *date* には、式、列式、ユーザー定義変数、または文字列リテラルを指定できます。  
このあいまいな状態を避けるためには、4 桁の西暦を使用して表記します。 2 桁の年の詳細については、「[two digit year cutoff サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)」を参照してください。
  
## <a name="return-type"></a>戻り値の型  
 **int**  
  
## <a name="return-value"></a>戻り値  
いずれの *datepart* も、対応する省略形を指定すると、同じ値が返されます。
  
戻り値は、[SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) およびログインの「[default language サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md)」で設定した言語環境に依存します。 *date* になんらかの形式の文字列リテラルを指定した場合、戻り値は、[SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md) を使って指定された形式に依存します。 date が日付データ型や時刻データ型の列式である場合、SET DATEFORMAT は戻り値に影響しません。
  
次の表は、`SELECT DATEPART(datepart,'2007-10-30 12:15:32.1234567 +05:10')` ステートメントについて、すべての *datepart* 引数と、対応する戻り値を一覧にしたものです。 *date* 引数のデータ型は **datetimeoffset(7)** です。 *datepart* に **nanosecond** を指定した場合の戻り値の精度は 9 桁 (.123456700) で、最後の 2 桁は常に 00 になります。
  
|*datepart*|戻り値|  
|---|---|
|**year, yyyy, yy**|2007|  
|**quarter, qq, q**|4|  
|**month, mm, m**|10|  
|**dayofyear, dy, y**|303|  
|**day, dd, d**|30|  
|**week, wk, ww**|45|  
|**weekday, dw**|1|  
|**hour, hh**|12|  
|**minute, n**|15|  
|**second, ss, s**|32|  
|**millisecond, ms**|123|  
|**microsecond, mcs**|123456|  
|**nanosecond, ns**|123456700|  
|**TZoffset, tz**|310|  
  
## <a name="week-and-weekday-datepart-arguments"></a>week および weekday (datepart 引数)
*datepart* に **week** (**wk**、**ww**) または **weekday** (**dw**) を指定した場合、戻り値は、[SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md) を使って設定された値に依存します。
  
*datepart* に **week** を指定した場合、返される数値は 1 月 1 日を起点としてカウントされます。たとえば、DATEPART (**wk**, 'Jan 1, *xxxx*') = 1 となります。ここで、*xxxx* には任意の年を指定できます。
  
次の表は、*datepart* に **week** および **weekday** を指定した場合の戻り値の一覧です。SET DATEFIRST 引数には、それぞれ '2007-04-21' が指定されています。 西暦 2007 年 1 月 1 日は月曜日です。 西暦 2007 年 4 月 21 日は土曜日です。 英語 (U.S.) の場合、SET DATEFIRST 7 (日曜日) が既定値になります。
  
|SET DATEFIRST<br /><br /> 引数|week<br /><br /> 戻り値|weekday<br /><br /> 戻り値|  
|---|---|---|
|1|16|6|  
|2|17|5|  
|3|17|4|  
|4|17|3|  
|5|17|2|  
|6|17|1|  
|7|16|7|  
  
## <a name="year-month-and-day-datepart-arguments"></a>year、month、day (datepart 引数)  
DATEPART (**year**、*date*)、DATEPART (**month**、*date*)、および DATEPART (**day**、*date*) で返される値は、それぞれ [YEAR](../../t-sql/functions/year-transact-sql.md)、[MONTH](../../t-sql/functions/month-transact-sql.md)、[DAY](../../t-sql/functions/day-transact-sql.md) の各関数で返される値と同じです。
  
## <a name="isoweek-datepart"></a>ISO_WEEK (datepart)  
ISO 8601 には、ISO 週日付方式 (週番号方式) が規定されています。 それぞれの週は、木曜日が出現する年と関連付けられます。 たとえば、2004 年の第 1 週 (2004W01) は、2003 年 12 月 29 日 月曜日から 2004 年 1 月 4 日 日曜日です。 年の最大の週番号は 52 または 53 になります。 この付番方法は、主に欧州諸国/地域で用いられ、それ以外の国/地域で使用されることはまれです。
  
各国/地域で採用されている付番方式は、ISO 標準に準拠していない場合があります。 次の表に示すように、少なくとも 6 とおりの可能性が考えられます。
  
|週の最初の日|年の最初の週の構成|2 回割り当てられる週の有無|利用されている地域|  
|---|---|---|---|
|日曜日|1 月 1 日<br /><br /> 最初の土曜日<br /><br /> 年の 1 ～ 7 日|可|United States|  
|月曜日|1 月 1 日<br /><br /> 最初の日曜日<br /><br /> 年の 1 ～ 7 日|可|欧州および英国|  
|月曜日|1 月 4 日<br /><br /> 最初の木曜日<br /><br /> 年の 4 ～ 7 日間|不可|ISO 8601、ノルウェー、およびスウェーデン|  
|月曜日|1 月 7 日<br /><br /> 最初の月曜日<br /><br /> 年の 7 日間|不可||  
|水曜日|1 月 1 日<br /><br /> 最初の火曜日<br /><br /> 年の 1 ～ 7 日|可||  
|土曜日|1 月 1 日<br /><br /> 最初の金曜日<br /><br /> 年の 1 ～ 7 日|可||  
  
## <a name="tzoffset"></a>TZoffset  
**TZoffset** (**tz**)分の数 (符号付き) として返されます。 次のステートメントは、310 分のタイム ゾーン オフセットを返します。
  
```sql
SELECT DATEPART (TZoffset, '2007-05-10  00:00:01.1234567 +05:10');  
```  
TZoffset 値が次のようにレンダリングされます。
- Datetimeoffset と datetime2 の場合は、TZoffset は、datetime2 のオフセットが 0 分では常に分単位で時間のオフセットを返します。
- Datetimeoffset またはその他の日付/時刻データ型を除き、datetime2 に暗黙的に変換できるデータ型時刻のオフセットを分単位で返します。
- その他のすべての型パラメーターは、エラーが発生します。
  
  
## <a name="smalldatetime-date-argument"></a>smalldatetime (date 引数)  
*date* に [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) を指定した場合、秒要素は 00 として返されます。
  
## <a name="default-returned-for-a-datepart-that-is-not-in-a-date-argument"></a>date 引数に存在しない datepart を指定した場合に返される既定値  
*date* 引数のデータ型に、指定された *datepart* が存在しない場合、*date* にリテラルが指定されるときだけ、その *datepart* の既定値が返されます。
  
たとえば、**date** データ型の既定の年月日は 1900-01-01 です。 次のステートメントでは、*datepart* 引数と *date* 引数に、それぞれ日付部分と時刻を表す値が指定されています。この場合、戻り値は `1900, 1, 1, 1, 2` になります。
  
```sql
SELECT DATEPART(year, '12:10:30.123')  
    ,DATEPART(month, '12:10:30.123')  
    ,DATEPART(day, '12:10:30.123')  
    ,DATEPART(dayofyear, '12:10:30.123')  
    ,DATEPART(weekday, '12:10:30.123');  
```  
  
*date* が変数またはテーブル列として指定され、その変数または列のデータ型に、指定された *datepart* が存在しない場合は、エラー 9810 が返されます。 次のコード例は、変数 *@t* に対して宣言されている **time** データ型では日付部分の年が無効なため、失敗します。
  
```sql
DECLARE @t time = '12:10:30.123';   
SELECT DATEPART(year, @t);  
```  
  
## <a name="fractional-seconds"></a>秒の小数部
次のステートメントでは、秒の小数部が返されます。
  
```sql
SELECT DATEPART(millisecond, '00:00:01.1234567'); -- Returns 123  
SELECT DATEPART(microsecond, '00:00:01.1234567'); -- Returns 123456  
SELECT DATEPART(nanosecond,  '00:00:01.1234567'); -- Returns 123456700  
```  
  
## <a name="remarks"></a>解説  
DATEPART は、選択リストのほか、WHERE 句、HAVING 句、GROUP BY 句、および ORDER BY 句で使用できます。
  
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、DATEPART は、文字列リテラルを暗黙的に **datetime2** 型にキャストします。 つまり、DATEPART では、日付が文字列として渡される場合、YDM 形式をサポートしません。 YDM 形式を使用するには、文字列を **datetime** 型または **smalldatetime** 型に明示的にキャストする必要があります。
  
## <a name="examples"></a>使用例  
次の例では、基準年を返します。 基準年は日付計算などに利用できます。 この例では、日付が数値で指定されています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、0 を 1900 年 1 月 1 日と解釈することに注意してください。
  
```sql
SELECT DATEPART(year, 0), DATEPART(month, 0), DATEPART(day, 0);  
-- Returns: 1900    1    1 */  
```  
  
次の例は、日付`12/20/1974`の日の部分を返します。
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEPART (day,'12/20/1974') FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
--------
20
```  
  
次の例は、日付`12/20/1974`の年の部分を返します。
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEPART (year,'12/20/1974') FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
--------
1974
```  
  
## <a name="see-also"></a>参照
[CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  
