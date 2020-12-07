---
description: ClusterProbability (DMX)
title: ClusterProbability (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cb2cc218ff18b23237c561a3cac1a9a68373f3ae
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726324"
---
# <a name="clusterprobability-dmx"></a>ClusterProbability (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  入力ケースが指定されたクラスターに所属する確率を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
ClusterProbability([<Node_Caption>])  
```  
  
## <a name="applies-to"></a>適用対象  
 この関数は、基になるデータマイニングモデルでクラスタリングがサポートされている場合にのみ使用できます。  
  
## <a name="return-type"></a>戻り値の型  
 スカラー値。  
  
## <a name="remarks"></a>解説  
 次の構文では、マイニングモデルコンテンツスキーマ行セットを使用して、マイニングモデルに存在するノードのキャプションを返します。  
  
```  
SELECT NODE_CAPTION FROM <model>.CONTENT  
```  
  
 この構文の使用方法の詳細については、「 [SELECT FROM &#60;model&#62;」を参照してください。DMX&#41;のコンテンツ &#40;](../dmx/select-from-model-content-dmx.md)ます。 マイニングモデルコンテンツスキーマ行セットの詳細については、「 [DMSCHEMA_MINING_MODEL_CONTENT 行セット](/previous-versions/sql/sql-server-2012/ms126267(v=sql.110))」を参照してください。  
  
 \<node caption>が指定されていない場合、関数は、入力ケースが最も可能性の高いクラスターに属する確率を返します。 **クラスター**関数を使用して、最も可能性の高いクラスターを返します。  
  
## <a name="examples"></a>例  
 次の例は、指定したケースが Cluster 2 というラベルが付けられたクラスターに存在する確率を返します。  
  
```  
SELECT  
  ClusterProbability('Cluster 2')  
From  
  [TM Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>参照  
 [DMX&#41;のクラスター &#40;](../dmx/cluster-dmx.md)   
 [DMX&#41; 関数リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41;&#40;関数 ](../dmx/functions-dmx.md)   
 [DMX&#41;&#40;一般的な予測関数 ](../dmx/general-prediction-functions-dmx.md)  
  
