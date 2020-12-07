---
description: PeriodsToDate (MDX)
title: PeriodsToDate (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8b18fe4d90a8a0c56424c5e0a7f3607ceea0eae4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471704"
---
# <a name="periodstodate-mdx"></a>PeriodsToDate (MDX)


  時間ディメンションで指定されているレベル内で、指定されたメンバーと同じレベルにある兄弟メンバーのセットを返します。先頭は最初の兄弟、末尾は指定されたメンバーになります。  
  
## <a name="syntax"></a>構文  
  
```  
  
PeriodsToDate( [ Level_Expression [ ,Member_Expression ] ] )  
```  
  
## <a name="arguments"></a>引数  
 *Level_Expression*  
 レベルを返す有効な多次元式 (MDX) 式です。  
  
 *Member_Expression*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 **PeriodsToDate**関数は、指定されたレベルのスコープ内で、指定されたメンバーと同じレベルにある期間のセットを返します。最初の期間から始まり、指定されたメンバーで終わります。  
  
-   レベルが指定されている場合、階層の現在のメンバーは推定 *階層*です。**Currentmember**。ここで、 *階層*は指定されたレベルの階層です。  
  
-   レベルもメンバーも指定されていない場合、レベルは、メジャーグループ内の Time 型の最初の次元の最初の階層の現在のメンバーの親レベルになります。  
  
 `PeriodsToDate( Level_Expression, Member_Expression )` は、以下の MDX 式と機能的に等価です。  
  
 `TopCount(Descendants(Ancestor(Member_Expression, Level_Expression), Member_Expression.Level), 1):Member_Expression`  
  
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
  
## <a name="see-also"></a>参照  
 [TopCount &#40;MDX&#41;](../mdx/topcount-mdx.md)   
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
