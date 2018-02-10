---
title: "集計関数 (TRANSACT-SQL) |Microsoft ドキュメント"
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
dev_langs: TSQL
helpviewer_keywords:
- functions [SQL Server], aggregate
- aggregate functions [SQL Server], about aggregate functions
- summarizing functions
- aggregate functions [SQL Server]
ms.assetid: 0c06ae42-eb0a-4d77-9d74-aa1e7f344009
caps.latest.revision: "30"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: be80391551ffb4896bc57903f5b42095e3f9f860
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="aggregate-functions-transact-sql"></a>集計関数 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

集計関数は、値の集まりに対して計算を実行し、1 つの値を返します。 COUNT を除くその他の集計関数は NULL 値を無視します。 集計関数は、SELECT ステートメントの GROUP BY 句と共に使用されることが多いです。
  
集計関数はすべて決定的です。 つまり集計関数は、特定の入力値を使用して呼び出されたときに、必ず同じ値を返します。 関数の決定性の詳細については、[決定的関数と非決定的関数](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)を参照してください。[OVER 句](../../t-sql/queries/select-over-clause-transact-sql.md)は、GROUPING と GROUPING_ID を除くすべての集計関数の後に使用できます。
  
集計関数を式として使用できるのは、次の箇所に限られます。
-   SELECT ステートメントの選択リスト (サブクエリまたは外部クエリ)  
-   HAVING 句  
  
[!INCLUDE[tsql](../../includes/tsql-md.md)]は次の集計関数を提供します。
  
|||  
|-|-|  
|[AVG](../../t-sql/functions/avg-transact-sql.md)|[MIN](../../t-sql/functions/min-transact-sql.md)|  
|[CHECKSUM_AGG](../../t-sql/functions/checksum-agg-transact-sql.md)|[SUM](../../t-sql/functions/sum-transact-sql.md)|  
|[COUNT](../../t-sql/functions/count-transact-sql.md)|[STDEV](../../t-sql/functions/stdev-transact-sql.md)|  
|[COUNT_BIG](../../t-sql/functions/count-big-transact-sql.md)|[STDEVP](../../t-sql/functions/stdevp-transact-sql.md)|  
|[GROUPING](../../t-sql/functions/grouping-transact-sql.md)|[VAR](../../t-sql/functions/var-transact-sql.md)|  
|[GROUPING_ID](../../t-sql/functions/grouping-id-transact-sql.md)|[VARP](../../t-sql/functions/varp-transact-sql.md)|  
|[MAX](../../t-sql/functions/max-transact-sql.md)||  
  
## <a name="see-also"></a>参照
[組み込み関数 &#40;Transact-SQL&#41;](../../t-sql/functions/functions.md)  
[OVER 句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  
