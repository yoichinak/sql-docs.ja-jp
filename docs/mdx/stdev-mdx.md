---
description: Stdev (MDX)
title: Stdev (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e443cd7be9301dc5b5907e49fd967b1507feae03
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386948"
---
# <a name="stdev-mdx"></a>Stdev (MDX)


  バイアスをかけない母集団の公式 (n-1 で除算) を使用して、セットに対して評価される数値式のサンプル標準偏差を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Stdev(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Numeric_Expression*  
 有効な数値式です。通常は、数値を返すセル座標の多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 **Stdev**関数は、バイアスをかける母集団の公式を使用し、 [StdevP](../mdx/stdevp-mdx.md)関数はバイアスをかける母集団の公式を使用します。  
  
## <a name="example"></a>例  
 次の例では、バイアスをかけない母集団の公式を使用して、2003 年度の最初の 3 か月に対して評価した、Internet Order Quantity の標準偏差を返します。  
  
```  
WITH MEMBER Measures.x AS   
   Stdev   
   ( { [Date].[Calendar].[Month].[January 2003],  
       [Date].[Calendar].[Month].[February 2003],  
       [Date].[Calendar].[Month].[March 2003]},  
    [Measures].[Internet Order Quantity])  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
