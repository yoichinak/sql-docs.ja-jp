---
description: 算術演算子 (DMX)
title: 算術演算子 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 77b9f300859b6ce1250ed9d36a33a88a3dd12fe1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426194"
---
# <a name="operators---arithmetic"></a>演算子 - 算術
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  データマイニング拡張機能 (DMX) では [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 、加算、減算、乗算、除算などの算術計算に算術演算子を使用できます。  
  
 次の表は、DMX がサポートする算術演算子を示しています。  
  
|演算子|説明|  
|--------------|-----------------|  
|[+ &#40;&#41; &#40;DMX&#41;を追加する ](../dmx/add-dmx.md)|2 つの数値を加算します。|  
|[-&#40;&#41; &#40;DMX&#41;を減算する ](../dmx/subtract-dmx.md)|ある数値から別の数値を減算します。|  
|[&#41; &#40;DMX&#41;を乗算&#42; &#40;](../dmx/multiply-dmx.md)|ある数値を別の数値によって乗算します。|  
|[ DMX&#41;&#41; &#40;分割&#40;](../dmx/divide-dmx.md)|1つの数値を別の数値で除算します。|  
  
 次の規則は、DMX 式の算術演算子の優先順位を決定します。  
  
-   式に複数の算術演算子がある場合、最初に乗算と除算が計算され、次に減算と加算が行われます。  
  
-   式のすべての算術演算子の優先順位が同じである場合、実行の順序は左から右になります。  
  
-   かっこ内の式は、他のすべての操作よりも優先されます。  
  
## <a name="see-also"></a>参照  
 [DMX&#41; リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-reference.md)   
 [DMX&#41; 関数リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41; オペレーターリファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [DMX&#41; ステートメントリファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-statements.md)   
 [DMX&#41; 構文表記規則を &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [DMX&#41; の構文要素を &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [DMX&#41;&#40;式 ](../dmx/expressions-dmx.md)   
 [DMX&#41;&#40;一般的な予測関数 ](../dmx/general-prediction-functions-dmx.md)   
 [DMX&#41;&#40;オペレーター ](../dmx/operators-dmx.md)   
 [構造と DMX 予測クエリの使用](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX 選択ステートメントについて](../dmx/understanding-the-dmx-select-statement.md)  
  
  
