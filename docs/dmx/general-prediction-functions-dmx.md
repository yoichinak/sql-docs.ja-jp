---
description: 一般的な予測関数 (DMX)
title: 一般的な予測関数 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 22fe85d0e51de59d0b25b6a3eb89d29edf655ee4
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726185"
---
# <a name="general-prediction-functions-dmx"></a>一般的な予測関数 (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  データマイニング拡張機能 (DMX) で **select** ステートメントを使用すると、さまざまな種類のクエリを作成できます。 クエリを使用すると、マイニング モデル自体の情報を返したり、新しい予測を作成したり、新しいデータを使用してトレーニングしてモデルを変更したりできます。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] には、クエリで返される情報の種類を制御するさまざまな特殊な関数が用意されています。 これらの関数を DMX クエリに追加すると、データの統計または列を取得できます。 ただし、各クエリの種類とモデルの種類では、特定の関数しかサポートされていません。  
  
## <a name="common-functions"></a>[共通の関数]  
 関数を使用すると、マイニングモデルから返される結果を拡張できます。 テーブル式を返す **SELECT** ステートメントには、次の関数を使用できます。  

:::row:::
    :::column:::
        [DMX&#41;&#40;下数 ](../dmx/bottomcount-dmx.md)  
        [DMX&#41;&#40;の割合 ](../dmx/bottompercent-dmx.md)  
        [Predict &#40;DMX&#41;](../dmx/predict-dmx.md)  
        [DMX&#41;&#40;RangeMax ](../dmx/rangemax-dmx.md)  
        [&#40;DMX&#41;の RangeMid ](../dmx/rangemid-dmx.md)  
    :::column-end:::
    :::column:::
        [DMX&#41;&#40;RangeMin ](../dmx/rangemin-dmx.md)  
        [DMX&#41;&#40;TopCount ](../dmx/topcount-dmx.md)  
        [DMX&#41;&#40;TopPercent ](../dmx/toppercent-dmx.md)  
        [DMX&#41;&#40;TopSum ](../dmx/topsum-dmx.md)  
    :::column-end:::
:::row-end:::

 また、ほぼすべてのモデルの種類で次の関数がサポートされています。  
  
-   [DMX&#41;&#40;存在 ](../dmx/exists-dmx.md)  
  
-   [IsDescendant &#40;DMX&#41;](../dmx/isdescendant-dmx.md)  
  
-   [DMX&#41;&#40;IsTestCase ](../dmx/istestcase-dmx.md)  
  
-   [DMX&#41;&#40;IsTrainingCase ](../dmx/istrainingcase-dmx.md)  
  
-   [Predict &#40;DMX&#41;](../dmx/predict-dmx.md)  
  
-   [DMX&#41;&#40;RangeMax ](../dmx/rangemax-dmx.md)  
  
-   [&#40;DMX&#41;の RangeMid ](../dmx/rangemid-dmx.md)  
  
-   [DMX&#41;&#40;RangeMin ](../dmx/rangemin-dmx.md)  
  
-   [DMX&#41;&#40;StructureColumn ](../dmx/structurecolumn-dmx.md)  
  
 個々のアルゴリズムでは、追加の関数がサポートされる場合があります。 各モデルの種類でサポートされている関数の一覧については、「 [データマイニングクエリ](/analysis-services/data-mining/data-mining-queries)」を参照してください。  
  
## <a name="functions-specific-to-select-syntax"></a>SELECT 構文に固有の関数  
 次の表に、 **SELECT** ステートメントの種類ごとに使用できる関数を示します。  
  
 DMX の関数に関する一般的な情報については、「 [データマイニング拡張機能 &#40;dmx&#41; 関数リファレンス](../dmx/data-mining-extensions-dmx-function-reference.md)」を参照してください。  
  
|クエリの種類|サポートされる関数|解説|  
|----------------|-------------------------|-------------|  
|[SELECT DISTINCT FROM \<model>](../dmx/select-distinct-from-model-dmx.md)|[DMX&#41;&#40;RangeMin ](../dmx/rangemin-dmx.md)<br /><br /> [&#40;DMX&#41;の RangeMid ](../dmx/rangemid-dmx.md)<br /><br /> [DMX&#41;&#40;RangeMax ](../dmx/rangemax-dmx.md)|これらの関数を使用すると、列が連続しているか分離されているかどうかにかかわらず、数値データ型を含む任意の列に対して最大値、最小値、および平均値を指定できます。|  
|[SELECT FROM \<model>.CONTENT](../dmx/select-from-model-content-dmx.md)<br /><br /> or<br /><br /> [SELECT FROM \<model>.DIMENSION_CONTENT](../dmx/select-from-model-dimension-content-dmx.md)|[IsDescendant &#40;DMX&#41;](../dmx/isdescendant-dmx.md)|この関数は、モデル内の指定されたノードの子ノードを取得します。また、この関数を使用すると、たとえば、マイニング モデル コンテンツのノードを繰り返し処理できます。 マイニングモデルコンテンツ内のノードの配置は、モデルの種類によって異なります。 各マイニングモデルの種類の構造については、「 [マイニングモデルコンテンツ &#40;Analysis Services-データマイニング&#41;](/analysis-services/data-mining/mining-model-content-analysis-services-data-mining)」を参照してください。<br /><br /> マイニングモデルコンテンツをディメンションとして保存した場合は、属性階層のクエリに使用できる他の多次元式 (MDX) 関数を使用することもできます。|  
|[SELECT FROM \<model>.CASES](../dmx/select-from-model-cases-dmx.md)|[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)<br /><br /> [ClientSettingsGeneralFlag クラス](../relational-databases/wmi-provider-configuration-classes/clientsettingsgeneralflag-class/clientsettingsgeneralflag-class.md)<br /><br /> [DMX&#41;&#40;IsTrainingCase ](../dmx/istrainingcase-dmx.md)<br /><br /> [DMX&#41;&#40;IsTestCase ](../dmx/istestcase-dmx.md)|Lag 関数は、タイムシリーズモデルでのみサポートされています。<br /><br /> IsTestCase 関数は、テストデータセットを作成するために、提示オプションを使用して作成された構造に基づくモデルでサポートされています。 モデルが、提示されたテストセットの構造に基づいていない場合、すべてのケースがトレーニングケースと見なされます。|  
|[SELECT FROM \<model>.SAMPLE_CASES](../dmx/select-from-model-sample-cases-dmx.md)|[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)|このコンテキストでは、IsInNode 関数は、一連の理想的なサンプルケースに属するケースを返します。|  
|[開始] を選択し \<model> ます。PMML|適用不可。 代わりに、XML クエリ関数を使用してください。|PMML 表現は、次のモデルの種類のみでサポートされます。<br /><br /> [!INCLUDE[msCoName](../includes/msconame-md.md)] デシジョンツリー<br /><br /> [!INCLUDE[msCoName](../includes/msconame-md.md)] クラスター|  
|[SELECT FROM \<model> PREDICTION JOIN](../dmx/select-from-model-prediction-join-dmx.md)|モデルの構築に使用するアルゴリズムに固有の予測関数。|各種類のモデルの予測関数の一覧については、「 [データマイニングクエリ](/analysis-services/data-mining/data-mining-queries)」を参照してください。|  
|[SELECT FROM \<model>](../dmx/select-from-model-dmx.md)|モデルの構築に使用するアルゴリズムに固有の予測関数。|各種類のモデルの予測関数の一覧については、「 [データマイニングクエリ](/analysis-services/data-mining/data-mining-queries)」を参照してください。|  
  
## <a name="see-also"></a>参照  
 [DMX&#41; リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-reference.md)   
 [DMX&#41; 関数リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41; オペレーターリファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [DMX&#41; ステートメントリファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-statements.md)   
 [DMX&#41; 構文表記規則を &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [DMX&#41; の構文要素を &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [構造と DMX 予測クエリの使用](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX 選択ステートメントについて](../dmx/understanding-the-dmx-select-statement.md)  
  
