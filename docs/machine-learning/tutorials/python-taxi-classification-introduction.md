---
title: Python のチュートリアル:二項分類を使用して NYC タクシーの料金を予測する
titleSuffix: SQL machine learning
description: この 5 部構成のチュートリアル シリーズでは、二項分類を使用して NYC タクシーの料金を予測するために、SQL 機械学習を使用して SQL Server ストアド プロシージャと T-SQL 関数に Python コードを埋め込む方法について説明します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/28/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||>=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 7b8e0e8df7bd2a5453299751df682e0c33502c25
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2020
ms.locfileid: "94585074"
---
# <a name="python-tutorial-predict-nyc-taxi-fares-with-binary-classification"></a>Python のチュートリアル:二項分類を使用して NYC タクシーの料金を予測する
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
SQL プログラマー向けのこの 5 部構成のチュートリアル シリーズでは、[SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) または[ビッグ データ クラスター](../../big-data-cluster/machine-learning-services.md)での Python 統合について説明します。
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
SQL プログラマー向けのこの 5 部構成のチュートリアル シリーズでは、[SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) での Python 統合について説明します。
::: moniker-end

::: moniker range=">=azuresqldb-mi-current||=sqlallproducts-allversions"
SQL プログラマー向けのこの 5 部構成のチュートリアル シリーズでは、[Azure SQL Managed Instance の Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview) での Python 統合について説明します。
::: moniker-end

SQL Server でサンプル データベースを使用して、Python ベースの機械学習ソリューションをビルドしてデプロイします。 T-SQL、Azure Data Studio または SQL Server Management Studio、およびデータベース インスタンスを SQL 機械学習と Python 言語サポートと共に使用します。

このチュートリアル シリーズでは、データ モデリング ワークフローで使用される Python 関数について説明します。 各回には、データの探索、二項分類モデルの構築とトレーニング、モデル デプロイが含まれます。 New York City Taxi and Limousine Commission (ニューヨーク市タクシー & リムジン協会) のサンプル データを使用します。 構築するモデルは、旅行が、時間、移動距離、乗車位置に基づいたヒントを生成する可能性があるかどうかを予測します。

このシリーズの第 1 回では、前提条件をインストールし、サンプル データベースを復元します。 第 2 回と 3 回では、いくつかの Python スクリプトを開発して、データを準備し、機械学習モデルをトレーニングします。 次の第 4 回と 5 回では、T-SQL ストアド プロシージャを使用して、データベース内でこれらの Python スクリプトを実行します。

この記事では、次のことを行います。

> [!div class="checklist"]
> + 必須コンポーネントをインストールする
> + サンプル データベースを復元する

[第 2 回](python-taxi-classification-explore-data.md) では、サンプル データを探索し、いくつかのプロットを生成します。

[第 3 回](python-taxi-classification-create-features.md) では、Transact-SQL 関数を使用して生データから特徴を作成する方法について説明します。 その後、その関数をストアド プロシージャから呼び出し、機能の値を含むテーブルを作成します。

[第 4 回](python-taxi-classification-train-model.md) では、モジュールを読み込み、必要な関数を呼び出して、SQL Server ストアド プロシージャを使用してモデルを作成およびトレーニングします。

[第 5 回](python-taxi-classification-deploy-model.md) では、第 4 回でトレーニングして保存したモデルを運用化する方法について説明します。

> [!NOTE]
> このチュートリアルは、R および Python の両方で利用可能です。 R バージョンについては、「[R のチュートリアル:二項分類を使用して NYC タクシーの料金を予測する](r-taxi-classification-introduction.md)」を参照してください。

## <a name="prerequisites"></a>前提条件

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
+ [SQL Server Machine Learning Services と Python](../install/sql-machine-learning-services-windows-install.md#verify-installation) をインストールする
::: moniker-end

+ [Python スクリプトを実行するアクセス許可を付与する](../security/user-permission.md)

+ [NYC タクシーのデモ データベース](demo-data-nyctaxi-in-sql.md)を復元する

すべてのタスクは、Azure Data Studio または [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] の [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャを使用して実行できます。

このチュートリアル シリーズでは、データベースと表の作成、データのインポート、SQL クエリの作成などの基本的なデータベース操作について理解していることを前提としています。 Python がわかっていることを前提としていないため、すべての Python コードが提供されます。

## <a name="background-for-sql-developers"></a>SQL 開発者向けの履歴

機械学習ソリューションを構築するプロセスは、複数のツールおよび複数の段階にわたる該当分野の専門家の連携に関連する可能性がある複雑なものです。

+ データの取得とクリーニング
+ モデリングに役立つデータと構築機能の探索
+ モデルのトレーニングと最適化
+ 運用環境に展開する

実際のコードの開発とテストは、専用の開発環境を使用して実行することをお勧めします。 ただし、スクリプトのテスト完了後は、Azure Data Studio または [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] の使い慣れた環境で [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャを使用して、それを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に容易にデプロイすることができます。 ストアド プロシージャでの外部コードのラップは、SQL Server でコードを運用する場合の主要なメカニズムとなります。

モデルをデータベースに保存した後、ストアド プロシージャを使用して [!INCLUDE[tsql](../../includes/tsql-md.md)] から予測モデルを呼び出すことができます。

Python を初めて使用する SQL プログラマーであろうと、SQL を初めて使用する Python 開発者であろうと、この 5 部構成のチュートリアル シリーズでは、Python と SQL Server を使用してデータベース内分析を行うための一般的なワークフローを紹介します。

## <a name="next-steps"></a>次のステップ

この記事では、次の内容について説明します。

> [!div class="checklist"]
> + 前提条件をインストールしました
> + サンプル データベースを復元しました

> [!div class="nextstepaction"]
> [Python のチュートリアル:データの調査と視覚化](python-taxi-classification-explore-data.md)