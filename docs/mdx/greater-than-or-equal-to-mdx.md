---
description: '&gt;= (以上) (MDX)'
title: '&gt;= (以上) (MDX) |Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1e9ce7d9f7e372ac9193751c258af63ba6f300fb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429934"
---
# <a name="gt-greater-than-or-equal-to-mdx"></a>&gt;= (以上) (MDX)


  1つの多次元式 (MDX) 式の値が、別の MDX 式の値以上であるかどうかを判断する比較演算を実行します。  
  
## <a name="syntax"></a>構文  
  
```  
  
MDX_Expression >= MDX_Expression  
```  
  
#### <a name="parameters"></a>パラメーター  
 *MDX_Expression*  
 有効な MDX 式です。  
  
## <a name="return-value"></a>戻り値  
 次の条件に基づくブール値。  
  
-   最初のパラメーターの値が2番目のパラメーターの値以上の場合に**true**を指定します。  
  
-   最初のパラメーターの値が2番目のパラメーターの値よりも小さい場合は**false** 。  
  
-   両方のパラメーターが null の場合、または1つのパラメーターが null で、もう一方のパラメーターが0の場合は**true** 。  
  
## <a name="examples"></a>例  
 この演算子の使用例を次に示します。  
  
```  
-- This query returns the gross profit margin (GPM)  
-- for Australia where the GPM is greater than or equal to 50%.  
With Member [Measures].[HighGPM] as  
  IIF(  
      [Measures].[Gross Profit Margin] >= .5,  
      [Measures].[Gross Profit Margin],  
      null)  
SELECT   
    NON EMPTY [Sales Territory].[Sales Territory Country].[Australia] ON 0,  
    NON EMPTY [Product].[Category].Members ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[HighGPM])  
```  
  
## <a name="see-also"></a>参照  
 [Mdx 演算子リファレンス &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
