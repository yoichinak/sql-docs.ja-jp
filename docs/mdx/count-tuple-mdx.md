---
description: Count (組) (MDX)
title: Count (組) (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4212e3ed86d10035793cecd45ab071feb57e5abf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500555"
---
# <a name="count-tuple-mdx"></a>Count (組) (MDX)


  組の次元数を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Tuple_Expression.Count  
```  
  
## <a name="arguments"></a>引数  
 *Tuple_Expression*  
 組を返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 組の次元数を返します。  
  
## <a name="example"></a>例  
 次のクエリの計算されるメジャーは、値2を返します。これは、組に存在する階層の数です `([Measures].[Internet Sales Amount], [Date].[Calendar].[Calendar Year].&[2001])` 。  
  
```  
WITH MEMBER MEASURES.COUNTTUPLE AS  
COUNT(([Measures].[Internet Sales Amount], [Date].[Calendar].[Calendar Year].&[2001]))  
SELECT MEASURES.COUNTTUPLE ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [&#40;ディメンション&#41; &#40;MDX&#41;のカウント ](../mdx/count-dimension-mdx.md)   
 [MDX&#41;&#41; &#40;&#40;階層レベルのカウント ](../mdx/count-hierarchy-levels-mdx.md)   
 [MDX&#41;&#41; &#40;設定 &#40;数 ](../mdx/count-set-mdx.md)   
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
