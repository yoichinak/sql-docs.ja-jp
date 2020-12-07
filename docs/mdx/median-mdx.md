---
title: 中央値 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b6f941e269bb9948dd39ba52db0ea4d0961c029a
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "68033856"
---
# <a name="median-mdx"></a>Median (MDX)


  セットに対して評価される数値式の中央値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Median(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Numeric_Expression*  
 有効な数値式です。通常は、数値を返すセル座標の多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 数値式が指定されている場合は、指定された数値式がセット全体で評価され、その評価から中央値が返されます。 数値式が指定されていない場合、指定されたセットは、セットのメンバーの現在のコンテキストで評価され、評価の中央値を返します。  
  
 中央値とは、順番に並べられた数値のセットの中央に位置する値です  (セット内の数値の合計を、セット内にある数値の数で除算する平均値とは異なります)。 中央値は、セット内の値の少なくとも半数が、その値以下になるような最小の値を選択することによって決まります。 セット内の値の数が奇数の場合、中央値は 1 つの値になります。 セット内の値の数が偶数の場合は、中央に位置する 2 つの値の合計を 2 で除算した値が返されます。  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] では、数値セットの中央値が計算される際、NULL 値は無視されます。  
  
## <a name="example"></a>例  
 次の例では、Adventure Works キューブ内の四半期、サブカテゴリ、および国ごとに、月ごとの売上の中央値を返します。  
  
```  
WITH MEMBER Measures.x AS Median   
   ([Date].[Calendar].CurrentMember.Children  
      , [Measures].[Reseller Order Quantity]  
   )  
SELECT Measures.x ON 0  
,NON EMPTY [Date].[Calendar].[Calendar Quarter]*   
   [Product].[Product Categories].[Subcategory].members *  
   [Geography].[Geography].[Country].Members  
ON 1  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
