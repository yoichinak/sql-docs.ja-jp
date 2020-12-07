---
description: Predict (DMX)
title: Predict (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4f53f331b078fce4f02e548a83a145dce8ba6a91
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426204"
---
# <a name="predict-dmx"></a>Predict (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  **Predict**関数は、指定された列の予測値 (値のセット) を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Predict(<scalar column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
Predict(<table column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
```  
  
## <a name="applies-to"></a>適用対象  
 スカラー列参照またはテーブル列参照のいずれかです。  
  
## <a name="return-type"></a>戻り値の型  
 \<scalar column reference>  
  
 or  
  
 \<table column reference>  
  
 戻り値の型は、この関数が適用される列の型によって異なります。  
  
> [!NOTE]  
>  包含、排他、INPUT_ONLY、INCLUDE_STATISTICS はテーブル列参照にのみ適用され、EXCLUDE_NULL と INCLUDE_NULL はスカラー列参照にのみ適用されます。  
  
## <a name="remarks"></a>解説  
 オプションには、EXCLUDE_NULL (既定)、INCLUDE_NULL、INCLUSIVE、EXCLUSIVE (既定)、INPUT_ONLY、および INCLUDE_STATISTICS が含まれています。  
  
> [!NOTE]  
>  タイムシリーズモデルの場合、Predict 関数では INCLUDE_STATISTICS がサポートされません。  
  
 INCLUDE_NODE_ID パラメーターを指定すると、結果の $NODEID 列が返されます。 NODE_ID は、特定のケースに対して予測が実行されるコンテンツノードです。 テーブルの列に対して Predict を使用する場合、このパラメーターは省略可能です。  
  
 *N*パラメーターは、テーブル列に適用されます。 予測の種類に基づいて返される行の数を設定します。 基になる列が sequence の場合は、 **PredictSequence** 関数を呼び出します。 基になる列が時系列の場合は、 **PredictTimeSeries** 関数を呼び出します。 予測の結合型の場合は、 **PredictAssociation** 関数を呼び出します。  
  
 **Predict**関数では、ポリモーフィズムがサポートされています。  
  
 使用される頻度の高い代替省略形は次のとおりです。  
  
-   [性別] は、 **Predict**([性別], EXCLUDE_NULL) の代替手段です。  
  
-   [Products 購入] は、 **予測**([products 購入]、EXCLUDE_NULL、排他) の代替手段です。  
  
    > [!NOTE]  
    >  この関数の戻り値の型は、それ自体が列参照と見なされます。 つまり、 **predict** 関数は、列参照を引数として受け取る他の関数の引数として使用できます (ただし、 **predict** 関数自体は除きます)。  
  
 テーブル値列の予測に INCLUDE_STATISTICS を渡すと、列 **$Probability** と **$Support** が結果のテーブルに追加されます。 これらの列は、入れ子になった入れ子になったテーブルレコードに存在する確率を示します。  
  
## <a name="examples"></a>例  
 次の例では、Predict 関数を使用して、一緒に販売される可能性が最も高い Adventure Works データベースの4つの製品を返します。 関数は、アソシエーションルールマイニングモデルに対して予測を行うため、前に説明したように **PredictAssociation** 関数を自動的に使用します。  
  
```  
SELECT  
    Predict([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,4)  
FROM     [Association]  
```  
  
 サンプルの結果 :  
  
 このクエリは、1つの列を含む1行のデータを返し `Expression` ますが、その列には次の入れ子になったテーブルが含まれています。  
  
|モデル|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291283016331743|0.252695851192499|  
|Water Bottle|2866|0.192620471805901|0.175205052318795|  
|Patch Kit|2113|0.142012232004839|0.132389356196586|  
|Mountain Tire Tube|1992|0.133879965051415|0.125304947722259|  
  
## <a name="see-also"></a>参照  
 [DMX&#41; 関数リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41;&#40;関数 ](../dmx/functions-dmx.md)   
 [DMX&#41;&#40;一般的な予測関数 ](../dmx/general-prediction-functions-dmx.md)  
  
  
