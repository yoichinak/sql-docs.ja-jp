---
description: Covariance (MDX)
title: 共変性 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 32471a48f0a669f7b72b5946f07403d6851dfb74
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500535"
---
# <a name="covariance-mdx"></a>Covariance (MDX)


  バイアスをかけた母集団の公式 (X と Y のペアの数で除算) を使用して、セットに対して評価された X と Y の値のペアの母共分散を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Covariance(Set_Expression,Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Numeric_Expression_y*  
 有効な数値式です。通常は、Y 軸の値を表す数値を返すセル座標の多次元式 (MDX) 式です。  
  
 *Numeric_Expression_x*  
 有効な数値式です。通常は、X 軸の値を表す数値を返すセル座標の多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 **共変性**関数は、指定されたセットを最初の数値式に対して評価し、y 軸の値を取得します。 次に、関数は、指定されたセットを2番目の数値式に対して評価し、x 軸の値のセットを取得します。 2番目の数値式が指定されていない場合、関数は、指定されたセット内のセルの現在のコンテキストを x 軸の値として使用します。  
  
 **共変性**関数は、バイアスをかける母集団の公式を使用します。 これは、バイアスをかける母集団の公式 (x と y のペアの数を除算した後、1を引く) を使用する [Coバリエーション](../mdx/covariancen-mdx.md) の関数とは対照的です。  
  
> [!NOTE]  
>  **共変性**関数は、空のセル、またはテキストや論理値を含むセルを無視します。 ただし、この関数には0の値を持つセルが含まれています。  
  
## <a name="example"></a>例  
 次の例は、共変性関数の使用方法を示しています。  
  
```  
WITH   
MEMBER [Measures].[CovarianceDemo] AS  
COVARIANCE([Date].[Date].[Date].Members, [Measures].[Internet Sales Amount], [Measures].[Internet Order Count])   
SELECT {[Measures].[CovarianceDemo]} ON 0   
FROM  
[Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
