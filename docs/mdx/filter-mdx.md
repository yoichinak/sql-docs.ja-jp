---
description: Filter (MDX)
title: フィルター (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 026e4720803d828ae9ba96a4d3df7f5a72d59e8d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387508"
---
# <a name="filter-mdx"></a>Filter (MDX)


  検索条件に基づいて、指定されたセットをフィルター処理した結果のセットを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Filter(Set_Expression, Logical_Expression )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Logical_Expression*  
 true または false に評価される有効な多次元式 (MDX) 論理式です。  
  
## <a name="remarks"></a>解説  
 **Filter**関数は、指定されたセット内の各組に対して指定された論理式を評価します。 関数は、論理式が **true**と評価される、指定されたセット内の各組で構成されるセットを返します。 **True**と評価される組がない場合は、空のセットが返されます。  
  
 **フィルター**関数は、 [IIf](../mdx/iif-mdx.md)関数と同様の方法で動作します。 **IIf**関数は、MDX 論理式の評価に基づいて2つのオプションのうち1つだけを返します。一方、**フィルター**関数は、指定された検索条件を満たす組のセットを返します。 実際には、 **フィルター** 関数は `IIf(Logical_Expression, Set_Expression.Current, NULL)` セット内の各組に対してを実行し、結果のセットを返します。  
  
## <a name="examples"></a>例  
 次の例では、クエリの Rows 軸で Filter 関数を使用して、Internet Sales Amount が $1万より大きい日付のみを返す方法を示します。  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `FILTER(`  
  
 `[Date].[Date].[Date].MEMBERS`  
  
 `,  [Measures].[Internet Sales Amount]>10000)`  
  
 `ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 フィルター関数は、計算されるメンバーの定義内でも使用できます。 次の例では、 `Measures.[Order Quantity]` `Date` **Adventure works** キューブから、ディメンションに含まれている2003の最初の9か月に対して集計されたメンバーの合計を返します。 **PeriodsToDate**関数は、**集計**関数の演算対象となるセット内の組を定義します。 **フィルター**関数は、前の期間の再販業者の Sales Amount メジャーの値が小さい方に、返される組を制限します。  
  
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
  
  
