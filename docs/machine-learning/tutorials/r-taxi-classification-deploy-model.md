---
title: R チュートリアル:SQL ストアド プロシージャで予測を実行する
titleSuffix: SQL machine learning
description: 全 5 回からなるこのチュートリアル シリーズの第 5 回では、SQL 機械学習を利用し、T-SQL 関数と共に SQL ストアド プロシージャに組み込まれた R スクリプトを運用化します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/15/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||>=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: e7657dcfe382ed87b31ca17e6c36d9019d1b84e2
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92412518"
---
# <a name="r-tutorial-run-predictions-in-sql-stored-procedures"></a>R チュートリアル:SQL ストアド プロシージャで予測を実行する
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

全 5 回からなるこのチュートリアル シリーズの第 5 回では、潜在的成果を予測するモデルを利用し、前回のチュートリアルでトレーニングし、保存したモデルを " *運用化* " します。 モデルは、他のアプリケーションから直接呼び出すことができるストアド プロシージャにラップされます。

この記事では、スコアリングを実行する 2 つの方法を実演します。

+ **バッチ スコアリング モード** :ストアド プロシージャへの入力には SELECT クエリを使用します。 このストアド プロシージャは、入力ケースに対応する観察のテーブルを返します。

+ **個別スコア付けモード** : 個々のパラメーター セットを入力として渡します。  このストアド プロシージャは、1 つの行または値を返します。

この記事では、次のことを行います。

> [!div class="checklist"]
> + バッチ スコアリングのストアド プロシージャを作成し、使用する
> + 1 つの行をスコアリングするためのストアド プロシージャを作成し、使用する

[パート 1 ](r-taxi-classification-introduction.md)では、前提条件をインストールしてサンプル データベースを復元しました。

[第 2 回](r-taxi-classification-explore-data.md) では、サンプル データを確認し、いくつかのプロットを生成しました。

[第 3 回](r-taxi-classification-create-features.md) では、Transact-SQL 関数を使用して生データから特徴を作成する方法を学習しました。 その後、その関数をストアド プロシージャから呼び出し、機能の値を含むテーブルを作成しました。

[第 4 回](r-taxi-classification-train-model.md) では、モジュールを読み込み、必要な関数を呼び出し、SQL Server ストアド プロシージャを使用してモデルを作成し、トレーニングしました。

## <a name="basic-scoring"></a>基本のスコアリング

ストアド プロシージャ **RPredict** は、ストアド プロシージャで `PREDICT` 呼び出しをラップするための基本構文を示します。

```sql
CREATE PROCEDURE [dbo].[RPredict] (@model varchar(250), @inquery nvarchar(max))
AS 
BEGIN 

DECLARE @lmodel2 varbinary(max) = (SELECT model FROM nyc_taxi_models WHERE name = @model);  
EXEC sp_execute_external_script @language = N'R',
  @script = N' 
    mod <- unserialize(as.raw(model));
    print(summary(mod))
    OutputDataSet <- data.frame(predict(mod, InputDataSet, type = "response"));
    str(OutputDataSet)
    print(OutputDataSet)
    ',
  @input_data_1 = @inquery,
  @params = N'@model varbinary(max)',
  @model = @lmodel2 
  WITH RESULT SETS (("Score" float));
END
GO
```

+ SELECT ステートメントは、シリアル化されたモデルをデータベースから取得し、R を利用してさらに処理するために R 変数 `mod` にモデルを保存します。

