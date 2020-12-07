---
description: IsInNode (DMX)
title: IsInNode (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 68f88915209a3a15cb7e8f1fd64e9d877655f3ac
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88352348"
---
# <a name="isinnode-dmx"></a>IsInNode (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  指定されたノードが現在のケースを含んでいるかどうかを示します。  
  
## <a name="syntax"></a>構文  
  
```  
  
IsInNode(<NodeID>)  
```  
  
## <a name="return-type"></a>戻り値の型  
 ブール型です。  
  
## <a name="remarks"></a>Remarks  
 **IsInNode** は、 [SELECT FROM &#60;model&#62; でのみ使用されます。DMX&#41;&#40;ケース ](../dmx/select-from-model-cases-dmx.md) は [&#60;モデル&#62; から選択します。DMX&#41;クエリを &#40;SAMPLE_CASES ](../dmx/select-from-model-sample-cases-dmx.md) します。  
  
## <a name="examples"></a>例  
 次の例では、IsInNode 関数で指定されたノードに関連付けられているモデルの作成に使用されたすべてのケースを返します。  
  
```  
Select * from [TM Decision Tree].Cases  
WHERE IsInNode('0')  
```  
  
## <a name="see-also"></a>参照  
 [DMX&#41; 関数リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41;&#40;関数 ](../dmx/functions-dmx.md)   
 [DMX&#41;&#40;一般的な予測関数 ](../dmx/general-prediction-functions-dmx.md)  
  
  
