---
title: チュートリアル:R でクラスタリングを実行するためのデータを準備する
titleSuffix: SQL machine learning
description: この 4 部構成のチュートリアル シリーズのパート 2 では、SQL 機械学習を使用して R でクラスタリングを実行するために、データベースからデータを準備します。
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.reviewer: garye, davidph
ms.date: 05/21/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 1c6bf16d51d0180b56007f237001d01cedfecf8d
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870281"
---
# <a name="tutorial-prepare-data-to-perform-clustering-in-r-with-sql-machine-learning"></a>チュートリアル:SQL 機械学習を使用して R でクラスタリングを実行するためのデータを準備する
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズのパート 2 では、SQL Server Machine Learning Services を使用して、またはビッグ データ クラスターで R でクラスタリングを実行するために、データベースからデータを準備します。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズのパート 2 では、SQL Server Machine Learning Services を使用して R でクラスタリングを実行するために、データベースからデータを準備します。
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズのパート 2 では、SQL Server 2016 R Services を使用して R でクラスタリングを実行するために、データベースからデータを準備します。
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズのパート 2 では、Azure SQL Managed Instance の Machine Learning Services を使用して R でクラスタリングを実行するために、データベースからデータを準備します。
::: moniker-end

この記事では、次の方法について学習します。

> [!div class="checklist"]
> * R を使用してさまざまな特徴に従って顧客を分類する
> * データベースから R データ フレームにデータを読み込む

[パート 1 ](r-clustering-model-introduction.md)では、前提条件をインストールしてサンプル データベースを復元しました。

[パート 3 ](r-clustering-model-build.md)では、R で K-Means クラスタリング モデルを作成し、トレーニングする方法を学びます。

[パート 4](r-clustering-model-deploy.md) では、新しいデータに基づいて R でクラスタリングを実行できるストアド プロシージャをデータベースに作成する方法について学びます。

## <a name="prerequisites"></a>前提条件

* このチュートリアルのパート 2 は、[**パート 1**](r-clustering-model-introduction.md) を完了していることを前提としています。

## <a name="separate-customers"></a>顧客を分離する

RStudio で新しい RScript ファイルを作成し、以下のスクリプトを実行します。
SQL クエリで、次の特徴に従って顧客を分類しています。

* **orderRatio** = 注文返品率 (注文の総数に対する部分的または完全に返品された注文の総数)
* **itemsRatio** = アイテム返品率 (購入されたアイテムの総数に対する返品されたアイテムの総数)
* **monetaryRatio** = 返品金額率 (合計購入金額に対する返されたアイテムの合計金額)
* **frequency** = 返品の頻度

**connStr** 関数では、**ServerName** を実際の接続情報に置き換えます。

```r
# Define the connection string to connect to the tpcxbb_1gb database

connStr <- "Driver=SQL Server;Server=ServerName;Database=tpcxbb_1gb;uid=Username;pwd=Password"

#Define the query to select data
input_query <- "
SELECT ss_customer_sk AS customer
    ,round(CASE 
            WHEN (
                       (orders_count = 0)
                    OR (returns_count IS NULL)
                    OR (orders_count IS NULL)
                    OR ((returns_count / orders_count) IS NULL)
                    )
                THEN 0.0
            ELSE (cast(returns_count AS NCHAR(10)) / orders_count)
            END, 7) AS orderRatio
    ,round(CASE 
            WHEN (
                     (orders_items = 0)
                  OR (returns_items IS NULL)
                  OR (orders_items IS NULL)
                  OR ((returns_items / orders_items) IS NULL)
                 )
            THEN 0.0
            ELSE (cast(returns_items AS NCHAR(10)) / orders_items)
            END, 7) AS itemsRatio
    ,round(CASE 
            WHEN (
                     (orders_money = 0)
                  OR (returns_money IS NULL)
                  OR (orders_money IS NULL)
                  OR ((returns_money / orders_money) IS NULL)
                 )
            THEN 0.0
            ELSE (cast(returns_money AS NCHAR(10)) / orders_money)
            END, 7) AS monetaryRatio
    ,round(CASE 
            WHEN (returns_count IS NULL)
            THEN 0.0
            ELSE returns_count
            END, 0) AS frequency
FROM (
    SELECT ss_customer_sk,
        -- return order ratio
        COUNT(DISTINCT (ss_ticket_number)) AS orders_count,
        -- return ss_item_sk ratio
        COUNT(ss_item_sk) AS orders_items,
        -- return monetary amount ratio
        SUM(ss_net_paid) AS orders_money
    FROM store_sales s
    GROUP BY ss_customer_sk
    ) orders
LEFT OUTER JOIN (
    SELECT sr_customer_sk,
        -- return order ratio
        count(DISTINCT (sr_ticket_number)) AS returns_count,
        -- return ss_item_sk ratio
        COUNT(sr_item_sk) AS returns_items,
        -- return monetary amount ratio
        SUM(sr_return_amt) AS returns_money
    FROM store_returns
    GROUP BY sr_customer_sk
    ) returned ON ss_customer_sk = sr_customer_sk";
```

## <a name="load-the-data-into-a-data-frame"></a>データをデータ フレームに読み込む

ここで、次のスクリプトを使用すると、クエリの結果が R データ フレームに返されます。

```r
# Query using input_query and get the results back
# to data frame customer_data

library(RODBC)

ch <- odbcDriverConnect(connStr)

customer_data <- sqlQuery(ch, input_query)

# Take a look at the data just loaded
head(customer_data, n = 5);
```

次のような結果が表示されます。

```results
  customer orderRatio itemsRatio monetaryRatio frequency
1    29727          0          0      0.000000         0
2    26429          0          0      0.041979         1
3    60053          0          0      0.065762         3
4    97643          0          0      0.037034         3
5    32549          0          0      0.031281         4
```

## <a name="clean-up-resources"></a>リソースをクリーンアップする

このチュートリアルを続行しない場合は、tpcxbb_1gb データベースを削除してください。

## <a name="next-steps"></a>次のステップ

このチュートリアル シリーズのパート 2 で学習した内容は次のとおりです。

* R を使用してさまざまな特徴に従って顧客を分類する
* データベースから R データ フレームにデータを読み込む

顧客データを使用する機械学習モデルをトレーニングするには、このチュートリアル シリーズの第 3 部に従ってください。

> [!div class="nextstepaction"]
> [SQL 機械学習を使用して R で予測モデルを作成する](r-clustering-model-build.md)
