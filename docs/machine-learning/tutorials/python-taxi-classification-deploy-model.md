---
title: Python のチュートリアル:SQL ストアド プロシージャで予測を実行する
titleSuffix: SQL machine learning
description: 全 5 回からなるこのチュートリアル シリーズの第 5 回では、SQL 機械学習を利用し、T-SQL 関数を使用して SQL ストアド プロシージャに組み込まれた Python スクリプトを運用化します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/29/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||>=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 7c67f28d8cefb03edc2a12b97657d4054359727c
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2020
ms.locfileid: "88180335"
---
# <a name="python-tutorial-run-predictions-using-python-embedded-in-a-stored-procedure"></a>Python のチュートリアル:ストアド プロシージャに埋め込まれた Python を使用した予測の実行
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

全 5 回からなるこのチュートリアル シリーズの第 5 回では、前回のチュートリアルでトレーニングし、保存したモデルを "*運用化*" する方法について学習します。

このシナリオでは、運用とは、スコアリングのためにモデルを実稼働環境にデプロイすることを意味します。 SQL Server との統合により、Python コードをストアド プロシージャに埋め込むことができるため、これは非常に簡単になります。 新しい入力に基づき、モデルから予測を取得するには、アプリケーションからストアド プロシージャを呼び出し、新しいデータを渡します。

チュートリアルのこの回では、Python モデルに基づいて予測を作成する 2 つの方法、つまりバッチ スコアリングと行ごとのスコアリングについて説明します。

+ **バッチ スコアリング:** 入力データの複数の行を指定するには、SELECT クエリを引数としてストアド プロシージャに渡します。 結果は、入力ケースに対応する観察のテーブルを返します。
+ **個別のスコアリング**:個々のパラメーター セットを入力パラメーターとして渡します。  このストアド プロシージャは、1 つの行または値を返します。

スコアリングに必要なすべての Python コードは、ストアド プロシージャの一部として提供されています。

この記事では、次のことを行います。

> [!div class="checklist"]
> + バッチ スコアリングのストアド プロシージャを作成し、使用する
> + 1 つの行をスコアリングするためのストアド プロシージャを作成し、使用する

[パート 1 ](python-taxi-classification-introduction.md)では、前提条件をインストールしてサンプル データベースを復元しました。

[第 2 回](python-taxi-classification-explore-data.md) では、サンプル データを探索し、いくつかのプロットを生成しました。

[第 3 回](python-taxi-classification-create-features.md) では、Transact-SQL 関数を使用して生データから特徴を作成する方法を学習しました。 その後、その関数をストアド プロシージャから呼び出し、機能の値を含むテーブルを作成しました。

[第 4 回](python-taxi-classification-train-model.md) では、モジュールを読み込み、必要な関数を呼び出し、SQL Server ストアド プロシージャを使用してモデルを作成し、トレーニングしました。

## <a name="batch-scoring"></a>バッチ スコアリング

最初の2つのストアド プロシージャは、ストアド プロシージャで Python 予測呼び出しをラップするための基本的な構文を示します。 どちらのストアドプロシージャでも、入力としてデータのテーブルが必要です。

