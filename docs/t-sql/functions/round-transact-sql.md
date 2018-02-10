---
title: "ROUND (TRANSACT-SQL) |Microsoft ドキュメント"
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
- ROUND_TSQL
- ROUND
dev_langs: TSQL
helpviewer_keywords:
- rounding expressions
- ROUND function [Transact-SQL]
ms.assetid: 23921ed6-dd6a-4c9e-8c32-91c0d44fe4b7
caps.latest.revision: "40"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: e9cb05c7f0b00f93f2602e114de2b502b8be0213
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="round-transact-sql"></a>ROUND (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指定された長さまたは有効桁数に丸めた数値を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
ROUND ( numeric_expression , length [ ,function ] )  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ROUND (numeric_expression , length )  
```  
  
## <a name="arguments"></a>引数  
 *numeric_expression*  
 **bit** 型を除く、真数型または概数型の[式](../../t-sql/language-elements/expressions-transact-sql.md)を指定します。  
  
 *length*  
 *numeric_expression* を丸める有効桁数です。 *length* は **tinyint** 型、**smallint** 型、または **int** 型の式である必要があります。 *length* に正の値を指定した場合、*numeric_expression* は *length* で指定した小数点以下桁数に丸められます。 *length* に負の値を指定した場合、*numeric_expression* は *length* で指定した小数点の左側の位置で丸められます。  
  
 *function*  
 実行する操作の種類です。 *function* は、**tinyint** 型、**smallint** 型、または **int** 型のいずれかである必要があります。 *function* を省略した場合、または 0 (既定値) を指定した場合、*numeric_expression* は丸められます。 0 以外の値を指定した場合、*numeric_expression* は切り捨てられます。  
  
## <a name="return-types"></a>戻り値の型  
 次のデータ型を返します。  
  
|式の結果|戻り値の型|  
|-----------------------|-----------------|  
|**tinyint**|**int**|  
|**smallint**|**int**|  
|**int**|**int**|  
|**bigint**|**bigint**|  
|**decimal**と**numeric**型 (p, s)|**decimal (p, s)**|  
|**money**と**smallmoney**カテゴリ|**money**|  
|**float**と**real**カテゴリ|**float**|  
  
## <a name="remarks"></a>解説  
 ROUND は常に値を返します。 *length* が負の値で、整数部の桁数より大きい場合、ROUND は 0 を返します。  
  
|例|結果|  
|-------------|------------|  
|ROUND (748.58、-4)|0|  
  
 ROUND は、*length* が負の値であるときは、データ型に関係なく、*numeric_expression* を丸めて返します。  
  
|使用例|結果|  
|--------------|------------|  
|ROUND (748.58,-1)|750.00|  
|ROUND (748.58、-2)|700.00|  
|ROUND(748.58, -3)|748.58 の既定値は decimal(5,2) となり、1000.00 を返すことができないため、結果は算術オーバーフローになります。|  
|4 桁までに丸めるには、入力のデータ型を変更します。 例:<br /><br /> `SELECT ROUND(CAST (748.58 AS decimal (6,2)),-3);`|1000.00|  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-round-and-estimates"></a>A. ROUND と概数を使用する  
 次の例では、`ROUND` を使用することにより最後の桁が常に概数になることを表す 2 つの式を示します。  
  
```  
SELECT ROUND(123.9994, 3), ROUND(123.9995, 3);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------- -----------  
123.9990    124.0000      
```  
  
### <a name="b-using-round-and-rounding-approximations"></a>B. ROUND を使用して概数を丸める  
 次の例では、数値を丸めて概数化します。  
  
```  
SELECT ROUND(123.4545, 2), ROUND(123.45, -2);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

 ```
--------  ----------
123.45    100.00
```
  
### <a name="c-using-round-to-truncate"></a>C. ROUND を使用して切り捨てを行う  
 次の例では、2 つの `SELECT` ステートメントを使用して、丸め処理と切り捨て処理の違いを示します。 最初のステートメントは、結果を丸めます。 2 番目のステートメントは、結果を切り捨てます。  
  
```  
SELECT ROUND(150.75, 0);  
GO  
SELECT ROUND(150.75, 0, 1);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--------  
151.00  
  
(1 row(s) affected)  
  
--------  
150.00  
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例:[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]と[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-round-and-estimates"></a>D. ROUND と概数を使用する  
 次の例では、`ROUND` を使用することにより最後の桁が常に概数になることを表す 2 つの式を示します。  
  
```  
SELECT ROUND(123.994999, 3), ROUND(123.995444, 3);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

 ```
--------  ---------
123.995000    123.995444
```
  
## <a name="see-also"></a>参照  
 [CEILING &#40;Transact-SQL&#41;](../../t-sql/functions/ceiling-transact-sql.md)   
 [データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [FLOOR &#40;Transact-SQL&#41;](../../t-sql/functions/floor-transact-sql.md)   
 [数学関数 &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
  
  

