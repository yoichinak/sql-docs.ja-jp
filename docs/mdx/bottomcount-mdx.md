---
description: 下端数 (MDX)
title: 下端数 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e331a84efe36cef11951afac3f304957e4ffcb00
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494980"
---
# <a name="bottomcount-mdx"></a>下端数 (MDX)


  セットを昇順に並べ替え、指定されたセット内の組を、値の小さい方から指定された数だけ返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
BottomCount(Set_Expression, Count [,Numeric_Expression])  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Count*  
 返す組の数を指定する有効な数値式です。  
  
 *Numeric_Expression*  
 有効な数値式です。通常は、数値を返すセル座標の多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 数値式が指定されている場合、この関数は、セットに対して評価される指定された数値式の値に基づいて、指定されたセット内の組を昇順で並べ替えます。 次に、下の **count** 関数は、指定された数の組を最小値で返します。  
  
> [!IMPORTANT]  
>  [TopCount](../mdx/topcount-mdx.md)関数のように、**下端のカウント**関数は、常に階層を解除します。  
  
 数値式が指定されていない場合、関数は、並べ替えを行わずに、一連のメンバーを自然な順序で返します。これは、 [末尾 (MDX)](../mdx/tail-mdx.md) 関数のように動作します。  
  
## <a name="example"></a>例  
 次の例では、Product SubCategory のメンバーを Reseller Sales Amount メジャーに基づいて並べ替え、売上金額が下から 5 番目までのメンバーについて、年度ごとの Reseller Order Quantity メジャーを返しています。  
  
```  
SELECT BottomCount([Product].[Product Categories].[Subcategory].Members  
   , 10  
   , [Measures].[Reseller Sales Amount]) ON 0,  
   [Date].[Calendar].[Calendar Year].Members ON 1  
  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Reseller Order Quantity]  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
