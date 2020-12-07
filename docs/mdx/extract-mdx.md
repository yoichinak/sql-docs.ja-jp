---
description: Extract (MDX)
title: Extract (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0b168794a38a515d4ace97d576710041eac86195
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387518"
---
# <a name="extract-mdx"></a>Extract (MDX)


  抽出された階層要素から組のセットを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Extract(Set_Expression, Hierarchy_Expression1 [,Hierarchy_Expression2, ...n] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Hierarchy_Expression1*  
 階層を返す有効な多次元式 (MDX) 式です。  
  
 *Hierarchy_Expression2*  
 階層を返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 **Extract**関数は、抽出された階層要素の組で構成されるセットを返します。 指定したセット内の組ごとに、指定した階層のメンバーが結果セット内の新しい組に抽出されます。 この関数は、重複する組を常に削除します。  
  
 **Extract**関数は、 [Crossjoin](../mdx/crossjoin-mdx.md)関数の反対のアクションを実行します。  
  
## <a name="examples"></a>例  
 次のクエリは、**空**でない関数によって返される一連の組に対して**Extract**関数を使用する方法を示しています。  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `//Returns the distinct combinations of Customer and Date for all purchases`  
  
 `//of Bike Racks or Bike Stands`  
  
 `EXTRACT(`  
  
 `NONEMPTY(`  
  
 `[Customer].[Customer].[Customer].MEMBERS`  
  
 `*`  
  
 `[Date].[Date].[Date].MEMBERS`  
  
 `*`  
  
 `{[Product].[Product Categories].[Subcategory].&[26],[Product].[Product Categories].[Subcategory].&[27]}`  
  
 `*`  
  
 `{[Measures].[Internet Sales Amount]}`  
  
 `)`  
  
 `,  [Customer].[Customer], [Date].[Date])`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
