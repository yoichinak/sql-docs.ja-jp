---
description: Sum (MDX)
title: Sum (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f65525836157f5ac106cfa7ba0d5458689583def
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449624"
---
# <a name="sum-mdx"></a>Sum (MDX)


  指定されたセットに対して評価される数値式の合計を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Sum( Set_Expression [ , Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 有効な多次元式 (MDX) セット式です。  
  
 *Numeric_Expression*  
 有効な数値式です。通常は、数値を返すセル座標の多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 数値式を指定すると、指定した数値式がセット全体で評価され、合計されます。 数値式を指定しなかった場合、指定したセットがセットのメンバーの現在のコンテキストで評価されてから、合計が算出されます。 SUM 関数を数値式ではない式に適用した場合、結果は不確定になります。  
  
> [!NOTE]  
>  Analysis Services では、数値セットの合計が計算される際、NULL 値は無視されます。  
  
## <a name="examples"></a>例  
 次の例では、2002 2001 暦年の属性階層のすべてのメンバーについて、再販業者の売上金額の合計を返します。  
  
```  
WITH MEMBER Measures.x AS SUM  
   ( { [Date].[Calendar Year].&[2001]  
         , [Date].[Calendar Year].&[2002] }  
      , [Measures].[Reseller Sales Amount]  
    )  
SELECT Measures.x ON 0  
,[Product].[Category].Members ON 1  
FROM [Adventure Works]  
```  
  
 次の例では、2002 年 7 月のインターネット販売にかかる運賃をその月の 20 日まで合計して返しています。  
  
```  
WITH MEMBER Measures.x AS SUM   
   (  
      MTD([Date].[Calendar].[Date].[July 20, 2002])  
     , [Measures].[Internet Freight Cost]  
     )  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
 次の例では、WITH MEMBER キーワードと **SUM** 関数を使用して、Measures ディメンション内の計算されるメンバーを定義します。これには、カナダの再販業者 Sales Amount メジャーの合計と、Geography ディメンションの Country 属性階層の米国メンバーが含まれます。  
  
```  
WITH MEMBER Measures.NorthAmerica AS SUM   
      (  
         {[Geography].[Country].&[Canada]  
            , [Geography].[Country].&[United States]}  
       ,[Measures].[Reseller Sales Amount]  
      )  
SELECT {[Measures].[NorthAmerica]} ON 0,  
[Product].[Category].members ON 1  
FROM [Adventure Works]  
```  
  
 多くの場合、 **SUM**関数は、階層の CURRENTMEMBER に応じて異なるセットを返す**YTD**のような**CURRENTMEMBER**関数または関数と共に使用されます。 たとえば、次のクエリは、年度の初めから ROWS 軸に表示されている日付までのすべての日付の Internet Sales Amount メジャーの合計を返します。  
  
 `WITH MEMBER MEASURES.YTDSUM AS`  
  
 `SUM(YTD(), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount], MEASURES.YTDSUM} ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
