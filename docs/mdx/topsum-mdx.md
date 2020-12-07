---
description: TopSum (MDX)
title: TopSum (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 665a1ace9df98303da19b861cdd3ce6340ec8368
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412914"
---
# <a name="topsum-mdx"></a>TopSum (MDX)


  セットを並べ替え、累積合計が少なくとも指定した値である最上位要素を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
TopSum(Set_Expression, Value, Numeric_Expression)   
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Value*  
 各組の比較対象となる値を指定する有効な数値式です。  
  
 *Numeric_Expression*  
 有効な数値式です。通常は、メジャーを返す多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 **TopSum**関数は、指定されたセットに対して評価される指定メジャーの合計を計算し、セットを降順に並べ替えます。 関数は、指定された数値式の合計が指定された値以上になる最大値を持つ要素を返します。 この関数は、累積合計が指定値以上になるセットの最小サブセットを返します。 要素は大きい方から順に返されます。  
  
> [!IMPORTANT]  
>  [BottomSum](../mdx/bottomsum-mdx.md)関数と同様に、 **TopSum**関数は常に階層を解除します。  
  
## <a name="example"></a>例  
 次の例では、自転車カテゴリについて、再販業者の Sales Amount メジャーを使用した累積合計が600万の合計値以上である geography ディメンションの Geography 階層における City レベルの最小のメンバーのセットが返されます (このセットのメンバーの数が最も多い sales のメンバーから)。  
  
```  
SELECT [Measures].[Reseller Sales Amount] ON 0,  
TopSum  
   ({[Geography].[Geography].[City].Members}  
   , 6000000  
   , [Measures].[Reseller Sales Amount]  
   ) ON 1  
FROM [Adventure Works]  
WHERE([Product].[Product Categories].Bikes)  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
