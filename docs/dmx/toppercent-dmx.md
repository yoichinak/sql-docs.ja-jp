---
description: TopPercent (DMX)
title: TopPercent (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f1193e43a00fc4c20487a92e8df3a9f705fa4490
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726093"
---
# <a name="toppercent-dmx"></a>TopPercent (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  **TopPercent**関数は、累積合計が少なくとも指定した割合になるテーブルの最上位行を、順位を下げる順序で返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
TopPercent(<table expression>, <rank expression>, <percent>)  
```  
  
## <a name="applies-to"></a>適用対象  
 などのテーブルを返す式、 \<table column reference> またはテーブルを返す関数。  
  
## <a name="return-type"></a>戻り値の型  
 \<table expression>  
  
## <a name="remarks"></a>解説  
 **TopPercent**関数は、各行の引数の評価値に基づいて、順位の降順で最上位の行を返し \<rank expression> ます。これは、値の合計 \<rank expression> が引数で指定された指定の割合以上になるようにするためです \<percent> 。 **TopPercent** は、指定された割合の値を維持しながら、可能な限り最小の要素数を返します。  
  
## <a name="examples"></a>例  
 次の例では、「 [基本的なデータマイニングチュートリアル](/previous-versions/sql/sql-server-2016/ms167167(v=sql.130))」を使用して作成したアソシエーションモデルに対して予測クエリを作成します。  
  
 TopPercent の動作を理解するために、入れ子になったテーブルのみを返す予測クエリを最初に実行すると便利な場合があります。  
  
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
  
 TopPercent 関数は、このクエリの結果を受け取り、最大値を持つ行を指定された割合に合計して返します。  
  
```  
SELECT   
TopPercent  
    (  
    Predict ([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $SUPPORT,  
    50)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 TopPercent 関数の最初の引数は、テーブル列の名前です。 この例では、Predict 関数を呼び出し、INCLUDE_STATISTICS 引数を使用して、入れ子になったテーブルが返されます。  
  
 TopPercent 関数の2番目の引数は、結果の並べ替えに使用する入れ子になったテーブルの列です。 この例では、INCLUDE_STATISTICS オプションを使用して、列 $SUPPORT、$PROBABILTY、および $ADJUSTED 確率を返します。 この例では $SUPPORT を使用します。サポート値は小数部分ではないため、検証が容易になるためです。  
  
 TopPercent 関数の3番目の引数は、パーセントを double として指定します。 合計サポートの50% に合計する上位製品の行を取得するには、「50」と入力します。  
  
 結果の例:  
  
|モデル|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.29...|0.25...|  
|Water Bottle|2866|0.19...|0.17...|  
|Patch kit|2113|0.14...|0.13...|  
|Mountain Tire Tube|1992|0.133...|0.12...|  
  
 **メモ** この例は、TopPercent の使用方法を示すことだけを目的としています。 データセットのサイズによっては、このクエリの実行に時間がかかることがあります。  
  
> [!WARNING]  
>  TOPPERCENT との MDX 関数では、割合の計算に使用される値に負の数値が含まれている場合、予期しない結果が発生する可能性があります。 この動作は、DMX 関数には影響しません。 詳細については、「 [&#41;&#40;MDX の割合 ](../mdx/bottompercent-mdx.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [DMX&#41; 関数リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41;&#40;関数 ](../dmx/functions-dmx.md)   
 [DMX&#41;&#40;一般的な予測関数 ](../dmx/general-prediction-functions-dmx.md)  
  
