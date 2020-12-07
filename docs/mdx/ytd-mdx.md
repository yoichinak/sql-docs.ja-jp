---
description: Ytd (MDX)
title: Ytd (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 14f286a304e03624a9ce20c1bd7b045dffc38688
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491370"
---
# <a name="ytd-mdx"></a>Ytd (MDX)


  指定されたメンバーと同じレベルにある兄弟メンバーのセットを返します。最初の兄弟から始まり、指定されたメンバーで終わります。これは、時間ディメンションの *Year* レベルによって制限されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
Ytd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>引数  
 *Member_Expression*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 メンバー式が指定されていない場合、既定値は、メジャーグループ内の*Time*型の最初の次元の*年*のレベルを持つ最初の階層の現在のメンバーになります。  
  
 **Ytd**関数は、レベルの基になる属性階層の Type プロパティが*Years*に設定されている[PeriodsToDate](../mdx/periodstodate-mdx.md)関数のショートカット関数です。 つまり、 `Ytd(Member_Expression)` はと同じです `PeriodsToDate(Year_Level_Expression,Member_Expression)` 。 Type プロパティが *FiscalYears*に設定されている場合、この関数は機能しないことに注意してください。  
  
## <a name="example"></a>例  
 次の例では、 `Measures.[Order Quantity]` `Date` **Adventure works** キューブから、ディメンションに含まれる2003年の最初の8か月間に集計された、メンバーの合計を返します。  
  
```  
WITH MEMBER [Date].[Calendar].[First8MonthsCY2003] AS  
    Aggregate(  
        YTD([Date].[Calendar].[Month].[August 2003])  
    )  
SELECT   
    [Date].[Calendar].[First8MonthsCY2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 **Ytd** は、パラメーターが指定されていない場合に頻繁に使用されます。つまり、 [CURRENTMEMBER &#40;MDX&#41;](../mdx/currentmember-mdx.md) 関数は、次のクエリに示すように、年度累計累計をレポートに表示します。  
  
 `WITH MEMBER MEASURES.YTDDEMO AS`  
  
 `AGGREGATE(YTD(), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount], MEASURES.YTDDEMO} ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
