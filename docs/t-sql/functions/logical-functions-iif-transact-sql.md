---
title: "IIF (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IIF_TSQL
- IIF
dev_langs: TSQL
helpviewer_keywords: IIF function
ms.assetid: e3ccf8ed-1cec-43ac-90b7-d8597c24b050
caps.latest.revision: "15"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: a7b58233c958d8ca9dc6b0fea9f9e69290d13679
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="logical-functions---iif-transact-sql"></a>論理関数 - IIF (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  True または false には、ブール式が評価されるかどうかによって、2 つの値のいずれかを返します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]です。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
IIF ( boolean_expression, true_value, false_value )  
```  
  
## <a name="arguments"></a>引数  
 *boolean_expression*  
 有効なブール式です。  
  
 この引数がブール式でない場合、構文エラーが発生します。  
  
 *true_value*  
 場合に返す値*boolean_expression*を true に評価します。  
  
 *false_value*  
 場合に返す値*boolean_expression*を false に評価します。  
  
## <a name="return-types"></a>戻り値の型  
 内の型からの優先順位が高いデータ型を返します*true_value*と*false_value*です。 詳細については、「[データ型の優先順位 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)」を参照してください。  
  
## <a name="remarks"></a>解説  
 IIF は CASE 式を簡略化して書き込みます。 最初の引数として渡されたブール式を評価し、評価の結果に基づいて他の 2 つの引数のいずれかを返します。 つまり、 *true_value*ブール式が true のかどうかに返されると、 *false_value*ブール式が false または不明なかどうかが返されます。 *true_value*と*false_value*任意の型を指定できます。 ブール式、NULL 処理、および戻り値の型に対する CASE 式に適用されるのと同じ規則が IIF にも適用されます。 詳細については、「[CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)」を参照してください。  
  
 IIF が CASE に変換されるという事実は、この関数の動作の他の側面にも影響を与えます。 CASE 式では最大 10 のレベルまで入れ子が許容されるため、IIF ステートメントでも最大 10 のレベルまで入れ子が許容されます。 また、IIF は、意味が同じ CASE 式として他のサーバーにリモート処理を行い、リモート処理された CASE 式のすべての動作を実行します。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-simple-iif-example"></a>A. 簡単な IIF の例  
  
```  
DECLARE @a int = 45, @b int = 40;  
SELECT IIF ( @a > @b, 'TRUE', 'FALSE' ) AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
--------  
TRUE  
  
(1 row(s) affected)  
```  
  
### <a name="b-iif-with-null-constants"></a>B. NULL 定数を使用する IIF  
  
```  
SELECT IIF ( 45 > 30, NULL, NULL ) AS Result;  
```  
  
 このステートメントの結果はエラーになります。  
  
### <a name="c-iif-with-null-parameters"></a>C. NULL パラメーターを使用する IIF  
  
```  
DECLARE @P INT = NULL, @S INT = NULL;  
SELECT IIF ( 45 > 30, @p, @s ) AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
--------  
NULL  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>参照  
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [CHOOSE &#40;Transact-SQL&#41;](../../t-sql/functions/logical-functions-choose-transact-sql.md)  
  
  
