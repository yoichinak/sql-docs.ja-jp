---
title: "SYSUTCDATETIME (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 12/01/2015
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
- SYSUTCDATETIME
- SYSUTCDATETIME_TSQL
dev_langs: TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- system time [SQL Server]
- functions [SQL Server], date and time
- time [SQL Server], functions
- date and time [SQL Server], SYSUTCDATETIME
- SYSUTCDATETIME function [SQL Server]
- time [SQL Server], system
ms.assetid: f14fc2cd-9ea8-4daf-88f4-418cf523ab55
caps.latest.revision: "39"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7279e9d23cc57d433059b44e82b20eebd80e275b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="sysutcdatetime-transact-sql"></a>SYSUTCDATETIME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを実行しているコンピューターの日付と時刻を含む **datetime2** 値を返します。 日付と時刻は UTC 時刻 (協定世界時) で返されます。 秒の小数部の有効桁数は 1 ～ 7 桁の範囲で指定できます。 既定の有効桁数は 7 桁です。  
  
> [!NOTE]  
>  1 秒未満の有効桁数で比較すると、SYSDATETIME と SYSUTCDATE の方が GETDATE と GETUTCDATE よりも高い精度を得ることができます。 SYSDATETIMEOFFSET には、システムのタイム ゾーン オフセットが含まれます。 SYSDATETIME、SYSUTCDATE、および SYSDATETIMEOFFSET は、日付と時刻型のいずれかの変数に割り当てることができます。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] の日付と時刻のデータ型および関数の概要については、「[日付と時刻のデータ型および関数](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
SYSUTCDATETIME ( )  
```  
  
## <a name="return-type"></a>戻り値の型  
 **datetime2**  
  
## <a name="remarks"></a>解説  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントでは、**datetime2** 式を参照できる場所であればどこでも、SYSUTCDATETIME を参照できます。  
  
 SYSUTCDATETIME は非決定的関数です。 この関数を列内で参照するビューと式には、インデックスを付けることができません。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、GetSystemTimeAsFileTime() Windows API を使用して日付と時刻の値を取得します。 精度は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが実行されているコンピューター ハードウェアおよび Windows のバージョンによって異なります。 この API の精度は 100 ナノ秒で固定されます。 精度は、GetSystemTimeAdjustment() Windows API を使用して確認できます。  
  
## <a name="examples"></a>使用例  
 次の例では、現在の日付と時刻を返す 6 つの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システム関数を使用して、日付、時刻、またはその両方を取得しています。 値は順番に返されるため、秒の小数部が異なる可能性があります。  
  
### <a name="a-showing-the-formats-that-are-returned-by-the-date-and-time-functions"></a>A. 日付および時刻の関数から返される形式を表示する  
 次の例では、日付と時刻の関数によって返されるさまざまな形式を表示します。  
  
```  
SELECT SYSDATETIME() AS SYSDATETIME  
    ,SYSDATETIMEOFFSET() AS SYSDATETIMEOFFSET  
    ,SYSUTCDATETIME() AS SYSUTCDATETIME  
    ,CURRENT_TIMESTAMP AS CURRENT_TIMESTAMP  
    ,GETDATE() AS GETDATE  
    ,GETUTCDATE() AS GETUTCDATE;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
SYSDATETIME()      2007-04-30 13:10:02.0474381
SYSDATETIMEOFFSET()2007-04-30 13:10:02.0474381 -07:00
SYSUTCDATETIME()   2007-04-30 20:10:02.0474381
CURRENT_TIMESTAMP  2007-04-30 13:10:02.047
GETDATE()          2007-04-30 13:10:02.047
GETUTCDATE()       2007-04-30 20:10:02.047
```  
  
### <a name="b-converting-date-and-time-to-date"></a>B. 日付と時刻を日付に変換する  
 次の例は、日付と時刻の値を`date`に変換する方法を示します。  
  
```  
SELECT CONVERT (date, SYSDATETIME())  
    ,CONVERT (date, SYSDATETIMEOFFSET())  
    ,CONVERT (date, SYSUTCDATETIME())  
    ,CONVERT (date, CURRENT_TIMESTAMP)  
    ,CONVERT (date, GETDATE())  
    ,CONVERT (date, GETUTCDATE());  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
2007-04-30
2007-04-30
2007-04-30
2007-04-30
2007-04-30
2007-04-30
```  
  
### <a name="c-converting-date-and-time-values-to-time"></a>C. 日付と時刻の値を時刻に変換する  
 次の例は、日付と時刻の値を`time`に変換する方法を示します。  
  
 ```
DECLARE @DATETIME DATETIME = GetDate();
DECLARE @TIME TIME
SELECT @TIME = CONVERT(time, @DATETIME)
SELECT @TIME AS 'Time', @DATETIME AS 'Date Time'
```
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Time             Date Time  
13:49:33.6330000 2009-04-22 13:49:33.633
```  
  
## <a name="see-also"></a>参照  
 [CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [日付および時刻データ型および関数 &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)   
 [AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)  
  
  


