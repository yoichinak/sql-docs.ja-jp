---
description: RangeMid (DMX)
title: RangeMid (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f6645750341fff6ba15438503956d5be5e8662f0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500907"
---
# <a name="rangemid-dmx"></a>RangeMid (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  分離された列に対して検出される予測バケットの中間点を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
RangeMid(<scalar column reference>)  
```  
  
## <a name="applies-to"></a>適用対象  
 分離スカラー列。  
  
## <a name="return-type"></a>戻り値の型  
 スカラー値。  
  
## <a name="remarks"></a>解説  
 [DMX&#41;&#40;の SELECT FROM &#60;モデル&#62; 予測結合](../dmx/select-from-model-prediction-join-dmx.md)で使用する場合、 **RangeMin**、 **Rangemid**、および**RangeMax**関数は、指定されたバケットの実際の境界値を返します。 たとえば、離散化列で予測を実行する場合、クエリは予測されたバケット数を離散化列に返します。 **RangeMin**、 **rangemid**、および**RangeMax**関数は、予測によって指定されるバケットを記述します。 **Rangemid**関数が予測結合ステートメントで使用されている場合、スカラー列参照には不連続の予測可能列のみを含めることができます。  
  
## <a name="examples"></a>例  
 次の例では、TM デシジョンツリーマイニングモデルの年収連続列の最小値、最大値、および平均値が返されます。  
  
```  
SELECT DISTINCT   
    RangeMin([Yearly Income]) AS [Bucket Minimum],  
    RangeMid([Yearly Income]) AS [Bucket Average],   
    RangeMax([Yearly Income]) AS [Bucket Maximum]  
FROM [TM Decision Tree]  
```  
  
## <a name="see-also"></a>参照  
 [DMX&#41; 関数リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41;&#40;関数 ](../dmx/functions-dmx.md)   
 [DMX&#41;&#40;一般的な予測関数 ](../dmx/general-prediction-functions-dmx.md)   
 [DMX&#41;&#40;RangeMax ](../dmx/rangemax-dmx.md)   
 [DMX&#41;&#40;RangeMin ](../dmx/rangemin-dmx.md)  
  
  
