---
title: "SIGN (Transact-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/03/2017
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
- SIGN_TSQL
- SIGN
dev_langs: TSQL
helpviewer_keywords:
- '- (negative)'
- + (positive sign)
- zero (0)
- SIGN function
- positive values [SQL Server]
- 0 (zero)
- negative values
ms.assetid: c3a98b52-6fbe-4127-a5c9-8a4922e83e28
caps.latest.revision: "33"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 883c0b862c0ab0b01f84a3089266cfb3fdedcede
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="sign-transact-sql"></a>SIGN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指定した式の符号として、正 (+1)、負 (-1)、ゼロ (0) のいずれかを返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
SIGN ( numeric_expression )  
```  
  

## <a name="arguments"></a>引数  
 *numeric_expression*  
 **bit** 型を除く、真数型または概数型の[式](../../t-sql/language-elements/expressions-transact-sql.md)を指定します。  
  
## <a name="return-types"></a>戻り値の型  
  
|指定した式|戻り値の型|  
|--------------------------|-----------------|  
|**bigint**|**bigint**|  
|**int/smallint/tinyint**|**int**|  
|**money/smallmoney**|**money**|  
|**numeric/decimal**|**numeric/decimal**|  
|**その他の種類**|**float**|  
  
## <a name="examples"></a>使用例  
 次の例では、-1 から 1 までの値の SIGN 値を返します。  
  
```  
DECLARE @value real  
SET @value = -1  
WHILE @value < 2  
   BEGIN  
      SELECT SIGN(@value)  
      SET NOCOUNT ON  
      SELECT @value = @value + 1  
      SET NOCOUNT OFF  
   END  
SET NOCOUNT OFF  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
(1 row(s) affected)  
  
------------------------   
-1.0                       
  
(1 row(s) affected)  
  
------------------------   
0.0                        
  
(1 row(s) affected)  
  
------------------------   
1.0                        
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例:[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]と[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 次の例では、3 つの数値の SIGN 値を返します。  
  
```  
SELECT SIGN(-125), SIGN(0), SIGN(564);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
-----  -----  -----  
-1     0      1
```  
  
## <a name="see-also"></a>参照  
 [数学関数 &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
  
  

