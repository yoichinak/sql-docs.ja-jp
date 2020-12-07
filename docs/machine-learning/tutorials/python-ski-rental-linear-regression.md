---
title: Python のチュートリアル:スキー レンタル
titleSuffix: SQL machine learning
description: この 4 部構成のチュートリアル シリーズでは、SQL 機械学習でスキー レンタルを予測する線形回帰モデルを Python で構築します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/26/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: fc700631df6289c0529fdfd65d73b630cfac00f1
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2020
ms.locfileid: "94585053"
---
# <a name="python-tutorial-predict-ski-rental-with-linear-regression-with-sql-machine-learning"></a>Python のチュートリアル:SQL 機械学習での線形回帰を使用したスキー レンタルの予測
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズでは、[SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) または[ビッグ データ クラスター](../../big-data-cluster/machine-learning-services.md)で Python と線形回帰を使用して、スキーのレンタル数を予測します。 このチュートリアルは、[Azure Data Studio で Python のノートブック](../../azure-data-studio/notebooks/notebooks-guidance.md)を使用します。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズでは、[SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) で Python と線形回帰を使用して、スキーのレンタル数を予測します。 このチュートリアルは、[Azure Data Studio で Python のノートブック](../../azure-data-studio/notebooks/notebooks-guidance.md)を使用します。
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
この 4 部構成のチュートリアル シリーズでは、[Azure SQL Managed Instance Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview) で Python と線形回帰を使用して、スキーのレンタル数を予測します。 このチュートリアルは、[Azure Data Studio で Python のノートブック](../../azure-data-studio/notebooks/notebooks-guidance.md)を使用します。
::: moniker-end

たとえば、スキー レンタル事業を所有していて、将来の日付に対するレンタル数を予測したい場合を考えてみましょう。 この情報は、在庫、スタッフおよび設備の準備に役立ちます。

このシリーズのパート 1 では、前提条件を設定します。 パート 2 と 3 では、ノートブックでいくつかの Python スクリプトを開発して、データを準備し、機械学習モデルをトレーニングします。 次にパート 3 では、T-SQL ストアド プロシージャを使用して、データベース内でこれらの Python スクリプトを実行します。

この記事では、次の方法について学習します。

> [!div class="checklist"]
> * サンプル データベースのインポート

[パート 2](python-ski-rental-linear-regression-prepare-data.md) では、データベースから Python データ フレームにデータを読み込み、Python でデータを準備する方法を学習します。

[パート 3](python-ski-rental-linear-regression-train-model.md) では、Python で線形回帰モデルをトレーニングする方法について学習します。

[パート 4](python-ski-rental-linear-regression-deploy-model.md) では、モデルをデータベースに格納した後、パート 2 と 3 で開発した Python スクリプトからストアド プロシージャを作成する方法について学習します。 ストアド プロシージャは、新しいデータに基づいて予測を行うためにサーバーで実行されます。

## <a name="prerequisites"></a>前提条件

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
* SQL Server Machine Learning Services - Machine Learning Services をインストールするには、[Windows インストール ガイド](../install/sql-machine-learning-services-windows-install.md)または [Linux インストール ガイド](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fmachine-learning%2Ftoc.json)に関するページを参照してください。 [SQL Server ビッグ データ クラスターで Machine Learning Services を有効にする](../../big-data-cluster/machine-learning-services.md)こともできます。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
* SQL Server Machine Learning Services - Machine Learning Services をインストールするには、[Windows インストール ガイド](../install/sql-machine-learning-services-windows-install.md)に関するページを参照してください。 
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
* Azure SQL Managed Instance Machine Learning Services - 詳細については、[Azure SQL Managed Instance の Machine Learning Services の概要](/azure/azure-sql/managed-instance/machine-learning-services-overview)に関するページを参照してください。

* サンプル データベースを Azure SQL Managed Instance に復元するための [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md)。
::: moniker-end

* Python IDE - このチュートリアルは、[Azure Data Studio](../../azure-data-studio/what-is.md) で Python のノートブックを使用します。 詳細については、「[Azure Data Studio でノートブックを使用する方法](../../azure-data-studio/notebooks/notebooks-guidance.md)」を参照してください。

* SQL クエリ ツール - このチュートリアルでは、[Azure Data Studio](../../azure-data-studio/what-is.md) を使用していることを前提としています。

* 追加の Python パッケージ - このチュートリアル シリーズの例では、既定ではインストールされない可能性がある次の Python パッケージを使用します。

  * pandas
  * pyodbc
  * sklearn

  これらのパッケージをインストールするには:
  1. Azure Data Studio ノートブックで、 **[パッケージの管理]** を選択します。
  2. **[パッケージの管理]** ペインで **[新規追加]** タブを選択します。
  3. 次の各パッケージについてパッケージ名を入力し、 **[検索]** をクリックし、 **[インストール]** をクリックします。

  また、 **[コマンド プロンプト]** を開き、Azure Data Studio で使用する Python のバージョンのインストール パス (たとえば `cd %LocalAppData%\Programs\Python\Python37-32`) に変更し、パッケージごとに `pip install` を実行する方法もあります。

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
* サンプル データベースのインポート

TutorialDB データベースからデータを準備するには、このチュートリアル シリーズのパート 2 の手順を実行します。

> [!div class="nextstepaction"]
> [Python のチュートリアル:線形回帰モデルをトレーニングするためのデータを準備する](python-ski-rental-linear-regression-prepare-data.md)