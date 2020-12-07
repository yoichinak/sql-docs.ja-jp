---
description: 先祖 (MDX)
title: 先祖 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9e08a0f281a9e48c3416bb00f6ee47322d554d9c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461664"
---
# <a name="ancestor-mdx"></a>先祖 (MDX)


  指定されたレベルまたはメンバーから指定された距離にある、指定されたメンバーの先祖を返す関数。  
  
## <a name="syntax"></a>構文  
  
```  
  
Level syntax  
Ancestor(Member_Expression, Level_Expression)  
  
Numeric syntax  
Ancestor(Member_Expression, Distance)  
```  
  
## <a name="arguments"></a>引数  
 *Member_Expression*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
 *Level_Expression*  
 レベルを返す有効な多次元式 (MDX) 式です。  
  
 *距離*  
 指定されたメンバーからの距離を指定する有効な数値式です。  
  
## <a name="remarks"></a>解説  
 **先祖**関数では、mdx メンバー式を使用して関数を指定し、メンバーの先祖であるレベルの mdx 式、またはそのメンバーの上位レベルの数を表す数値式のいずれかを指定します。 この情報を使用して、 **先祖** 関数は、そのレベルの先祖メンバーを返します。  
  
> [!NOTE]  
>  先祖メンバーだけでなく、先祖メンバーを含むセットを返すには、 [&#40;MDX&#41;](../mdx/ancestors-mdx.md) 関数の先祖を使用します。  
  
 レベル式が指定されている場合、 **先祖** 関数は指定されたレベルで指定されたメンバーの先祖を返します。 指定されたメンバーが指定されたレベルと同じ階層内にない場合、関数はエラーを返します。  
  
 距離が指定されている場合、 **先祖** 関数は、メンバー式で指定された階層内で指定されたステップ数である、指定されたメンバーの先祖を返します。 メンバーには、属性階層、ユーザー定義階層、または場合によっては親子階層のメンバーを指定できます。 1を指定すると、メンバーの親が返され、2個のメンバーの祖父母 (存在する場合) が返されます。 数値として 0 が指定された場合はそのメンバー自体を返します。  
  
> [!NOTE]  
>  この形式の **先祖** 関数は、親のレベルが不明な場合、または名前を指定できない場合に使用します。  
  
## <a name="examples"></a>例  
 次の例では、レベル式を使用して、オーストラリアの州ごとの Internet Sales Amount と、オーストラリアの Internet Sales Amount の合計の割合を返します。  
  
```  
WITH MEMBER Measures.x AS [Measures].[Internet Sales Amount] /   
   (  
   [Measures].[Internet Sales Amount],    
      Ancestor   
         (  
         [Customer].[Customer Geography].CurrentMember,  
            [Customer].[Customer Geography].[Country]  
         )  
   ), FORMAT_STRING = '0%'  
SELECT {[Measures].[Internet Sales Amount], Measures.x} ON 0,  
{  
   Descendants   
      (  
        [Customer].[Customer Geography].[Country].&[Australia],  
           [Customer].[Customer Geography].[State-Province], SELF   
      )  
} ON 1  
FROM [Adventure Works]  
```  
  
 次の例では、数値式を使用して、オーストラリアの州ごとの Internet Sales Amount と、すべての国における Internet Sales Amount の合計の割合を返します。  
  
```  
WITH MEMBER Measures.x AS [Measures].[Internet Sales Amount] /   
   (  
      [Measures].[Internet Sales Amount],  
         Ancestor   
            ([Customer].[Customer Geography].CurrentMember, 2)  
   ), FORMAT_STRING = '0%'  
SELECT {[Measures].[Internet Sales Amount], Measures.x} ON 0,  
{  
   Descendants   
      (  
         [Customer].[Customer Geography].[Country].&[Australia],  
            [Customer].[Customer Geography].[State-Province], SELF   
      )  
} ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
