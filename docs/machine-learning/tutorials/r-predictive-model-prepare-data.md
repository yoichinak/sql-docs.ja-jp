---
title: チュートリアル:R で予測モデルをトレーニングするためのデータを準備する
titleSuffix: SQL machine learning
description: この 4 部構成のチュートリアル シリーズのパート 2 では、SQL 機械学習を使用して R で予測モデルをトレーニングするためのデータを準備します。
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.reviewer: garye, davidph
ms.date: 05/21/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: a4a12d71818ad4b900a7959904c47cb0baad4357
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870313"
---
# <a name="tutorial-prepare-data-to-train-a-predictive-model-in-r-with-sql-machine-learning"></a>チュートリアル:SQL 機械学習を使用して R で予測モデルをトレーニングするためのデータを準備する
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズのパート 2 では、R を使用してデータベースからデータを準備します。このシリーズの後半では、このデータを利用し、SQL Server Machine Learning Services またはビッグ データ クラスターを使用して R で予測モデルをトレーニングしてデプロイします。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズのパート 2 では、R を使用してデータベースからデータを準備します。このシリーズの後半では、このデータを利用して、SQL Server Machine Learning Services を使用して R で予測モデルをトレーニングしてデプロイします。
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズのパート 2 では、R を使用してデータベースからデータを準備します。このシリーズの後半では、このデータを利用して、SQL Server R Services を使用して R で予測モデルをトレーニングしてデプロイします。
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズのパート 2 では、R を使用してデータベースからデータを準備します。このシリーズの後半では、このデータを利用して、Azure SQL Managed Instance の Machine Learning Services で R の予測モデルのトレーニングおよびデプロイを行います。
::: moniker-end

この記事では、次の方法について学習します。

> [!div class="checklist"]
> * サンプル データベースをデータベースに復元する
> * データベースから R データ フレームにデータを読み込む
> * R でカテゴリとしていくつかの列を識別してデータを準備する

[第 1 部](r-predictive-model-introduction.md)では、サンプル データベースを復元する方法を学習しました。

[パート 3](r-predictive-model-train.md) では、R で機械学習モデルをトレーニングする方法について学習します。

[パート 4](r-predictive-model-deploy.md) では、モデルをデータベースに格納した後、パート 2 と 3 で開発した R スクリプトからストアド プロシージャを作成する方法について学習します。 ストアド プロシージャは、新しいデータに基づいて予測を行うためにサーバーで実行されます。

## <a name="prerequisites"></a>前提条件

このチュートリアルのパート 2 では、[**パート 1**](r-predictive-model-introduction.md) とその前提条件を完了していることを前提としています。

## <a name="load-the-data-into-a-data-frame"></a>データをデータ フレームに読み込む

R でデータを使用するには、データベースからデータ フレーム (`rentaldata`) にデータを読み込みます。

RStudio で新しい RScript ファイルを作成し、以下のスクリプトを実行します。 **ServerName** を実際の接続情報に置き換えます。

```r
#Define the connection string to connect to the TutorialDB database
connStr <- "Driver=SQL Server;Server=ServerName;Database=TutorialDB;uid=Username;pwd=Password"


#Get the data from the table
library(RODBC)

ch <- odbcDriverConnect(connStr)

#Import the data from the table
rentaldata <- sqlFetch(ch, "dbo.rental_data")

#Take a look at the structure of the data and the top rows
head(rentaldata)
str(rentaldata)
```

次のような結果が表示されます。

```results
   Year  Month  Day  RentalCount  WeekDay  Holiday  Snow
1  2014    1     20      445         2        1      0
2  2014    2     13       40         5        0      0
3  2013    3     10      456         1        0      0
4  2014    3     31       38         2        0      0
5  2014    4     24       23         5        0      0
6  2015    2     11       42         4        0      0
'data.frame':       453 obs. of  7 variables:
$ Year       : int  2014 2014 2013 2014 2014 2015 2013 2014 2013 2015 ...
$ Month      : num  1 2 3 3 4 2 4 3 4 3 ...
$ Day        : num  20 13 10 31 24 11 28 8 5 29 ...
$ RentalCount: num  445 40 456 38 23 42 310 240 22 360 ...
$ WeekDay    : num  2 5 1 2 5 4 1 7 6 1 ...
$ Holiday    : int  1 0 0 0 0 0 0 0 0 0 ...
$ Snow       : num  0 0 0 0 0 0 0 0 0 0 ...
```

## <a name="prepare-the-data"></a>データを準備する

このサンプル データベースでは、ほとんどの準備が既に行われていますが、ここでもう 1 つ準備を行います。
以下の R スクリプトを使用して、データ型を "*因子*" に変更し、"*カテゴリ*" として 3 つの列を識別します。



```r
#Changing the three factor columns to factor types
rentaldata$Holiday <- factor(rentaldata$Holiday);
rentaldata$Snow    <- factor(rentaldata$Snow);
rentaldata$WeekDay <- factor(rentaldata$WeekDay);



#Visualize the dataset after the change
str(rentaldata);
```

次のような結果が表示されます。

```results
data.frame':      453 obs. of  7 variables:
$ Year       : int  2014 2014 2013 2014 2014 2015 2013 2014 2013 2015 ...
$ Month      : num  1 2 3 3 4 2 4 3 4 3 ...
$ Day        : num  20 13 10 31 24 11 28 8 5 29 ...
$ RentalCount: num  445 40 456 38 23 42 310 240 22 360 ...
$ WeekDay    : Factor w/ 7 levels "1","2","3","4",..: 2 5 1 2 5 4 1 7 6 1 ...
$ Holiday    : Factor w/ 2 levels "0","1": 2 1 1 1 1 1 1 1 1 1 ...
$ Snow       : Factor w/ 2 levels "0","1": 1 1 1 1 1 1 1 1 1 1 ...
```

これで、トレーニングのためのデータの準備ができました。

## <a name="clean-up-resources"></a>リソースをクリーンアップする

このチュートリアルを続行しない場合は、TutorialDB データベースを削除してください。

## <a name="next-steps"></a>次のステップ

このチュートリアル シリーズのパート 2 で学習した内容は次のとおりです。

* R データ フレームにサンプル データを読み込む
* R でカテゴリとしていくつかの列を識別してデータを準備する

TutorialDB データベースのデータを使用する機械学習モデルを作成するには、このチュートリアル シリーズのパート 3 に従ってください。

> [!div class="nextstepaction"]
> [SQL 機械学習を使用して R で予測モデルを作成する](r-predictive-model-train.md)
