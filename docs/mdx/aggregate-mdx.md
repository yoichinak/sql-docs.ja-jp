---
description: Aggregate (MDX)
title: Aggregate (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d1e3f00ffbf662422f162d493a585d3972518431
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461695"
---
# <a name="aggregate-mdx"></a>Aggregate (MDX)


  セット式によって返されるセルに対して集計することによって計算された数値を返します。 数値式が指定されていない場合は、メジャーごとに指定されている既定の集計演算子を使用して、現在のクエリ コンテキスト内で各メジャーを集計します。 数値式が指定されている場合、この関数は最初に、指定されたセット内の各セルの数値式を評価し、次に合計を計算します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Aggregate(Set_Expression [ ,Numeric_Expression ])  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Numeric_Expression*  
 有効な数値式です。通常は、数値を返すセル座標の多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 空の組のセットまたは空のセットを指定した場合、この関数は空の値を返します。  
  
 次の表では、 **集計** 関数がさまざまな集計関数でどのように動作するかを説明します。  
  
|集計演算子|結果|  
|--------------------------|------------|  
|SUM|セット全体の値の合計を返します。|  
|Count|セットの値の数を返します。|  
|Max|セットに対する最大値を返します。|  
|Min|セット全体の最小値を返します。|  
|準加法集計関数|図形を時間軸に投影した後の、セットに対する準加法の動作の計算を返します。|  
|Distinct Count|スライサー軸にセットが含まれている場合、サブキューブに寄与するファクトデータ全体を集計します。<br /><br /> セットのメンバーごとに個別のカウントを返します。 結果は、計算に必要なセルのセキュリティではなく、集計されるセルのセキュリティに依存します。 セットにセル セキュリティが指定されているとエラーが生成されますが、指定されているセットの粒度より下位のセル セキュリティは無視されます。 セットの計算によってエラーが生成されます。 セットの粒度よりも下位の計算は無視されます。 1 つのメンバーとそのメンバーの子が 1 つ以上含まれているセット全体に対する個別カウントは、子メンバーに関与するファクト全体の個別カウントになります。|  
|集計できない属性|値の合計を返します。|  
|混合集計関数|サポートされていないので、エラーが発生します。|  
|単項演算子|影響しません。値は合計を算出することによって集計されます。|  
|計算されるメジャー|計算されるメジャーが確実に適用されるように、解決順序を設定します。|  
|計算されるメンバー|通常の規則が適用されます。つまり、最後の解決順序が優先されます。|  
|代入|割り当ては、メジャー集計関数に従って集計されます。 メジャー集計関数が個別カウントの場合、代入の合計が算出されます。|  
  
## <a name="examples"></a>例  
 次の例では、 `Measures.[Order Quantity]` `Date` **Adventure works** キューブから、ディメンションに含まれる2003年の最初の8か月間に集計された、メンバーの合計を返します。  
  
```  
WITH MEMBER [Date].[Calendar].[First8Months2003] AS  
    Aggregate(  
        PeriodsToDate(  
            [Date].[Calendar].[Calendar Year],   
            [Date].[Calendar].[Month].[August 2003]  
        )  
    )  
SELECT   
    [Date].[Calendar].[First8Months2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 次の例では、2003年の第2半期の最初の2か月を集計しています。  
  
```  
WITH MEMBER [Date].[Calendar].[First2MonthsSecondSemester2003] AS  
    Aggregate(  
        PeriodsToDate(  
            [Date].[Calendar].[Calendar Semester],   
            [Date].[Calendar].[Month].[August 2003]  
        )  
    )  
SELECT   
    [Date].[Calendar].[First2MonthsSecondSemester2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 次の例では、 Aggregate 関数を使用して評価された、ユーザー選択の State-Province メンバー値に基づいて、1 つ前の期よりも売上が減少した再販業者の数を返します。 Product ディメンションの製品カテゴリに対して、減少した売上の値を返すには、 **Hierarchize** および **ドリルダウンレベル** 関数を使用します。  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS   
   Count(  
      Filter(  
         Existing(Reseller.Reseller.Reseller),   
            [Measures].[Reseller Sales Amount] < ([Measures].[Reseller Sales Amount],  
            [Date].Calendar.PrevMember)  
            )  
         )  
MEMBER [Geography].[State-Province].x AS   
   Aggregate (   
      {[Geography].[State-Province].&[WA]&[US],   
      [Geography].[State-Province].&[OR]&[US] }   
         )  
SELECT NON EMPTY Hierarchize (  
   AddCalculatedMembers (  
      {DrillDownLevel({[Product].[All Products]})}  
         )  
   )  
        DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE ([Geography].[State-Province].x,   
    [Date].[Calendar].[Calendar Quarter].&[2003]&[4],  
    [Measures].[Declining Reseller Sales])  
```  
  
## <a name="see-also"></a>参照  
 [PeriodsToDate &#40;MDX&#41;](../mdx/periodstodate-mdx.md)   
 [子 &#40;MDX&#41;](../mdx/children-mdx.md)   
 [Hierarchize &#40;MDX&#41;](../mdx/hierarchize-mdx.md)   
 [MDX&#41;&#41; &#40;設定 &#40;数 ](../mdx/count-set-mdx.md)   
 [MDX&#41;のフィルター処理 &#40;](../mdx/filter-mdx.md)   
 [MDX&#41;&#40;の Add演算メンバー ](../mdx/addcalculatedmembers-mdx.md)   
 [MDX&#41;&#40;ドリルダウンレベル ](../mdx/drilldownlevel-mdx.md)   
 [MDX&#41;&#40;プロパティ ](../mdx/properties-mdx.md)   
 [PrevMember &#40;MDX&#41;](../mdx/prevmember-mdx.md)   
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
