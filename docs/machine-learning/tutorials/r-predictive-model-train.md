---
title: チュートリアル:R で予測モデルをトレーニングおよび比較する
titleSuffix: SQL machine learning
description: この 4 部構成のチュートリアル シリーズのパート 3 では、SQL 機械学習を使用して R で 2 つの予測モデルを開発してから、最も正確なモデルを選択します。
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.reviewer: garye, davidph
ms.date: 05/21/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 597cbdc270c902b6c13f17b6fe66a369357a539d
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870305"
---
# <a name="tutorial-create-a-predictive-model-in-r-with-sql-machine-learning"></a>チュートリアル:SQL 機械学習を使用して R で予測モデルを作成する
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズのパート 3 では、R で予測モデルをトレーニングします。このシリーズの次のパートでは、Machine Learning Services またはビッグ データ クラスターを使用して、このモデルを SQL Server データベースにデプロイします。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズのパート 3 では、R で予測モデルをトレーニングします。このシリーズの次のパートでは、Machine Learning Services を使用して、このモデルを SQL Server データベースにデプロイします。
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズのパート 3 では、R で予測モデルをトレーニングします。このシリーズの次のパートでは、SQL Server R Services を使用して、このモデルをデータベースにデプロイします。
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズのパート 3 では、R で予測モデルをトレーニングします。このシリーズの次のパートでは、Machine Learning Services を使用して、このモデルを Azure SQL Managed Instance データベースにデプロイします。
::: moniker-end

この記事では、次の方法について学習します。

> [!div class="checklist"]
> * 2 つの機械学習モデルをトレーニングする
> * 両方のモデルで予測を行う
> * 結果を比較して最も正確なモデルを選択する

[第 1 部](r-predictive-model-introduction.md)では、サンプル データベースを復元する方法を学習しました。

[パート 2](r-predictive-model-prepare-data.md) では、データベースから Python データ フレームにデータを読み込み、R でデータを準備する方法を学習しました。

[パート 4](r-predictive-model-deploy.md) では、モデルをデータベースに格納した後、パート 2 と 3 で開発した Python スクリプトからストアド プロシージャを作成する方法について学習します。 ストアド プロシージャは、新しいデータに基づいて予測を行うためにサーバーで実行されます。

## <a name="prerequisites"></a>前提条件

このチュートリアル シリーズのパート 3 は、[**パート 1**](r-predictive-model-introduction.md)の前提条件を満たし、[**パート 2**](r-predictive-model-prepare-data.md)の手順を完了していることを前提としています。

## <a name="train-two-models"></a>2 つのモデルをトレーニングする

スキー レンタル データに最適なモデルを見つけるために、2 つの異なるモデル (線形回帰とデシジョン ツリー) を作成し、どちらの予測がより正確であるかを調べます。 このシリーズのパート 1 で作成したデータ フレーム `rentaldata` を使用します。

```r
#First, split the dataset into two different sets:
# one for training the model and the other for validating it
train_data = rentaldata[rentaldata$Year < 2015,];
test_data  = rentaldata[rentaldata$Year == 2015,];


#Use the RentalCount column to check the quality of the prediction against actual values
actual_counts <- test_data$RentalCount;

#Model 1: Use lm to create a linear regression model, trained with the training data set
model_lm <- lm(RentalCount ~  Month + Day + WeekDay + Snow + Holiday, data = train_data);

#Model 2: Use rpart to create a decision tree model, trained with the training data set
library(rpart);
model_rpart  <- rpart(RentalCount ~ Month + Day + WeekDay + Snow + Holiday, data = train_data);
```

## <a name="make-predictions-from-both-models"></a>両方のモデルで予測を行う

予測関数を使用し、トレーニング済みの各モデルを使ってレンタル数を予測します。

```r
#Use both models to make predictions using the test data set.
predict_lm <- predict(model_lm, test_data)
predict_lm <- data.frame(RentalCount_Pred = predict_lm, RentalCount = test_data$RentalCount, 
                         Year = test_data$Year, Month = test_data$Month,
                         Day = test_data$Day, Weekday = test_data$WeekDay,
                         Snow = test_data$Snow, Holiday = test_data$Holiday)

predict_rpart  <- predict(model_rpart,  test_data)
predict_rpart <- data.frame(RentalCount_Pred = predict_rpart, RentalCount = test_data$RentalCount, 
                         Year = test_data$Year, Month = test_data$Month,
                         Day = test_data$Day, Weekday = test_data$WeekDay,
                         Snow = test_data$Snow, Holiday = test_data$Holiday)

#To verify it worked, look at the top rows of the two prediction data sets.
head(predict_lm);
head(predict_rpart);
```

```results
    RentalCount_Pred  RentalCount  Month  Day  WeekDay  Snow  Holiday
1         27.45858          42       2     11     4      0       0
2        387.29344         360       3     29     1      0       0
3         16.37349          20       4     22     4      0       0
4         31.07058          42       3      6     6      0       0
5        463.97263         405       2     28     7      1       0
6        102.21695          38       1     12     2      1       0
    RentalCount_Pred  RentalCount  Month  Day  WeekDay  Snow  Holiday
1          40.0000          42       2     11     4      0       0
2         332.5714         360       3     29     1      0       0
3          27.7500          20       4     22     4      0       0
4          34.2500          42       3      6     6      0       0
5         645.7059         405       2     28     7      1       0
6          40.0000          38       1     12     2      1       0
```

## <a name="compare-the-results"></a>結果を比較する

次に、どちらのモデルで最善の予測が得られるかを調べます。 これを行うための迅速で簡単な方法は、基本的なプロット関数を使用して、トレーニング データの実際の値と予測値の差を表示することです。

```r
#Use the plotting functionality in R to visualize the results from the predictions
par(mfrow = c(1, 1));
plot(predict_lm$RentalCount_Pred - predict_lm$RentalCount, main = "Difference between actual and predicted. lm")
plot(predict_rpart$RentalCount_Pred  - predict_rpart$RentalCount,  main = "Difference between actual and predicted. rpart")
```

![2 つのモデルを比較する](./media/compare-models.png)

2 つのモデルのうち、デシジョン ツリー モデルの方がより正確であるように見えます。

## <a name="clean-up-resources"></a>リソースをクリーンアップする

このチュートリアルを続行しない場合は、TutorialDB データベースを削除してください。

## <a name="next-steps"></a>次のステップ

このチュートリアル シリーズのパート 3 で学習した内容は次のとおりです。

* 2 つの機械学習モデルをトレーニングする
* 両方のモデルで予測を行う
* 結果を比較して最も正確なモデルを選択する

作成した機械学習モデルをデプロイするには、このチュートリアル シリーズのパート 4 の手順に従います。

> [!div class="nextstepaction"]
> [SQL 機械学習を使用して R で予測モデルをデプロイする](r-predictive-model-deploy.md)
