---
description: PredictTimeSeries (DMX)
title: PredictTimeSeries (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 02b85cc4197b0ffafef7a83566e4041a7d290548
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727675"
---
# <a name="predicttimeseries-dmx"></a>PredictTimeSeries (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  予測される時系列データの将来値を返します。 時系列データは連続していて、入れ子になったテーブルまたはケーステーブルに格納できます。 **PredictTimeSeries**関数は、常に入れ子になったテーブルを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
PredictTimeSeries(<table column reference>)  
PredictTimeSeries(<table column reference>, n)  
PredictTimeSeries(<table column reference>, n-start, n-end)  
PredictTimeSeries(<scalar column reference>)  
PredictTimeSeries(<scalar column reference>, n)  
PredictTimeSeries(<scalar column reference>, n-start, n-end)  
PredictTimeSeries(<table column reference>, n, REPLACE_MODEL_CASES | EXTEND_MODEL_CASES) PREDICTION JOIN <source query>  
PredictTimeSeries(<table column reference>, n-start, n-end, REPLACE_MODEL_CASES | EXTEND_MODEL_CASES) PREDICTION JOIN <source query>  
PredictTimeSeries(<scalar column reference>, n, REPLACE_MODEL_CASES | EXTEND_MODEL_CASES) PREDICTION JOIN <source query>  
PredictTimeSeries(<scalar column reference>, n-start, n-end, REPLACE_MODEL_CASES | EXTEND_MODEL_CASES) PREDICTION JOIN <source query>  
```  
  
## <a name="arguments"></a>引数  
 *\<table column reference>*, *\<scalar column referenc>*  
 予測する列の名前を指定します。 列には、スカラーデータまたは表形式データを含めることができます。  
  
 *n*  
 予測する次のステップの数を指定します。 *N*に値が指定されていない場合の既定値は1です。  
  
 *n* を0にすることはできません。 少なくとも1つの予測を作成しない場合、関数はエラーを返します。  
  
 *n-開始、n 終了*  
 時系列ステップの範囲を指定します。  
  
 *n-start* は整数である必要があり、0にすることはできません。  
  
 *n-end* は、 *n 開始*より大きい整数でなければなりません。  
  
 *\<source query>*  
 予測の作成に使用される外部データを定義します。  
  
 REPLACE_MODEL_CASES |EXTEND_MODEL_CASES  
 新しいデータの処理方法を示します。  
  
 REPLACE_MODEL_CASES は、モデル内のデータポイントを新しいデータに置き換える必要があることを指定します。 ただし、予測は、既存のマイニングモデルのパターンに基づいています。  
  
 EXTEND_MODEL_CASES を指定すると、新しいデータが元のトレーニング データセットに追加されます。 将来の予測は、新しいデータを使い果たした後にのみ複合データセットに基づいて作成されます。  
  
 これらの引数は、PREDICTION JOIN ステートメントを使用して新しいデータを追加する場合にのみ使用できます。 予測結合クエリを使用し、引数を指定しない場合、既定値は EXTEND_MODEL_CASES になります。  
  
## <a name="return-type"></a>戻り値の型  
 \<*table expression*>。  
  
## <a name="remarks"></a>解説  
 [!INCLUDE[msCoName](../includes/msconame-md.md)]タイムシリーズアルゴリズムでは、予測結合ステートメントを使用して新しいデータを追加した場合、履歴予測はサポートされません。  
  
 予測結合では、予測プロセスは常に、元のトレーニングシリーズの最後の直後の時間ステップで開始されます。 これは、新しいデータを追加した場合でも当てはまります。 したがって、 *n* パラメーターと *n 開始* パラメーターの値には、0より大きい整数を指定する必要があります。  
  
> [!NOTE]  
>  新しいデータの長さは、予測の開始位置には影響しません。 そのため、新しいデータを追加して新しい予測を作成する場合は、予測の開始位置を新しいデータの長さより大きい値に設定するか、予測の終了位置を新しいデータの長さだけ拡張するようにします。  
  
## <a name="examples"></a>例  
 次の例では、既存のタイムシリーズモデルに対して予測を行う方法を示します。  
  
-   最初の例は、現在のモデルに基づいて、指定された数の予測を作成する方法を示しています。  
  
-   2番目の例では、REPLACE_MODEL_CASES パラメーターを使用して、指定したモデルのパターンを新しいデータセットに適用する方法を示します。  
  
-   3番目の例では、EXTEND_MODEL_CASES パラメーターを使用して、マイニングモデルを新しいデータで更新する方法を示します。  
  
 タイムシリーズモデルの使用方法の詳細については、「データマイニングチュートリアル」、「 [レッスン 2: 予測シナリオの構築」 (中級者向けデータマイニングチュートリアル &#40;&#41;](/previous-versions/sql/sql-server-2016/ms169846(v=sql.130)) と [時系列予測 DMX のチュートリアル](/previous-versions/sql/sql-server-2016/cc879270(v=sql.130))) を参照してください。  
  
> [!NOTE]  
>  モデルの結果は異なる場合があります。次の例の結果は、結果の形式を説明することのみを目的としています。  
  
### <a name="example-1-predicting-a-number-of-time-slices"></a>例 1: 複数のタイムスライスを予測する  
 次の例では、 **PredictTimeSeries** 関数を使用して、次の3回のステップの予測を返し、ヨーロッパと太平洋地域の M200 シリーズに結果を制限します。 この特定のモデルでは、予測可能な属性は Quantity であるため、 `[Quantity]` PredictTimeSeries 関数の最初の引数としてを使用する必要があります。  
  
```  
SELECT FLATTENED  
    [Forecasting].[Model Region],  
    PredictTimeSeries([Forecasting].[Quantity],3)AS t   
FROM  
    [Forecasting]  
WHERE [Model Region] = 'M200 Europe'  
OR [Model Region] = 'M200 Pacific'  
```  
  
 期待される結果:  
  
|モデル領域|$TIME|t. 数量|  
|------------------|-------------|----------------|  
|M200 ヨーロッパ|7/25/2008 12:00:00 AM|121|  
|M200 ヨーロッパ|8/25/2008 12:00:00 AM|142|  
|M200 ヨーロッパ|9/25/2008 12:00:00 AM|152|  
|M200 太平洋|7/25/2008 12:00:00 AM|46|  
|M200 太平洋|8/25/2008 12:00:00 AM|44|  
|M200 太平洋|9/25/2008 12:00:00 AM|42|  
  
 この例では、フラット化されたキーワードを使用して、結果を読みやすくしています。  FLATTENED キーワードを使用せずに、階層的な行セットを返す場合、このクエリでは 2 つの列が返されます。 1 つ目の列には [ModelRegion] の値、2 つ目の列には入れ子になったテーブルが含まれます。入れ子になったテーブルには、予測されているタイム スライスを示す $TIME と予測された値を含む Quantity という 2 つの列が含まれています。  
  
### <a name="example-2-adding-new-data-and-using-replace_model_cases"></a>例 2: 新しいデータを追加して REPLACE_MODEL_CASES を使用する  
 特定の地域のデータが間違っていることがわかっており、モデル内のパターンを使用するが、新しいデータに合わせて予測を調整する場合を考えてみます。 または、別のリージョンにより信頼性の高い傾向があり、最も信頼性の高いモデルを別のリージョンのデータに適用する場合もあります。  
  
 このようなシナリオでは、REPLACE_MODEL_CASES パラメーターを使用して、履歴データとして使用するデータの新しいセットを指定できます。 このようにすると、射影は指定されたモデルのパターンに基づいて行われますが、新しいデータポイントの終了からスムーズに進みます。 このシナリオの完全なチュートリアルについては、「 [&#40;中級者向けデータマイニングチュートリアル&#41;](/previous-versions/sql/sql-server-2016/cc879290(v=sql.130))」を参照してください。  
  
 次の PREDICTION JOIN クエリでは、データを置き換えて新しい予測を作成する構文を示します。 置換データの場合、この例では Amount 列と Quantity 列の値を取得し、それぞれを2で乗算しています。  
  
```  
SELECT [Forecasting].[Model Region],  
    PredictTimeSeries([Forecasting].[Quantity], 3, REPLACE_MODEL_CASES)   
FROM  
    [Forecasting]  
PREDICTION JOIN  
  OPENQUERY([Adventure Works DW Multidimensional 2012],  
    'SELECT [ModelRegion],   
    ([Quantity] * 2) as Quantity,  
    ([Amount] * 2) as Amount,  
      [ReportingDate]  
    FROM [dbo].vTimeSeries  
    WHERE ModelRegion = N''M200 Pacific''  
    ') AS t  
ON  
  [Forecasting].[Model Region] = t.[ Model Region] AND  
[Forecasting].[Reporting Date] = t.[ReportingDate] AND  
[Forecasting].[Quantity] = t.[Quantity] AND  
[Forecasting].[Amount] = t.[Amount]  
```  
  
 次の表は、予測の結果を比較したものです。  
  
 元の予測:  
  
|モデル領域|ReportingDate|Quantity|  
|-|-|-|  
|M200 太平洋|7/25/2008 12:00:00 AM|46|  
|M200 太平洋|8/25/2008 12:00:00 AM|44|  
|M200 太平洋|9/25/2008 12:00:00 AM|42|  
  
 更新された予測:  
  
|モデル領域|ReportingDate|Quantity|  
|-|-|-|  
|M200 太平洋|7/25/2008 12:00:00 AM|91|  
|M200 太平洋|8/25/2008 12:00:00 AM|89|  
|M200 太平洋|9/25/2008 12:00:00 AM|84|  
  
### <a name="example-3-adding-new-data-and-using-extend_model_cases"></a>例 3: 新しいデータを追加して EXTEND_MODEL_CASES を使用する  
 例3は、 *EXTEND_MODEL_CASES* オプションを使用して新しいデータを提供する方法を示しています。これは、既存のデータ系列の最後に追加されます。 既存のデータ ポイントを置き換えるのではなく、新しいデータをモデルに追加します。  
  
 次の例では、NATURAL PREDICTION JOIN の後の SELECT ステートメントで新しいデータを指定します。 この構文では複数行の新しい入力を指定できますが、それぞれの新しい入力行のタイムスタンプが一意である必要があります。  
  
```  
SELECT [Model Region],  
    PredictTimeSeries([Forecasting].[Quantity], 5, EXTEND_MODEL_CASES)   
FROM  
    [Forecasting]  
NATURAL PREDICTION JOIN  
    (SELECT  
        1 as [Reporting Date],  
        10 as [Quantity],  
        'M200 Europe' AS [Model Region]  
    UNION SELECT   
        2 as [Reporting Date],  
        15 as [Quantity],  
        'M200 Europe' AS [Model Region]  
) AS T  
WHERE ([Model Region] = 'M200 Europe'  
 OR [Model Region] = 'M200 Pacific')  
```  
  
 クエリでは *EXTEND_MODEL_CASES* オプションが使用されるため、では、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 予測に対して次の操作を実行します。  
  
-   2 か月分の新しいデータをモデルに追加して、トレーニング ケースの合計サイズを大きくします。  
  
-   前のケース データの末尾から予測を開始します。 したがって、最初の2つの予測は、モデルに追加した新しい実際の売上データを表します。  
  
-   新しく展開されたモデルに基づいて、残りの3つのタイムスライスの新しい予測を返します。  
  
 次の表は、例2のクエリの結果を示しています。 M200 ヨーロッパに返される最初の2つの値は、指定した新しい値とまったく同じであることに注意してください。 この動作は仕様であり、新しいデータの末尾から予測を開始するには、開始時刻と終了時刻のステップを指定する必要があります。  
  
 また、太平洋地域については、新しいデータを指定していません。 したがって、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] は、5 つすべてのタイム スライスの新しい予測を返します。  
  
 Quantity: M200 ヨーロッパ。 EXTEND_MODEL_CASES:  
  
|$TIME|Quantity|  
|-----------|--------------|  
|7/25/2008 0:00|10|  
|8/25/2008 0:00|15|  
|9/25/2008 0:00|72|  
|10/25/2008 0:00|69|  
|11/25/2008 0:00|68|  
  
 Quantity: M200 太平洋。 EXTEND_MODEL_CASES:  
  
|$TIME|Quantity|  
|-----------|--------------|  
|7/25/2008 0:00|46|  
|8/25/2008 0:00|44|  
|9/25/2008 0:00|42|  
|10/25/2008 0:00|42|  
|11/25/2008 0:00|38|  
  
## <a name="example-4-returning-statistics-in-a-time-series-prediction"></a>例 4: 時系列予測の統計を返す  
 **PredictTimeSeries**関数では、パラメーターとして*INCLUDE_STATISTICS*がサポートされていません。 ただし、次のクエリを使用して、時系列クエリの予測統計を返すことができます。 この方法は、テーブル列を入れ子にしているモデルにも使用できます。  
  
 この特定のモデルでは、予測可能な属性は Quantity であるため、 `[Quantity]` PredictTimeSeries 関数の最初の引数としてを使用する必要があります。 モデルで異なる予測可能な属性を使用している場合は、別の列名に置き換えることができます。  
  
```  
SELECT FLATTENED [Model Region],  
(SELECT   
     $Time,  
     [Quantity] as [PREDICTION],   
     PredictVariance([Quantity]) AS [VARIANCE],  
     PredictStdev([Quantity]) AS [STDEV]  
FROM  
      PredictTimeSeries([Quantity], 3) AS t  
) AS t  
FROM Forecasting  
WHERE [Model Region] = 'M200 Europe'  
OR [Model Region] = 'M200 North America'  
```  
  
 サンプルの結果 :  
  
|モデル領域|$TIME|t. 予測|t.VARIANCE|t. STDEV|  
|------------------|-------------|------------------|----------------|-------------|  
|M200 ヨーロッパ|7/25/2008 12:00:00 AM|121|11.6050581415597|3.40661975300439|  
|M200 ヨーロッパ|8/25/2008 12:00:00 AM|142|10.678201866621|3.26775180615374|  
|M200 ヨーロッパ|9/25/2008 12:00:00 AM|152|9.86897842568614|3.14149302493037|  
|M200 North America|7/25/2008 12:00:00 AM|163|1.20434529288162|1.20434529288162|  
|M200 North America|8/25/2008 12:00:00 AM|178|1.65031343900634|1.65031343900634|  
|M200 North America|9/25/2008 12:00:00 AM|156|1.68969399185442|1.68969399185442|  
  
> [!NOTE]  
>  この例では、FLATTENED キーワードを使用して、結果を表形式でわかりやすくしました。ただし、プロバイダーで階層的な行セットがサポートされている場合は、FLATTENED キーワードを省略できます。 フラット化されたキーワードを省略した場合、クエリは2つの列、データ系列を識別する値を含む最初の列、 `[Model Region]` および統計の入れ子になったテーブルを含む2番目の列を返します。  
  
## <a name="see-also"></a>参照  
 [DMX&#41; 関数リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [タイムシリーズモデルのクエリ例](/analysis-services/data-mining/time-series-model-query-examples)   
 [Predict &#40;DMX&#41;](../dmx/predict-dmx.md)  
  
