---
title: "SYSDATETIME (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/14/2017
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
- SYSDATETIME_TSQL
- SYSDATETIME
dev_langs: TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- date and time [SQL Server], SYSDATETIME
- current date and time [SQL Server]
- functions [SQL Server], time
- system date and time [SQL Server]
- system time [SQL Server]
- SYSDATETIME function [SQL Server]
- functions [SQL Server], date and time
- time [SQL Server], functions
- dates [SQL Server], current date and time
- dates [SQL Server], system date and time
- time [SQL Server], system
ms.assetid: cba4999e-a9d4-4742-abc9-4a4f109206b6
caps.latest.revision: "37"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 4e0f33419d2ea3986ebeab02399066cb8efa6487
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="sysdatetime-transact-sql"></a>SYSDATETIME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを実行しているコンピューターの日付と時刻を含む **datetime2(7)** 値を返します。  
  
> [!NOTE]  
>  1 秒未満の有効桁数で比較すると、SYSDATETIME と SYSUTCDATETIME の方が GETDATE と GETUTCDATE よりも高い精度を得ることができます。 SYSDATETIMEOFFSET には、システムのタイム ゾーン オフセットが含まれます。 SYSDATETIME、SYSUTCDATETIME、および SYSDATETIMEOFFSET は、date 型と time 型の任意の変数に割り当てることができます。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] の日付と時刻のデータ型および関数の概要については、「[日付と時刻のデータ型および関数 &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
SYSDATETIME ( )  
```  
  
## <a name="return-type"></a>戻り値の型  
 **datetime2(7)**  
  
## <a name="remarks"></a>解説  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントでは、**datetime2(7)** 式を参照できる場所であればどこでも、SYSDATETIME を参照できます。  
  
 SYSDATETIME は非決定的関数です。 この関数を列内で参照するビューと式には、インデックスを付けることができません。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、GetSystemTimeAsFileTime() Windows API を使用して日付と時刻の値を取得します。 精度は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが実行されているコンピューター ハードウェアおよび Windows のバージョンによって異なります。 この API の精度は 100 ナノ秒で固定されます。 精度は、GetSystemTimeAdjustment() Windows API を使用して確認できます。  
  
## <a name="examples"></a>使用例  
 次の例では、現在の日付と時刻を返す 6 つの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システム関数を使用して、日付、時刻、またはその両方を取得しています。 値は順番に返されるため、秒の小数部が異なる可能性があります。  
  
### <a name="a-getting-the-current-system-date-and-time"></a>A. 現在のシステム日付と時刻を取得する  
  
```  
SELECT SYSDATETIME()  
    ,SYSDATETIMEOFFSET()  
    ,SYSUTCDATETIME()  
    ,CURRENT_TIMESTAMP  
    ,GETDATE()  
    ,GETUTCDATE();  
/* Returned:  
SYSDATETIME()      2007-04-30 13:10:02.0474381  
SYSDATETIMEOFFSET()2007-04-30 13:10:02.0474381 -07:00  
SYSUTCDATETIME()   2007-04-30 20:10:02.0474381  
CURRENT_TIMESTAMP  2007-04-30 13:10:02.047  
GETDATE()          2007-04-30 13:10:02.047  
GETUTCDATE()       2007-04-30 20:10:02.047  
*/
```    
  
### <a name="b-getting-the-current-system-date"></a>B. 現在のシステム日付を取得する  
  
```  
SELECT CONVERT (date, SYSDATETIME())  
    ,CONVERT (date, SYSDATETIMEOFFSET())  
    ,CONVERT (date, SYSUTCDATETIME())  
    ,CONVERT (date, CURRENT_TIMESTAMP)  
    ,CONVERT (date, GETDATE())  
    ,CONVERT (date, GETUTCDATE());  
  
/* All returned 2007-04-30 */  
```  
  
### <a name="c-getting-the-current-system-time"></a>C. 現在のシステム時刻を取得する  
  
```  
SELECT CONVERT (time, SYSDATETIME())  
    ,CONVERT (time, SYSDATETIMEOFFSET())  
    ,CONVERT (time, SYSUTCDATETIME())  
    ,CONVERT (time, CURRENT_TIMESTAMP)  
    ,CONVERT (time, GETDATE())  
    ,CONVERT (time, GETUTCDATE());  
  
/* Returned  
SYSDATETIME()      13:18:45.3490361  
SYSDATETIMEOFFSET()13:18:45.3490361  
SYSUTCDATETIME()   20:18:45.3490361  
CURRENT_TIMESTAMP  13:18:45.3470000  
GETDATE()          13:18:45.3470000  
GETUTCDATE()       20:18:45.3470000  
*/  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例:[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]と[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-getting-the-current-system-date-and-time"></a>D: 現在のシステム日付と時刻を取得する  
  
```  
SELECT SYSDATETIME();  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
--------------------------  
7/20/2013 2:49:59 PM
```  
  
## <a name="see-also"></a>参照  
 [CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [日付および時刻データ型および関数 &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)  
  
  

