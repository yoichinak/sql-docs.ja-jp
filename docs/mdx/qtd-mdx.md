---
description: Qtd (MDX)
title: Qtd (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ea3bd80fa85d95dd3adf52793d5895425b40b9fe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500455"
---
# <a name="qtd-mdx"></a>Qtd (MDX)


  指定されたメンバーと同じレベルにある兄弟メンバーのセットを返します。最初の兄弟から始まり、指定されたメンバーで終わります。これは、時間ディメンションの *Quarter* レベルによって制限されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
Qtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>引数  
 *Member_Expression*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 メンバー式が指定されていない場合、既定値は、メジャーグループ内の*Time*型の最初の次元で、*四半期*型のレベルを持つ最初の階層の現在のメンバーになります。  
  
 **Qtd**関数は、 [PeriodsToDate &#40;MDX&#41;](../mdx/periodstodate-mdx.md)関数の、レベル式の引数が*Quarter*に設定されている関数のショートカット関数です。 つまり、`Qtd(Member_Expression)` と `PeriodsToDate(Quarter_Level_Expression, Member_Expression)` は機能的に等価です。  
  
## <a name="example"></a>例  
 次の例では、 `Measures.[Order Quantity]` `Date` **Adventure works** キューブから、ディメンションに含まれている calendar year 2003 の第3四半期の最初の2か月を集計した、メンバーの合計を返します。  
  
```  
WITH MEMBER [Date].[Calendar].[First2MonthsSecondSemester2003] AS  
    Aggregate(  
        QTD([Date].[Calendar].[Month].[August 2003])  
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
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
