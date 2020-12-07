---
title: Python のチュートリアル:モデルのトレーニングと保存
titleSuffix: SQL machine learning
description: 全 5 回からなるこのチュートリアル シリーズの第 4 回では、SQL Server の Transact-SQL と SQL 機械学習を使用し、Python でモデルをトレーニングし、保存します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/29/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||>=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 18cd0c279493dcb41d043d3f76d6debe71eb402c
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194475"
---
# <a name="python-tutorial-train-and-save-a-python-model-using-t-sql"></a>Python のチュートリアル:T-SQL を使用して Python モデルをトレーニングし保存する
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

全 5 回からなるこのチュートリアル シリーズの第 4 回では、Python パッケージの **scikit-learn** と **revoscalepy** を使用して、機械学習モデルをトレーニングする方法について説明します。 これらの Python ライブラリは、SQL Server 機械学習と共に、既にインストールされています。

SQL Server ストアド プロシージャを使用してモデルを作成およびトレーニングするには、モジュールを読み込んでから、必要な関数を呼び出します。 このモデルには、このチュートリアル シリーズの過去のレッスンで作成したデータ機能が必要です。 最後に、トレーニング済みのモデルを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルに保存します。

この記事では、次のことを行います。

> [!div class="checklist"]
> + SQL ストアド プロシージャを使用してモデルを作成し、トレーニングする
> + トレーニング済みのモデルを SQL テーブルに保存する

[パート 1 ](python-taxi-classification-introduction.md)では、前提条件をインストールしてサンプル データベースを復元しました。

[第 2 回](python-taxi-classification-explore-data.md) では、サンプル データを探索し、いくつかのプロットを生成しました。

[第 3 回](python-taxi-classification-create-features.md) では、Transact-SQL 関数を使用して生データから特徴を作成する方法を学習しました。 その後、その関数をストアド プロシージャから呼び出し、機能の値を含むテーブルを作成しました。

[第 5 回](python-taxi-classification-deploy-model.md) では、第 4 回でトレーニングして保存したモデルを運用化する方法について説明します。

## <a name="split-the-sample-data-into-training-and-testing-sets"></a>トレーニング セットとテスト セットへのデータの分割

1. **PyTrainTestSplit** という名のストアドプロシージャを作成し、nyctaxi_sample テーブルのデータを 2 つに分割します。nyctaxi_sample_training と nyctaxi_sample_testing です。 

   このストアド プロシージャは既に作成されているはずですが、以下のコードを実行して作成することもできます。

   ```sql
   DROP PROCEDURE IF EXISTS PyTrainTestSplit;
   GO

   CREATE PROCEDURE [dbo].[PyTrainTestSplit] (@pct int)
   AS
   
   DROP TABLE IF EXISTS dbo.nyctaxi_sample_training
   SELECT * into nyctaxi_sample_training FROM nyctaxi_sample WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) < @pct
   
   DROP TABLE IF EXISTS dbo.nyctaxi_sample_testing
   SELECT * into nyctaxi_sample_testing FROM nyctaxi_sample
   WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) > @pct
   GO
   ```

2. カスタム分割を使用してデータを分割するには、ストアド プロシージャを実行し、トレーニング セットに割り当てられたデータの比率を表す整数を入力します。 たとえば、次のステートメントでは、60% のデータがトレーニング セットに割り当てられます。

   ```sql
   EXEC PyTrainTestSplit 60
   GO
   ```

## <a name="build-a-logistic-regression-model"></a>ロジスティック回帰モデルの作成

データの準備完了後、それを使用してモデルをトレーニングできます。 これを行うには、トレーニング データ テーブルの入力として、Python コードを実行するストアド プロシージャを呼び出します。 このチュートリアルでは、2 つのモデル (二項分類モデル) を作成します。

+ ストアドプロシージャ **PyTrainScikit** は、**scikit-learn** パッケージを使用して、チップ予測モデルを作成します。
+ ストアドプロシージャ **TrainTipPredictionModelRxPy** は、**revoscalepy** パッケージを使用して、チップ予測モデルを作成します。

それぞれのストアド プロシージャは、入力したデータを使用して、ロジスティック回帰モデルを作成およびトレーニングします。 すべての Python コードは、システムストアドプロシージャ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)にラップされます。

新しいデータでモデルを再トレーニングしやすくするために、別のストアド プロシージャに sp_execute_external_script の呼び出しをラップし、新しいトレーニング データをパラメーターとして渡します。 このセクションでは、このプロセスを、順を追って説明します。

### <a name="pytrainscikit"></a>PyTrainScikit

1. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] で新しい**クエリ** ウィンドウを開き、次のステートメントを実行して、ストアド プロシージャ **PyTrainScikit** を作成します。  ストアド プロシージャには入力データの定義が含まれているため、入力クエリを提供する必要はありません。

   ```sql
   DROP PROCEDURE IF EXISTS PyTrainScikit;
   GO

   CREATE PROCEDURE [dbo].[PyTrainScikit] (@trained_model varbinary(max) OUTPUT)
   AS
   BEGIN
   EXEC sp_execute_external_script
     @language = N'Python',
     @script = N'
   import numpy
   import pickle
   from sklearn.linear_model import LogisticRegression
   
   ##Create SciKit-Learn logistic regression model
   X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
   y = numpy.ravel(InputDataSet[["tipped"]])
   
   SKLalgo = LogisticRegression()
   logitObj = SKLalgo.fit(X, y)
   
   ##Serialize model
   trained_model = pickle.dumps(logitObj)
   ',
   @input_data_1 = N'
   select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, 
   dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
   from nyctaxi_sample_training
   ',
   @input_data_1_name = N'InputDataSet',
   @params = N'@trained_model varbinary(max) OUTPUT',
   @trained_model = @trained_model OUTPUT;
   ;
   END;
   GO
   ```