+ スコア付けの新しいケースは、ストアド プロシージャの最初のパラメーター、`@inquery`で指定された [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリから取得されます。 クエリ データが読み取られると、行が既定のデータ フレーム `InputDataSet`に保存されます。 このデータ フレームは [PREDICT](/sql/t-sql/queries/predict-transact-sql) 関数に渡され、これによりスコアが生成されます。
  
  `OutputDataSet <- data.frame(predict(mod, InputDataSet, type = "response"));`
  
  data.frame には 1 つの行を含めることができるため、一括または 1 回のスコア付けに同じコードを利用できます。
  
+ `PREDICT` 関数により返される値は、ドライバーに任意の金額のチップが与えられる確率を表す **float** です。

## <a name="batch-scoring-a-list-of-predictions"></a>バッチ スコアリング (予測の一覧)

より一般的なシナリオは、バッチ モードで複数の観測の予測を生成することです。 この手順では、バッチ スコアリングのしくみを見てみましょう。

1. 最初に、使用する入力データの小さなセットを取得します。 このクエリは、予測に必要な乗客数とその他の機能を利用し、乗車の "上位 10" 一覧を作成します。
  
   ```sql
   SELECT TOP 10 a.passenger_count AS passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance
   
   FROM (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a

   LEFT OUTER JOIN

   (SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample TABLESAMPLE (70 percent) REPEATABLE (98052)    )b

   ON a.medallion=b.medallion AND a.hack_license=b.hack_license 
   AND a.pickup_datetime=b.pickup_datetime
   WHERE b.medallion IS NULL
   ```

   **サンプルの結果**

   ```text
   passenger_count   trip_time_in_secs    trip_distance  dropoff_datetime          direct_distance
   1                 283                  0.7            2013-03-27 14:54:50.000   0.5427964547
   1                 289                  0.7            2013-02-24 12:55:29.000   0.3797099614
   1                 214                  0.7            2013-06-26 13:28:10.000   0.6970098661
   ```

2. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] で **RPredictBatchOutput** という名前のストアド プロシージャを作成します。

   ```sql
   CREATE PROCEDURE [dbo].[RPredictBatchOutput] (@model varchar(250), @inquery nvarchar(max))
   AS
   BEGIN
   DECLARE @lmodel2 varbinary(max) = (SELECT model FROM nyc_taxi_models WHERE name = @model);
   EXEC sp_execute_external_script 
     @language = N'R',
     @script = N'
       mod <- unserialize(as.raw(model));
       print(summary(mod))
       OutputDataSet <- data.frame(predict(mod, InputDataSet, type = "response"));
       str(OutputDataSet)
       print(OutputDataSet)
     ',
     @input_data_1 = @inquery,
     @params = N'@model varbinary(max)',
     @model = @lmodel2
     WITH RESULT SETS ((Score float));
   END
   ```

3. 変数にクエリ テキストを指定し、それをパラメーターとしてストアド プロシージャに渡します。

   ```sql
   -- Define the input data
   DECLARE @query_string nvarchar(max)
   SET @query_string='SELECT TOP 10 a.passenger_count as passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance FROM  (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample  )a   LEFT OUTER JOIN (SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample TABLESAMPLE (70 percent) REPEATABLE (98052))b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'
   
   -- Call the stored procedure for scoring and pass the input data
   EXEC [dbo].[RPredictBatchOutput] @model = 'RTrainLogit_model', @inquery = @query_string;
   ```
  
このストアド プロシージャは、上位 10 の各乗車の予測を表す一連の値を返します。 ただし、上位の乗車は、比較的短い乗車距離の一人の乗客でもあり、その場合、ドライバーがチップを得られる可能性はほとんどありません。

> [!TIP]
> "チップあり" と "チップなし" の結果のみを返すのではなく、予測の確率スコアを返し、WHERE 句を _Score_ 列の値に適用します。0.5 や 0.7 などのしきい値を使用すると、スコアを "チップを得る確率が高い" または "チップを得る確率が低い" として分類することもできます。 この手順はストアド プロシージャに含まれていませんが、導入は簡単です。

## <a name="single-row-scoring-of-multiple-inputs"></a>複数の入力による単一行のスコア付け

場合によっては、複数の入力値を渡し、それらの値に基づいて1つの予測を得ることがあります。 たとえば、Excel ワークシート、Web アプリケーション、または Reporting Services レポートを設定して、ストアド プロシージャを呼び出し、それらのアプリケーションからユーザーが入力または選択した入力を提供することができます。

