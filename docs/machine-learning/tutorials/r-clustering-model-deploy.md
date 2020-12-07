---
title: チュートリアル:R でクラスタリング モデルをデプロイする
titleSuffix: SQL machine learning
description: この 4 部構成のチュートリアル シリーズのパート 4 では、SQL 機械学習を使用して R でクラスタリング モデルをデプロイします。
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.reviewer: garye, davidph
ms.date: 05/21/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 62b4f2d934a8591063e7c14ada914ac3a556866a
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870295"
---
# <a name="tutorial-deploy-a-clustering-model-in-r-with-sql-machine-learning"></a>チュートリアル:SQL 機械学習を使用して R でクラスタリング モデルをデプロイする
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズのパート 4 では、SQL Server Machine Learning Services またはビッグ データ クラスターを使用して、R で開発されたクラスタリング モデルをデータベースにデプロイします。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズのパート 4 では、SQL Server Machine Learning Services を使用して、R で開発されたクラスタリング モデルをデータベースにデプロイします。
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズのパート 4 では、SQL Server R Services を使用して、R で開発されたクラスタリング モデルをデータベースにデプロイします。
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズのパート 4 では、Azure SQL Managed Instance Machine Learning Services を使用して、R で開発されたクラスタリング モデルをデータベースにデプロイします。
::: moniker-end

新しい顧客が登録する際、クラスタリングを定期的に実行するには、どのアプリからでも R スクリプトを呼び出せる必要があります。 これを行うには、SQL ストアド プロシージャ内に R スクリプトを配置して、データベースに R スクリプトをデプロイします。 モデルはデータベースで実行されるため、データベースに格納されているデータに対して、容易にトレーニングできます。

この記事では、次の方法について学習します。

> [!div class="checklist"]
> * モデルを生成するストアド プロシージャの作成
> * クラスタリングを実行する
> * クラスタリング情報の使用

[パート 1 ](r-clustering-model-introduction.md)では、前提条件をインストールしてサンプル データベースを復元しました。

[パート 2 ](r-clustering-model-prepare-data.md)では、データベースからデータを準備してクラスタリングを実行する方法を学びました。

[パート 3 ](r-clustering-model-build.md)では、R で K-Means クラスタリング モデルを作成し、トレーニングする方法を学びました。

## <a name="prerequisites"></a>前提条件

* このチュートリアル シリーズのパート 4 は、[**パート 1**](r-clustering-model-introduction.md)の前提条件を満たし、[**パート 2**](r-clustering-model-build.md)および [**パート 3**](r-clustering-model-build.md)の手順を完了していることを前提としています。

## <a name="create-a-stored-procedure-that-generates-the-model"></a>モデルを生成するストアド プロシージャの作成

以下の T-SQL スクリプトを実行して、ストアド プロシージャを作成します。 このプロシージャにより、このチュートリアル シリーズのパート 2 と 3 で行われた手順が再度実行されます。

* 購入・返却履歴に基づく顧客の分類
* K-Means アルゴリズムを使用した、4 つの顧客クラスターの生成

このプロシージャにより、結果として作成された顧客のクラスター マッピングがデータベース テーブル **customer_return_clusters** に格納されます。

