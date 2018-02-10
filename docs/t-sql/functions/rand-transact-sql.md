---
title: "RAND (Transact-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RAND
- RAND_TSQL
dev_langs: TSQL
helpviewer_keywords:
- RAND function
- values [SQL Server], random float
- random float value
ms.assetid: 363c84d6-b9fa-49ba-9a75-e44f27535ff6
caps.latest.revision: "22"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 665367907867911d9097fa17d3d05e356a35a014
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="rand-transact-sql"></a>RAND (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  0 と 1 の間の範囲 (両端値は含みません) の **float** 型の擬似乱数を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
RAND ( [ seed ] )  
```  
  
## <a name="arguments"></a>引数  
 *シード*  
 シード値となる整数型の[式](../../t-sql/language-elements/expressions-transact-sql.md) (**tinyint**、**smallint**、または **int**) です。 *seed* を指定しない場合は、SQL Server データベース エンジンによってシード値がランダムに割り当てられます。 指定したシード値について、返される結果は常に同じです。  
  
## <a name="return-types"></a>戻り値の型  
 **float**  
  
## <a name="remarks"></a>解説  
 同じシード値を使用して RAND() を繰り返し呼び出しても、同じ結果が返されます。  
  
 1 つの接続について、指定したシード値で RAND() を呼び出すと、以降のすべての RAND() の呼び出しで、シード値を指定した RAND() の呼び出しに基づいた結果が生成されます。 たとえば、次のクエリでは、同じ数値のシーケンスが常に返されます。  
  
```  
SELECT RAND(100), RAND(), RAND()   
```  
  
## <a name="examples"></a>使用例  
 次の例では、RAND 関数によって生成される 4 つの異なる乱数を生成します。  
  
```  
DECLARE @counter smallint;  
SET @counter = 1;  
WHILE @counter < 5  
   BEGIN  
      SELECT RAND() Random_Number  
      SET @counter = @counter + 1  
   END;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [数学関数 &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
  
  
