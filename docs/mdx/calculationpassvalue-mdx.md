---
description: CalculationPassValue (MDX)
title: 電卓 Ationpass Value (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 98d30326b709f7bd651b7941e48d412a7b875ffd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88425044"
---
# <a name="calculationpassvalue-mdx"></a>CalculationPassValue (MDX)


  キューブに対して指定された計算パスを評価し、多次元式 (MDX) 式の数値または文字列値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
      Numeric syntax  
CalculationPassValue(Numeric_Expression,Pass_Value [, ABSOLUTE | RELATIVE [,ALL]])  
String syntax  
CalculationPassValue(String_Expression ,Pass_Value [, ABSOLUTE | RELATIVE [,ALL]])  
```  
  
## <a name="arguments"></a>引数  
 *Numeric_Expression*  
 有効な数値式です。通常は、数値を返すセル座標の多次元式 (MDX) 式です。  
  
 *String_Expression*  
 有効な文字列式です。通常は、文字列として表現された数値を返すセル座標の有効な多次元式 (MDX) 式です。  
  
 *Pass_Value*  
 計算パス番号を指定する有効な数値式です。  
  
 ABSOLUTE  
 *Pass_Value*パラメーターに、計算パスの0から始まるインデックスが含まれていることを示すアクセスフラグ値。 アクセス フラグ値が指定されていない場合は、ABSOLUTE が既定のアクセス フラグ値になります。  
  
 RELATIVE  
 *Pass_Value*パラメーターに、トリガーする計算の計算パスからの相対オフセットが含まれていることを示すアクセスフラグ値。 このオフセットが 0 より小さい計算パス インデックスになる場合は、計算パス 0 が使用されます。したがって、エラーは発生しません。  
  
 ALL  
 このフラグが設定されている場合、ストレージエンジンによって読み込まれた値を除き、すべての値が null になります。 このフラグが設定されていない場合は、何の計算も適用されずに値が集計されます。  
  
## <a name="remarks"></a>解説  
 数値式が指定されると、この関数は、指定された計算パス内で指定されている (さらに、必要に応じてアクセス フラグとアクセス フラグ修飾子で修飾されている) MDX 数値式を評価し、数値を返します。  
  
 文字列式が指定されている場合、関数は、指定された計算パスで指定された MDX 文字列式を評価し、必要に応じてアクセスフラグとアクセスフラグ修飾子で修飾することによって、文字列値を返し*ます。*  
  
 での自動再帰解決を使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] すると、この関数はあまり実用的ではありません。  
  
> [!NOTE]  
>  MDX スクリプト内では、管理者のみが計算 **Ationpass value** 関数を使用できます。 この関数を含む MDX スクリプトが、管理者特権を持たないロールのコンテキストで実行されている場合、エラーが発生します。  
  
## <a name="see-also"></a>参照  
 [計算 Ationcurrentpass &#40;MDX&#41;](../mdx/calculationcurrentpass-mdx.md)   
 [IIf &#40;MDX&#41;](../mdx/iif-mdx.md)   
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
