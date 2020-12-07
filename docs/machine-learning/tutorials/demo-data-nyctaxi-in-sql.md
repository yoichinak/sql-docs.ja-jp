---
title: チュートリアルの NYC タクシーのデモ データ
description: ニューヨーク市のタクシーのサンプル データを含むデータベースを作成します。 このデータセットは、SQL Server Machine Learning Services 用の R および Python チュートリアルで使用されます。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 10/31/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||>=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 2dab1d48ca2aa98e4a70a08bac492366f2632b79
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584962"
---
# <a name="nyc-taxi-demo-data-for-sql-server-python-and-r-tutorials"></a>SQL Server Python および R チュートリアル用の NYC タクシー のデモ データ
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

この記事では、[New York City Taxi and Limousine Commission (ニューヨーク市のタクシーとリムジンのコミッション)](http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml) からのパブリック データで構成されるサンプル データベースを設定する方法について説明します。 このデータは、SQL Server でのデータベース内分析のために、いくつかの R および Python のチュートリアルで使用されています。 サンプル コードの実行速度を高めるために、データの代表的な 1% のサンプルを作成しました。 システムでは、データベース バックアップ ファイルが 90 MB をわずかに上回り、プライマリ データ テーブル内に 170 万行が提供されます。

この演習を完了するには、[SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md?view=sql-server-2017&preserve-view=true)、またはデータベース バックアップ ファイルを復元し、T-SQL クエリを実行できる別のツールが必要です。

このデータセットを使用したチュートリアルとクイックスタートには、次のものがあります。

+ [SQL Server で R を使用したデータベース内分析について学習する](r-taxi-classification-introduction.md)
+ [SQL Server で Python を使用したデータベース内分析について学習する](python-taxi-classification-introduction.md)

## <a name="download-files"></a>ファイルのダウンロード

サンプル データベースは、Microsoft によってホストされる SQL Server 2016 BAK ファイルです。 SQL Server 2016 以降で復元できます。 ファイルのダウンロードは、リンクをクリックするとすぐに開始されます。 

ファイル サイズは約 90 MB です。

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
>[!NOTE]
>サンプル データベースを [SQL Server ビッグ データ クラスター](../../big-data-cluster/big-data-cluster-overview.md)で復元するには、[NYCTaxi_Sample.bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak) をダウンロードして、「[SQL Server ビッグ データ クラスターのマスター インスタンスにデータベースを復元する](../../big-data-cluster/data-ingestion-restore-database.md)」の指示に従います。
::: moniker-end

::: moniker range=">=azuresqldb-mi-current||=sqlallproducts-allversions"
>[!NOTE]
>[Azure SQL Managed Instance の Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview) でサンプル データベースを復元するには、[Azure SQL Managed Instance にデータベースを復元する](/azure/azure-sql/managed-instance/restore-sample-database-quickstart)方法に関するクイックスタートの指示に従ってください。NYC タクシー デモ データベース .bak ファイル [https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak) が使用されます。
::: moniker-end

1. [NYCTaxi_Sample .bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak) をクリックして、データベースのバックアップ ファイルをダウンロードします。

2. ファイルを C:\Program files\Microsoft SQL Server\MSSQL-instance-name\MSSQL\Backup フォルダーにコピーします。

3. Management Studio で、 **[データベース]** を右クリックし、 **[ファイルおよびファイル グループの復元]** を選択します。

4. データベース名として「*NYCTaxi_Sample*」と入力します。

5. **[デバイスから]** をクリックし、[ファイルの選択] ページを開いてバックアップ ファイルを選択します。 **[追加]** をクリックして、NYCTaxi_Sample.bak を選択します。

6. **[復元]** チェックボックスをオンにし、 **[OK]** をクリックしてデータベースを復元します。

## <a name="review-database-objects"></a>データベース オブジェクトの確認
   
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスにデータベース オブジェクトが存在することを確認します。 データベース、テーブル、関数、ストアド プロシージャが表示されます。
  
   ![rsql_devtut_BrowseTables](media/rsql-devtut-browsetables.png "rsql_devtut_BrowseTables")

### <a name="objects-in-nyctaxi_sample-database"></a>NYCTaxi_Sample データベース内のオブジェクト

次の表は、NYC タクシー デモ データベースで作成されたオブジェクトをまとめたものです。

