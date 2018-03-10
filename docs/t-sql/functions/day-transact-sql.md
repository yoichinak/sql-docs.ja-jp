---
title: "DAY (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 07/30/2017
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
- DAY_TSQL
- DAY
dev_langs: TSQL
helpviewer_keywords:
- date and time [SQL Server], DAY
- dates [SQL Server], functions
- DAY function [SQL Server]
- dates [SQL Server], days
- functions [SQL Server], date and time
- dateparts [SQL Server], day
ms.assetid: 2f4410ea-fd3e-4d69-ac4b-3b0091a084bc
caps.latest.revision: "41"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 444df60a2cfe3adae045020b3db8d673946dccb1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="day-transact-sql"></a>DAY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

指定された *date* の日 (月初から数えた日) を整数で返します。
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] の日付と時刻のデータ型および関数の概要については、「[日付と時刻のデータ型および関数 &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)」を参照してください。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
DAY ( date )  
```  
  
## <a name="arguments"></a>引数  
*date*  
**time** 、**date**、**smalldatetime**、**datetime**、**datetime2**、**datetimeoffset** のいずれかの値に解決可能な式を指定します。 *date* 引数には、式、列式、ユーザー定義変数、または文字列リテラルを指定できます。
  
## <a name="return-type"></a>戻り値の型  
**int**
  
## <a name="return-value"></a>戻り値  
DAY は、[DATEPART](../../t-sql/functions/datepart-transact-sql.md) (**day**, *date*) と同じ値を返します。
  
*date* に時刻部分だけが含まれている場合、返される値は基準日の 1 となります。
  
## <a name="examples"></a>使用例  
次のステートメントから`30`です。 これは、日を表す値です。
  
```sql
SELECT DAY('2015-04-30 01:01:01.1234567');  
```  
  
次のステートメントでは、`1900, 1, 1` が返されます。 *date* の引数は、値 `0` です。 [SQL Server][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、`0` を 1900 年 1 月 1 日と解釈します。
  
```sql
SELECT YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="see-also"></a>参照
[CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  


