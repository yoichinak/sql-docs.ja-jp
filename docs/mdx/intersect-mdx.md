---
description: Intersect (MDX)
title: Intersect (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9216b334caf67191e231c3ec0389da3fb7493b24
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471844"
---
# <a name="intersect-mdx"></a>Intersect (MDX)


  2つの入力セットの積集合を返します。オプションで重複部分を保持します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Intersect(Set_Expression1 , Set_Expression2 [ , ALL ] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression1*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Set_Expression2*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 **Intersect**関数は、2つのセットの積集合を返します。 既定では、関数は、セットの交差前に両方のセットから重複部分を削除します。 指定された 2 つのセットの次元は同一である必要があります。  
  
 省略可能な **ALL** フラグは、重複部分を保持します。 **ALL**が指定されている場合、 **Intersect**関数は重複しない要素と同じように交差します。また、2番目のセットに一致する重複がある最初のセット内の重複部分と交差します。 指定された 2 つのセットの次元は同一である必要があります。  
  
## <a name="example"></a>例  
 次のクエリは 2003 年と 2004 年を返します。2 つのメンバーは指定された両方のセットに示されます。  
  
 `SELECT`  
  
 `INTERSECT(`  
  
 `{[Date].[Calendar Year].&[2001], [Date].[Calendar Year].&[2002],[Date].[Calendar Year].&[2003]}`  
  
 `, {[Date].[Calendar Year].&[2002],[Date].[Calendar Year].&[2003], [Date].[Calendar Year].&[2004]})`  
  
 `ON 0`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 次のクエリは、指定された2つのセットに異なる階層のメンバーが含まれているために失敗します。  
  
 `SELECT`  
  
 `INTERSECT(`  
  
 `{[Date].[Calendar Year].&[2001]}`  
  
 `, {[Customer].[City].&[Abingdon]&[ENG]})`  
  
 `ON 0`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
