---
title: チュートリアル:R でクラスタリング モデルを作成する
titleSuffix: SQL machine learning
description: この 4 部構成のチュートリアル シリーズのパート 3 では、SQL 機械学習を使用して R でクラスタリングを実行するために、K-Means モデルをビルドします。
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.reviewer: garye, davidph
ms.date: 05/21/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 62c7a271a7caf3afa588a48c0ac54ef86a38f785
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870338"
---
# <a name="tutorial-build-a-clustering-model-in-r-with-sql-machine-learning"></a>チュートリアル:SQL 機械学習を使用して R でクラスタリング モデルをビルドする
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズのパート 3 では、クラスタリングを実行するために、R で K-Means モデルをビルドします。 このシリーズの次のパートでは、SQL Server Machine Learning Services またはビッグ データ クラスターを使用して、このモデルをデータベースにデプロイします。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズのパート 3 では、クラスタリングを実行するために、R で K-Means モデルをビルドします。 このシリーズの次の部では、SQL Server Machine Learning Services を使用して、このモデルをデータベースにデプロイします。
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズのパート 3 では、クラスタリングを実行するために、R で K-Means モデルをビルドします。 このシリーズの次のパートでは、SQL Server R Services を使用して、このモデルをデータベースにデプロイします。
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズのパート 3 では、クラスタリングを実行するために、R で K-Means モデルをビルドします。 このシリーズの次の部では、Azure SQL Managed Instance Machine Learning Services を使用し、データベースにこのモデルをデプロイします。
::: moniker-end

この記事では、次の方法について学習します。

> [!div class="checklist"]
> * K-Means アルゴリズムのクラスター数を定義する
> * クラスタリングを実行する
> * 結果を分析する

[パート 1 ](r-clustering-model-introduction.md)では、前提条件をインストールしてサンプル データベースを復元しました。

[パート 2 ](r-clustering-model-prepare-data.md)では、データベースからデータを準備してクラスタリングを実行する方法を学びました。

[パート 4 ](r-clustering-model-deploy.md)では、新しいデータに基づいて R でクラスタリングを実行できるストアド プロシージャをデータベースに作成する方法について説明します。

## <a name="prerequisites"></a>前提条件

* このチュートリアル シリーズのパート 3 は、[**パート 1**](r-clustering-model-introduction.md)の前提条件を満たし、[**パート 2**](r-clustering-model-prepare-data.md)の手順を完了していることを前提としています。

## <a name="define-the-number-of-clusters"></a>クラスターの数を定義する

顧客データのクラスター化には、データをグループ化する最も単純かつ有名な方法の 1 つ、**K-Means** クラスタリング アルゴリズムを使用します。
K-Means の詳細については、[K-means クラスタリング アルゴリズムの詳細ガイド](https://www.kdnuggets.com/2019/05/guide-k-means-clustering-algorithm.html)に関するページを参照してください。

このアルゴリズムでは、次の 2 つの入力を受け取ります。データ自体、および定義済みの数値 "*k*" は、生成するクラスターの数を表します。
出力は、クラスター間でパーティション分割された入力データを持つ *k* クラスターとなっています。

アルゴリズムで使用するクラスターの数を決定するには、抽出されたクラスターの数によって、グループ内の平方和のプロットを使用します。 使用するクラスターの数は、プロットの曲がっている部分または "カギ" の部分になります。

```r
# Determine number of clusters by using a plot of the within groups sum of squares,
# by number of clusters extracted. 
wss <- (nrow(customer_data) - 1) * sum(apply(customer_data, 2, var))
for (i in 2:20)
    wss[i] <- sum(kmeans(customer_data, centers = i)$withinss)
plot(1:20, wss, type = "b", xlab = "Number of Clusters", ylab = "Within groups sum of squares")
```

![カギ線グラフ](./media/elbow-graph.png)

グラフに基づいて、*k = 4* の値をまず試します。 *k* 値は、顧客を 4 つのクラスターにグループ化します。

## <a name="perform-clustering"></a>クラスタリングを実行する

次の R スクリプトでは、関数 **kmeans** を使用して、クラスタリングを実行します。

```r
# Output table to hold the customer group mappings.
# Generate clusters using Kmeans and output key / cluster to a table
# called return_cluster

## create clustering model
clust <- kmeans(customer_data[,2:5],4)

## create clustering ouput for table
customer_cluster <- data.frame(cluster=clust$cluster,customer=customer_data$customer,orderRatio=customer_data$orderRatio,
        itemsRatio=customer_data$itemsRatio,monetaryRatio=customer_data$monetaryRatio,frequency=customer_data$frequency)

## write cluster output to DB table
sqlSave(ch, customer_cluster, tablename = "return_cluster")

# Read the customer returns cluster table from the database
customer_cluster_check <- sqlFetch(ch, "return_cluster")

head(customer_cluster_check)
```

## <a name="analyze-the-results"></a>結果を分析する

K-Means を使用してクラスタリングを実行したので、次の手順は、結果を分析してアクションにつながる情報を得られるか確認することです。

```r
#Look at the clustering details to analyze results
clust[-1]
```

```results
$centers
   orderRatio itemsRatio monetaryRatio frequency
1 0.621835791  0.1701519    0.35510836  1.009025
2 0.074074074  0.0000000    0.05886575  2.363248
3 0.004807692  0.0000000    0.04618708  5.050481
4 0.000000000  0.0000000    0.00000000  0.000000

$totss
[1] 40191.83

$withinss
[1] 19867.791   215.714   660.784     0.000

$tot.withinss
[1] 20744.29

$betweenss
[1] 19447.54

$size
[1]  4543   702   416 31675

$iter
[1] 3

$ifault
[1] 0

```

4 つのクラスターは、[パート 2 ](r-clustering-model-prepare-data.md#separate-customers)で定義した変数を使用して指定されます。

* *orderRatio* = 注文返品率 (注文の総数に対する部分的または完全に返品された注文の総数)
* *itemsRatio* = アイテム返品率 (購入されたアイテムの総数に対する返品されたアイテムの総数)
* *monetaryRatio* = 返品金額率 (合計購入金額に対する返されたアイテムの合計金額)
* *frequency* = 返品の頻度

多くの場合、K-Means を使用したデータ マイニングでは結果をさらに詳しく分析し、各クラスターについて理解を深めるためにさらに手順を進める必要がありますが、これにより良いスタートを切ることができるようになります。
これらの結果を解釈するいくつかの方法を次に示します。

* クラスター 1 (もっとも大きいクラスター) はアクティブでない顧客グループであると考えられます (すべての値が 0)。
* クラスター 3 は、戻り値の動作の観点では目立つグループであるように見えます。

## <a name="clean-up-resources"></a>リソースをクリーンアップする

このチュートリアルを続行しない場合は、tpcxbb_1gb データベースを削除してください。

## <a name="next-steps"></a>次のステップ

このチュートリアル シリーズのパート 3 で学習した内容は次のとおりです。

* K-Means アルゴリズムのクラスター数を定義する
* クラスタリングを実行する
* 結果を分析する

作成した機械学習モデルをデプロイするには、このチュートリアル シリーズのパート 4 の手順に従います。

> [!div class="nextstepaction"]
> [SQL 機械学習を使用して R でクラスタリング モデルをデプロイする](r-clustering-model-deploy.md)