このセクションでは、乗客数、乗車距離など、複数の入力を受け取るストアド プロシージャを使用して 1 つの予測を作成する方法について説明します。 ストアド プロシージャは、以前に格納された R モデルに基づいてスコアを作成します。
  
外部アプリケーションからストアド プロシージャを呼び出す場合は、データが R モデルの要件と一致していることを確認してください。 場合によっては、入力データを R データ型にキャストまたは変換できなければなりません。あるいは、データ型やデータ長を検証する必要があります。

1. ストアド プロシージャ **RPredictSingleRow** を作成します。
  
   ```sql
   CREATE PROCEDURE [dbo].[RPredictSingleRow] @model varchar(50), @passenger_count int = 0, @trip_distance float = 0, @trip_time_in_secs int = 0, @pickup_latitude float = 0, @pickup_longitude float = 0, @dropoff_latitude float = 0, @dropoff_longitude float = 0
   AS
   BEGIN
   DECLARE @inquery nvarchar(max) = N'SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count, @trip_distance, @trip_time_in_secs,  @pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude)';
   DECLARE @lmodel2 varbinary(max) = (SELECT model FROM nyc_taxi_models WHERE name = @model);
   EXEC sp_execute_external_script  
     @language = N'R',
     @script = N'  
       mod <- unserialize(as.raw(model));  
       print(summary(mod));  
       OutputDataSet <- data.frame(predict(mod, InputDataSet, type = "response"));
       str(OutputDataSet);
       print(OutputDataSet); 
       ',  
     @input_data_1 = @inquery,  
     @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,@trip_time_in_secs int ,  @pickup_latitude float ,@pickup_longitude float ,@dropoff_latitude float ,@dropoff_longitude float', @model = @lmodel2, @passenger_count =@passenger_count, @trip_distance=@trip_distance, @trip_time_in_secs=@trip_time_in_secs, @pickup_latitude=@pickup_latitude, @pickup_longitude=@pickup_longitude, @dropoff_latitude=@dropoff_latitude, @dropoff_longitude=@dropoff_longitude  
     WITH RESULT SETS ((Score float));  
   END
   ```

2. 手動で値を指定し、お試しください。
  
   新しい **クエリ** ウィンドウを開き、ストアド プロシージャを呼び出して、各パラメーターの値を指定します。 パラメーターは、モデルで使用される特徴列を表し、必須です。

   ```sql
   EXEC [dbo].[RPredictSingleRow] @model = 'RTrainLogit_model',
   @passenger_count = 1,
   @trip_distance = 2.5,
   @trip_time_in_secs = 631,
   @pickup_latitude = 40.763958,
   @pickup_longitude = -73.973373,
   @dropoff_latitude =  40.782139,
   @dropoff_longitude = -73.977303
   ```

   または、ストアド プロシージャの [パラメーターでサポー](../../relational-databases/stored-procedures/specify-parameters.md)トされている短い形式を使用します。
  
   ```sql
   EXEC [dbo].[RPredictSingleRow] 'RTrainLogit_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
   ```

3. この結果は、これらの上位 10 の乗車ではチップが与えられる確率が低い (ゼロ) ことを示しています。これは、すべてが比較的短い乗車距離の一人の乗客であるためです。

## <a name="conclusions"></a>まとめ

これで、ストアド プロシージャに R コードを埋め込む方法を学習できました。これらのプラクティスを拡張して独自のモデルを構築することができます。 [!INCLUDE[tsql](../../includes/tsql-md.md)] との統合により、R モデルを展開して予測することと、企業データ ワークフローの一部としてモデルを組み込み、維持することが簡単になります。

## <a name="next-steps"></a>次のステップ

この記事では、次の内容について説明します。

> [!div class="checklist"]
> + バッチ スコアリングのストアド プロシージャを作成し、使用しました
> + 1 つの行をスコアリングするためのストアド プロシージャを作成し、使用しました

R の詳細については、[SQL Server の R 拡張機能](../concepts/extension-r.md)に関するページを参照してください。