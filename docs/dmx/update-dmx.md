---
description: 更新 (DMX)
title: 更新 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d74a59aaea079a5d3c1945b92813f6d276591b78
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88394878"
---
# <a name="update-dmx"></a>更新 (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  データマイニングモデルの **NODE_CAPTION** 列を変更します。  
  
## <a name="syntax"></a>構文  
  
```  
  
UPDATE <model>.CONTENT  
SET NODE_CAPTION='new caption'  
[WHERE <condition expression>]  
```  
  
## <a name="arguments"></a>引数  
 *model*  
 モデル識別子。  
  
 *新しいキャプション*  
 **NODE_CAPTION**列の新しい名前を含む文字列。  
  
 *条件式*  
 任意。 列リストから返される値を制限する条件。  
  
## <a name="examples"></a>例  
 次の例では、 **UPDATE** ステートメントによって、クラスターの既定の名前が `Cluster 1` `001` よりわかりやすい名前に変更され `Likely Customers` ます。  
  
```  
UPDATE [TM Clustering].CONTENT  
SET NODE_CAPTION= 'Likely Customers'  
WHERE NODE_UNIQUE_NAME = '001'  
```  
  
## <a name="see-also"></a>参照  
 [DMX&#41; データ定義ステートメント &#40;のデータマイニング拡張機能](../dmx/dmx-statements-data-definition.md)   
 [DMX&#41; データ操作ステートメントを &#40;データマイニング拡張機能](../dmx/dmx-statements-data-manipulation.md)   
 [データ マイニング拡張機能 &#40;DMX&#41; ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
