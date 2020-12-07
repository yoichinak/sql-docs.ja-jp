---
description: DistinctCount (MDX)
title: DistinctCount (MDX) |Microsoft Docs
ms.date: 11/12/2020
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 28807d1a24f97a6b197ad56d0434399ab53cd742
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584849"
---
# <a name="distinctcount-mdx"></a>DistinctCount (MDX)


  セット内の個別の空でないタプルの数を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
DistinctCount(Set_Expression)  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>注釈  
 **DistinctCount** 関数は、と同じです `Count(Distinct(Set_Expression), EXCLUDEEMPTY)` 。  
  
## <a name="examples"></a>例  
 次のクエリでは、DistinctCount 関数の使用方法を示します。  
  
 `WITH SET MySet AS`  
  
 `{[Customer].[Customer Geography].[Country].&[Australia],[Customer].[Customer Geography].[Country].&[Australia],`  
  
 `[Customer].[Customer Geography].[Country].&[Canada],[Customer].[Customer Geography].[Country].&[France],`  
  
 `[Customer].[Customer Geography].[Country].&[United Kingdom],[Customer].[Customer Geography].[Country].&[United Kingdom]}`  
  
 `*`  
  
 `{([Date].[Calendar].[Date].&[20010701],[Measures].[Internet Sales Amount] )}`  
  
 `//Returns the value 3 because Internet Sales Amount is null`  
  
 `//for the UK on the date specified`  
  
 `MEMBER MEASURES.SETDISTINCTCOUNT AS`  
  
 `DISTINCTCOUNT(MySet)`  
  
 `SELECT {MEASURES.SETDISTINCTCOUNT} ON 0`  
  
 `FROM [Adventure Works]`  
 
DistinctCount 関数は、セット内の個別の項目数を返します。この例では、省略可能な2番目のパラメーターを使用して、指定された組の値を持たない項目を除外します。 この場合、最初のパラメーターのセットには4つの個別の項目がありますが、この関数は3を返します。これは、オーストラリア、カナダ、フランスのみが、Internet Sales Amount の2001年7月1日のデータを持っているためです。
 
## <a name="see-also"></a>参照  
 [MDX&#41;&#41; &#40;設定 &#40;数 ](../mdx/count-set-mdx.md)   
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
