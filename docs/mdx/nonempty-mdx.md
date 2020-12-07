---
description: NonEmpty (MDX)
title: 空でない (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b887988327908f128633349de52f39a17d1e0978
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483725"
---
# <a name="nonempty-mdx"></a>NonEmpty (MDX)


  指定されたセットと 2 番目のセットのクロス積に基づいて、指定されたセットから空ではない組のセットを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
NONEMPTY(set_expression1 [,set_expression2])  
```  
  
## <a name="arguments"></a>引数  
 *set_expression1*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *set_expression2*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 この関数は、2番目のセット内の組全体で評価されるときに、空でない最初の指定されたセット内の組を返します。 **空**でない関数は計算を考慮し、重複する組を保持します。 2番目のセットが指定されていない場合、式は、属性階層のメンバーの現在の座標とキューブ内のメジャーのコンテキストで評価されます。  
  
> [!NOTE]  
>  非推奨の [NonEmptyCrossjoin &#40;MDX&#41;](../mdx/nonemptycrossjoin-mdx.md) 関数ではなく、この関数を使用します。  
  
> [!IMPORTANT]  
>  空以外は、組自体ではなく、組によって参照されるセルの特性です。  
  
## <a name="examples"></a>例  
 次のクエリは、 **空**でないの簡単な例を示しています。この例では、2001年7月1日に Internet Sales Amount の null 以外の値を持つすべての顧客が返されます。  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `NONEMPTY(`  
  
 `[Customer].[Customer].[Customer].MEMBERS`  
  
 `, {([Date].[Calendar].[Date].&[20010701], [Measures].[Internet Sales Amount])}`  
  
 `)`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 次の例では、顧客と購入日を含む組のセットを返します。 **フィルター** 関数と **空** でない関数を使用して、各顧客が購入した最後の日付を検索します。  
  
 `WITH SET MYROWS AS FILTER`  
  
 `(NONEMPTY`  
  
 `([Customer].[Customer Geography].[Customer].MEMBERS`  
  
 `* [Date].[Date].[Date].MEMBERS`  
  
 `, [Measures].[Internet Sales Amount]`  
  
 `) AS MYSET`  
  
 `, NOT(MYSET.CURRENT.ITEM(0)`  
  
 `IS MYSET.ITEM(RANK(MYSET.CURRENT, MYSET)).ITEM(0))`  
  
 `)`  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `MYROWS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>関連項目  
 [DefaultMember &#40;MDX&#41;](../mdx/defaultmember-mdx.md)   
 [MDX&#41;のフィルター処理 &#40;](../mdx/filter-mdx.md)   
 [IsEmpty &#40;MDX&#41;](../mdx/isempty-mdx.md)   
 [Mdx 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [NonEmptyCrossjoin &#40;MDX&#41;](../mdx/nonemptycrossjoin-mdx.md)  
  
  
