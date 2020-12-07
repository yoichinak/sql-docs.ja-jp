---
description: LinRegPoint (MDX)
title: LinRegPoint (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4f298d58b14f3005b86f8fa7773a4faef1c94c79
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429844"
---
# <a name="linregpoint-mdx"></a>LinRegPoint (MDX)


  セットの線形回帰を計算し、回帰直線の *y 切片* の値を返します。 y = ax + b (x の特定の値)。  
  
## <a name="syntax"></a>構文  
  
```  
  
LinRegPoint(Slice_Expression_x, Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>引数  
 *Slice_Expression_x*  
 有効な数値式です。通常は、スライサー軸の値を表す数値を返すセル座標の多次元式 (MDX) 式です。  
  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Numeric_Expression_y*  
 有効な数値式です。通常は、Y 軸の値を表す数値を返すセル座標の多次元式 (MDX) 式です。  
  
 *Numeric_Expression_x*  
 有効な数値式です。通常は、X 軸の値を表す数値を返すセル座標の多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 最小二乗法を使用する線形回帰では、回帰直線の式 (つまり、一連の点に最適な線) が計算されます。 回帰直線の式は次のようになります。ここで、は傾き、b は切片です。  
  
 y = ax+b  
  
 **Linregpoint**関数は、y 軸の値を取得するために、指定されたセットを2番目の数値式に対して評価します。 次に、関数は、指定されたセットを3番目の数値式に対して評価し、x 軸の値を取得します。 3番目の数値式が指定されていない場合、関数は、指定されたセット内のセルの現在のコンテキストを x 軸の値として使用します。 X 軸の引数を指定しないことは、時間ディメンションでよく使用されます。  
  
 線型回帰直線が計算された後、1 番目の数値式に対して回帰直線式の値が計算され、返されます。  
  
> [!NOTE]  
>  **Linregpoint**関数は、空のセルまたはテキストを含むセルを無視します。 ただし、この関数には0の値を持つセルが含まれています。  
  
## <a name="example"></a>例  
 次の例では、売上数量と店舗売上の統計的関係に基づいて、過去 10 期間の予測売上数量を返しています。  
  
```  
LinRegPoint([Measures].[Unit Sales],LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
