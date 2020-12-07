---
title: チュートリアル:R で予測モデルをデプロイする
titleSuffix: SQL machine learning
description: この 4 部構成のチュートリアルのパート 4 では、SQL 機械学習を使用して R で予測モデルをデプロイします。
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.reviewer: garye, davidph
ms.date: 05/21/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: bed9217da00b7ca2cdd9bbb43e92d58c8f59b678
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870273"
---
# <a name="tutorial-deploy-a-predictive-model-in-r-with-sql-machine-learning"></a>チュートリアル:SQL 機械学習を使用して R で予測モデルをデプロイする
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズのパート 4 では、Machine Learning Services を使用して、R で開発された機械学習モデルを SQL Server Machine Learning Services またはビッグ データ クラスターにデプロイします。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズのパート 4 では、Machine Learning Services を使用して、R で開発された機械学習モデルを SQL Server にデプロイします。
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズのパート 4 では、SQL Server R Services を使用して、R で開発された機械学習モデルを SQL Server にデプロイします。
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズのパート 4 では、Machine Learning Services を使用して、R で開発された機械学習モデルを Azure SQL Managed Instance にデプロイします。
::: moniker-end

この記事では、次の方法について学習します。

> [!div class="checklist"]
> * 機械学習モデルを生成するストアド プロシージャを作成する
> * データベース テーブルにモデルを格納する
> * モデルを使用して予測を行うストアド プロシージャを作成する
> * 新しいデータでモデルを実行する

[第 1 部](r-predictive-model-introduction.md)では、サンプル データベースを復元する方法を学習しました。

[パート 2](r-predictive-model-prepare-data.md) では、サンプル データベースをインポートし、R での予測モデルのトレーニングに使用されるデータを準備する方法を学習しました。

[パート 3](r-predictive-model-train.md) では、R で複数の機械学習モデルを作成してトレーニングしてから、最も正確なものを選ぶ方法を学習しました。

## <a name="prerequisites"></a>前提条件

このチュートリアルのパート 4 は、[**パート 1**](r-predictive-model-introduction.md)の前提条件を満たし、[**パート 2**](r-predictive-model-prepare-data.md)および [**パート 3**](r-predictive-model-train.md)の手順を完了していることを前提としています。

## <a name="create-a-stored-procedure-that-generates-the-model"></a>モデルを生成するストアド プロシージャの作成

このチュートリアル シリーズのパート 3 では、デシジョン ツリー (dtree) モデルが最も正確であると判断しました。 ここでは、開発した R スクリプトを使用して、R パッケージの rpart を利用し、dtree モデルをトレーニングして生成するストアド プロシージャ (`generate_rental_model`) を作成します。

Azure Data Studio で以下のコマンドを実行します。

```sql
USE [TutorialDB]
DROP PROCEDURE IF EXISTS generate_rental_model;
GO
CREATE PROCEDURE generate_rental_model (@trained_model VARBINARY(max) OUTPUT)
AS
BEGIN
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'
rental_train_data$Month   <- factor(rental_train_data$Month);
rental_train_data$Day     <- factor(rental_train_data$Day);
rental_train_data$Holiday <- factor(rental_train_data$Holiday);
rental_train_data$Snow    <- factor(rental_train_data$Snow);
rental_train_data$WeekDay <- factor(rental_train_data$WeekDay);

#Create a dtree model and train it using the training data set
library(rpart);
model_dtree <- rpart(RentalCount ~ Month + Day + WeekDay + Snow + Holiday, data = rental_train_data);
#Serialize the model before saving it to the database table
trained_model <- as.raw(serialize(model_dtree, connection=NULL));
'
        , @input_data_1 = N'
            SELECT RentalCount
                 , Year
                 , Month
                 , Day
                 , WeekDay
                 , Snow
                 , Holiday
            FROM dbo.rental_data
            WHERE Year < 2015
            '
        , @input_data_1_name = N'rental_train_data'
        , @params = N'@trained_model varbinary(max) OUTPUT'
        , @trained_model = @trained_model OUTPUT;
END;
GO
```

## <a name="store-the-model-in-a-database-table"></a>データベース テーブルにモデルを格納する

TutorialDB データベースにテーブルを作成し、そのテーブルにモデルを保存します。