|**オブジェクト名です。**|**オブジェクトの種類**|**説明**|
|----------|------------------------|---------------|
|**NYCTaxi_Sample** | database | データベースと 2 つのテーブルを作成します。<br /><br />dbo. nyctaxi_sample テーブル:メインの NYC タクシー データセットを格納します。 ストレージとクエリのパフォーマンスを向上させるために、クラスター化列ストア インデックスをテーブルに追加します。 NYC タクシー データセットの 1% のサンプルが、このテーブルに挿入されます。<br /><br />dbo.nyc_taxi_models テーブル:トレーニング済みの Advanced Analytics モデルを保持するために使用します。|
|**fnCalculateDistance** |スカラー値関数 (scalar-valued function) | 乗車と降車の場所間の直線距離を計算します。 この関数は、[データ機能の作成](r-taxi-classification-create-features.md)、[モデルのトレーニングと保存](r-taxi-classification-train-model.md)、[R モデルの運用](r-taxi-classification-deploy-model.md)に使用されます。|
|**fnEngineerFeatures** |テーブル値関数 (table-valued function) | モデル トレーニング用の新しいデータ機能を作成します。 この関数は、[データ機能の作成](r-taxi-classification-create-features.md)、[モデルのトレーニングと保存](r-taxi-classification-deploy-model.md)、R モデルの運用に使用されます。|


ストアド プロシージャは、さまざまなチュートリアルに記載されている R および Python スクリプトを使用して作成されます。 次のテーブルは、さまざまなレッスンでスクリプトを実行するときに、必要に応じて NYC タクシー デモ データベースに追加できるストアド プロシージャをまとめたものです。

|**ストアド プロシージャ**|**Language**|**説明**|
|-------------------------|------------|---------------|
|**RxPlotHistogram** |R | 変数のヒストグラムをプロットする RevoScaleR rxHistogram 関数を呼び出し、バイナリ オブジェクトとしてプロットを返します。 このストアド プロシージャは、[データの調査と視覚化](r-taxi-classification-explore-data.md)のために使用されます。|
|**RPlotRHist** |R| Hist 関数を使用してグラフィックを作成し、出力をローカル PDF ファイルとして保存します。 このストアド プロシージャは、[データの調査と視覚化](r-taxi-classification-explore-data.md)のために使用されます。|
|**RxTrainLogitModel**  |R| R パッケージを呼び出して、ロジスティック回帰モデルをトレーニングします。 モデルは、tipped 列の値を予測し、ランダムに選択した 70% のデータを使用してトレーニングされます。 ストアド プロシージャの出力は、テーブル nyc_taxi_models に保存されているトレーニング済みのモデルです。 このストアド プロシージャは、[モデルのトレーニングと保存](r-taxi-classification-train-model.md)のために使用されます。|
|**RxPredictBatchOutput**  |R | モデルを使用して予測を作成するトレーニング済みモデルを呼び出します。 ストアド プロシージャは、その入力パラメーターとしてクエリを受け取り、入力行のスコアを格納する数値の列を返します。 このストアド プロシージャは、[可能性のある結果の予測](r-taxi-classification-deploy-model.md)のために使用されます。|
|**RxPredictSingleRow**  |R| モデルを使用して予測を作成するトレーニング済みモデルを呼び出します。 このストアド プロシージャは、インライン パラメーターとして渡された個々の機能の値と共に、入力として新しい監視を受け取り、新しい監視の結果を予測する値を返します。 このストアド プロシージャは、[可能性のある結果の予測](r-taxi-classification-deploy-model.md)のために使用されます。|

## <a name="query-the-data"></a>データにクエリを実行する

検証手順として、クエリを実行してデータがアップロードされたことを確認します。

1. オブジェクト エクスプローラーの [データベース] で、**NYCTaxi_Sample** データベースを右クリックし、新しいクエリを開始します。

2. いくつかの単純なクエリを実行します。

    ```sql
    SELECT TOP(10) * FROM dbo.nyctaxi_sample;
    SELECT COUNT(*) FROM dbo.nyctaxi_sample;
    ```
データベースには 170 万行が含まれています。

3. データベース内には、データセットが格納されている **nyctaxi_sample** テーブルがあります。 テーブルは、[columnstore インデックス](../../relational-databases/indexes/columnstore-indexes-overview.md)を追加することにより、セットベースの計算に対して最適化されています。 次のステートメントを実行して、テーブルの簡単な概要を生成します。

    ```sql
    SELECT DISTINCT [passenger_count]
        , ROUND (SUM ([fare_amount]),0) as TotalFares
        , ROUND (AVG ([fare_amount]),0) as AvgFares
    FROM [dbo].[nyctaxi_sample]
    GROUP BY [passenger_count]
    ORDER BY  AvgFares DESC
    ````
結果は、次のスクリーンショットに示すようになります。

  ![テーブルの概要情報](media/nyctaxidatatablesummary.png "Query results")

## <a name="next-steps"></a>次のステップ

NYC タクシー サンプル データをハンズオン学習で使用できるようになりました。

+ [SQL Server で R を使用したデータベース内分析について学習する](r-taxi-classification-introduction.md)
+ [SQL Server で Python を使用したデータベース内分析について学習する](python-taxi-classification-introduction.md)