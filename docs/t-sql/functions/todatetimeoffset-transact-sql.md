---
title: "TODATETIMEOFFSET (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/13/2017
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
- TO_DATETIMEOFFSET_TSQL
- SWITCH_TZ_TSQL
- SWITCH_TZ
- TO_DATETIMEOFFSET
dev_langs: TSQL
helpviewer_keywords:
- date and time [SQL Server], TODATETIMEOFFSET
- TODATETIMEOFFSET function
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
ms.assetid: b5fafc08-efd4-4a3b-a0b3-068981a0a685
caps.latest.revision: "37"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: b6a8e329f2dc0db17bfb7e0e1a99657f7d436365
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="todatetimeoffset-transact-sql"></a>TODATETIMEOFFSET (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  **datetime2** 式から変換された **datetimeoffset** 値を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
TODATETIMEOFFSET ( expression , time_zone )  
```  
  
## <a name="arguments"></a>引数  
 *式 (expression)*  
 [datetime2](../../t-sql/data-types/datetime2-transact-sql.md)値に解決される[式](../../t-sql/language-elements/expressions-transact-sql.md) 。  
  
> [!NOTE]  
>  式の型を **text**、**ntext**、または **image** にすることはできません。これらの型を **varchar** または **nvarchar** に暗黙的に変換することができないためです。  
  
 *time_zone*  
 タイム ゾーン オフセットを表す式です。たとえば、分単位で表す式 (整数の場合) は -120、時間と分単位で表す式 (文字列の場合) は '+13.00' です。 範囲は +14 ～ -14 (時間) です。 式は、指定された time_zone のローカル時刻で解釈されます。  
  
> [!NOTE]  
>  式が文字列の場合、{+|-}TZH:THM の形式にする必要があります。  
  
## <a name="return-type"></a>戻り値の型  
 **datetimeoffset**です。 有効桁数は *datetime* 引数と同じです。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-changing-the-time-zone-offset-of-the-current-date-and-time"></a>A. 現在の日付と時刻のタイム ゾーン オフセットを変更する  
 次の例では、現在の日付と時刻のゾーン オフセットを、タイム ゾーン `-07:00` に変更します。  
  
```  
DECLARE @todaysDateTime datetime2;  
SET @todaysDateTime = GETDATE();  
SELECT TODATETIMEOFFSET (@todaysDateTime, '-07:00');  
-- RETURNS 2007-08-30 15:51:34.7030000 -07:00  
```  
  
### <a name="b-changing-the-time-zone-offset-in-minutes"></a>B. タイム ゾーン オフセットを分単位で変更する  
 次の例では、現在のタイム ゾーンを `-120` 分に変更します。  
  
```  
DECLARE @todaysDate datetime2;  
SET @todaysDate = GETDATE();  
SELECT TODATETIMEOFFSET (@todaysDate, -120);  
-- RETURNS 2007-08-30 15:52:37.8770000 -02:00  
```  
  
### <a name="c-adding-a-13-hour-time-zone-offset"></a>C. 13 時間のタイム ゾーン オフセットを追加する  
 次の例では、日付と時刻に 13 時間のタイム ゾーン オフセットを追加します。  
  
```  
DECLARE @dateTime datetimeoffset(7)= '2007-08-28 18:00:30';  
SELECT TODATETIMEOFFSET (@dateTime, '+13:00');  
-- RETURNS 2007-08-28 18:00:30.0000000 +13:00  
```  
  
## <a name="see-also"></a>参照  
 [CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [日付および時刻データ型および関数 &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)   
 [AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)  
  
  

