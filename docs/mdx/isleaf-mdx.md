---
description: IsLeaf (MDX)
title: IsLeaf (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1b7dd1d76b417633ff50a77b3f2822e6f7cfd462
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471824"
---
# <a name="isleaf-mdx"></a>IsLeaf (MDX)


  指定されたメンバーがリーフメンバーであるかどうかを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
IsLeaf(Member_Expression)   
```  
  
## <a name="arguments"></a>引数  
 *Member_Expression*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 **Isleaf**関数は、指定されたメンバーがリーフメンバーである場合に**true**を返します。 それ以外の場合、関数は **false**を返します。  
  
## <a name="example"></a>例  
 次の例では、[Date] の場合に TRUE を返します。[会計]。CurrentMember はリーフメンバーです。  
  
 `WITH MEMBER MEASURES.ISLEAFDEMO AS`  
  
 `IsLeaf([Date].[Fiscal].CURRENTMEMBER)`  
  
 `SELECT {MEASURES.ISLEAFDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
