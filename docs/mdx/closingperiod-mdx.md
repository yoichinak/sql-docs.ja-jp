---
description: ClosingPeriod (MDX)
title: ClosingPeriod (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f457a941c8967ce6f3c6700760ff95d5c2999d0f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487635"
---
# <a name="closingperiod-mdx"></a>ClosingPeriod (MDX)


  指定されたレベルで指定されたメンバーの子孫のうち、最後の兄弟であるメンバーを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
ClosingPeriod( [ Level_Expression [ ,Member_Expression ] ] )  
```  
  
## <a name="arguments"></a>引数  
 *Level_Expression*  
 レベルを返す有効な多次元式 (MDX) 式です。  
  
 *Member_Expression*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 この関数は、主に Time 型のディメンションに対して使用することを目的としていますが、どのディメンションでも使用できます。  
  
-   レベル式が指定されている場合、 **Closingperiod** 関数は、指定されたレベルを含むディメンションを使用し、指定されたレベルの既定のメンバーの子孫のうち、最後の兄弟を返します。  
  
-   レベル式とメンバー式の両方が指定されている場合、 **Closingperiod** 関数は、指定されたレベルで指定されたメンバーの子孫のうち、最後の兄弟を返します。  
  
-   レベル式もメンバー式も指定されていない場合、 **Closingperiod** 関数は、Time 型のキューブ内のディメンションの既定のレベルとメンバー (存在する場合) を使用します。  
  
 **Closingperiod**関数は、次の MDX ステートメントと同じです。  
  
 `Tail(Descendants(Member_Expression, Level_Expression), 1)`.  
  
> [!NOTE]  
>  [OpeningPeriod](../mdx/openingperiod-mdx.md)関数は、 **OpeningPeriod**関数が最後の兄弟ではなく最初の兄弟を返す点を除いて、 **closingperiod**関数に似ています。  
  
## <a name="examples"></a>例  
 次の例では、Date ディメンションの FY2007 メンバーの既定のメジャーの値を返します (これにはセマンティックの種類が Time である)。 このメンバーが返されるのは、[All] レベルの最初の子孫が Fiscal Year レベルであるためです。Fiscal 階層は、階層コレクション内の最初のユーザー定義階層であるため既定の階層です。また、FY 2007 メンバーはこの階層内のこのレベルにある最後の兄弟です。  
  
```  
SELECT ClosingPeriod() ON 0  
FROM [Adventure Works]  
```  
  
 次の例では、日付と時刻の属性階層の date. date. date レベルにある、2006年11月30日の既定のメジャーの値を返します。 このメンバーは、Date 属性階層の [All] レベルの子孫の最後の兄弟です。  
  
```  
SELECT ClosingPeriod ([Date].[Date].[Date]) ON 0  
FROM [Adventure Works]  
```  
  
 次の例では、December, 2003 メンバーの既定のメジャーに対応する値が返されます。これは、Calendar ユーザー定義階層の Year レベルにある 2003 メンバーの子孫の最後の兄弟です。  
  
```  
SELECT ClosingPeriod ([Date].[Calendar].[Month],[Date].[Calendar].[Calendar Year].&[2003]) ON 0  
FROM [Adventure Works]  
```  
  
 次の例では、6月の2003メンバーの既定のメジャーの値を返します。これは、会計ユーザー定義階層の year レベルにある2003メンバーの子孫の最後の兄弟です。  
  
```  
SELECT ClosingPeriod ([Date].[Fiscal].[Month],[Date].[Fiscal].[Fiscal Year].&[2003]) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [OpeningPeriod &#40;MDX&#41;](../mdx/openingperiod-mdx.md)   
 [Mdx 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [LastSibling &#40;MDX&#41;](../mdx/lastsibling-mdx.md)  
  
  
