---
title: Python のチュートリアル:データを準備する
titleSuffix: SQL machine learning
description: この 4 部構成のチュートリアル シリーズの第 2 部では、Python を使用して、SQL 機械学習によりスキー レンタルを予測するデータを準備します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/26/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 07b2cf5a77199f64d89d8dd61f8ec89268d759c5
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2020
ms.locfileid: "88173409"
---
# <a name="python-tutorial-prepare-data-to-train-a-linear-regression-model-with-sql-machine-learning"></a>Python のチュートリアル:SQL 機械学習で線形回帰モデルをトレーニングするためのデータを準備する
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズの第 2 部では、Python を使用してデータベースからデータを準備します。 このシリーズの後半では、本データを使用して、ビッグ データ クラスター上の SQL Server Machine Learning Services を使用して Python で線形回帰モデルをトレーニングし、デプロイします。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズの第 2 部では、Python を使用してデータベースからデータを準備します。 このシリーズの後半では、本データを使用して、SQL Server Machine Learning Services とともに Python で線形回帰モデルをトレーニングし、デプロイします。
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズの第 2 部では、Python を使用してデータベースからデータを準備します。 このシリーズの後半では、本データを使用して、Azure SQL Managed Instance Machine Learning Services とともに Python で線形回帰モデルをトレーニングし、デプロイします。
::: moniker-end

この記事では、次の方法について学習します。

> [!div class="checklist"]
> * データベースから **pandas**データ フレームにデータを読み込む
> * いくつかの列を削除して Python でデータを準備する

[第 1 部](python-ski-rental-linear-regression.md)では、サンプル データベースを復元する方法を学習しました。

[パート 3](python-ski-rental-linear-regression-train-model.md) では、Python で線形回帰機械学習モデルをトレーニングする方法について学習します。

[第 4 部](python-ski-rental-linear-regression-deploy-model.md)では、モデルをデータベースに格納した後、第 2 部と 3 部で開発した Python スクリプトからストアド プロシージャを作成する方法について学習します。 ストアド プロシージャは、新しいデータに基づいて予測を行うためにサーバーで実行されます。

## <a name="prerequisites"></a>前提条件

* このチュートリアルのパート 2 は、[パート 1](python-ski-rental-linear-regression.md) とその前提条件を完了していることを前提としています。

## <a name="explore-and-prepare-the-data"></a>データの探索と準備

Python でデータを使用するために、データベースから、pandas データ フレームにデータを読み込みます。

Azure Data Studio で新しい Python notebook を作成し、次のスクリプトを実行します。 

次の Python スクリプトでは、データベースの **dbo.rental_data** テーブルから、データセットを pandas データ フレーム **df** にインポートします。

接続文字列で、必要に応じて接続の詳細を置き換えます。

```python
import pyodbc
import pandas
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error

# Connection string to your SQL Server instance
conn_str = pyodbc.connect('DRIVER={ODBC Driver 17 for SQL Server}; SERVER=<server>; DATABASE=TutorialDB;UID=<username>;PWD=<password>)

query_str = 'SELECT Year, Month, Day, Rentalcount, Weekday, Holiday, Snow FROM dbo.rental_data'

df = pandas.read_sql(sql=query_str, con=conn_str)

print("Data frame:", df)

# Get all the columns from the dataframe.
columns = df.columns.tolist()

# Filter the columns to remove ones we don't want to use in the training
columns = [c for c in columns if c not in ["Year"]]
```

次のような結果が表示されます。

```results
Data frame:      Year  Month  Day  RentalCount  WeekDay  Holiday  Snow
0    2014      1   20          445        2        1     0
1    2014      2   13           40        5        0     0
2    2013      3   10          456        1        0     0
3    2014      3   31           38        2        0     0
4    2014      4   24           23        5        0     0
..    ...    ...  ...          ...      ...      ...   ...
448  2013      2   19           57        3        0     1
449  2015      3   18           26        4        0     0
450  2015      3   24           29        3        0     1
451  2014      3   26           50        4        0     1
452  2015     12    6          377        1        0     1

[453 rows x 7 columns]
```

## <a name="next-steps"></a>次のステップ

このチュートリアル シリーズの第 2 部では、次の手順を完了しました。

* データベースから **pandas**データ フレームにデータを読み込む
* いくつかの列を削除して Python でデータを準備する

TutorialDB データベースのデータを使用する機械学習モデルをトレーニングするには、このチュートリアル シリーズのパート 3 に従ってください。

> [!div class="nextstepaction"]
> [Python のチュートリアル:線形回帰モデルをトレーニングする](python-ski-rental-linear-regression-train-model.md)