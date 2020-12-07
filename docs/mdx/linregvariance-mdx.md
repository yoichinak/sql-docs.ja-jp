---
description: LinRegVariance (MDX)
title: LinRegVariance (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: bd223530c0b184dd723abbb68c2acccd1240d870
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88477034"
---
# <a name="linregvariance-mdx"></a>LinRegVariance (MDX)


  セットの線形回帰を計算し、回帰直線 (y = ax + b) に関連付けられている変位を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
LinRegVariance(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] ] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Numeric_Expression_y*  
 有効な数値式です。通常は、Y 軸の値を表す数値を返すセル座標の多次元式 (MDX) 式です。  
  
 *Numeric_Expression_x*  
 有効な数値式です。通常は、X 軸の値を表す数値を返すセル座標の多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 最小二乗法を使用する線形回帰では、回帰直線の式 (つまり、一連の点に最適な線) が計算されます。 回帰直線の式は次のようになります。ここで、は傾き、b は切片です。  
  
 y = ax+b  
  
 **Linregvariance**関数は、y 軸の値を取得するために、最初の数値式に対して指定された setagainst 評価します。 次に、関数は、指定されている場合、2番目の数値式に対して指定した setagainst 評価し、x 軸の値を取得します。 2番目の数値式が指定されていない場合、関数は、指定されたセット内のセルの現在のコンテキストを x 軸の値として使用します。 X 軸の引数を指定しないことは、時間ディメンションでよく使用されます。  
  
 **Linregvariance**関数は、点のセットを取得した後、直線式が点にどのように適合するかを示す統計的変位を返します。  
  
> [!NOTE]  
>  **Linregvariance**関数は、空のセル、またはテキストや論理値を含むセルを無視します。 ただし、この関数には0の値を持つセルが含まれています。  
  
## <a name="example"></a>例  
 次の例では、売上数量メジャーと店舗売上メジャーの点に対して直線式がどの程度適合しているかを示す統計的変位を返しています。  
  
```  
LinRegVariance(LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
