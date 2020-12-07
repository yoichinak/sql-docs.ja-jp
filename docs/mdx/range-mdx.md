---
description: ': (範囲) (MDX)'
title: ': (範囲) (MDX) |Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d52a78a1fcdefa4ee7bf09fa4125b488165e09c4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500465"
---
# <a name="-range-mdx"></a>: (範囲) (MDX)


  自然な順序で並べたセットを返すセット演算を実行します。指定された 2 つのメンバーが終端になり、その 2 つのメンバーの間にあるすべてのメンバーがセットのメンバーに含まれます。  
  
## <a name="syntax"></a>構文  
  
```  
  
Member_Expression : Member_Expression      
```  
  
#### <a name="parameters"></a>パラメーター  
 *Member_Expression*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
## <a name="return-value"></a>戻り値  
 指定したメンバーと、指定したメンバー間のすべてのメンバーを含むセット。  
  
## <a name="remarks"></a>解説  
 両方のパラメーターに、ディメンションの同じレベルと同じ階層にあるメンバーを指定する必要があります。 両方のパラメーターが同じメンバーを指定している場合、 **: (範囲)** 演算子は、指定されたメンバーだけを含むセットを返します。 最初のパラメーターが Null の場合、このセットには、2番目のパラメーターで指定したメンバーのレベルの先頭から、そのメンバーまでのすべてのメンバーが含まれます。 2番目のパラメーターが Null の場合、このセットには、最初のパラメーターで指定されたメンバーのすべてのメンバーが含まれます。このメンバーは、同じレベルの最後のメンバーを含みます。  
  
 MDX にこのセット演算子と等価な関数はありません。  
  
## <a name="examples"></a>例  
 この演算子の使用例を次に示します。  
  
```  
-- This query returns the freight cost per user  
-- for products, averaged by month, for the first quarter.  
With Member [Measures].[Freight Per Customer] as  
 (  
     [Measures].[Internet Freight Cost]  
     /   
     [Measures].[Customer Count]  
)  
  
SELECT   
    {[Ship Date].[Calendar].[Month].&[2004]&[1] : [Ship Date].[Calendar].[Month].&[2004]&[3]} ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[Freight Per Customer])  
```  
  
## <a name="see-also"></a>参照  
 [Mdx 演算子リファレンス &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
