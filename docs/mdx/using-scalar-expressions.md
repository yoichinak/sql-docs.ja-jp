---
description: スカラー関数の使用
title: スカラー式を使用する |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cc13d94aaf44e563a9519f797effee7cbeb74305
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491396"
---
# <a name="using-scalar-expressions"></a>スカラー関数の使用


  多次元式 (MDX) では、スカラー関数は MDX 構文の要素であり、評価されるときに評価のコンテキスト内で 1 つの値を返します。  
  
 スカラー式には、MDX の文字列、数値、および日付の式が含まれます。  
  
 通常、スカラー式は計算されるメンバーの定義で使用されます。これは、計算されるメンバーがスカラー値を返す必要があるためです。 次のクエリは、さまざまな種類のスカラー式を使用するメジャーディメンションの計算されるメンバーの例を示しています。  
  
 `WITH`  
  
 `MEMBER MEASURES.NumericValue AS 10`  
  
 `MEMBER MEASURES.NumericExpression AS 10 + 10`  
  
 `MEMBER MEASURES.NumericExpressionBasedOnMeasure AS [Measures].[Internet Sales Amount] + 10`  
  
 `MEMBER MEASURES.StringValue AS "10"`  
  
 `MEMBER MEASURES.ConcatenatedString AS "10" + "10"`  
  
 `MEMBER MEASURES.StringFunction AS MEASURES.CURRENTMEMBER.NAME`  
  
 `MEMBER MEASURES.TodaysDate AS NOW()`  
  
 `SELECT`  
  
 `{MEASURES.NumericValue,MEASURES.NumericExpression,MEASURES.NumericExpressionBasedOnMeasure,`  
  
 `MEASURES.StringValue, MEASURES.ConcatenatedString, MEASURES.StringFunction, MEASURES.TodaysDate}`  
  
 `ON COLUMNS`  
  
 `FROM [Adventure Works]`  
  
 メジャー (計算される、またはそれ以外の場合) が返すことができるデータ型は、OLE バリアント型だけです。 したがって、場合によっては、メジャー値を特定の型にキャストして、予測される動作を受け入れることも必要になります。 次のクエリは、この例を示しています。  
  
```  
WITH  
//Two calculated measures that return strings  
MEMBER MEASURES.NumericString1 AS "10"  
MEMBER MEASURES.NumericString2 AS "10"  
//In this case, the + operator acts to concatenate the strings  
MEMBER MEASURES.Concatenation AS MEASURES.NumericString1 + MEASURES.NumericString2  
//Casting one value to an integer with the CINT function causes the second measure  
//to be treated as an integer too, so that the + operator now acts to add the values  
MEMBER MEASURES.Addition AS CINT(MEASURES.NumericString1) + MEASURES.NumericString2  
SELECT  
{MEASURES.NumericString1,MEASURES.NumericString2,MEASURES.Concatenation,MEASURES.Addition }  
ON COLUMNS  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [MDX &#40;式&#41;](../mdx/expressions-mdx.md)  
  
  
