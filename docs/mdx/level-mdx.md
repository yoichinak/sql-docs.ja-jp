---
description: Level (MDX)
title: レベル (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cfe1c3374b15b34a47fb1bd19b7233dd96db7151
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429884"
---
# <a name="level-mdx"></a>Level (MDX)


  メンバーのレベルを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Member_Expression.Level  
```  
  
## <a name="arguments"></a>引数  
 *Member_Expression*  
 メンバーを返す有効な多次元式 (MDX) です。  
  
### <a name="examples"></a>例  
 次の例では、 **レベル** 関数を使用して、Adventure works キューブ内のすべての月を返します。  
  
```  
SELECT[Date].[Fiscal].[Month].[February 2002].Level.Members ON 0,  
[Measures].[Internet Sales Amount] ON 1  
FROM [Adventure Works]  
```  
  
 次の例では、 **レベル** 関数を使用して、Adventure works キューブの Model name 属性階層にあるすべての目的の自転車ショップのレベル名を返します。  
  
```  
WITH MEMBER Measures.x AS   
   [Product].[Model Name].[All-Purpose Bike Stand].Level.Name  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
