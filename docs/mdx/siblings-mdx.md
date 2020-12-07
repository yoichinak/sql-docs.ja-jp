---
description: Siblings (MDX)
title: 兄弟 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cfced6c9fb760903ef93a26e8e417df3d6cabd40
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500435"
---
# <a name="siblings-mdx"></a>Siblings (MDX)


  指定されたメンバー自体を含めて、メンバーの兄弟を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Member_Expression.Siblings   
```  
  
## <a name="arguments"></a>引数  
 *Member_Expression*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
### <a name="example"></a>例  
 次の例では、2003年1月2003および2月2003の兄弟の既定のメジャーを返し、3月2003を含みます。  
  
```  
SELECT [Date].[Calendar].[Month].[March 2003].Siblings ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