2. 次の SQL ステートメントを実行して、トレーニング済みのモデルをテーブル nyc\_taxi_models に挿入します。

   ```sql
   DECLARE @model VARBINARY(MAX);
   EXEC PyTrainScikit @model OUTPUT;
   INSERT INTO nyc_taxi_models (name, model) VALUES('SciKit_model', @model);
   ```

   データ処理とモデルの調整には、数分かかることがあります。 Python の **stdout** ストリームにパイプ出力されるメッセージが、[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] の **[メッセージ]** ウィンドウに表示されます。 たとえば、次のように入力します。

   ```text
   STDOUT message(s) from external script:
   C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy
   ```

3. テーブル *nyc\_taxi_models* を開きます。 _model_列にシリアル化されたモデルを含む新しい行が 1 つ追加されます。

   ```text
   SciKit_model
   0x800363736B6C6561726E2E6C696E6561....
   ```

### <a name="traintippredictionmodelrxpy"></a>TrainTipPredictionModelRxPy

このストアド プロシージャは、新しい **revoscalepy** パッケージを使用します。これは Python 用の新しいパッケージです。 これには、R 言語の **RevoScaleR** パッケージに提供されているものと同様のオブジェクト、変換、およびアルゴリズムが含まれています。 

**revoscalepy** を使用すると、リモート コンピューティング コンテキストの作成、コンピューティング コンテキスト間でのデータ移動、データ変換、および、ロジスティック、線形回帰、デシジョンツリーなどの一般的アルゴリズムを使用した、予測モデルのトレーニングを行うことができます。 詳細については、[SQL Server の revoscalepy モジュール](../python/ref-py-revoscalepy.md)および [revoscalepy 関数参照](/r-server/python-reference/revoscalepy/revoscalepy-package)に関するページを参照してください。

1. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] で新しい**クエリ** ウィンドウを開き、次のステートメントを実行して、ストアド プロシージャ _TrainTipPredictionModelRxPy_ を作成します。  ストアド プロシージャには、既に入力データの定義が含まれているため、入力クエリを提供する必要はありません。

   ```sql
   DROP PROCEDURE IF EXISTS TrainTipPredictionModelRxPy;
   GO

   CREATE PROCEDURE [dbo].[TrainTipPredictionModelRxPy] (@trained_model varbinary(max) OUTPUT)
   AS
   BEGIN
   EXEC sp_execute_external_script 
     @language = N'Python',
     @script = N'
   import numpy
   import pickle
   from revoscalepy.functions.RxLogit import rx_logit
   
   ## Create a logistic regression model using rx_logit function from revoscalepy package
   logitObj = rx_logit("tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance", data = InputDataSet);
   
   ## Serialize model
   trained_model = pickle.dumps(logitObj)
   ',
   @input_data_1 = N'
   select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, 
   dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
   from nyctaxi_sample_training
   ',
   @input_data_1_name = N'InputDataSet',
   @params = N'@trained_model varbinary(max) OUTPUT',
   @trained_model = @trained_model OUTPUT;
   ;
   END;
   GO
   ```

   このストアド プロシージャは、モデル トレーニングの一環として、以下の手順を実行します。

   + SELECT クエリにより、カスタム スカラー関数 _fnCalculateDistance_ が適用され、乗車場所と降車場所間の直線距離が計算されます。 クエリの結果は、Python の既定の入力変数 `InputDataset` に格納されます。
   + 二項変数 _tipped_ が*ラベル*または結果列として使用され、モデルは、_passenger_count_、_trip_distance_、_trip_time_in_secs_、および _direct_distance_ の機能列を使用して調整されます。
   + トレーニング済みモデルはシリアル化され、Python 変数`logitObj`に格納されます。 T-SQL キーワードの OUTPUT を追加することにより、変数をストアド プロシージャの出力として追加できます。 次の手順では、この変数を使用して、モデルのバイナリコードをデータベース テーブル _nyc_taxi_models_ に挿入します。 このメカニズムにより、モデルの格納と再利用が容易になります。

2. 以下のようにストアド プロシージャを実行し、トレーニングした **revoscalepy** モデルを、テーブル *nyc_taxi_models* に挿入します。

   ```sql
   DECLARE @model VARBINARY(MAX);
   EXEC TrainTipPredictionModelRxPy @model OUTPUT;
   INSERT INTO nyc_taxi_models (name, model) VALUES('revoscalepy_model', @model);
   ```

   データの処理とモデルの調整には、しばらく時間がかかる場合があります。 Python の **stdout** ストリームにパイプ出力されるメッセージが、[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] の **[メッセージ]** ウィンドウに表示されます。 たとえば、次のように入力します。

   ```text
   STDOUT message(s) from external script:
   C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy
   ```

3. テーブル *nyc_taxi_models*を開きます。 _model_列にシリアル化されたモデルを含む新しい行が 1 つ追加されます。

   ```text
   revoscalepy_model
   0x8003637265766F7363616c....
   ```

次回のチュートリアルでは、トレーニング済みのモデルを使用して予測を作成します。

## <a name="next-steps"></a>次のステップ

この記事では、次の内容について説明します。

> [!div class="checklist"]
> + SQL ストアド プロシージャを使用してモデルを作成し、トレーニングした
> + トレーニング済みのモデルを SQL テーブルに保存した

> [!div class="nextstepaction"]
> [Python のチュートリアル:ストアド プロシージャに埋め込まれた Python を使用した予測の実行](python-taxi-classification-deploy-model.md)