---
title: コントローラー ダッシュボードで SQL Server ビッグ データ クラスターを管理する
titleSuffix: Manage SQL Server big data cluster with controller dashboard
description: Azure Data Studio のノートブックを使用して、ビッグ データ クラスターの管理とトラブルシューティングを行います。
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 64352409e567c5854d348dce8e6545317b41bc01
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725823"
---
# <a name="manage-big-data-clusters-for-sql-server-controller-dashboard"></a>SQL Server コントローラー ダッシュボードのビッグ データ クラスターを管理する

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

**azdata** とクラスターの状態ノートブックに加えて、SQL Server ビッグ データ クラスターの状態を表示する別の方法があります。 **接続** Viewlet を使用して、SQL Server ビッグ データ クラスター コントローラーを追加できます。 これにより、ダッシュボードを使用してクラスターの正常性を表示できます。

![dashboard](media/manage-with-controller-dashboard/controller-dashboard.png)
## <a name="prerequisites"></a>前提条件

ノートブックを起動するには、次の前提条件が要件です。

* [Azure Data Studio](../azure-data-studio/download-azure-data-studio.md) の最新版
* [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 拡張機能が Azure Data Studio にインストールされている](../azure-data-studio/data-virtualization-extension.md)

上記に加えて、SQL Server 2019 ビッグ データ クラスターでは以下のものも必要です。

* **azdata**
    - [Windows インストーラー](../azdata/install/deploy-install-azdata-installer.md)
    - [Linux パッケージ マネージャー](../azdata/install/deploy-install-azdata-linux-package.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Azure CLI](/cli/azure/install-azure-cli)

## <a name="add-sql-server-big-data-cluster-controller"></a>SQL Server ビッグ データ クラスター コントローラーを追加する

1. 左側のウィンドウで、[接続] ビューをクリックします。
2. [接続] ビューの下部にある **[SQL Server Big Data Clusters]\(SQL Server ビッグ データ クラスター\)** をクリックして展開します。
3. **[Add SQL Server big data cluster controller]\(SQL Server ビッグ データ クラスター コントローラーの追加\)** をクリックすると、新しいダイアログが表示されます。

## <a name="add-new-controller"></a>新しいコントローラーを追加する

1. クラスターの名前を追加します。
2. クラスター管理サービスの URL を追加します。 これは、BDC ダッシュボードのサービス エンドポイントのテーブルで確認できます。または、クラスター管理者に問い合わせてください。
3. ユーザー名とパスワードを追加します。

## <a name="launch-controller-dashboard"></a>コントローラー ダッシュボードを起動する

1. コントローラーが正常に追加されると、[SQL Server Big Data Clusters]\(SQL Server ビッグ データ クラスター\) の下に表示されます。
2. ダッシュボードを起動するには、コントローラーを右クリックし、 **[管理]** をクリックします。

## <a name="controller-dashboard"></a>コントローラー ダッシュボード

1. コントローラー ダッシュボードには、次の 3 つの主要なコンポーネントがあります。

    - ダッシュボードの操作が含まれている上部の**ツール バー**。
    - ダッシュボードのさまざまなビューを変更する左側の**ナビゲーション ウィンドウ**。
    - ページの大部分をカバーしている**ビュー**。

2. **[Big data cluster overview]\(ビッグ データ クラスターの概要\)** ページでは、次の情報を確認できます。

    - クラスターに関する情報が表示される **[Cluster Properties]\(クラスターのプロパティ\)** 。
    - すべてのクラスター コンポーネントの概要と異常なコンポーネントが表示される **[Cluster Overview]\(クラスターの概要\)**
    - SQL Server ビッグ データ クラスター内のさまざまなサービスをコピーしたり、サービスにアクセスしたりするための **[Service Endpoints]\(サービス エンドポイント\)** 。

3. **ナビゲーション ウィンドウ**では、サービスの一覧を見ることができ、クリックすると追加のクラスターの詳細が表示されます。 これは、 **[Cluster Overview]\(クラスターの概要\)** でサービスをクリックしたときのビューと同じです。

4. **[Cluster Details]\(クラスターの詳細\)** の各ビューは、同じ UI コンポーネントで構成されています。

    - コンポーネントの状態と正常性ステータスが共有される **[Health Status Details]\(正常性状態の詳細\)** 。
    - Grafana と Kibana により追加のメトリックとログが表示される **[Metrics and Logs]\(メトリックとログ\)** 。

1. 問題のあるコンポーネントが表示されている場合、ツール バーの **[Troubleshoot]\(トラブルシューティング\)** をクリックして、問題の診断に役立つノートブックが含まれる Jupyter Book を起動します。

## <a name="next-steps"></a>次の手順

コントローラーの詳細については、[コントローラーのドキュメント](concept-controller.md)を参照してください。