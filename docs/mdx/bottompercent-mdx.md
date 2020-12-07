---
description: BottomPercent (MDX)
title: 下% (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1b3ce341526270335564e9f67ccb89612854e098
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494984"
---
# <a name="bottompercent-mdx"></a>BottomPercent (MDX)


  セットを昇順で並べ替え、累積合計が指定した割合以上になる下限値を持つ組のセットを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
BottomPercent(Set_Expression, Percentage, Numeric_Expression)   
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Percentage*  
 返される組の割合を指定する有効な数値式です。  
  
 *Numeric_Expression*  
 有効な数値式です。通常は、数値を返すセル座標の多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 **下端のパーセント**関数は、指定されたセットに対して評価される指定された数値式の合計を計算し、セットを昇順に並べ替えます。 次に、値の合計の累積パーセントが指定した割合以上になるように、最も小さい値を持つ要素を返します。 この関数は、累積合計が指定した割合以上になるセットの最小サブセットを返します。 要素は大きい方から順に返されます。  
  
> [!IMPORTANT]  
>  [TopPercent](../mdx/toppercent-mdx.md)関数のように、一番下の関数は、常に階層を**解除します**。 詳細については、「Order 関数」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、自転車カテゴリについて、再販業者の Sales Amount メジャーを使用している累積合計が累積合計の15% 以上である、2003会計年度の geography ディメンションの Geography 階層にある City レベルの最小のメンバーのセットを返します。  
  
```  
SELECT  
[Product].[Product Categories].Bikes ON 0,  
BottomPercent  
   ({[Geography].[Geography].[City].Members}  
   , 15  
   , ([Measures].[Reseller Sales Amount],[Product].[Product Categories].Bikes)  
   ) ON 1  
FROM [Adventure Works]  
WHERE ([Measures].[Reseller Sales Amount],[Date].[Fiscal].[Fiscal Year].[FY 2003])  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
