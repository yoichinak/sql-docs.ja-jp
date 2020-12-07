---
description: PredictHistogram (DMX)
title: PredictHistogram (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cbeaa08cd118e032465f8456c0d7d7e111562f88
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727704"
---
# <a name="predicthistogram-dmx"></a>PredictHistogram (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  指定された列の予測のためのヒストグラムを表すテーブルを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
PredictHistogram(<scalar column reference> | <cluster column reference>)  
```  
  
## <a name="applies-to"></a>適用対象  
 スカラー列参照またはクラスター列参照。 アソシエーションアルゴリズムを除くすべてのアルゴリズムの種類で使用でき [!INCLUDE[msCoName](../includes/msconame-md.md)] ます。  
  
## <a name="return-type"></a>戻り値の型  
 テーブルです。  
  
## <a name="remarks"></a>解説  
 ヒストグラムでは、統計列が生成されます。 返されるヒストグラムの列構造は、 **PredictHistogram** 関数で使用される列参照の型によって異なります。  
  
## <a name="scalar-columns"></a>スカラー列  
 では \<scalar column reference> 、 **PredictHistogram** 関数が返すヒストグラムは、次の列で構成されています。  
  
-   予測されている値。  
  
-   **$Support**  
  
-   **$Probability**  
  
-   **$ProbabilityVariance**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)] データマイニングアルゴリズムでは、 **$ProbabilityVariance**はサポートされていません。 アルゴリズムの場合、この列には常に0が格納され [!INCLUDE[msCoName](../includes/msconame-md.md)] ます。  
  
-   **$ProbabilityStdev**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)] データマイニングアルゴリズムでは、 **$ProbabilityStdev**はサポートされていません。 アルゴリズムの場合、この列には常に0が格納され [!INCLUDE[msCoName](../includes/msconame-md.md)] ます。  
  
-   **$AdjustedProbability**  
  
     **$AdjustedProbability**列は、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] [!INCLUDE[msCoName](../includes/msconame-md.md)] データマイニング仕様の OLE DB の拡張機能です。  
  
## <a name="cluster-columns"></a>クラスター列  
 に対して **PredictHistogram** 関数が返すヒストグラムは、次の列で構成されてい \<cluster column reference> ます。  
  
-   **$Cluster** (クラスター名を表します)  
  
-   **$Distance**  
  
-   **$Probability**  
  
## <a name="examples"></a>例  
 次の例では、単一クエリの自転車の購入者列の予測された状態を返します。 このクエリでは、 **PredictHistogram** 関数を使用して取得された調整済みの確率に基づいて、自転車購入者属性の上位2つの最も可能性の高い状態が返されます。  
  
```  
SELECT  
  [TM Decision Tree].[Bike Buyer],  
  TopCount(PredictHistogram([Bike Buyer]),$AdjustedProbability,3)  
From  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>参照  
 [DMX&#41;のクラスター &#40;](../dmx/cluster-dmx.md)   
 [ClusterProbability &#40;DMX&#41;](../dmx/clusterprobability-dmx.md)   
 [DMX&#41;&#40;PredictAdjustedProbability ](../dmx/predictadjustedprobability-dmx.md)   
 [&#40;DMX&#41;の PredictProbability ](../dmx/predictprobability-dmx.md)   
 [&#40;DMX&#41;の PredictStdev ](../dmx/predictstdev-dmx.md)   
 [&#40;DMX&#41;の PredictSupport ](../dmx/predictsupport-dmx.md)   
 [&#40;DMX&#41;の PredictVariance ](../dmx/predictvariance-dmx.md)   
 [データマイニングアルゴリズム &#40;Analysis Services-データマイニング&#41;](/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [DMX&#41; 関数リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41;&#40;関数 ](../dmx/functions-dmx.md)   
 [DMX&#41;&#40;一般的な予測関数 ](../dmx/general-prediction-functions-dmx.md)  
  
