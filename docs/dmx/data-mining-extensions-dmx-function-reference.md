---
description: データマイニング拡張機能 (DMX) 関数リファレンス
title: データマイニング拡張機能 (DMX) 関数リファレンス |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3066c971a434f1fab0dd2963003d53e37585983a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88414148"
---
# <a name="data-mining-extensions-dmx-function-reference"></a>データマイニング拡張機能 (DMX) 関数リファレンス
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] は、データ マイニング拡張機能 (DMX) 言語のいくつかの関数をサポートしています。 関数では、予測クエリの結果が拡張され、予測に関する詳細情報が含まれます。 また、関数を使用すると、予測の結果を返す方法をより細かく制御できます。 次の表に、DMX での関数の使用方法を理解するのに役立つリソースへのリンクを示します。  
  
|機能|説明|  
|--------------|-----------------|  
|[DMX&#41;&#40;一般的な予測関数 ](../dmx/general-prediction-functions-dmx.md)|すべてのモデルの種類で使用できる関数を一覧表示し、特定の種類のマイニングモデルに対してクエリを実行する方法に関する詳細情報へのリンクを示します。|  
|[構造と DMX 予測クエリの使用](../dmx/structure-and-usage-of-dmx-prediction-queries.md)|DMX を使用して予測クエリを作成する方法の概要について説明します。|  
|[DMX&#41;&#40;下数 ](../dmx/bottomcount-dmx.md)|順位付け式に基づいてデータを昇順に並べ替え、最下位行から指定数を含むテーブルを返します。|  
  
 次の表は、DMX がサポートする関数の一覧を示しています。  
  
|機能|説明|  
|--------------|-----------------|  
|[DMX&#41;&#40;下数 ](../dmx/bottomcount-dmx.md)|順位付け式に基づいて昇順に並べ替えた、テーブル式の最後の n 項目行を含むテーブルを返します。|  
|[DMX&#41;&#40;の割合 ](../dmx/bottompercent-dmx.md)|順位付け式に基づいて、指定された割合の式に一致する最下位行の最小数を含むテーブルを返します。|  
|[DMX&#41;&#40;BottomSum ](../dmx/bottomsum-dmx.md)|順位付け式に基づいて、指定された sum 式に一致する最下位行の最小数を含むテーブルを返します。|  
|[Cluster &#40;DMX&#41;](../dmx/cluster-dmx.md)|入力ケースを含んでいる可能性が最も高いクラスターを返します。|  
|[ClusterProbability &#40;DMX&#41;](../dmx/clusterprobability-dmx.md)|入力ケースがクラスターに所属する確率を返します。|  
|[DMX&#41;&#40;存在 ](../dmx/exists-dmx.md)|指定した SELECT ステートメントから返された結果セットに少なくとも 1 行が含まれる場合は true を返します。|  
|[IsDescendant &#40;DMX&#41;](../dmx/isdescendant-dmx.md)|現在のノードが、指定されたノードから下降しているかどうかを示します。|  
|[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)|指定したノードにケースが含まれているかどうかを示します。|  
|[DMX&#41;&#40;IsTestCase ](../dmx/istestcase-dmx.md)|ケースがテストケースのセットに属しているかどうかを示します。|  
|[DMX&#41;&#40;IsTrainingCase ](../dmx/istrainingcase-dmx.md)|ケースがトレーニングケースのセットに属しているかどうかを示します。|  
|[Lag &#40;DMX&#41;](../dmx/lag-dmx.md)|現在のケースの日付とデータの最後の日付の間のタイムスライスを返します。|  
|[Predict &#40;DMX&#41;](../dmx/predict-dmx.md)|指定された列に対して予測を実行します。|  
|[PredictAdjustedProbability &#40;DMX&#41;](../dmx/predictadjustedprobability-dmx.md)|指定された予測可能列の調整済みの確率を返します。|  
|[PredictAssociation &#40;DMX&#41;](../dmx/predictassociation-dmx.md)|列の結合メンバーシップを予測します。|  
|[PredictCaseLikelihood &#40;DMX&#41;](../dmx/predictcaselikelihood-dmx.md)|入力したケースが既存のモデル内に収まる確率を返します。 この関数は、クラスターモデルでのみ使用できます。|  
|[PredictHistogram &#40;DMX&#41;](../dmx/predicthistogram-dmx.md)|指定された列のヒストグラムを表すテーブルを返します。|  
|[PredictNodeId &#40;DMX&#41;](../dmx/predictnodeid-dmx.md)|選択したケースの NodeID を返します。|  
|[PredictProbability &#40;DMX&#41;](../dmx/predictprobability-dmx.md)|指定された列の確率を返します。|  
|[PredictSequence (DMX)](../dmx/predictsequence-dmx.md)|シーケンス内の次の値を予測します。|  
|[PredictStdev &#40;DMX&#41;](../dmx/predictstdev-dmx.md)|指定された列の標準偏差値を取得します。|  
|[PredictSupport &#40;DMX&#41;](../dmx/predictsupport-dmx.md)|列のサポート値を返します。|  
|[PredictTimeSeries &#40;DMX&#41;](../dmx/predicttimeseries-dmx.md)|時系列の将来の値を予測します。|  
|[PredictVariance &#40;DMX&#41;](../dmx/predictvariance-dmx.md)|指定された列の分散値を返します。|  
|[DMX&#41;&#40;RangeMax ](../dmx/rangemax-dmx.md)|指定された分離列に対して検出された予測バケットの上限値を返します。|  
|[&#40;DMX&#41;の RangeMid ](../dmx/rangemid-dmx.md)|指定された分離列に対して検出された予測バケットの中間値を返します。|  
|[DMX&#41;&#40;RangeMin ](../dmx/rangemin-dmx.md)|指定された分離列に対して検出された予測バケットの下限値を返します。|  
|[DMX&#41;&#40;StructureColumn ](../dmx/structurecolumn-dmx.md)|指定されたテーブルマイニング構造列の値を返します。|  
|[DMX&#41;&#40;TopCount ](../dmx/topcount-dmx.md)|指定された最上位行数を含むテーブルを、順位付け式に基づいて降順で返します。|  
|[DMX&#41;&#40;TopPercent ](../dmx/toppercent-dmx.md)|順位付け式に基づいて、指定された割合の式に一致する最上位行の最小数を含むテーブルを返します。|  
|[DMX&#41;&#40;TopSum ](../dmx/topsum-dmx.md)|順位付け式に基づいてデータを降順に並べ替え、最上位行から指定された合計式を満たすまでの最小行数を含むテーブルを返します。|  
  
## <a name="see-also"></a>参照  
 [DMX&#41; オペレーターリファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [DMX&#41; ステートメントリファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-statements.md)   
 [DMX&#41; 構文表記規則を &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [DMX&#41; の構文要素を &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [DMX&#41;&#40;一般的な予測関数 ](../dmx/general-prediction-functions-dmx.md)   
 [構造と DMX 予測クエリの使用](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX 選択ステートメントについて](../dmx/understanding-the-dmx-select-statement.md)  
  
  
