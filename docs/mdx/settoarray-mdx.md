---
description: SetToArray (MDX)
title: SetToArray (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f5b0c4b39761e25065b2c262943b4ce335fccf6e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386978"
---
# <a name="settoarray-mdx"></a>SetToArray (MDX)


  1つ以上のセットを、ユーザー定義関数で使用する配列に変換します。  
  
## <a name="syntax"></a>構文  
  
```  
  
SetToArray(Set_Expression1 [ ,Set_Expression2,...n ][ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression1*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Set_Expression2*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Numeric_Expression*  
 有効な数値式です。通常は、数値を返すセル座標の多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 **Settoarray**関数は、ユーザー定義関数で使用する1つ以上のセットを配列に変換します。 結果の配列内のディメンションの数は、指定されたセットの数と同一になります。  
  
 省略可能な数値式では、配列セルの値を指定できます。 数値式が指定されていない場合は、セットのクロス結合が現在のコンテキストで評価されます。  
  
 この結果作成される配列では、セルの座標がセットの並び順に対応します。 たとえば、`SA`、`SB`、`SC` という 3 つのセットがあるとします。 それぞれのセットには 2 つの要素があります。 MDX ステートメントでは、 `SetToArray(SA, SB, SC)` 次の3次元配列が作成されます。  
  
```  
(SA1, SB1, SC1) (SA2, SB1, SC1) (SA1, SB2, SC1) (SA2, SB2, SC1)   
(SA1, SB1, SC2) (SA2, SB1, SC2) (SA1, SB2, SC2) (SA2, SB2, SC2)   
```  
  
> [!NOTE]  
>  **Settoarray**関数の戻り値の型は、バリアント型である VT_ARRAY です。 そのため、 **Settoarray** 関数の出力は、ユーザー定義関数への入力としてのみ使用する必要があります。  
  
## <a name="example"></a>例  
 次の例では、配列を返します。  
  
```  
SetToArray([Geography].[Geography].Members, [Measures].[Internet Sales Amount])  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
