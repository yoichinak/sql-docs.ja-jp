---
description: CASE ステートメント (MDX)
title: CASE ステートメント (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7a5907eb58fa102c46fa22af97116c4fad0f217a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466504"
---
# <a name="case-statement-mdx"></a>CASE ステートメント (MDX)


  複数の比較から、条件付きで特定の値を返します。 case ステートメントには、次の 2 種類があります。  
  
-   式を一連の単純式と比較して特定の値を返す単純な case ステートメント。  
  
-   一連のブール式を評価して特定の値を返す検索 case ステートメント。  
  
## <a name="syntax"></a>構文  
  
```  
  
Simple Case Statement  
CASE [input_expression]  
WHEN when_expression THEN when_true_result_expression  
[...n]  
[ELSE else_result_expression]  
END  
  
Search Case Statement  
CASE   
WHEN Boolean_expression THEN when_true_result_expression  
[...n]  
[ELSE else_result_expression]  
END  
```  
  
## <a name="arguments"></a>引数  
 *input_expression*  
 スカラー値に解決される多次元式 (MDX) 式です。  
  
 *when_expression*  
 *Input_expression*の評価対象となる指定したスカラー値。 true に評価されると、 *else_result_expression*のスカラー値が返されます。  
  
 *when_true_result_expression*  
 WHEN 句が true と評価されたときに返されるスカラー値。  
  
 *else_result_expression*  
 WHEN 句が true に評価されなかった場合に返されるスカラー値。  
  
 *Boolean_expression*  
 スカラー値に評価される MDX 式。  
  
## <a name="remarks"></a>解説  
 ELSE 句がなく、すべての WHEN 句が false と評価された場合、結果は空のセルになります。  
  
## <a name="simple-case-expression"></a>単純 Case 式  
 MDX では、 *input_expression* をスカラー値に解決することで、単純 case 式を評価します。 このスカラー値は、 *when_expression*のスカラー値と比較されます。 2つのスカラー値が一致する場合、CASE ステートメントは *when_true_expression*の値を返します。 2 つのスカラー値が一致しなかった場合は、次の WHEN 句が評価されます。 すべての WHEN 句が false と評価された場合、ELSE 句の *else_result_expression* の値 (存在する場合) が返されます。  
  
 次の例では、再販業者の注文数メジャーを複数の WHEN 句に対して評価し、各年の再販業者の注文数メジャーの値に基づいて結果を返します。 WHEN 句の *when_expression* で指定されたスカラー値と一致しない再販業者の注文数の値については、 *else_result_expression* のスカラー値が返されます。  
  
```  
WITH MEMBER [Measures].x AS   
CASE [Measures].[Reseller Order Count]  
   WHEN 0 THEN 'NONE'  
   WHEN 1 THEN 'SMALL'  
   WHEN 2 THEN 'SMALL'  
   WHEN 3 THEN 'MEDIUM'  
   WHEN 4 THEN 'MEDIUM'  
   WHEN 5 THEN 'LARGE'  
   WHEN 6 THEN 'LARGE'  
      ELSE 'VERY LARGE'  
END  
SELECT Calendar.[Calendar Year] on 0  
, NON EMPTY [Geography].[Postal Code].Members ON 1  
FROM [Adventure Works]  
WHERE [Measures].x  
```  
  
## <a name="searched-case-expression"></a>検索 case 式  
 Case 式を使用してより複雑な評価を実行するには、検索 case 式を使用します。 検索式の 1 つである検索 case 式を使用すると、入力式が一定範囲内の値であるかどうかを評価できます。 MDX では、CASE ステートメントでこれらの句が出現する順序で WHEN 句が評価されます。  
  
 次の例では、複数の WHEN 句のそれぞれに対して、指定された *Boolean_expression* に対して再販業者の注文数メジャーが評価されます。 年ごとの Reseller Order Count メジャーの値に基づいて、結果が返されます。 句は表示される順序で評価されるため、6より大きい値には、各値を明示的に指定しなくても、"非常に大きい" 値を簡単に割り当てることができます。 WHEN 句で指定されていない再販業者の注文数の値については、 *else_result_expression* のスカラー値が返されます。  
  
```  
WITH MEMBER [Measures].x AS   
CASE   
   WHEN [Measures].[Reseller Order Count] > 6 THEN 'VERY LARGE'  
   WHEN [Measures].[Reseller Order Count] > 4 THEN 'LARGE'  
   WHEN [Measures].[Reseller Order Count] > 2 THEN 'MEDIUM'  
   WHEN [Measures].[Reseller Order Count] > 0 THEN 'SMALL'  
   ELSE "NONE"  
END  
SELECT Calendar.[Calendar Year] on 0,  
NON EMPTY [Geography].[Postal Code].Members on 1  
FROM [Adventure Works]  
WHERE [Measures].x  
```  
  
## <a name="see-also"></a>参照  
 [MDX スクリプト ステートメント &#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
