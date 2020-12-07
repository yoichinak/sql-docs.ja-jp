---
description: '&lt;&gt; (等しくない)MDX'
title: '&lt;&gt; (等しくない)(MDX) |Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8c2651c7d542ac0a8707c20e8b32f4ba33ac7b54
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471794"
---
# <a name="ltgt-not-equal-to-mdx"></a>&lt;&gt; (等しくない)MDX


  1つの多次元式 (MDX) 式の値が、別の MDX 式の値と等しくないかどうかを判断する比較演算を実行します。  
  
## <a name="syntax"></a>構文  
  
```  
  
MDX_Expression <> MDX_Expression  
```  
  
#### <a name="parameters"></a>パラメーター  
 *MDX_Expression*  
 有効な MDX 式です。  
  
## <a name="return-value"></a>戻り値  
 次の条件に基づくブール値。  
  
-   両方のパラメーターが null 以外であり、最初のパラメーターが2番目のパラメーターと等しくない場合は**true** 。  
  
-   両方のパラメーターが null 以外の場合、および最初のパラメーターが2番目のパラメーターと等しい場合は**false** 。  
  
-   いずれか一方または両方のパラメーターが NULL 値に評価される場合は、NULL です。  
  
## <a name="see-also"></a>参照  
 [Mdx 演算子リファレンス &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
