---
title: 記憶域プールから CSV データを仮想化する
subtitle: SQL Server ビッグ データ クラスター
description: ビッグ データ クラスターで CSV ファイルの仮想化を行うための CREATE EXTERNAL TABLE の詳細な手順
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.date: 04/24/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: polybase
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.metadata: seo-lt-2019
ms.openlocfilehash: 6625e985781f3980c44bef9b6dbd408243ac78a9
ms.sourcegitcommit: 67befbf7435f256e766bbce6c1de57799e1db9ad
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2020
ms.locfileid: "92523852"
---
# <a name="virtualize-csv-data-from-storage-pool-big-data-clusters"></a>記憶域プール (ビッグ データ クラスター) から CSV データを仮想化する

SQL Server ビッグ データ クラスターでは、HDFS の CSV ファイルからデータを仮想化できます。 このプロセスでは、データを元の場所に維持したまま、他のテーブルと同様に SQL Server インスタンスからクエリを実行することができます。 この機能では PolyBase コネクタを使用して、ETL プロセスの必要性を最小限に抑えます。 データ仮想化の詳細については、「[PolyBase とは](../relational-databases/polybase/polybase-guide.md)」を参照してください。

## <a name="prerequisites"></a>前提条件

- [展開済みのビッグ データ クラスター](deployment-guidance.md)
- [Azure Data Studio](../azure-data-studio/download-azure-data-studio.md)

## <a name="select-or-upload-a-csv-file-for-data-virtualization"></a>データの仮想化に使用する CSV ファイルを選択またはアップロードする 

Azure Data Studio (ADS) で、ご使用のビッグ データ クラスターの [SQL Server マスター インスタンスに接続します](connect-to-big-data-cluster.md#master)。 接続したら、オブジェクト エクスプローラーで HDFS 要素を展開して、データを仮想化する CSV ファイルを見つけます。 

このチュートリアルでは、 **Data** という名前の新しいディレクトリを作成します。

1. HDFS ルート ディレクトリのコンテキスト メニューを右クリックします。
2. **[新しいディレクトリ]** をクリックします。
3. 新しいディレクトリに " *Data* " という名前を付けます。

サンプル データをアップロードします。 簡単なチュートリアルの場合は、サンプルの csv データ ファイルを使用できます。 この記事では、[米国運輸省](https://www.transtats.bts.gov/OT_Delay/OT_DelayCause1.asp?pn=1)の航空会社の遅延の原因データを使用します。 生データをダウンロードし、ご使用のコンピューターにデータを抽出します。 ファイルに *airline_delay_causes.csv* という名前を付けます。

抽出後にサンプル ファイルをアップロードするには:

1. Azure Data Studio で、作成した新しいディレクトリを " *右クリック* " します。 
2. **[ファイルのアップロード]** をクリックします。

![HDFS の csv ファイルの例](media/data-virtualization/100-csv-sample-file-hdfs.png)

Azure Data Studio により、ファイルがビッグ データ クラスターの HDFS にアップロードされます。

## <a name="create-the-storage-pool-external-data-source-in-your-target-database"></a>ターゲット データベースに記憶域プールの外部データ ソースを作成する

ビッグ データ クラスターでは、記憶域プールの外部データ ソースは、既定ではデータベース内には作成されません。 外部テーブルを作成するには、事前に次の Transact-SQL クエリを使用して、ターゲット データベースに既定の **SqlStoragePool** 外部データ ソースを作成します。 最初に必ず、クエリのコンテキストを実際のターゲット データベースに変更してください。

```sql
-- Create the default storage pool source for SQL Big Data Cluster
IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
    CREATE EXTERNAL DATA SOURCE SqlStoragePool
    WITH (LOCATION = 'sqlhdfs://controller-svc/default');
```

## <a name="create-the-external-table"></a>外部テーブルを作成する

ADS から、CSV ファイルを右クリックして、コンテキスト メニューから **[Create External Table From CSV File]\(CSV ファイルからの外部テーブルの作成\)** を選択します。 HDFS 内のディレクトリの下にある CSV ファイルが同じスキーマに従っている場合、そのディレクトリのファイルから外部テーブルを作成することもできます。 これにより、個々のファイルを処理する必要なしにディレクトリ レベルでデータを仮想化でき、結合されたデータに対する結合された結果セットを取得できます。Azure Data Studio により外部テーブルを作成する手順が示されます。

データベース、データソース、テーブル名、スキーマ、およびテーブルの外部ファイル形式の名前を指定します。

**[次へ]** をクリックします。

## <a name="preview-data"></a>データをプレビューする

Azure Data Studio により、インポートされたデータのプレビューが提供されます。

![インポートされたデータのプレビューが含まれる [Create External Table From CSV]\(CSV から外部テーブルを作成する\) ウィンドウを示すスクリーンショット。](media/data-virtualization/130-csv-preview-data.png)

プレビューの表示が終わったら、 **[次へ]** をクリックして続行します。

## <a name="modify-columns"></a>列を変更する

次のウィンドウでは、作成する外部テーブルの列を変更できます。 列の名前とデータ型を変更でき、null 許容型の行にすることができます。 

![手順 3「列を変更する」が示されている [Create External Table From CSV]\(CSV から外部テーブルを作成する\) ウィンドウのスクリーンショット。](media/data-virtualization/140-csv-modify-columns.png)

変換先の列を確認したら、 **[次へ]** をクリックします。

## <a name="summary"></a>まとめ

このステップでは、選択内容の要約が提供されます。 SQL Server 名、データベース名、テーブル名、テーブル スキーマ、および外部テーブル情報が提供されます。 このステップでは、スクリプトを生成するか、テーブルを作成するかを選択できます。 **[スクリプトの生成]** では、外部データ ソースを作成するためのスクリプトが T-SQL で生成されます。 **[テーブルの作成]** では、外部データ ソースが作成されます。

![概要画面](media/data-virtualization/150-csv-virtualize-data-summary.png)

**[テーブルの作成]** をクリックすると、SQL Server によって出力先データベースに外部テーブルが作成されます。

**[スクリプトの生成]** をクリックすると、Azure Data Studio によって外部テーブルを作成するための T-SQL クエリが作成されます。

テーブルが作成されたら、SQL Server インスタンスから T-SQL を使用して直接クエリを実行できるようになります。

## <a name="next-steps"></a>次のステップ

SQL Server のビッグ データ クラスターおよび関連するシナリオについて詳しくは、「[SQL Server ビッグ データ クラスターとは](big-data-cluster-overview.md)」をご覧ください。
