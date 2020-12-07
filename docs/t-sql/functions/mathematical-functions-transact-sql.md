---
description: 数学関数 (Transact-SQL)
title: 数学関数 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- calculations [SQL Server]
- mathematical functions [SQL Server]
- functions [SQL Server], mathematical
ms.assetid: 46495a2e-81d0-4677-9d72-9db083cd1023
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7d3f3d6cc5bbd7730e229df06724635f707034b2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88422706"
---
# <a name="mathematical-functions-transact-sql"></a>数学関数 (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

次のスカラー関数では、通常、引数として提供される入力値に基づいて計算を実行し、数値を返します。  
  
- [ABS](../../t-sql/functions/abs-transact-sql.md)
- [ACOS](../../t-sql/functions/acos-transact-sql.md)
- [ASIN](../../t-sql/functions/asin-transact-sql.md)
- [ATAN](../../t-sql/functions/atan-transact-sql.md)
- [ATN2](../../t-sql/functions/atn2-transact-sql.md)
- [CEILING](../../t-sql/functions/ceiling-transact-sql.md)
- [COS](../../t-sql/functions/cos-transact-sql.md)
- [COT](../../t-sql/functions/cot-transact-sql.md)
- [DEGREES](../../t-sql/functions/degrees-transact-sql.md)
- [EXP](../../t-sql/functions/exp-transact-sql.md)
- [FLOOR](../../t-sql/functions/floor-transact-sql.md)
- [LOG](../../t-sql/functions/log-transact-sql.md)
- [LOG10](../../t-sql/functions/log10-transact-sql.md)
- [PI](../../t-sql/functions/pi-transact-sql.md)
- [POWER](../../t-sql/functions/power-transact-sql.md)
- [RADIANS](../../t-sql/functions/radians-transact-sql.md)  
- [RAND](../../t-sql/functions/rand-transact-sql.md)  
- [ROUND](../../t-sql/functions/round-transact-sql.md)  
- [SIGN](../../t-sql/functions/sign-transact-sql.md)  
- [SIN](../../t-sql/functions/sin-transact-sql.md)  
- [SQRT](../../t-sql/functions/sqrt-transact-sql.md)  
- [SQUARE](../../t-sql/functions/square-transact-sql.md)  
- [TAN](../../t-sql/functions/tan-transact-sql.md)
  
> [!NOTE]  
> ABS、CEILING、DEGREES、FLOOR、POWER、RADIANS、SIGN などの算術関数では、入力値と同じデータ型の値を返します。 EXP、LOG、LOG10、SQUARE、SQRT などの三角関数やその他の関数は、その入力値を**float** 型にキャストし、**float** 型の値を返します。  
  
RAND を除く、すべての数学関数が決定論的関数です。 これは、特定の入力値のセットを使用して呼び出されるたびに、同じ結果を返すことを意味します。 RAND は、seed パラメーターが指定されている場合にのみ決定的です。 関数の決定性の詳細については、次を参照してください。[決定的関数と非決定的関数です](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。  
  
## <a name="see-also"></a>参照

- [算術演算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/arithmetic-operators-transact-sql.md)
- [組み込み関数 &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
