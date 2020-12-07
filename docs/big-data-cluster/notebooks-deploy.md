---
title: '展開: Azure Data Studio ノートブック'
titleSuffix: SQL Server Big Data Clusters
description: Azure Data Studio からノートブックでコードとドキュメントを使用し、SQL Server ビッグ データ クラスターを展開する方法について説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bcf42d76f855e6fc722caa18f3c0d3c3672f9ec7
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725843"
---
# <a name="deploy-sql-server-big-data-cluster-with-azure-data-studio-notebook"></a>Azure Data Studio ノートブックを使用して SQL Server ビッグ データ クラスターを展開する

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] では、展開ノートブックを含む Azure Data Studio の拡張機能が提供されています。 展開ノートブックには、SQL Server ビッグ データ クラスターを作成するために Azure Data Studio 内で使用できるドキュメントとコードが含まれています。

もともとは、オープン ソース プロジェクトとして実装され、[ノートブック](../azure-data-studio/notebooks/notebooks-guidance.md)は [Azure Data Studio](../azure-data-studio/download-azure-data-studio.md?view=sql-server-ver15) 内に実装されていました。 テキスト セル内のテキストに対してはマークダウンを、また、コード セル内にコードを記述するには利用可能なカーネルの 1 つを使用できます。

ノートブックを使用して、[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] に対してビッグ データ クラスターを展開できます。

## <a name="prerequisites"></a>前提条件

ノートブックも起動するには、次の前提条件が要件です。

* [Azure Data Studio Insiders ビルド](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master)の最新バージョンがインストールされていること

上記に加えて、SQL Server 2019 ビッグ データ クラスターを展開するには、以下も必要になります。

* [azdata](../azdata/install/deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Azure CLI (Azure に展開する場合)](/cli/azure/install-azure-cli?view=azure-cli-latest)

## <a name="launch-the-notebook"></a>ノートブックを起動する

1. Azure Data Studio を起動します。

2. **[接続]** タブで、省略記号 **[...]** を選択し、 **[Deploy SQL Server...]\(SQL Server の展開...\)** を選択します。

   ![SQL Server を展開する](media/notebooks-deploy/deploy-notebooks.png)

3. 展開のオプションで、 **[SQL Server Big Data Cluster]\(SQL Server ビッグ データ クラスター\)** を選択します。

4. **[オプション]** 下にある **[展開ターゲット]** から、 **[New Azure Kubernetes Cluster]\(新しい Azure Kubernetes クラスター\)** または **[Existing Azure Kubernetes Service cluster]\(既存の Azure Kubernetes Service クラスター\)** のどちらかを選択します。

5. プライバシーとライセンス条項に同意する

6. このダイアログでは、選択した種類の SQL 展開に必要なツールがホストに存在するかどうかも確認されます。 ツールの確認が成功するまで、 **[選択]** ボタンは有効になりません。

7. **[選択]** ボタンを選択します。 この操作により、展開エクスペリエンスが起動されます。

## <a name="set-deployment-configuration-template"></a>展開構成テンプレートを設定する

以下の手順のようにして、展開プロファイルの設定をカスタマイズできます。

### <a name="target-configuration-template"></a>対象の構成テンプレート

使用可能なテンプレートから対象の構成テンプレートを選択します。 使用可能なプロファイルは、前のダイアログで選択した展開ターゲットの種類に応じてフィルター処理されています。

   ![展開構成テンプレート ステップ 1](media/notebooks-deploy/deployment-configuration-template.png)

### <a name="azure-settings"></a>Azure の設定

展開ターゲットが新しい AKS の場合、AKS クラスターを作成するには、Azure サブスクリプション ID、リソース グループ、AKS クラスター名、VM 数、サイズ、その他の追加情報が必要です。

   ![Azure の設定](media/notebooks-deploy/azure-settings.png)

展開ターゲットが既存の Kubernetes クラスターの場合は、ウィザードによって、Kubernetes クラスターの設定をインポートするための *kube* 構成ファイルへのパスを入力するように求められます。 SQL Server 2019 ビッグ データ クラスターを展開できる、適切なクラスター コンテキストが選択されていることを確認します。

   ![ターゲット クラスターのコンテキスト](media/notebooks-deploy/target-cluster-context.png)

### <a name="cluster-docker-and-ad-settings"></a>クラスター、Docker、AD の設定

1. SQL Server 2019 BDC のクラスター名、管理者のユーザー名、パスワードを入力します。
注:コントローラーと SQL Server に同じアカウントが使用されます。

   ![クラスターの設定](media/notebooks-deploy/cluster-settings.png)

2. 必要に応じて Docker の設定を入力します

   ![Docker の設定](media/notebooks-deploy/docker-settings.png)

3. AD 認証が使用可能な場合は、AD の設定を入力します

   ![Active Directory の設定](media/notebooks-deploy/active-directory-settings.png)

### <a name="service-settings"></a>サービスの設定

この画面には、**スケール**、**エンドポイント**、**ストレージ**、その他の**詳細なストレージ設定**など、さまざまな設定の入力があります。 適切な値を入力し、 **[次へ]** を選択してください。

#### <a name="scale-settings"></a>スケールの設定

ビッグ データ クラスター内の各コンポーネントのインスタンス数を入力します。

Spark インスタンスは HDFS に含めることができます。 それは、記憶域プールに含まれるか、または専用の Spark プールに含まれます。

   ![サービスの設定](media/notebooks-deploy/service-settings.png)

これらの各コンポーネントの詳細については、[マスター インスタンス](concept-master-instance.md)、[データ プール](concept-data-pool.md)、[記憶域プール](concept-storage-pool.md)、[コンピューティング プール](concept-compute-pool.md)を参照してください。

#### <a name="endpoint-settings"></a>エンドポイントの設定

既定のエンドポイントがあらかじめ入力されています。 ただし、必要に応じて変更できます。

   ![エンドポイントの設定](media/notebooks-deploy/endpoint-settings.png)

#### <a name="storage-settings"></a>ストレージの設定

ストレージの設定には、データとログのストレージ クラスおよび要求サイズが含まれます。 設定は、ストレージ、データ、および SQL Server のマスター プール全体に適用できます。

   ![ストレージの設定](media/notebooks-deploy/storage-settings.png)

#### <a name="advanced-storage-settings"></a>詳細なストレージ設定

**[Advanced storage settings]\(詳細なストレージ設定\)** では、その他のストレージ設定を追加できます

* 記憶域プール (HDFS)
* データ プール
* SQL Server マスター

   ![詳細なストレージ設定](media/notebooks-deploy/advanced-storage-settings.png)

### <a name="summary"></a>まとめ

この画面には、SQL Server 2019 ビッグ データ クラスターを展開するために指定したすべての入力がまとめられています。 **[Save config files]\(構成ファイルの保存\)** ボタンを使用して、構成ファイルをダウンロードできます。 展開の構成全体をノートブックにスクリプト化するには、 **[Script to Notebook]\(ノートブックにスクリプト化\)** を選択します。 ノートブックを開き、 **[Run Cells]\(セルの実行\)** を選択して、選択したターゲットへの SQL Server 2019 BDC の展開を始めます。

   ![まとめ](media/notebooks-deploy/deploy-sql-server-big-data-cluster-on-a-new-AKS-cluster.png)

## <a name="next-steps"></a>次のステップ

展開の詳細については、[SQL Server ビッグ データ クラスターの展開ガイダンス](deployment-guidance.md)に関するページを参照してください。