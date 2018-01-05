---
title: "DATEDIFF_BIG (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATEDIFF_BIG
- DATEDIFF_BIG_TSQL
helpviewer_keywords:
- DATEDIFF_BIG function [SQL Server]
- dates [SQL Server]. functions
- date and time [SQL Server], DATEDIFF_BIG
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
ms.assetid: 19ac1693-3cfa-400d-bf83-20a9cb46599a
caps.latest.revision: "7"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 6c8228f0db3e37fe3bf6425d60fd4f9067e92220
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="datediffbig-transact-sql"></a>DATEDIFF_BIG (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

指定された数 (符号付きの多倍長整数) を返します*datepart* 、指定された間の差*startdate*と*enddate*です。
  
すべての概要については[!INCLUDE[tsql](../../includes/tsql-md.md)]日付と時刻のデータ型および関数を参照してください[日付と時刻のデータ型および関数 &#40;TRANSACT-SQL と #41 です。](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
  
DATEDIFF_BIG ( datepart , startdate , enddate )  
```  
  
## <a name="arguments"></a>引数  
*datepart*  
一部である*startdate*と*enddate*を超えました。 境界の種類を指定します。 次の表にリストのすべての有効な*datepart*引数。 ユーザー定義変数に相当するものは無効です。
  
|*datepart*|省略形|  
|---|---|
|**year**|**yy、yyyy**|  
|**quater**|**qq、q**|  
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
 署名   
        **bigint**  
  
## <a name="return-value"></a>戻り値  
指定した startdate と enddate 間の指定した datepart 境界を返します。 数 (符号付き bigint) を超えました。
-   各*datepart*とその省略形は、同じ値を返します。  
  
戻り値が範囲外の場合**bigint** (9,223,372,036,854,775,807 に-9,223,372,036,854,775,808)、エラーが返されます。 **ミリ秒**、最大時間差*startdate*と*enddate*は、24 日 20 時間 31 分 23.647 秒です。 **2 番目**、差の最大値は 68 年です。
  
場合*startdate*と*enddate*が両方割り当てられている時間の値のみ、 *datepart*時刻ではありません*datepart*0 が返されます。
  
タイム ゾーン オフセットのコンポーネント*startdate*または*endate*戻り値の計算では使用されません。
  
[Smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)が 1 分間にのみが正確なときに、 **smalldatetime**の値が使用*startdate*または*enddate*秒ミリ秒は常に、戻り値で 0 に設定します。
  
日付データ型の変数に時刻値だけが割り当てられた場合、欠落している日付要素の値は既定値である 1900-01-01 に設定されます。 時刻データ型または日付データ型の変数に日付値だけが割り当てられた場合、欠落している時刻要素の値は既定値である 00:00:00 に設定されます。 いずれか*startdate*または*enddate*ある時刻部分のみおよびその他ののみ、日付部分、欠落している時刻および日付の部分は、既定値に設定されます。
  
場合*startdate*と*enddate*の別の日付データ型は、1 つ以上の時刻の部分または秒の小数部の有効桁数よりも、他には、他の欠落している要素が 0 に設定されます。
  
## <a name="datepart-boundaries"></a>datepart 境界
次のステートメントが同じである*startdate*と同じ*endate*です。 2 つの日付は隣接しており、時間的な差は .0000001 秒です。 間の違い、 *startdate*と*endate*の各ステートメント内の 1 つのカレンダーまたは時刻の境界を越えるその*datepart*です。 いずれのステートメントも戻り値は 1 です。 この例で異なる年を使用し、両方*startdate*と*endate*同じカレンダーの週の戻り値では、**週**0 になります。

```sql
SELECT DATEDIFF_BIG(year, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(quarter, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(month, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(dayofyear, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(day, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(week, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(hour, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(minute, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(second, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(millisecond, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
```
  
## <a name="remarks"></a>解説  
選択リストで使用できます DATEDIFF_BIG WHERE、HAVING 句、GROUP BY および ORDER BY 句。
  
DATEDIFF_BIG としての文字列リテラルを暗黙的にキャストする、 **datetime2**型です。 つまり、DATEDIFF_BIG サポートしていないこと YDM 形式、日付が文字列として渡される場合。 文字列を明示的にキャストする必要があります、 **datetime**または**smalldatetime** YDM 形式を使用する型。
  
SET DATEFIRST を指定するのには影響しません DATEDIFF_BIG です。 常に DATEDIFF_BIG では、日曜日を週の最初の日としてを使用して、関数が決定的であることを確認します。
  
## <a name="examples"></a>使用例  
次の例の引数としてさまざまな種類の式を使用して、 *startdate*と*enddate*パラメーター。
  
### <a name="specifying-columns-for-startdate-and-enddate"></a>startdate と enddate に列を指定する  
次の例では、テーブルの 2 つの列に日付を格納し、両者の差を日単位で計算しています。
  
```sql
CREATE TABLE dbo.Duration  
    (  
    startDate datetime2  
    ,endDate datetime2  
    );  
INSERT INTO dbo.Duration(startDate,endDate)  
    VALUES('2007-05-06 12:10:09','2007-05-07 12:10:09');  
SELECT DATEDIFF_BIG(day,startDate,endDate) AS 'Duration'  
FROM dbo.Duration;  
-- Returns: 1  
```  
  
その他の多くの例は、密接に関連する例を参照してください[DATEDIFF &#40;です。TRANSACT-SQL と #41 です。](../../t-sql/functions/datediff-transact-sql.md).
  
## <a name="see-also"></a>参照
[CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Datediff 関数 &#40;です。TRANSACT-SQL と #41 です。](../../t-sql/functions/datediff-transact-sql.md)
  
  
