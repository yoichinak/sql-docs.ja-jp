---
description: Coバリエーション (MDX)
title: Coバリエーション (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e9475b7402a5317c18ad0ac5d4065ca2f4fdce26
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500525"
---
# <a name="covariancen-mdx"></a>Coバリエーション (MDX)


  バイアスをかけない母集団の公式 (x と y のペアの数で除算) を使用して、セットに対して評価された値の x と y のペアのサンプル共分散を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
CovarianceN(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Numeric_Expression_y*  
 有効な数値式です。通常は、Y 軸の値を表す数値を返すセル座標の多次元式 (MDX) 式です。  
  
 *Numeric_Expression_x*  
 有効な数値式です。通常は、X 軸の値を表す数値を返すセル座標の多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 **Coバリエーションの en**関数は、指定されたセットを最初の数値式に対して評価し、y 軸の値を取得します。 次に、関数は、指定されたセットを2番目の数値式に対して評価し、x 軸の値のセットを取得します。 2番目の数値式が指定されていない場合、関数は、指定されたセット内のセルの現在のコンテキストを x 軸の値として使用します。  
  
 **Coバリエーション**の関数は、バイアスをかける母集団の公式を使用します。 これは、バイアスをかける母集団の公式 (x と y のペアの数で除算) を使用する [共変性](../mdx/covariance-mdx.md) 関数とは対照的です。  
  
> [!NOTE]  
>  **Coバリエーション**の関数は、空のセル、またはテキストまたは論理値を含むセルを無視します。 ただし、この関数には0の値を持つセルが含まれています。  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
