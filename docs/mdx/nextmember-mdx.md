---
description: NextMember (MDX)
title: NextMember (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 33824ba605fc3acd0a994d0e0a6b411afdda2306
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483744"
---
# <a name="nextmember-mdx"></a>NextMember (MDX)


  指定されたメンバーを含むレベルの次のメンバーを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Member_Expression.NextMember   
```  
  
## <a name="arguments"></a>引数  
 *Member_Expression*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 **Nextmember**関数は、指定されたメンバーを含む、同じレベルの次のメンバーを返します。  
  
## <a name="example"></a>例  
 次の例では、8月2001メンバーの次のメンバーとして8月2001メンバーが返されます。  
  
```  
SELECT [Date].[Calendar].[Month].[July 2001].NextMember ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