```sql
USE [tpcxbb_1gb]
DROP PROC IF EXISTS generate_customer_return_clusters;
GO
CREATE procedure [dbo].[generate_customer_return_clusters]
AS
/*
  This procedure uses R to classify customers into different groups
  based on their purchase & return history.
*/
BEGIN
    DECLARE @duration FLOAT
    , @instance_name NVARCHAR(100) = @@SERVERNAME
    , @database_name NVARCHAR(128) = db_name()
-- Input query to generate the purchase history & return metrics
    , @input_query NVARCHAR(MAX) = N'
SELECT ss_customer_sk AS customer,
    round(CASE 
            WHEN (
                    (orders_count = 0)
                    OR (returns_count IS NULL)
                    OR (orders_count IS NULL)
                    OR ((returns_count / orders_count) IS NULL)
                    )
                THEN 0.0
            ELSE (cast(returns_count AS NCHAR(10)) / orders_count)
            END, 7) AS orderRatio,
    round(CASE 
            WHEN (
                    (orders_items = 0)
                    OR (returns_items IS NULL)
                    OR (orders_items IS NULL)
                    OR ((returns_items / orders_items) IS NULL)
                    )
                THEN 0.0
            ELSE (cast(returns_items AS NCHAR(10)) / orders_items)
            END, 7) AS itemsRatio,
    round(CASE 
            WHEN (
                    (orders_money = 0)
                    OR (returns_money IS NULL)
                    OR (orders_money IS NULL)
                    OR ((returns_money / orders_money) IS NULL)
                    )
                THEN 0.0
            ELSE (cast(returns_money AS NCHAR(10)) / orders_money)
            END, 7) AS monetaryRatio,
    round(CASE 
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
    ) returned ON ss_customer_sk = sr_customer_sk
 '
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N'
# Define the connection string

connStr <- paste("Driver=SQL Server; Server=", instance_name,
                 "; Database=", database_name,
                 "; uid=Username;pwd=Password; ",
                 sep="" )

# Input customer data that needs to be classified.
# This is the result we get from the query.
library(RODBC)

ch <- odbcDriverConnect(connStr);

customer_data <- sqlQuery(ch, input_query)

sqlDrop(ch, "customer_return_clusters")

## create clustering model
clust <- kmeans(customer_data[,2:5],4)

## create clustering output for table
customer_cluster <- data.frame(cluster=clust$cluster,customer=customer_data$customer,orderRatio=customer_data$orderRatio,
            itemsRatio=customer_data$itemsRatio,monetaryRatio=customer_data$monetaryRatio,frequency=customer_data$frequency)

## write cluster output to DB table
sqlSave(ch, customer_cluster, tablename = "customer_return_clusters")

## clean up
odbcClose(ch)
'
    , @input_data_1 = N''
    , @params = N'@instance_name nvarchar(100), @database_name nvarchar(128), @input_query nvarchar(max), @duration float OUTPUT'
    , @instance_name = @instance_name
    , @database_name = @database_name
    , @input_query = @input_query
    , @duration = @duration OUTPUT;
END;

GO
```

## <a name="perform-clustering"></a>クラスタリングを実行する

ストアド プロシージャを作成したところで、次のスクリプトを実行してクラスタリングを実行します。

```sql
--Empty table of the results before running the stored procedure
TRUNCATE TABLE customer_return_clusters;

--Execute the clustering
--This will load the table customer_return_clusters with cluster mappings
EXECUTE [dbo].[generate_customer_return_clusters];
```

それが動作することと、実際に顧客とそのクラスター マッピングの一覧が表示されていることを確認します。

```sql
--Select data from table customer_return_clusters
--to verify that the clustering data was loaded
SELECT TOP (5) *
FROM customer_return_clusters;
```

```result
cluster  customer  orderRatio  itemsRatio  monetaryRatio  frequency
1        29727     0           0           0              0
4        26429     0           0           0.041979       1
2        60053     0           0           0.065762       3
2        97643     0           0           0.037034       3
2        32549     0           0           0.031281       4
```

## <a name="use-the-clustering-information"></a>クラスタリング情報の使用

クラスタリングのプロシージャはデータベースに格納されているため、同じデータベースに格納されている顧客データに対し、効率的にクラスタリングを実行できます。 顧客データが更新されるたびにプロシージャを実行し、更新されたクラスタリング情報を利用できます。

たとえば、クラスター 0 (非アクティブなグループ) の顧客にプロモーションメールを送るとします (本チュートリアルの[第 3 部](r-clustering-model-build.md#analyze-the-results)で 4 つのクラスターについて説明しています)。 以下のコードは、クラスター 0 の顧客のメール アドレスを選択します。

```sql
USE [tpcxbb_1gb]
--Get email addresses of customers in cluster 0 for a promotion campaign
SELECT customer.[c_email_address], customer.c_customer_sk
  FROM dbo.customer
  JOIN
  [dbo].[customer_clusters] as c
  ON c.Customer = customer.c_customer_sk
  WHERE c.cluster = 0
```

**c. cluster** 値を変更して、他のクラスターの顧客のメール アドレスを返すことができます。

## <a name="clean-up-resources"></a>リソースをクリーンアップする

このチュートリアルの終了後は、tpcxbb_1gb データベースを削除してかまいません。

## <a name="next-steps"></a>次のステップ

このチュートリアル シリーズのパート 4 で学習した内容は次のとおりです。

* モデルを生成するストアド プロシージャの作成
* SQL 機械学習でクラスタリングを実行する
* クラスタリング情報の使用

Machine Learning Services における R の使用について詳しくは、以下を参照してください。

* [単純な R スクリプトを実行する](quickstart-r-create-script.md)
* [R データ構造体、型、およびオブジェクト](quickstart-r-data-types-and-objects.md)
* [R 関数](quickstart-r-functions.md)
