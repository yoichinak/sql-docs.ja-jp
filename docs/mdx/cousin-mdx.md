---
description: いとこ (MDX)
title: いとこ (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: eff78bb06f935311f178d2e39be11bec3e959776
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500545"
---
# <a name="cousin-mdx"></a>いとこ (MDX)


  親メンバーの下で、指定した子メンバーと同じ相対位置にある子メンバーを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Cousin( Member_Expression , Ancestor_Member_Expression )  
```  
  
## <a name="arguments"></a>引数  
 *Member_Expression*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
 *Ancestor_Member_Expression*  
 先祖メンバーを返す有効な多次元式 (MDX) メンバー式です。  
  
## <a name="remarks"></a>解説  
 この関数は、レベル内のメンバーの順序と位置を操作します。 2 つの階層が存在し、一方の階層に 4 つ、他方の階層に 5 つのレベルがあるとすると、一方の階層の 3 番目のレベルに対応する "いとこ" の位置関係に当たる子メンバーは他方の階層の 3 番目のレベルです。  
  
## <a name="examples"></a>例  
 次の例では、2003年の年のレベルにある先祖に基づいて、2002会計年度の第4四半期のいとこを取得します。 取得される子メンバーは、2003 会計年度の第 4 四半期です。  
  
```  
SELECT Cousin   
   ( [Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002],  
     [Date].[Fiscal].[FY 2003]  
   ) ON 0  
FROM [Adventure Works]  
```  
  
 次の例では、2004年の第2四半期の四半期レベルで、その先祖に基づいて2002年7月の会計年度のいとこを取得します。 取得したいとこは、2003年10月の月です。  
  
```  
SELECT Cousin   
   ([Date].[Fiscal].[Month].[July 2002] ,  
    [Date].[Fiscal].[Fiscal Quarter].[Q2 FY 2004]  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
