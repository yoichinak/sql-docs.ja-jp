---
title: チュートリアル:R で予測モデルを開発する
titleSuffix: SQL machine learning
description: この 4 部構成のチュートリアル シリーズでは、SQL 機械学習を使用して R で予測モデルをトレーニングするためのデータを開発します。
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.reviewer: garye, davidph
ms.date: 05/26/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 774c59b22a6c12dafa5f7191439ebdfd7bf0ac52
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870350"
---
# <a name="tutorial-develop-a-predictive-model-in-r-with-sql-machine-learning"></a>チュートリアル:SQL 機械学習を使用して R で予測モデルを開発する
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズでは、[SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) または[ビッグ データ クラスター](../../big-data-cluster/machine-learning-services.md)で R と機械学習モデルを使用して、スキーのレンタル数を予測します。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズでは、[SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) で R と機械学習モデルを使用して、スキーのレンタル数を予測します。
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズでは、[SQL Server R Services](../r/sql-server-r-services.md) で R と機械学習モデルを使用して、スキーのレンタル数を予測します。
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズでは、[Azure SQL Managed Instance の Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview) で R と機械学習モデルを使用して、スキーのレンタル数を予測します。
::: moniker-end

たとえば、スキー レンタル事業を所有していて、将来の日付に対するレンタル数を予測したい場合を考えてみましょう。 この情報は、在庫、スタッフおよび設備の準備に役立ちます。

このシリーズのパート 1 では、前提条件を設定します。 パート 2 と 3 では、ノートブックでいくつかの R スクリプトを開発して、データを準備し、機械学習モデルをトレーニングします。 その後、パート 3 では、T-SQL ストアド プロシージャを使用してデータベース内でそれらの R スクリプトを実行します。

この記事では、次の方法について学習します。

> [!div class="checklist"]
> * サンプル データベースを復元する 

[パート 2](r-predictive-model-prepare-data.md) では、データベースから Python データ フレームにデータを読み込み、R でデータを準備する方法を学習します。

[パート 3](r-predictive-model-train.md) では、R で機械学習モデルをトレーニングする方法について学習します。

[パート 4](r-predictive-model-deploy.md) では、モデルをデータベースに格納した後、パート 2 と 3 で開発した R スクリプトからストアド プロシージャを作成する方法について学習します。 ストアド プロシージャは、新しいデータに基づいて予測を行うためにサーバーで実行されます。

## <a name="prerequisites"></a>前提条件

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
* SQL Server Machine Learning Services - Machine Learning Services をインストールするには、[Windows インストール ガイド](../install/sql-machine-learning-services-windows-install.md)または [Linux インストール ガイド](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fmachine-learning%2Ftoc.json)に関するページを参照してください。 [SQL Server ビッグ データ クラスターで Machine Learning Services を有効にする](../../big-data-cluster/machine-learning-services.md)こともできます。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
* SQL Server Machine Learning Services - Machine Learning Services をインストールするには、[Windows インストール ガイド](../install/sql-machine-learning-services-windows-install.md)に関するページを参照してください。 
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
* SQL Server 2016 R Services。 R Services をインストールするには、[Windows インストール ガイド](../install/sql-r-services-windows-install.md)に関するページを参照してください。 
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
* Azure SQL Managed Instance の Machine Learning Services。 詳細については、[Azure SQL Managed Instance の Machine Learning Services の概要](/azure/azure-sql/managed-instance/machine-learning-services-overview)に関するページを参照してください。

* サンプル データベースを Azure SQL Managed Instance に復元するための [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md)。
::: moniker-end

* R IDE - このチュートリアルでは [RStudio Desktop](https://www.rstudio.com/products/rstudio/download/) を使用します。

* RODBC - このドライバーは、このチュートリアルで開発する R スクリプトで使用します。 まだインストールされていない場合は、R コマンド `install.packages("RODBC")` を使用してインストールします。 RODBC の詳細については、「[CRAN-Package RODBC](https://CRAN.R-project.org/package=RODBC)」を参照してください。

* SQL クエリ ツール - このチュートリアルでは、[Azure Data Studio](../../azure-data-studio/what-is.md) を使用していることを前提としています。 詳細については、「[Azure Data Studio でノートブックを使用する方法](../../azure-data-studio/notebooks/notebooks-guidance.md)」を参照してください。

## <a name="restore-the-sample-database"></a>サンプル データベースを復元する

このチュートリアルで使用するサンプル データベースは、ダウンロードして使用できるように **.bak** データベース バックアップ ファイルに保存されています。

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
> [!NOTE]
> ビッグ データ クラスターで Machine Learning Services を使用している場合は、[SQL Server ビッグ データ クラスターのマスター インスタンスにデータベースを復元する](../../big-data-cluster/data-ingestion-restore-database.md)方法に関する記事を参照してください。
::: moniker-end

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
1. ファイル [TutorialDB.bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/TutorialDB.bak) をダウンロードします。

1. Azure Data Studio で、以下の詳細情報を使用して、「[バックアップ ファイルからデータベースを復元する](../../azure-data-studio/tutorial-backup-restore-sql-server.md#restore-a-database-from-a-backup-file)」に記載されている手順に従います。

   * ダウンロードした **TutorialDB.bak** ファイルからインポートします
   * ターゲット データベースに "TutorialDB" という名前を指定します

1. **dbo.rental_data** テーブルに対してクエリを実行して、復元されたデータベースが存在することを確認できます。

   ```sql
   USE TutorialDB;
   SELECT * FROM [dbo].[rental_data];
   ```
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
1. ファイル [TutorialDB.bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/TutorialDB.bak) をダウンロードします。

1. 次の詳細を使用して、SQL Server Management Studio で [Managed Instance へのデータベースの復元](/azure/sql-database/sql-database-managed-instance-get-started-restore)の指示に従います。

   * ダウンロードした **TutorialDB.bak** ファイルからインポートします
   * ターゲット データベースに "TutorialDB" という名前を指定します

1. **dbo.rental_data** テーブルに対してクエリを実行して、復元されたデータベースが存在することを確認できます。

   ```sql
   USE TutorialDB;
   SELECT * FROM [dbo].[rental_data];
   ```
::: moniker-end

## <a name="clean-up-resources"></a>リソースをクリーンアップする

このチュートリアルを続行しない場合は、TutorialDB データベースを削除してください。
## <a name="next-steps"></a>次のステップ

このチュートリアル シリーズの第 1 部では、これらの手順を完了しました。

* 必須コンポーネントのインストール
* サンプル データベースの復元

機械学習モデル用にデータを準備するには、このチュートリアル シリーズの第 2 部の手順を実行します。

> [!div class="nextstepaction"]
> [R で予測モデルをトレーニングするためのデータを準備する](r-predictive-model-prepare-data.md)