---
title: R チュートリアル:モデルのトレーニングと保存
titleSuffix: SQL machine learning
description: 全 5 回からなるこのチュートリアル シリーズの第 4 回では、SQL Server の Transact-SQL と SQL 機械学習を使用し、R でモデルをトレーニングし、保存します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/15/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||>=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: d42d51371b0641fe460150e68fe96c5eb68e09cb
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92412549"
---
# <a name="r-tutorial-train-and-save-model"></a>R チュートリアル:モデルのトレーニングと保存
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

全 5 回からなるこのチュートリアル シリーズの第 4 回では、R を使用して機械学習モデルをトレーニングする方法について説明します。前回のチュートリアルで作成したデータ機能を使用してモデルをトレーニングし、トレーニング済みのモデルを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルに保存します。 この場合、R パッケージは [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]と共に既にインストールされているため、SQL からすべてを実行できます。

この記事では、次のことを行います。

> [!div class="checklist"]
> + SQL ストアド プロシージャを使用してモデルを作成し、トレーニングする
> + トレーニング済みのモデルを SQL テーブルに保存する

[パート 1 ](r-taxi-classification-introduction.md)では、前提条件をインストールしてサンプル データベースを復元しました。

[第 2 回](r-taxi-classification-explore-data.md) では、サンプル データを確認し、いくつかのプロットを生成しました。

[第 3 回](r-taxi-classification-create-features.md) では、Transact-SQL 関数を使用して生データから特徴を作成する方法を学習しました。 その後、その関数をストアド プロシージャから呼び出し、機能の値を含むテーブルを作成しました。

[第 5 回](r-taxi-classification-deploy-model.md) では、第 4 回でトレーニングして保存したモデルを運用化する方法について説明します。

## <a name="create-the-stored-procedure"></a>ストアド プロシージャを作成する

T-SQL から R を呼び出すときは、システムストアドプロシージャ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) を使用します。 ただし、モデルの再トレーニングなど、頻繁に繰り返すプロセスでは、別のストアド プロシージャに `sp_execute_external_script` への呼び出しをカプセル化する方が簡単です。

1. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] で、新しい **[クエリ]** ウィンドウを開きます。

2. 次のステートメントを実行して、ストアド プロシージャ **RTrainLogitModel** を作成します。 このストアド プロシージャでは、入力データを定義し、 **glm** を使用して、ロジスティック回帰モデルを作成します。

   ```sql
   CREATE PROCEDURE [dbo].[RTrainLogitModel] (@trained_model varbinary(max) OUTPUT)
   
   AS
   BEGIN
     DECLARE @inquery nvarchar(max) = N'
       select tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance,
       pickup_datetime, dropoff_datetime,
       dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
       from nyctaxi_sample
       tablesample (70 percent) repeatable (98052)
   '
   
     EXEC sp_execute_external_script @language = N'R',
                                     @script = N'
   ## Create model
   logitObj <- glm(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = InputDataSet, family = binomial)
   summary(logitObj)
   
   ## Serialize model 
   trained_model <- as.raw(serialize(logitObj, NULL));
   ',
     @input_data_1 = @inquery,
     @params = N'@trained_model varbinary(max) OUTPUT',
     @trained_model = @trained_model OUTPUT; 
   END
   GO
   ```

   + モデルをテストするために一部のデータが残っていることを確認するために、トレーニング目的で、データの70% がタクシー データ テーブルからランダムに選択されます。

   + SELECT クエリによって、カスタムのスカラー関数 *fnCalculateDistance* が使用され、乗車位置と降車位置直線距離が計算されます。 クエリの結果は R の既定の入力変数 `InputDataset` に格納されます。
  
   + R スクリプトは、R 関数 **glm** を呼び出して、ロジスティック回帰モデルを作成します。
  
     二項変数 _tipped_ が *ラベル* または結果列として使用され、モデルは、  _passenger_count_ 、 _trip_distance_ 、 _trip_time_in_secs_ 、および _direct_distance_ の機能列を使用して調整されます。
  
   + R 変数 `logitObj` に保存されたトレーニング済みのモデルはシリアル化され、出力パラメーターとして返されます。

## <a name="train-and-deploy-the-r-model-using-the-stored-procedure"></a>ストアド プロシージャを使用した R モデルのトレーニングとデプロイ

ストアド プロシージャには、既に入力データの定義が含まれているため、入力クエリを提供する必要はありません。

1. R モデルをトレーニングしてデプロイするには、ストアド プロシージャを呼び出してデータベース テーブル _nyc_taxi_models_ に挿入します。これにより、将来の予測に使用できるようになります。

   ```sql
   DECLARE @model VARBINARY(MAX);
   EXEC RTrainLogitModel @model OUTPUT;
   INSERT INTO nyc_taxi_models (name, model) VALUES('RTrainLogit_model', @model);
   ```

2. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] の **[メッセージ]** ウィンドウに、次のように R の **stdout** ストリームにパイプ処理されるメッセージが表示されていないか注意してください。 

   "外部スクリプトからの STDOUT メッセージ:読み取られる行:1193025、処理された行数の合計:1193025、合計チャンク時間:0.093 秒"

3. ステートメントが完了したら、テーブル *nyc_taxi_models* を開きます。 データの処理とモデルの調整には、しばらく時間がかかる場合があります。

   _model_ 列にシリアル化されたモデル、および _name_ 列にモデル名 **TrainLog_model** を含む、1 つの新しい行が追加されていることがわかります。

   ```text
   model                        name
   ---------------------------- ------------------
   0x580A00000002000302020....  RTrainLogit_model
   ```

次回のチュートリアルでは、トレーニング済みのモデルを使用して予測を作成します。

## <a name="next-steps"></a>次のステップ

この記事では、次の内容について説明します。

> [!div class="checklist"]
> + SQL ストアド プロシージャを使用してモデルを作成し、トレーニングした
> + トレーニング済みのモデルを SQL テーブルに保存した

> [!div class="nextstepaction"]
> [R チュートリアル:SQL ストアド プロシージャで予測を実行する](r-taxi-classification-deploy-model.md)
