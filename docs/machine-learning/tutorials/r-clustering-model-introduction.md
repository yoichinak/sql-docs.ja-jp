---
title: チュートリアル:R でクラスタリング モデルを開発する
titleSuffix: SQL Machine Learning
description: この 4 部構成のチュートリアル シリーズでは、SQL 機械学習を使用して R でクラスタリングを実行するためにモデルを開発します。
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.reviewer: garye, davidph
ms.date: 05/26/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 8ee1d60eb9af4232957ff9c1a7df4b976366513f
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870334"
---
# <a name="tutorial-develop-a-clustering-model-in-r-with-sql-machine-learning"></a>チュートリアル:SQL 機械学習を使用して R でクラスタリング モデルを開発する
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズでは、R を使用して、[ビッグ データ クラスター](../../big-data-cluster/machine-learning-services.md)上の [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) で K-Means クラスタリング モデルを開発および展開して、顧客データを分類します。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズでは、R を使用して、[SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) で K-Means クラスタリング モデルを開発および展開して、顧客データをクラスター化します。
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズでは、R を使用して、[SQL Server R Services](../r/sql-server-r-services.md) で K-Means クラスタリング モデルを開発および展開して、顧客データをクラスター化します。
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズでは、R を使用して、「[Azure SQL Managed Instance の Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview)」で K-Means クラスタリング モデルを開発およびデプロイして、顧客データをクラスター化します。
::: moniker-end

このシリーズの第 1 部では、チュートリアルの前提条件を設定してから、サンプル データセットをデータベースに復元します。 第 2 部と第 3 部では、Azure Data Studio ノートブックでいくつかの R スクリプトを開発して、このサンプル データを準備し、機械学習モデルをトレーニングします。 その後、第 4 部では、ストアド プロシージャを使用してデータベース内でそれらの R スクリプトを実行します。

*クラスター化* は、グループのメンバーにある意味で類似点があるグループにデータを編成すること、として説明できます。 このチュートリアル シリーズでは、小売事業を営んでいる場合を想定しています。 **K-Means** アルゴリズムを使用して、製品の購入と返品のデータセット内で、顧客のクラスタリングを実行します。 顧客をクラスタリングすることで、特定のグループをターゲットして、マーケティングの取り組みをより効果的に進めることができます。 K-Means クラスタリングは、類似性に基づいてデータのパターンを探す *教師なし学習* アルゴリズムです。

この記事では、次の方法について学習します。

> [!div class="checklist"]
> * サンプル データベースを復元する

[第 2 部](r-clustering-model-prepare-data.md)では、データベースからデータを準備してクラスタリングを実行する方法を学びます。

[第 3 部](r-clustering-model-build.md)では、R で K-Means クラスタリング モデルを作成し、トレーニングする方法を学びます。

[第 4 部](r-clustering-model-deploy.md)では、新しいデータに基づいて R でクラスタリングを実行できるストアド プロシージャをデータベースに作成する方法について学びます。

## <a name="prerequisites"></a>前提条件

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
* [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) に Python 言語オプションがあること。[Windows インストール ガイド](../install/sql-machine-learning-services-windows-install.md)または [Linux インストール ガイド](../../linux/sql-server-linux-setup-machine-learning.md?toc=%252fsql%252fmachine-learning%252ftoc.json&view=sql-server-linux-ver15&preserve-view=true)に記載されているインストール手順に従ってください。 [SQL Server ビッグ データ クラスターで Machine Learning Services を有効にする](../../big-data-cluster/machine-learning-services.md)こともできます。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
* [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) に R 言語オプションがあること。[Windows インストール ガイド](../install/sql-machine-learning-services-windows-install.md)に記載されているインストール手順に従ってください。
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
* Azure SQL Managed Instance の Machine Learning Services。 詳細については、[Azure SQL Managed Instance の Machine Learning Services の概要](/azure/azure-sql/managed-instance/machine-learning-services-overview)に関するページを参照してください。

* サンプル データベースを Azure SQL Managed Instance に復元するための [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md)。
::: moniker-end

* [Azure Data Studio](../../azure-data-studio/what-is.md) SQL 用の Azure Data Studio では、ノートブックを使用します。 ノードブックの詳細については、「[Azure Data Studio でノートブックを使用する方法](../../azure-data-studio/notebooks/notebooks-guidance.md)」を参照してください。

* R IDE - このチュートリアルでは [RStudio Desktop](https://www.rstudio.com/products/rstudio/download/) を使用します。

* RODBC - このドライバーは、このチュートリアルで開発する R スクリプトで使用します。 まだインストールされていない場合は、R コマンド `install.packages("RODBC")` を使用してインストールします。 RODBC の詳細については、「[CRAN-Package RODBC](https://CRAN.R-project.org/package=RODBC)」を参照してください。

## <a name="restore-the-sample-database"></a>サンプル データベースを復元する

このチュートリアルで使用するサンプル データセットは、ダウンロードして使用できるように **.bak** データベース バックアップ ファイルに保存されています。 このデータセットは、[トランザクション処理性能評議会 (TPC)](http://www.tpc.org/) によって提供される [tpcx-bb](http://www.tpc.org/tpcx-bb/default5.asp) データセットから派生しています。

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
> [!NOTE]
> ビッグ データ クラスターで Machine Learning Services を使用している場合は、[SQL Server ビッグ データ クラスターのマスター インスタンスにデータベースを復元する](../../big-data-cluster/data-ingestion-restore-database.md)方法に関する記事を参照してください。
::: moniker-end

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
1. [tpcxbb_1gb.bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/tpcxbb_1gb.bak) ファイルをダウンロードします。

1. Azure Data Studio で、以下の詳細情報を使用して、「[バックアップ ファイルからデータベースを復元する](../../azure-data-studio/tutorial-backup-restore-sql-server.md#restore-a-database-from-a-backup-file)」に記載されている手順に従います。

   * ダウンロードした **tpcxbb_1gb.bak** ファイルからインポートします
   * ターゲット データベースに "tpcxbb_1gb" という名前を指定します

1. **dbo.customer** テーブルに対してクエリを実行することで、データベースを復元した後にデータセットが存在することを確認できます。

    ```sql
    USE tpcxbb_1gb;
    SELECT * FROM [dbo].[customer];
    ```
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
1. [tpcxbb_1gb.bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/tpcxbb_1gb.bak) ファイルをダウンロードします。

1. 次の詳細を使用して、SQL Server Management Studio で [Managed Instance へのデータベースの復元](/azure/sql-database/sql-database-managed-instance-get-started-restore)の指示に従います。

   * ダウンロードした **tpcxbb_1gb.bak** ファイルからインポートします
   * ターゲット データベースに "tpcxbb_1gb" という名前を指定します

1. **dbo.customer** テーブルに対してクエリを実行することで、データベースを復元した後にデータセットが存在することを確認できます。

    ```sql
    USE tpcxbb_1gb;
    SELECT * FROM [dbo].[customer];
    ```
::: moniker-end

## <a name="clean-up-resources"></a>リソースをクリーンアップする

このチュートリアルを続行しない場合は、tpcxbb_1gb データベースを削除してください。

## <a name="next-steps"></a>次のステップ

このチュートリアル シリーズの第 1 部では、これらの手順を完了しました。

* 必須コンポーネントのインストール
* サンプル データベースの復元

機械学習モデル用にデータを準備するには、このチュートリアル シリーズの第 2 部の手順を実行します。

> [!div class="nextstepaction"]
> [クラスタリングを実行するためのデータを準備する](r-clustering-model-prepare-data.md)