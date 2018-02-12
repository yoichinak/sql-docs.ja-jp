---
title: "COUNT_BIG (TRANSACT-SQL) |Microsoft ドキュメント"
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
- COUNT_BIG_TSQL
- COUNT_BIG
dev_langs: TSQL
helpviewer_keywords:
- totals [SQL Server], COUNT_BIG function
- counting items in group
- groups [SQL Server], number of items in
- number of group items
- COUNT_BIG function
ms.assetid: f2e3601f-487e-4917-bb01-47b1047908cd
caps.latest.revision: "44"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b0165fefcc715becfb9c59644ed0ddd96cca9c07
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="countbig-transact-sql"></a>COUNT_BIG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

グループ内のアイテムの数を返します。 COUNT_BIG は COUNT 関数と同じように動作します。 2 つの関数の違いは、戻り値のデータ型だけです。 COUNT_BIG は常に **bigint** データ型の値を返します。 COUNT は常に **int** データ型の値を返します。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
-- Syntax for SQL Server and Azure SQL Database  
  
COUNT_BIG ( { [ ALL | DISTINCT ] expression } | * )  
   [ OVER ( [ partition_by_clause ] [ order_by_clause ] ) ]  
```  
  
```sql
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  

-- Aggregation Function Syntax  
COUNT_BIG ( { [ [ ALL | DISTINCT ] expression ] | * } )  
  
-- Analytic Function Syntax  
COUNT_BIG ( { expression | * } ) OVER ( [ <partition_by_clause> ] )  
```  
  
## <a name="arguments"></a>引数  
ALL  
すべての値にこの集計関数を適用します。 ALL が既定値です。
  
DISTINCT  
COUNT_BIG で、NULL でない一意な値の数を返します。
  
*expression*  
任意のデータ型の[式](../../t-sql/language-elements/expressions-transact-sql.md)を指定します。 集計関数とサブクエリは使用できません。
  
*\**  
すべての行をカウントし、テーブル内の行の総数を返します。 COUNT_BIG(*\**) はパラメーターをとりません。また、DISTINCT と共に使用することもできません。 COUNT_BIG(*\**) では、この関数の定義上、特定の列についての情報は使用されないため、*expression* パラメーターは必要ありません。 COUNT_BIG(*\**) では、指定されたテーブルの行数が重複行も含めて返されます。 各行は 1 行としてカウントされ、 これには NULL 値を保持している行も含まれます。
  
ALL  
すべての値にこの集計関数を適用します。 ALL が既定値です。
  
DISTINCT  
値の出現回数にかかわらず、各値の一意なインスタンスだけに AVG を適用することを指定します。
  
*expression*  
**bit** データ型を除く、真数データ型または概数データ型の[式](../../t-sql/language-elements/expressions-transact-sql.md)を指定します。 集計関数とサブクエリは使用できません。
  
OVER **(** [ *partition_by_clause* ] [ *order_by_clause* ] **)**  
*partition_by_clause* は、FROM 句で生成された結果セットをパーティションに分割します。このパーティションに関数が適用されます。 指定しない場合、関数ではクエリ結果セットのすべての行を 1 つのグループとして扱います。 *order_by_clause* は、演算が実行される論理的順序を指定します。 *order_by_clause* は必須です。 詳細については、「[OVER 句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)」を参照してください。
  
## <a name="return-types"></a>戻り値の型
**bigint**
  
## <a name="remarks"></a>解説  
COUNT_BIG(\*) では、グループ内の項目数が返されます。 これには NULL 値と重複値も含まれます。
  
COUNT_BIG (ALL *expression*) はグループ内の各行に対して *expression* を評価し、非 NULL 値の数を返します。
  
COUNT_BIG (DISTINCT *expression*) はグループ内の各行に対して *expression* を評価し、一意の非 NULL 値の数を返します。
  
COUNT_BIG は、OVER 句や ORDER BY 句なしで使用される場合は決定的関数です。 OVER 句や ORDER BY 句と共に使用される場合は、非決定的関数です。 詳細については、「 [決定的関数と非決定的関数](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)」を参照してください。
  
## <a name="examples"></a>使用例  
例については、「[COUNT &#40;Transact-SQL&#41;](../../t-sql/functions/count-transact-sql.md)」を参照してください。
  
## <a name="see-also"></a>参照
[集計関数 &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[COUNT &#40;Transact-SQL&#41;](../../t-sql/functions/count-transact-sql.md)  
[int、bigint、smallint、および tinyint &#40;Transact-SQL&#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)  
[OVER 句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  
