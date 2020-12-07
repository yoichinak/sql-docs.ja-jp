---
description: Hierarchize (MDX)
title: Hierarchize (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3c1683819420d150e2f9b330ba94bc9e228d167f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429914"
---
# <a name="hierarchize-mdx"></a>Hierarchize (MDX)


  階層内のセットのメンバーを並べ替えます。  
  
## <a name="syntax"></a>構文  
  
```  
  
Hierarchize(Set_Expression [ , POST ] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 **Hierarchize**関数は、指定されたセットのメンバーを階層順に編成します。 この関数は、常に重複部分を保持します。  
  
-   **POST**が指定されていない場合、関数は、レベル内のメンバーを自然な順序で並べ替えます。 その自然な順序は、他の並べ替え条件が指定されていない場合の、階層におけるメンバーの既定の順序です。 子メンバーは親メンバーの直後になります。  
  
-   **Post**を指定した場合、 **Hierarchize**関数は、自然な順序を使用して、レベル内のメンバーを並べ替えます。 言い換えると、子メンバーは親の前に配置されます。  
  
## <a name="example"></a>例  
 次の例では、カナダのメンバーをドリルアップします。 **Hierarchize**関数は、指定されたセットメンバーを階層の順序で整理するために使用されます。これは、**ドリルダウンメンバー**関数によって要求されます。  
  
```  
SELECT DrillUpMember   
   (  
      Hierarchize  
         (  
            {[Geography].[Geography].[Country].[Canada]  
            ,[Geography].[Geography].[Country].[United States]  
            ,[Geography].[Geography].[State-Province].[Alberta]  
            ,[Geography].[Geography].[State-Province].[Brunswick]  
            ,[Geography].[Geography].[State-Province].[Colorado]   
            }  
         ), {[Geography].[Geography].[Country].[United States]}  
   )  
ON 0  
FROM [Adventure Works]  
```  
  
 次の例では、 `Measures.[Order Quantity]` `Date` **Adventure works** キューブから、ディメンションに含まれている2003の最初の9か月に対して集計されたメンバーの合計を返します。 **PeriodsToDate**関数は、集計関数の演算対象となるセット内の組を定義します。 **Hierarchize**関数は、指定されたメンバーのセットのメンバーを Product ディメンションから階層順に編成します。  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS Count  
   (Filter  
      (Existing  
         (Reseller.Reseller.Reseller),   
            [Measures].[Reseller Sales Amount] <   
               ([Measures].[Reseller Sales Amount],[Date].Calendar.PrevMember)  
        )  
    )  
MEMBER [Geography].[State-Province].x AS Aggregate   
( {[Geography].[State-Province].&[WA]&[US],   
   [Geography].[State-Province].&[OR]&[US] }   
)  
SELECT NON EMPTY HIERARCHIZE   
   (AddCalculatedMembers   
      ({DrillDownLevel  
         ({[Product].[All Products]})}  
        )  
    ) DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE ([Geography].[State-Province].x,   
   [Date].[Calendar].[Calendar Quarter].&[2003]&[4],  
   [Measures].[Declining Reseller Sales])  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
