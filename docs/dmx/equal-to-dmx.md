---
description: = (等号) (DMX)
title: = (等しい) (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ba57583c8af1b739335abc27c33eaaf2ea54dc1f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88413359"
---
# <a name="-equal-to-dmx"></a>= (等号) (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  1つのデータマイニング拡張機能 (DMX) 式の値が、別の DMX 式の値と等しいかどうかを判断する比較演算を実行します。  
  
## <a name="syntax"></a>構文  
  
```  
  
DMX_Expression = DMX_Expression   
```  
  
#### <a name="parameters"></a>パラメーター  
 *DMX_Expression*  
 有効な DMX 式です。  
  
## <a name="return-value"></a>戻り値  
 両方のパラメーターが NULL 以外であり、1 番目のパラメーターの値が 2 番目のパラメーターの値と等しい場合、TRUE を含むブール値です。 両方のパラメーターが null 以外で、最初のパラメーターの値が2番目のパラメーターの値と等しくない場合、ブール値には FALSE が含まれます。 ブール値には、いずれかのパラメーターまたは両方のパラメーターが null 値に評価される場合、null 値が含まれます。  
  
## <a name="see-also"></a>参照  
 [DMX&#41;&#40;比較演算子 ](../dmx/operators-comparison.md)   
 [DMX&#41; オペレーターリファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [DMX&#41;&#40;オペレーター ](../dmx/operators-dmx.md)  
  
  
