---
description: TopCount (DMX)
title: TopCount (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 23a9a1594c31bda040a22ad3914af8b8e7d3603f
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726085"
---
# <a name="topcount-dmx"></a>TopCount (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  式によって指定された順位の降順で、指定された数の最上位行を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
TopCount(<table expression>, <rank expression>, <count>)  
```  
  
## <a name="applies-to"></a>適用対象  
 などのテーブルを返す式、 \<table column reference> またはテーブルを返す関数。  
  
## <a name="return-type"></a>戻り値の型  
 \<table expression>  
  
## <a name="remarks"></a>解説  
 引数によって指定された値によって、 \<rank expression> 引数に指定された行の順位の降順が決定され、 \<table expression> 引数に指定されている最上位の行の数 \<count> が返されます。  
  
 TopCount 関数は、最初に、結合された予測を有効にするために導入されており、一般的には、 **SELECT TOP** 句と **ORDER BY** 句を含むステートメントと同じ結果を生成します。 予測の数の指定をサポートする **Predict (DMX)** 関数を使用すると、結合された予測のパフォーマンスが向上します。  
  
 ただし、TopCount を使用する必要がある場合もあります。 たとえば、DMX は、サブ select ステートメントの **TOP** 修飾子をサポートしていません。 また、 [PredictHistogram &#40;DMX&#41;](../dmx/predicthistogram-dmx.md) 関数は、 **TOP**の追加をサポートしていません。  
  
## <a name="examples"></a>例  
 次の例は、「 [基本的なデータマイニングチュートリアル](/previous-versions/sql/sql-server-2016/ms167167(v=sql.130))」で作成したアソシエーションモデルに対する予測クエリです。 クエリは同じ結果を返しますが、最初の例では TopCount を使用し、2番目の例では Predict 関数を使用します。  
  
 TopCount の動作を理解するために、入れ子になったテーブルのみを返す予測クエリを最初に実行すると便利な場合があります。  
  
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
  
 TopCount 関数は、このクエリの結果を受け取り、指定された数の最小値の行を返します。  
  
```  
SELECT   
TopCount  
    (  
    Predict ([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $SUPPORT,  
    3)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 TopCount 関数の最初の引数は、テーブル列の名前です。 この例では、Predict 関数を呼び出し、INCLUDE_STATISTICS 引数を使用して、入れ子になったテーブルが返されます。  
  
 TopCount 関数の2番目の引数は、結果の並べ替えに使用する入れ子になったテーブルの列です。 この例では、INCLUDE_STATISTICS オプションを使用して、列 $SUPPORT、$PROBABILTY、および $ADJUSTED 確率を返します。 この例では、$SUPPORT を使用して結果を順位付けします。  
  
 3番目の引数、TopCount 関数は、返される行の数を整数として指定します。 $SUPPORT 順に並べ替えられた上位3つの製品を取得するには、「3」と入力します。  
  
 結果の例:  
  
|モデル|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.29...|0.25...|  
|Water Bottle|2866|0.19...|0.17...|  
|Patch kit|2113|0.14...|0.13...|  
  
 ただし、この種類のクエリは、実稼働設定のパフォーマンスに影響を与える可能性があります。 これは、クエリがアルゴリズムからすべての予測のセットを返し、これらの予測を並べ替え、上位3を返すためです。  
  
 次の例は、同じ結果を返すが実行時間が大幅に短縮される代替ステートメントを示しています。 この例では、TopCount を、引数として複数の予測を受け取る Predict 関数に置き換えます。 また、この例では、 **$SUPPORT** キーワードを使用して、入れ子になったテーブル列を直接取得します。  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3, $SUPPORT)  
```  
  
 結果には、サポート値によって並べ替えられた上位3件の予測が含まれます。 $SUPPORT を $PROBABILITY または $ADJUSTED_PROBABILITY に置き換えると、確率または調整済みの確率で順位付けされた予測を取得できます。 詳細については、「 **Predict (DMX)**」を参照してください。  
  
## <a name="see-also"></a>参照  
 [DMX&#41;&#40;関数 ](../dmx/functions-dmx.md)   
 [DMX&#41;&#40;一般的な予測関数 ](../dmx/general-prediction-functions-dmx.md)   
 [DMX&#41;&#40;下数 ](../dmx/bottomcount-dmx.md)   
 [DMX&#41;&#40;TopPercent ](../dmx/toppercent-dmx.md)   
 [DMX&#41;&#40;TopSum ](../dmx/topsum-dmx.md)  
  
