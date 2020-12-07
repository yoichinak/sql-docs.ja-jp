---
title: Python のチュートリアル:クラスター データを準備する
titleSuffix: SQL machine learning
description: この 4 部構成のチュートリアル シリーズの第 2 部では、SQL データを準備し、SQL 機械学習を使用して Python でクラスタリングを実行します。
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 05/21/2020
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 2cd244454b78e1199d59dcfe6539498328eac674
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870445"
---
# <a name="python-tutorial-prepare-data-to-categorize-customers-with-sql-machine-learning"></a>Python のチュートリアル:SQL 機械学習を使用して顧客を分類するデータを準備する
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズの第 2 部では、Python を使用してデータベースからデータを復元して準備します。 このシリーズの後半では、このデータを使用して、ビッグ データ クラスター上の SQL Server Machine Learning Services を使用して Python でクラスタリング モデルをトレーニングし展開します。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズの第 2 部では、Python を使用してデータベースからデータを復元して準備します。 このシリーズの後半では、このデータを使用して、SQL Server Machine Learning Services を使用する Python でクラスタリング モデルをトレーニングし展開します。
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズの第 2 部では、Python を使用してデータベースからデータを復元して準備します。 このシリーズの後半では、本データを使用して、Azure SQL Managed Instance Machine Learning Services とともに Python でクラスタリング モデルをトレーニングし、デプロイします。
::: moniker-end

この記事では、次の方法について学習します。

> [!div class="checklist"]
> * Python を使用して異なるディメンションに沿って顧客を分離する
> * データベースから Python データ フレームにデータを読み込む

[パート 1 ](python-clustering-model.md)では、前提条件をインストールしてサンプル データベースを復元しました。

[第 3 部](python-clustering-model-build.md)では、Python で K-Means クラスタリング モデルを作成し、トレーニングする方法を学びました。

[パート 4 ](python-clustering-model-deploy.md)では、新しいデータに基づいて Python でクラスタリングを実行できるストアド プロシージャをデータベースに作成する方法について説明します。

## <a name="prerequisites"></a>前提条件

* このチュートリアルの第 2 部は、[**第 1 部**](python-clustering-model.md)の前提条件を完了していることを前提としています。

## <a name="separate-customers"></a>顧客を分離する

顧客のクラスタリングを準備するには、まず次のディメンションに従って顧客を分離します。

* **orderRatio** = 注文返品率 (注文の総数に対する部分的または完全に返品された注文の総数)
* **itemsRatio** = アイテム返品率 (購入されたアイテムの総数に対する返品されたアイテムの総数)
* **monetaryRatio** = 返品金額率 (合計購入金額に対する返されたアイテムの合計金額)
* **frequency** = 返品の頻度

Azure Data Studio で新しいノートブックを開き、次のスクリプトを入力します。

接続文字列で、必要に応じて接続の詳細を置き換えます。

```python
# Load packages.
import pyodbc
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
from scipy.spatial import distance as sci_distance
from sklearn import cluster as sk_cluster

################################################################################################

## Connect to DB and select data

################################################################################################

# Connection string to connect to SQL Server named instance.
conn_str = pyodbc.connect('DRIVER={ODBC Driver 17 for SQL Server}; SERVER=<server>; DATABASE=tpcxbb_1gb; UID=<username>; PWD=<password>')

input_query = '''SELECT
ss_customer_sk AS customer,
ROUND(COALESCE(returns_count / NULLIF(1.0*orders_count, 0), 0), 7) AS orderRatio,
ROUND(COALESCE(returns_items / NULLIF(1.0*orders_items, 0), 0), 7) AS itemsRatio,
ROUND(COALESCE(returns_money / NULLIF(1.0*orders_money, 0), 0), 7) AS monetaryRatio,
COALESCE(returns_count, 0) AS frequency
FROM
(
  SELECT
    ss_customer_sk,
    -- return order ratio
    COUNT(distinct(ss_ticket_number)) AS orders_count,
    -- return ss_item_sk ratio
    COUNT(ss_item_sk) AS orders_items,
    -- return monetary amount ratio
    SUM( ss_net_paid ) AS orders_money
  FROM store_sales s
  GROUP BY ss_customer_sk
) orders
LEFT OUTER JOIN
(
  SELECT
    sr_customer_sk,
    -- return order ratio
    count(distinct(sr_ticket_number)) as returns_count,
    -- return ss_item_sk ratio
    COUNT(sr_item_sk) as returns_items,
    -- return monetary amount ratio
    SUM( sr_return_amt ) AS returns_money
FROM store_returns
GROUP BY sr_customer_sk ) returned ON ss_customer_sk=sr_customer_sk'''


# Define the columns we wish to import.
column_info = {
    "customer": {"type": "integer"},
    "orderRatio": {"type": "integer"},
    "itemsRatio": {"type": "integer"},
    "frequency": {"type": "integer"}
}
```

## <a name="load-the-data-into-a-data-frame"></a>データをデータ フレームに読み込む

クエリの結果は、Pandas **read_sql** 関数を使用して Python に返されます。 プロセスの一部として、前のスクリプトで定義した列情報を使用します。

```python
customer_data = pandas.read_sql(input_query, conn_str)
```

次に、データ フレームの先頭を表示して、正しく表示されているかどうかを確認します。

```python
print("Data frame:", customer_data.head(n=5))
```

```results
Rows Read: 37336, Total Rows Processed: 37336, Total Chunk Time: 0.172 seconds
Data frame:     customer  orderRatio  itemsRatio  monetaryRatio  frequency
0    29727.0    0.000000    0.000000       0.000000          0
1    97643.0    0.068182    0.078176       0.037034          3
2    57247.0    0.000000    0.000000       0.000000          0
3    32549.0    0.086957    0.068657       0.031281          4
4     2040.0    0.000000    0.000000       0.000000          0
```

## <a name="clean-up-resources"></a>リソースをクリーンアップする

このチュートリアルを続行しない場合は、tpcxbb_1gb データベースを削除してください。

## <a name="next-steps"></a>次のステップ

このチュートリアル シリーズの第 2 部では、次の手順を完了しました。

* Python を使用して異なるディメンションに沿って顧客を分離する
* データベースから Python データ フレームにデータを読み込む

顧客データを使用する機械学習モデルをトレーニングするには、このチュートリアル シリーズの第 3 部に従ってください。

> [!div class="nextstepaction"]
> [Python のチュートリアル:予測モデルを作成する](python-clustering-model-build.md)