+ 使用するモデルの正確な名前は、ストアド プロシージャへの入力パラメーターとして提供されます。 ストアド プロシージャは、ストアド プロシージャの SELECT ステートメントを使用して、データベーステーブル `nyc_taxi_models`.table から、シリアル化されたモデルを読み込みます。
+ シリアル化されたモデルは、Python を使用して`mod`さらに処理するために、Python 変数に格納されます。
+ スコア付けが必要な新しいケースは、`@input_data_1` で指定された [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリから取得されます。 クエリ データが読み取られると、行が既定のデータ フレーム `InputDataSet`に保存されます。
+ どちらのストアド プロシージャも、`sklearn` の関数を使用して精度メトリック (曲線の下の領域) を計算します。 AUC などの精度メトリックは、ターゲットラベル (_チップ_列) も指定する場合にのみ生成できます。 予測には、ターゲット ラベル (変数 `y`) は必要ありませんが、精度メトリックの計算には必要です。

  したがって、スコア付けされるデータのターゲット ラベルがない場合は、ストアド プロシージャを変更して、AUC の計算を削除し、特徴 (ストアド プロシージャの変数 `X`) からチップを得る確率のみを返すことができます。

### <a name="predicttipscikitpy"></a>PredictTipSciKitPy

次の T-SQL ステートメントを実行して、ストアド プロシージャを作成します。 このストアド プロシージャによって、そのパッケージに固有の関数が使用されるため、scikit-learn パッケージに基づくモデルが必要です。

入力を含むデータフレームは、ロジスティック回帰モデルの`predict_proba`関数`mod`に渡されます。 `predict_proba`関数（`probArray = mod.predict_proba(X)`）は、(金額を問わず) チップを得えられる確率を表す**浮動**を返します。

```sql
DROP PROCEDURE IF EXISTS PredictTipSciKitPy;
GO

CREATE PROCEDURE [dbo].[PredictTipSciKitPy] (@model varchar(50), @inquery nvarchar(max))
AS
BEGIN
DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
EXEC sp_execute_external_script
  @language = N'Python',
  @script = N'
import pickle;
import numpy;
from sklearn import metrics

mod = pickle.loads(lmodel2)
X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
y = numpy.ravel(InputDataSet[["tipped"]])

probArray = mod.predict_proba(X)
probList = []
for i in range(len(probArray)):
  probList.append((probArray[i])[1])

probArray = numpy.asarray(probList)
fpr, tpr, thresholds = metrics.roc_curve(y, probArray)
aucResult = metrics.auc(fpr, tpr)
print ("AUC on testing data is: " + str(aucResult))

OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
',  
  @input_data_1 = @inquery,
  @input_data_1_name = N'InputDataSet',
  @params = N'@lmodel2 varbinary(max)',
  @lmodel2 = @lmodel2
WITH RESULT SETS ((Score float));
END
GO
```

### <a name="predicttiprxpy"></a>PredictTipRxPy

このストアド プロシージャは同じ入力を使用し、前のストアド プロシージャと同じ種類のスコアを作成しますが、SQL Server Machine Learning で提供されている **revoscalepy** パッケージの関数を使用します。

```sql
DROP PROCEDURE IF EXISTS PredictTipRxPy;
GO

CREATE PROCEDURE [dbo].[PredictTipRxPy] (@model varchar(50), @inquery nvarchar(max))
AS
BEGIN
DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
EXEC sp_execute_external_script 
  @language = N'Python',
  @script = N'
import pickle;
import numpy;
from sklearn import metrics
from revoscalepy.functions.RxPredict import rx_predict;

mod = pickle.loads(lmodel2)
X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
y = numpy.ravel(InputDataSet[["tipped"]])

probArray = rx_predict(mod, X)
probList = probArray["tipped_Pred"].values 

probArray = numpy.asarray(probList)
fpr, tpr, thresholds = metrics.roc_curve(y, probArray)
aucResult = metrics.auc(fpr, tpr)
print ("AUC on testing data is: " + str(aucResult))

OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
',
  @input_data_1 = @inquery,
  @input_data_1_name = N'InputDataSet',
  @params = N'@lmodel2 varbinary(max)',
  @lmodel2 = @lmodel2
WITH RESULT SETS ((Score float));
END
GO
```

## <a name="run-batch-scoring-using-a-select-query"></a>SELECT クエリを利用したバッチ スコアリング

ストアド プロシージャ **PredictTipSciKitPy** と **PredictTipRxPy** には、次の2つの入力パラメーターが必要です。

+ スコアリングのためにデータを取得するクエリ
+ トレーニング済みのモデルの名前

これらの引数をストアド プロシージャに渡すことで、特定のモデルを選択したり、スコアリングに使用するデータを変更したりできます。

1. スコアリングに **scikit-learn** モデルを使用するには、ストアド プロシージャ **PredictTipSciKitPy** を呼び出して、モデル名とクエリ文字列を入力として渡します。

   ```sql
   DECLARE @query_string nvarchar(max) -- Specify input query
     SET @query_string='
     select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
     dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
     from nyctaxi_sample_testing'
   EXEC [dbo].[PredictTipSciKitPy] 'SciKit_model', @query_string;
   ```

   このストアド プロシージャは、入力クエリの一部として渡された各乗車について予測確率を返します。 

   クエリの実行に SSMS (SQL Server Management Studio) を使用している場合、確率は **[結果]** ペインにテーブルとして表示されます。 [**メッセージ**] ペインには、精度メトリック (AUC または曲線の下の面積) が出力され、0.56 に近い値が表示されます。

2. スコアリングに **revoscalepy** モデルを使用するには、ストアド プロシージャ **PredictTipRxPy** を呼び出して、モデル名とクエリ文字列を入力として渡します。

   ```sql
   DECLARE @query_string nvarchar(max) -- Specify input query
     SET @query_string='
     select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
     dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
     from nyctaxi_sample_testing'
   EXEC [dbo].[PredictTipRxPy] 'revoscalepy_model', @query_string;
   ```

## <a name="single-row-scoring"></a>単一行のスコアリング

バッチ スコアリングではなく、アプリケーションから値を取得し、単一のケースを渡し、それらの値に基づいて単一の結果を返すことが必要になる場合があります。 たとえば、Excel ワークシート、web アプリケーション、またはレポートを設定して、ストアド プロシージャを呼び出し、ユーザーが入力または選択した入力に渡すことができます。

このセクションでは、次の2つのストアド プロシージャを呼び出して単一の予測を作成する方法について説明します。

+ [PredictTipSingleModeSciKitPy](#predicttipsinglemodescikitpy) は、scikit-learn モデルを使用して単一行スコアリングを目的として設計されています。
+ [PredictTipSingleModeRxPy](#predicttipsinglemoderxpy) は、revoscalepy モデルを使用して単一行スコアリングを目的として設計されています。
+ まだモデルをトレーニングしていない場合は、[第 5 回](python-taxi-classification-train-model.md)に戻ってください。

どちらのモデルも、乗客数、走行距離などの一連の単一値を入力として受け取ります。 テーブル値関数の `fnEngineerFeatures` は、入力から緯度と経度の値を使用して、新しい機能 (直線距離) に変換します。 [第 4 回](python-taxi-classification-create-features.md)には、このテーブル値関数の説明が含まれています。

どちらのストアド プロシージャも、Python モデルに基づいてスコアを作成します。

> [!NOTE]
>
> 外部アプリケーションからストアド プロシージャを呼び出すときに、Python モデルに必要なすべての入力機能を提供することが重要です。 エラーを回避するには、データ型とデータ長を検証するだけでなく、入力データを Python データ型にキャストまたは変換することが必要になる場合があります。

### <a name="predicttipsinglemodescikitpy"></a>PredictTipSingleModeSciKitPy

少し時間を取って、**scikit-learn** モデルを使用してスコアリングを実行するストアド プロシージャのコードをレビューします。

```sql
DROP PROCEDURE IF EXISTS PredictTipSingleModeSciKitPy;
GO

CREATE PROCEDURE [dbo].[PredictTipSingleModeSciKitPy] (@model varchar(50), @passenger_count int = 0,
  @trip_distance float = 0,
  @trip_time_in_secs int = 0,
  @pickup_latitude float = 0,
  @pickup_longitude float = 0,
  @dropoff_latitude float = 0,
  @dropoff_longitude float = 0)
AS
BEGIN
  DECLARE @inquery nvarchar(max) = N'
  SELECT * FROM [dbo].[fnEngineerFeatures]( 
    @passenger_count,
    @trip_distance,
    @trip_time_in_secs,
    @pickup_latitude,
    @pickup_longitude,
    @dropoff_latitude,
    @dropoff_longitude)
    '
DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
EXEC sp_execute_external_script 
  @language = N'Python',
  @script = N'
import pickle;
import numpy;

# Load model and unserialize
mod = pickle.loads(model)

# Get features for scoring from input data
X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]

# Score data to get tip prediction probability as a list (of float)
probList = []
probList.append((mod.predict_proba(X)[0])[1])

# Create output data frame
OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
',
  @input_data_1 = @inquery,
  @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,
    @trip_time_in_secs int ,
    @pickup_latitude float ,
    @pickup_longitude float ,
    @dropoff_latitude float ,
    @dropoff_longitude float',
    @model = @lmodel2,
    @passenger_count =@passenger_count ,
    @trip_distance=@trip_distance,
    @trip_time_in_secs=@trip_time_in_secs,
    @pickup_latitude=@pickup_latitude,
    @pickup_longitude=@pickup_longitude,
    @dropoff_latitude=@dropoff_latitude,
    @dropoff_longitude=@dropoff_longitude
WITH RESULT SETS ((Score float));
END
GO
```

### <a name="predicttipsinglemoderxpy"></a>PredictTipSingleModeRxPy

次のストアド プロシージャは、**revoscalepy** モデルを使用してスコアリングを実行します。

```sql
DROP PROCEDURE IF EXISTS PredictTipSingleModeRxPy;
GO

CREATE PROCEDURE [dbo].[PredictTipSingleModeRxPy] (@model varchar(50), @passenger_count int = 0,
  @trip_distance float = 0,
  @trip_time_in_secs int = 0,
  @pickup_latitude float = 0,
  @pickup_longitude float = 0,
  @dropoff_latitude float = 0,
  @dropoff_longitude float = 0)
AS
BEGIN
DECLARE @inquery nvarchar(max) = N'
  SELECT * FROM [dbo].[fnEngineerFeatures]( 
    @passenger_count,
    @trip_distance,
    @trip_time_in_secs,
    @pickup_latitude,
    @pickup_longitude,
    @dropoff_latitude,
    @dropoff_longitude)
  '
DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
EXEC sp_execute_external_script 
  @language = N'Python',
  @script = N'
import pickle;
import numpy;
from revoscalepy.functions.RxPredict import rx_predict;

# Load model and unserialize
mod = pickle.loads(model)

# Get features for scoring from input data
X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]

# Score data to get tip prediction probability as a list (of float)

probArray = rx_predict(mod, X)

probList = []
probList = probArray["tipped_Pred"].values

# Create output data frame
OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
',
  @input_data_1 = @inquery,
  @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,
    @trip_time_in_secs int ,
    @pickup_latitude float ,
    @pickup_longitude float ,
    @dropoff_latitude float ,
    @dropoff_longitude float',
    @model = @lmodel2,
    @passenger_count =@passenger_count ,
    @trip_distance=@trip_distance,
    @trip_time_in_secs=@trip_time_in_secs,
    @pickup_latitude=@pickup_latitude,
    @pickup_longitude=@pickup_longitude,
    @dropoff_latitude=@dropoff_latitude,
    @dropoff_longitude=@dropoff_longitude
WITH RESULT SETS ((Score float));
END
GO
```

### <a name="generate-scores-from-models"></a>モデルからスコアを生成する

ストアド プロシージャが作成されれば、どちらのモデルに基づいても簡単にスコアを生成できます。 新しい**クエリ** ウィンドウを開き、ストアド プロシージャを呼び出します。機能列のそれぞれにパラメーターを入力または貼り付けます。 値は次の機能に利用され、次の順序で並んでいます。

+ *passenger_count*
+ *trip_distance*
+ *trip_time_in_secs*
+ *pickup_latitude*
+ *pickup_longitude*
+ *dropoff_latitude*
+ *dropoff_longitude*

1. **revoscalepy** モデルを使用して予測を生成するには、次のステートメントを実行します。
  
   ```sql
   EXEC [dbo].[PredictTipSingleModeRxPy] 'revoscalepy_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
   ```

2. **scikit-learn** モデルを使用してスコアを生成するには、次のステートメントを実行します。

   ```sql
   EXEC [dbo].[PredictTipSingleModeSciKitPy] 'SciKit_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
   ```

両方のプロシージャからの出力結果は、指定されたパラメーターまたは特徴を使用したときの、タクシー乗車で支払われるチップの確率です。

## <a name="conclusions"></a>まとめ

このチュートリアル シリーズでは、ストアド プロシージャに埋め込まれた Python コードを操作する方法について説明しました。 [!INCLUDE[tsql](../../includes/tsql-md.md)] との統合により、Python モデルを展開して予測することと、エンタープライズ データ ワークフローの一部としてモデルを組み込み、維持することが簡単になります。

## <a name="next-steps"></a>次のステップ

この記事では、次の内容について説明します。

> [!div class="checklist"]
> + バッチ スコアリングのストアド プロシージャを作成し、使用しました
> + 1 つの行をスコアリングするためのストアド プロシージャを作成し、使用しました

Python の詳細については、[SQL Server の Python 拡張機能](../concepts/extension-python.md)に関するページを参照してください。
