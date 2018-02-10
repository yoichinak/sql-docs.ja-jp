---
title: "COS (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 07/24/2017
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
- COS
- COS_TSQL
dev_langs: TSQL
helpviewer_keywords:
- cosine
- COS function
ms.assetid: c9fa8ae1-3373-4f3e-9b97-fa05077c1040
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ef4c3de755304ff2b61452570fe218ab42382f37
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="cos-transact-sql"></a>COS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

指定した角度の三角関数のコサイン値を、指定した式に基づいてラジアン単位で返す数学関数です。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
COS ( float_expression )  
```  
  
## <a name="arguments"></a>引数  
*float_expression*  
**float** 型の[式](../../t-sql/language-elements/expressions-transact-sql.md)を指定します。
  
## <a name="return-types"></a>戻り値の型
**float**
  
## <a name="examples"></a>使用例  
次の例では、指定した角度のコサインを返します。
  
```sql
DECLARE @angle float;  
SET @angle = 14.78;  
SELECT 'The COS of the angle is: ' + CONVERT(varchar,COS(@angle));  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
The COS of the angle is: -0.599465                        
  
(1 row(s) affected)  
```  

## <a name="examples"></a>使用例
  
[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]と[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  


次の例では、指定した角度のコサインを返します。
  
```sql
SELECT COS(14.76) AS cosCalc1, COS(-0.1472738) AS cosCalc2;   
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
cosCalc1  cosCalc2
--------  --------
-0.58     0.99
```
  
## <a name="see-also"></a>参照
[数学関数 &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)
  
  

