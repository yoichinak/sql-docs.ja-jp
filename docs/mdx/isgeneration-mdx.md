---
description: IsGeneration (MDX)
title: IsGeneration (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e7b7f3df41af6af51a826352814fc6aef52ef0a0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471834"
---
# <a name="isgeneration-mdx"></a>IsGeneration (MDX)


  指定したメンバーが指定したジェネレーションに存在するかどうかを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
IsGeneration(Member_Expression, Generation_Number)   
```  
  
## <a name="arguments"></a>引数  
 *Member_Expression*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
 *Generation_Number*  
 指定されたメンバーの評価対象となる世代を指定する有効な数値式です。  
  
## <a name="remarks"></a>解説  
 **Isgeneration**関数は、指定されたメンバーが指定されたジェネレーション番号に含まれる場合に**true**を返します。 それ以外の場合、関数は **false**を返します。 また、指定されたメンバーが空のメンバーに評価される場合、 **Isgeneration** 関数は **false**を返します。  
  
 世代インデックスの作成上の目的から、リーフ メンバーの世代インデックスは 0 になっています。 非リーフ メンバーの世代インデックスを判別するには、まず指定されたメンバーのすべての子メンバーの和集合から最高の世代インデックスを取得し、そのインデックスに 1 を加算します。 非リーフ メンバーの世代インデックスはこのような方法で決定されるので、1 つの非リーフ メンバーが複数の世代に属することもあり得ます。  
  
## <a name="example"></a>例  
 次の例では、[Date] の場合に TRUE を返します。[会計]。CurrentMember は2番目の生成の一部です。  
  
 `WITH MEMBER MEASURES.ISGENERATIONDEMO AS`  
  
 `IsGeneration([Date].[Fiscal].CURRENTMEMBER, 2)`  
  
 `SELECT {MEASURES.ISGENERATIONDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
