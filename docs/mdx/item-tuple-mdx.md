---
description: Item (組) (MDX)
title: 項目 (組) (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1e98e6901c018a6c8be5187024e5462cc8d19547
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483955"
---
# <a name="item-tuple-mdx"></a>Item (組) (MDX)


  セットから組を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Index syntax  
Set_Expression.Item(Index)  
  
String expression syntax  
Set_Expression.Item(String_Expression1 [ ,String_Expression2,...n])  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *String_Expression1*  
 有効な文字列式です。通常は、文字列で表現される組です。  
  
 *String_Expression2*  
 有効な文字列式です。通常は、文字列で表現される組です。  
  
 *Index*  
 返されるセット内の位置によって特定の組を指定する有効な数値式です。  
  
## <a name="remarks"></a>解説  
 **Item**関数は、指定されたセットから組を返します。 **Item**関数を呼び出すには、次の3つの方法があります。  
  
-   1つの文字列式が指定されている場合、 **Item** 関数は、指定された組を返します。 たとえば、"([2005]) のようになります。Q3、[Store05]) "。  
  
-   複数の文字列式が指定されている場合、 **Item** 関数は、指定された座標によって定義された組を返します。 文字列の数は軸の数と一致している必要があり、各文字列で一意の階層を識別しなければなりません。 たとえば、"[2005] のようになります。Q3 "," [Store05] "  
  
-   整数が指定されている場合、 **Item** 関数は、 *Index*で指定された0から始まる位置にある組を返します。  
  
## <a name="examples"></a>例  
 次の例では、([1996], Sales) が返されます。  
  
 `{([1996],Sales), ([1997],Sales), ([1998],Sales)}.Item(0)`  
  
 次の例では、レベル式を使用して、オーストラリアの州ごとの Internet Sales Amount と、オーストラリアの Internet Sales Amount の合計の割合を返します。 この例では、Item 関数を使用して、 **先祖** 関数によって返されるセットから最初の (および組のみの) を抽出します。  
  
```  
WITH MEMBER Measures.x AS [Measures].[Internet Sales Amount] /   
   ( [Measures].[Internet Sales Amount],    
      Ancestors   
      ( [Customer].[Customer Geography].CurrentMember,  
        [Customer].[Customer Geography].[Country]  
      ).Item (0)  
   ), FORMAT_STRING = '0%'  
SELECT {[Measures].[Internet Sales Amount], Measures.x} ON 0,  
{ Descendants   
   ( [Customer].[Customer Geography].[Country].&[Australia],  
     [Customer].[Customer Geography].[State-Province], SELF   
   )   
} ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
