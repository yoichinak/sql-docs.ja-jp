---
title: "MONTH (TRANSACT-SQL) |Microsoft ドキュメント"
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
- MONTH_TSQL
- MONTH
dev_langs: TSQL
helpviewer_keywords:
- values [SQL Server], date and time
- dates [SQL Server], functions
- month of year [SQL Server]
- date and time [SQL Server], MONTH
- dateparts [SQL Server], month
- functions [SQL Server], date and time
- dates [SQL Server], MONTH
- MONTH function [SQL Server]
ms.assetid: 9dd8aff7-b0fc-45df-b316-ead14ee9b8b7
caps.latest.revision: "29"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 9fff55128e9e5eda2d78646826ddeca2a25e6b56
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="month-transact-sql"></a>MONTH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指定された *date* の月を表す整数を返します。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] の日付と時刻のデータ型および関数の概要については、「[日付と時刻のデータ型および関数 &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
MONTH ( date )  
```  
  
## <a name="arguments"></a>引数  
 *date*  
 **time** 、**date**、**smalldatetime**、**datetime**、**datetime2**、**datetimeoffset** のいずれかの値に解決可能な式を指定します。 *date* 引数には、式、列式、ユーザー定義変数、または文字列リテラルを指定できます。  
  
## <a name="return-type"></a>戻り値の型  
 **int**  
  
## <a name="return-value"></a>戻り値  
 [MONTH](../../t-sql/functions/datepart-transact-sql.md) は、DATEPART (**month**, *date*) と同じ値を返します。  
  
 *date* に時刻部分だけが含まれている場合、返される値は基準月の 1 となります。  
  
## <a name="examples"></a>使用例  
 次のステートメントでは、`4` が返されます。 これは、月を表す値です。  
  
```  
SELECT MONTH('2007-04-30T01:01:01.1234567 -07:00');  
```  
  
 次のステートメントでは、`1900, 1, 1` が返されます。 *date* の引数は、値 `0` です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、`0` を 1900 年 1 月 1 日と解釈します。  
  
```  
SELECT YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例:[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]と[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 次の例では、`4`を返します。 これは、月を表す値です。  
  
```  
-- Uses AdventureWorks  
  
SELECT TOP 1 MONTH('2007-04-30T01:01:01.1234')   
FROM dbo.DimCustomer;  
```  
  
 次の例では、`1900, 1, 1` を返します。 *date* の引数は、値 `0` です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、`0` を 1900 年 1 月 1 日と解釈します。  
  
```  
-- Uses AdventureWorks  
  
SELECT TOP 1 YEAR(0), MONTH(0), DAY(0) FROM dbo.DimCustomer;  
```  
  
## <a name="see-also"></a>参照  
 [CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  

