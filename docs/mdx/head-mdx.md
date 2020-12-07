---
description: Head (MDX)
title: Head (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 51a832bf38d3834c44f9b31f5bbfd27833d6d691
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429924"
---
# <a name="head-mdx"></a>Head (MDX)


  重複部分を保持したまま、セット内の最初に指定した数の要素を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Head(Set_Expression [ ,Count ] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Count*  
 返す組の数を指定する有効な数値式です。  
  
## <a name="remarks"></a>解説  
 **Head**関数は、指定されたセットの先頭から指定された数の組を返します。 要素の順序は保持されます。 Count の既定値は 1 です。 指定された組数が1より小さい場合、 **Head** 関数は空のセットを返します。 指定された組数がセット内の組数を超える場合は、元のセットを返します。  
  
## <a name="example"></a>例  
 次の例では、階層とは無関係に、Reseller Gross Profit に基づいて、売上が上位 5 番目までの製品のサブカテゴリを返します。 **Head**関数は、結果が**Order**関数を使用して並べ替えられた後に、結果内の最初の5つのセットのみを返すために使用されます。  
  
```  
SELECT   
[Measures].[Reseller Gross Profit] ON 0,  
Head  
   (Order   
      ([Product].[Product Categories].[SubCategory].members  
         ,[Measures].[Reseller Gross Profit]  
         ,BDESC  
      )  
   ,5  
   ) ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [末尾 &#40;MDX&#41;](../mdx/tail-mdx.md)   
 [項目 &#40;組&#41; &#40;MDX&#41;](../mdx/item-tuple-mdx.md)   
 [項目 &#40;メンバー&#41; &#40;MDX&#41;](../mdx/item-member-mdx.md)   
 [MDX&#41;&#40;順位付け ](../mdx/rank-mdx.md)   
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
