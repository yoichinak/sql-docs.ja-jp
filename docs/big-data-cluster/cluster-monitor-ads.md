---
title: Azure Data Studio を使用してクラスターを監視する
titleSuffix: SQL Server Big Data Clusters
description: SQL Server 2019 ビッグ データ クラスター上の Azure Data Studio を使用したクラスターの監視。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 09/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4c4dc9956b8c3f9802feb839096195c09664d0d6
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92378402"
---
# <a name="monitor-cluster-status-with-azure-data-studio"></a>Azure Data Studio を使用してクラスターの状態を監視する

この記事では、Azure Data Studio を使用して、ビッグ データ クラスターの状態を表示する方法について説明します。

## <a name="use-azure-data-studio"></a><a id="datastudio"></a> Azure Data Studio を使用する

[Azure Data Studio](https://aka.ms/getazuredatastudio) の最新の **Insider ビルド** をダウンロードしたら、SQL Server ビッグ データ クラスター ダッシュボードを使用して、サービス エンドポイントとビッグ データ クラスターの状態を表示できます。 以下の機能の一部については、最初は Azure Data Studio の Insider ビルドでのみ使用可能となります。

1. まず、Azure Data Studio でご利用のビッグ データ クラスターへの接続を作成します。 詳細については、「[Azure Data Studio を使用して SQL Server ビッグ データ クラスターに接続する](connect-to-big-data-cluster.md)」を参照してください。

1. ビッグ データ クラスター エンドポイントを右クリックし、 **[管理]** をクリックします。

   ![[管理] を右クリックする](media/view-cluster-status/right-click-manage.png)

1. **[SQL Server Big Data Cluster]\(SQL Server ビッグ データ クラスター\)** タブを選択して、ビッグ データ クラスターのダッシュボードにアクセスします。

   ![ビッグ データ クラスター ダッシュボード](media/view-cluster-status/bdc-dashboard.png)

### <a name="service-endpoints"></a>サービス エンドポイント

ビッグ データ クラスター内のさまざまなサービスに簡単にアクセスできるようにすることが重要です。 ビッグ データ クラスター ダッシュボードには、サービス エンドポイントを表示してコピーすることを可能にするサービス エンドポイント テーブルが用意されています。

![サービス エンドポイント](media/view-cluster-status/service-endpoints.png)

これらのサービスに接続するためにエンドポイントが必要なときにコピーして貼り付けることができるエンドポイントが、それらのサービスに一覧表示されます。 たとえば、エンドポイントの右側にあるコピー アイコンをクリックして、そのエンドポイントを要求するテキスト ウィンドウに貼り付けることができます。 [クラスターの状態ノートブック](#notebook)を実行するには、クラスター管理サービスのエンドポイントが必要です。

### <a name="dashboards"></a>ダッシュボード

サービス エンドポイント テーブルには、次の項目を監視するためのダッシュボードもいくつか公開されます。

- メトリック (Grafana)
- ログ (Kibana)
- Spark ジョブの監視
- Spark リソースの管理

これらのリンクを直接クリックできます。 これらのダッシュボードにアクセスするときは、認証が必要になります。 メトリックとログのダッシュボードの場合は、環境変数 **AZDATA_USERNAME** と **AZDATA_PASSWORD** を使用して、展開時に設定するコントローラー管理者の資格情報を指定します。 Spark ダッシュボードでは、AD に統合されたクラスターの AD ID、またはクラスター内で基本認証を使用している場合は、 **AZDATA_USERNAME** および **AZDATA_PASSWORD** というゲートウェイ (Knox) 資格情報が使用されます。

[!INCLUDE [big-data-cluster-root-user](../includes/big-data-cluster-root-user.md)]

### <a name="cluster-status-notebook"></a><a id="notebook"></a> クラスターの状態ノートブック

1. クラスターの状態ノートブックを起動して、ビッグ データ クラスターのクラスターの状態を表示することもできます。 ノートブックを起動するには、 **[クラスターの状態]** タスクをクリックします。

    ![起動する](media/view-cluster-status/cluster-status-launch.png)

2. 開始する前に、次の項目が必要です。

    - ビッグ データのクラスター名
    - コントローラーのユーザー名
    - コントローラーのパスワード
    - コントローラー エンドポイント

    既定のビッグ データ クラスター名は、展開時にカスタマイズしない限り、 **mssql-cluster** となります。 コントローラー エンドポイントは、サービス エンドポイント テーブル内のビッグ データ クラスター ダッシュボードから見つけることができます。 エンドポイントは、 **クラスター管理サービス** として一覧表示されます。 資格情報がわからない場合は、ご利用のクラスターを展開した管理者に問い合わせてください。

3. 上部のツールバーで **[セルの実行]** をクリックします。

4. ご利用の資格情報を求めるプロンプトに従います。 ビッグ データのクラスター名、コントローラーのユーザー名、コントローラーのパスワードの各資格情報を入力したら、Enter キーを押します。

    > [!Note]
    > ご利用のビッグ データを使用して設定された構成ファイルがない場合は、コントローラー エンドポイントの指定を求められます。 それを入力するか貼り付けてから、Enter キーを押して続行します。

5. 正常に接続された場合、ノートブックの残りの部分には、ビッグ データ クラスターの各コンポーネントの出力が表示されます。 特定のコード セルを再実行する場合は、コード セル上にマウス ポインターを移動し、 **[実行]** アイコンをクリックします。


## <a name="next-steps"></a>次のステップ

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]の詳細については、「[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]とは](big-data-cluster-overview.md)」を参照してください。