1. モデルを格納するためのテーブル (`rental_models`) を作成します。

    ```sql
    USE TutorialDB;
    DROP TABLE IF EXISTS rental_models;
    GO
    CREATE TABLE rental_models (
          model_name VARCHAR(30) NOT NULL DEFAULT('default model') PRIMARY KEY
        , model VARBINARY(MAX) NOT NULL
        );
    GO
    ```

1. バイナリ オブジェクトとしてテーブルにモデルを保存します。モデル名は "DTree" です。

    ```sql
    -- Save model to table
    TRUNCATE TABLE rental_models;
    
    DECLARE @model VARBINARY(MAX);
    
    EXECUTE generate_rental_model @model OUTPUT;
    
    INSERT INTO rental_models (
          model_name
        , model
        )
    VALUES (
         'DTree'
        , @model
        );
    
    SELECT *
    FROM rental_models;
    ```

## <a name="create-a-stored-procedure-that-makes-predictions"></a>予測を行うストアド プロシージャを作成する

トレーニング済みのモデルと一連の新しいデータを使用して予測するストアド プロシージャ (`predict_rentalcount_new`) を作成します。

```sql
-- Stored procedure that takes model name and new data as input parameters and predicts the rental count for the new data
USE [TutorialDB]
DROP PROCEDURE IF EXISTS predict_rentalcount_new;
GO
CREATE PROCEDURE predict_rentalcount_new (
      @model_name VARCHAR(100)
    , @input_query NVARCHAR(MAX)
    )
AS
BEGIN
    DECLARE @model VARBINARY(MAX) = (
            SELECT model
            FROM rental_models
            WHERE model_name = @model_name
            );

    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'
#Convert types to factors
rentals$Month   <- factor(rentals$Month);
rentals$Day     <- factor(rentals$Day);
rentals$Holiday <- factor(rentals$Holiday);
rentals$Snow    <- factor(rentals$Snow);
rentals$WeekDay <- factor(rentals$WeekDay);

#Before using the model to predict, we need to unserialize it
rental_model <- unserialize(model);

#Call prediction function
rental_predictions <- predict(rental_model, rentals);
rental_predictions <- data.frame(rental_predictions);
'
        , @input_data_1 = @input_query
        , @input_data_1_name = N'rentals'
        , @output_data_1_name = N'rental_predictions'
        , @params = N'@model varbinary(max)'
        , @model = @model
    WITH RESULT SETS(("RentalCount_Predicted" FLOAT));
END;
GO
```

## <a name="execute-the-model-with-new-data"></a>新しいデータでモデルを実行する

ここで、ストアド プロシージャ `predict_rentalcount_new` を使用して、新しいデータからレンタル数を予測できます。

```sql
-- Use the predict_rentalcount_new stored procedure with the model name and a set of features to predict the rental count
EXECUTE dbo.predict_rentalcount_new @model_name = 'DTree'
    , @input_query = '
        SELECT CONVERT(INT,  3) AS Month
             , CONVERT(INT, 24) AS Day
             , CONVERT(INT,  4) AS WeekDay
             , CONVERT(INT,  1) AS Snow
             , CONVERT(INT,  1) AS Holiday
        ';
GO
```

次のような結果が表示されるはずです。

```results
RentalCount_Predicted
332.571428571429
```

データベースでモデルを正常に作成し、トレーニングしてデプロイしました。 そうしたら、ストアド プロシージャでそのモデルを使用して、新しいデータに基づいて値を予測します。


## <a name="clean-up-resources"></a>リソースをクリーンアップする

TutorialDB データベースの使用が終わったら、それをサーバーから削除します。

## <a name="next-steps"></a>次のステップ

このチュートリアル シリーズのパート 4 で学習した内容は次のとおりです。

* 機械学習モデルを生成するストアド プロシージャを作成する
* データベース テーブルにモデルを格納する
* モデルを使用して予測を行うストアド プロシージャを作成する
* 新しいデータでモデルを実行する

Machine Learning Services における R の使用について詳しくは、以下を参照してください。

* [単純な R スクリプトを実行する](quickstart-r-create-script.md)
* [R データ構造体、型、およびオブジェクト](quickstart-r-data-types-and-objects.md)
* [R 関数](quickstart-r-functions.md)
