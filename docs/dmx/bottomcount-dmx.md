---
description: 下端のカウント (DMX)
title: 下端のカウント (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 24a19fc748da4ef521bb9781941911efb08e0132
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727750"
---
# <a name="bottomcount-dmx"></a>下端のカウント (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  式によって指定されたランクの増加順に、指定された最下位の行数を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
BottomCount(<table expression>, <rank expression>, <count>)  
```  
  
## <a name="applies-to"></a>適用対象  
 などのテーブルを返す式、 \<table column reference> またはテーブルを返す関数。  
  
## <a name="return-type"></a>戻り値の型  
 \<table expression>  
  
## <a name="remarks"></a>解説  
 引数によって指定された値によって、 \<rank expression> 引数に指定された行のランクの増加順序が決定され、 \<table expression> 引数に指定されている最下位行の数 \<count> が返されます。  
  
## <a name="examples"></a>例  
 次の例では、「 [基本的なデータマイニングチュートリアル](/previous-versions/sql/sql-server-2016/ms167167(v=sql.130))」を使用して作成したアソシエーションモデルに対して予測クエリを作成します。  
  
 下位カウントのしくみを理解するために、入れ子になったテーブルのみを返す予測クエリを最初に実行すると便利な場合があります。  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 10)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
> [!NOTE]  
>  この例では、入力として指定された値に単一引用符が含まれているため、その前に別の単一引用符を付けてエスケープする必要があります。 エスケープ文字を挿入するための構文がわからない場合は、予測クエリビルダーを使用してクエリを作成できます。 ドロップダウンリストから値を選択すると、必要なエスケープ文字が挿入されます。 詳細については、「 [データマイニングデザイナーでの単一クエリの作成](/analysis-services/data-mining/create-a-singleton-query-in-the-data-mining-designer)」を参照してください。  
  
 結果の例:  
  
|モデル|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291283016|0.252695851|  
|Water Bottle|2866|0.192620472|0.175205052|  
|Patch kit|2113|0.142012232|0.132389356|  
|Mountain Tire Tube|1992|0.133879965|0.125304948|  
|Mountain-200|1755|0.117951475|0.111260823|  
|Road Tire Tube|1588|0.106727603|0.101229538|  
|Cycling Cap|1473|0.098998589|0.094256014|  
|Fender Set - Mountain|1415|0.095100477|0.090718432|  
|Mountain Bottle Cage|1367|0.091874454|0.087780332|  
|道路ボトルケージ|1195|0.080314537|0.077173962|  
  
 下端のカウント関数は、このクエリの結果を取得し、指定した割合に合計する最小値の行を返します。  
  
```  
SELECT   
BottomCount  
    (  
    Predict ([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $SUPPORT,  
    3)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 最優先カウント関数の最初の引数は、テーブル列の名前です。 この例では、Predict 関数を呼び出し、INCLUDE_STATISTICS 引数を使用して、入れ子になったテーブルが返されます。  
  
 下方向カウント関数の2番目の引数は、結果の並べ替えに使用する入れ子になったテーブルの列です。 この例では、INCLUDE_STATISTICS オプションを使用して、列 $SUPPORT、$PROBABILTY、および $ADJUSTED 確率を返します。 この例では $SUPPORT を使用します。サポート値は小数部分ではないため、検証が容易になるためです。  
  
 下の3番目の引数は、行の数を指定します。 $SUPPORT で順位が付けられた、最下位 3 つの行を取得するには、「3」と入力します。  
  
 結果の例:  
  
|モデル|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|道路ボトルケージ|1195|0.080314537|0.077173962|  
|Mountain Bottle Cage|1367|0.091874454|0.087780332|  
|Fender Set - Mountain|1415|0.095100477|0.090718432|  
  
 **メモ** この例は、下端の使用方法を示すためだけに提供されています。 データセットのサイズによっては、このクエリの実行に時間がかかることがあります。  
  
## <a name="see-also"></a>参照  
 [DMX&#41;&#40;関数 ](../dmx/functions-dmx.md)   
 [DMX&#41;&#40;一般的な予測関数 ](../dmx/general-prediction-functions-dmx.md)   
 [DMX&#41;&#40;の割合 ](../dmx/bottompercent-dmx.md)   
 [DMX&#41;&#40;BottomSum ](../dmx/bottomsum-dmx.md)   
 [DMX&#41;&#40;TopCount ](../dmx/topcount-dmx.md)  
  
