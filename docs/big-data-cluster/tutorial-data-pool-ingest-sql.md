---
title: SQL Server のデータ プールにデータを取り込む
titleSuffix: SQL Server big data clusters
description: このチュートリアルでは、SQL Server 2019 ビッグ データ クラスターのデータ プールにデータを取り込む方法について説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d7e24258e61412584b7364f8dae7d07a1581727b
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100043547"
---
# <a name="tutorial-ingest-data-into-a-sql-server-data-pool-with-transact-sql"></a>チュートリアル: Transact-SQL を使用して SQL Server のデータ プールにデータを取り込む

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

このチュートリアルでは、Transact-SQL を使用して [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]の[データ プール](concept-data-pool.md)にデータを取り込む方法について説明します。 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]を使用すると、さまざまなソースからデータを取り込み、それをデータ プールのインスタンス間で分散することができます。

このチュートリアルでは、以下の内容を学習します。

> [!div class="checklist"]
> * データ プールに外部テーブルを作成する
> * サンプルの Web クリックストリーム データをデータ プール テーブルに挿入する。
> * データ プール テーブルのデータをローカル テーブルと結合する。

> [!TIP]
> 必要に応じて、このチュートリアルのコマンド用のスクリプトをダウンロードして実行できます。 手順については、GitHub の[データ プールのサンプル](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-pool)を参照してください。

## <a name="prerequisites"></a><a id="prereqs"></a> 前提条件

- [ビッグ データ ツール](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 の拡張機能**
- [ビッグ データ クラスターにサンプル データを読み込む](tutorial-load-sample-data.md)

## <a name="create-an-external-table-in-the-data-pool"></a>データ プールに外部テーブルを作成する

次の手順では、**web_clickstream_clicks_data_pool** という名前のデータ プールに外部テーブルを作成します。 このテーブルは、ビッグ データ クラスターにデータを取り込むための場所として使用できます。

1. Azure Data Studio で、ビッグ データ クラスターの SQL Server マスター インスタンスに接続します。 詳細については、「[SQL Server マスター インスタンスに接続する](connect-to-big-data-cluster.md#master)」を参照してください。

1. **[サーバー]** ウィンドウで接続をダブルクリックして、SQL Server マスター インスタンスのサーバー ダッシュボードを表示します。 **[新しいクエリ]** を選択します。

   ![SQL Server マスター インスタンス クエリ](./media/tutorial-data-pool-ingest-sql/sql-server-master-instance-query.png)

1. 次の Transact-SQL コマンドを実行し、マスター インスタンスの **Sales** データベースにコンテキストを変更します。

   ```sql
   USE Sales
   GO
   ```

1. まだ存在しない場合は、データ プールへの外部データ ソースを作成します。

   ```sql
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
     CREATE EXTERNAL DATA SOURCE SqlDataPool
     WITH (LOCATION = 'sqldatapool://controller-svc/default');
   ```

1. データ プールで、**web_clickstream_clicks_data_pool** という名前の外部テーブルを作成します。

   ```sql
   IF NOT EXISTS(SELECT * FROM sys.external_tables WHERE name = 'web_clickstream_clicks_data_pool')
      CREATE EXTERNAL TABLE [web_clickstream_clicks_data_pool]
      ("wcs_user_sk" BIGINT , "i_category_id" BIGINT , "clicks" BIGINT)
      WITH
      (
         DATA_SOURCE = SqlDataPool,
         DISTRIBUTION = ROUND_ROBIN
      );
   ```

データ プールの外部テーブルの作成は、ブロッキング操作です。 指定したテーブルがすべてのバックエンド データ プール ノードで作成されると、制御が戻ります。 作成操作中にエラーが発生した場合、エラー メッセージが呼び出し元に返されます。

## <a name="load-data"></a>データの読み込み

次の手順では、前の手順で作成した外部テーブルを使用して、サンプルの Web クリックストリーム データをデータ プールに取り込みます。

1. `INSERT INTO` ステートメントを使用して、クエリの結果をデータ プール (**web_clickstream_clicks_data_pool** 外部テーブル) に挿入します。

   ```sql
   INSERT INTO web_clickstream_clicks_data_pool
   SELECT wcs_user_sk, i_category_id, COUNT_BIG(*) as clicks
     FROM sales.dbo.web_clickstreams_hdfs
   INNER JOIN sales.dbo.item it ON (wcs_item_sk = i_item_sk
                           AND wcs_user_sk IS NOT NULL)
   GROUP BY wcs_user_sk, i_category_id
   HAVING COUNT_BIG(*) > 100;
   ```

1. 2 つの SELECT クエリを使用して、挿入されたデータを検査します。

   ```sql
   SELECT count(*) FROM [dbo].[web_clickstream_clicks_data_pool]
   SELECT TOP 10 * FROM [dbo].[web_clickstream_clicks_data_pool]  
   ```

## <a name="query-the-data"></a>データにクエリを実行する

データ プールのクエリから格納された結果を、**Sales** テーブルのローカル データと結合します。

```sql
SELECT TOP (100)
   w.wcs_user_sk,
   SUM( CASE WHEN i.i_category = 'Books' THEN 1 ELSE 0 END) AS book_category_clicks,
   SUM( CASE WHEN w.i_category_id = 1 THEN 1 ELSE 0 END) AS [Home & Kitchen],
   SUM( CASE WHEN w.i_category_id = 2 THEN 1 ELSE 0 END) AS [Music],
   SUM( CASE WHEN w.i_category_id = 3 THEN 1 ELSE 0 END) AS [Books],
   SUM( CASE WHEN w.i_category_id = 4 THEN 1 ELSE 0 END) AS [Clothing & Accessories],
   SUM( CASE WHEN w.i_category_id = 5 THEN 1 ELSE 0 END) AS [Electronics],
   SUM( CASE WHEN w.i_category_id = 6 THEN 1 ELSE 0 END) AS [Tools & Home Improvement],
   SUM( CASE WHEN w.i_category_id = 7 THEN 1 ELSE 0 END) AS [Toys & Games],
   SUM( CASE WHEN w.i_category_id = 8 THEN 1 ELSE 0 END) AS [Movies & TV],
   SUM( CASE WHEN w.i_category_id = 9 THEN 1 ELSE 0 END) AS [Sports & Outdoors]
FROM [dbo].[web_clickstream_clicks_data_pool] as w
INNER JOIN (SELECT DISTINCT i_category_id, i_category FROM item) as i
   ON i.i_category_id = w.i_category_id
GROUP BY w.wcs_user_sk;
```

## <a name="clean-up"></a>クリーンアップ

このチュートリアルで作成されたデータベース オブジェクトを削除するには、次のコマンドを使用します。

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstream_clicks_data_pool];
```

## <a name="next-steps"></a>次のステップ

Spark ジョブを使用してデータ プールにデータを取り込む方法について説明します。
> [!div class="nextstepaction"]
> [Spark ジョブを使用してデータを取り込む](tutorial-data-pool-ingest-spark.md)
