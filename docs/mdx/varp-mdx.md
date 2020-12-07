---
description: VarP (MDX)
title: VarP (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c850ba60ac9900228c6adaa03aa97b46b1abddf1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429724"
---
# <a name="varp-mdx"></a>VarP (MDX)


  バイアスをかけた母集団の公式 ( *n*-1 で除算) を使用して、セットに対して評価される数値式の母分散を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
VarP(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Numeric_Expression*  
 有効な数値式です。通常は、数値を返すセル座標の多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 **VarP**関数は、指定されたセットに対して評価される、指定された数値式のバイアスをかけた分散を返します。  
  
 **VarP**関数は、バイアスをかける母集団の公式を使用し、 [Var](../mdx/var-mdx.md)関数はバイアスを使用しない母集団の公式を使用します。  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
