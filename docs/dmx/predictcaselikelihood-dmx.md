---
description: PredictCaseLikelihood 度 (DMX)
title: PredictCaseLikelihood 度 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a08ec4809b281205386abad429afe339e0dbb1d1
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727712"
---
# <a name="predictcaselikelihood-dmx"></a>PredictCaseLikelihood 度 (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  この関数は、入力したケースが既存のモデルに適合する確率を返します。 クラスターモデルでのみ使用されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
PredictCaseLikelihood([NORMALIZED|NONNORMALIZED])  
```  
  
## <a name="arguments"></a>引数  
 NORMALIZED  
 戻り値は、モデル内のケースの確率をモデルのないケースの確率で除算した結果を格納します。  
  
 NONNORMALIZED  
 戻り値は、ケースの未加工の確率、つまりケース属性の確率の積を格納します。  
  
## <a name="applies-to"></a>適用対象  
 [!INCLUDE[msCoName](../includes/msconame-md.md)]クラスタリング [!INCLUDE[msCoName](../includes/msconame-md.md)] アルゴリズムとシーケンスクラスターアルゴリズムを使用して作成されたモデル。  
  
## <a name="return-type"></a>戻り値の型  
 0から1までの倍精度浮動小数点数。 1に近い数値は、このモデルでケースが発生する確率が高いことを示します。 値が 0 に近いほど、このモデルでケースが発生する確率が低くなります。  
  
## <a name="remarks"></a>解説  
 既定では、 **Predictcaselikelihood** 関数の結果は正規化されます。 通常、正規化された値は、ケース内の属性の数が増え、任意の 2 つのケースの未加工の確率の差が小さくなるほど、有用性が増します。  
  
 次の式は、x と y を指定して正規化された値を計算するために使用します。  
  
-   x = クラスタリング モデルに基づいたケースの確率値  
  
-   y = トレーニングケースのカウントに基づいてケースの対数確率として計算された、大文字と小文字の区別の確率  
  
-   Z = Exp (log (x)-Log (Y))  
  
 正規化 = (z/(1 + z))  
  
## <a name="examples"></a>例  
 次の例では、DW データベースに基づくクラスターモデル内で、指定したケースが発生する確率を返し [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] ます。  
  
```  
SELECT  
  PredictCaseLikelihood() AS Default_Likelihood,  
  PredictCaseLikelihood(NORMALIZED) AS Normalized_Likelihood,  
  PredictCaseLikelihood(NONNORMALIZED) AS Raw_Likelihood,  
FROM  
  [TM Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
 期待される結果:  
  
|Default_Likelihood|Normalized_Likelihood|Raw_Likelihood|  
|-------------------------|----------------------------|---------------------|  
|6.30672792729321 e-08|6.30672792729321 e-08|9.5824454056846 e-48|  
  
 これらの結果の違いは、正規化の影響を示します。 **Caselikelihood**の生の値は、ケースの確率が約20% であることを示します。しかし、結果を正規化すると、ケースの確率が非常に低いことが明らかになります。  
  
## <a name="see-also"></a>参照  
 [データマイニングアルゴリズム &#40;Analysis Services-データマイニング&#41;](/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [DMX&#41; 関数リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41;&#40;関数 ](../dmx/functions-dmx.md)   
 [DMX&#41;&#40;一般的な予測関数 ](../dmx/general-prediction-functions-dmx.md)  
  
