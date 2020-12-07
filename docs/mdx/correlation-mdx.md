---
description: Correlation (MDX)
title: 相関関係 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ae050b681830b81ffa63ae82c714d69d54b03c91
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387648"
---
# <a name="correlation-mdx"></a>Correlation (MDX)


  セットに対して評価される X と Y の値の組の相関係数を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Correlation( Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Numeric_Expression_y*  
 有効な数値式です。通常は、Y 軸の値を表す数値を返すセル座標の多次元式 (MDX) 式です。  
  
 *Numeric_Expression_x*  
 有効な数値式です。通常は、X 軸の値を表す数値を返すセル座標の多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 **相関**関数は、最初に最初の数値式に対して指定されたセットを評価し、y 軸の値を取得することで、2つの値のペアの相関係数を計算します。 次に、関数は、指定されたセットを2番目の数値式 (存在する場合) に対して評価し、x 軸の値のセットを取得します。 2番目の数値式が指定されていない場合、関数は、指定されたセット内のセルの現在のコンテキストを x 軸の値として使用します。  
  
> [!NOTE]  
>  **関連付け**関数は、空のセル、またはテキストや論理値を含むセルを無視します。 ただし、この関数には0の値を持つセルが含まれています。  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
