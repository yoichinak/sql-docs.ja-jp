---
title: Grafana ダッシュボードを使用したクラスターの監視
titleSuffix: SQL Server Big Data Clusters
description: SQL Server 2019 ビッグ データ クラスター上で Grafana ダッシュボードを使用したクラスターの監視。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 09/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ee0ceb3a9f86fc2a7fabe44e9279b7e63dabfb8b
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98091687"
---
# <a name="monitor-cluster-with-azdata-and-grafana-dashboard"></a>azdata と Grafana ダッシュボードを使用してクラスターを監視する

この記事では、SQL Server ビッグ データ クラスター内でアプリケーションを監視する方法について説明します。

## <a name="prerequisites"></a>前提条件

- [SQL Server 2019 ビッグ データ クラスター](deployment-guidance.md)
- [azdata コマンドライン ユーティリティ](../azdata/install/deploy-install-azdata.md)

## <a name="capabilities"></a>機能

SQL Server 2019 では、アプリケーションの作成、削除、説明、初期化、一覧の実行、更新を行うことができます。 次の表では、**azdata** で使用できるアプリケーションの展開コマンドについて説明します。

|コマンド |説明 |
|:---|:---|
|`azdata bdc endpoint list` | ビッグ データ クラスターのエンドポイントを一覧表示します。 |


次の例を利用し、**Grafana ダッシュボード** のエンドポイントをリストアップできます。

```bash
azdata bdc endpoint list --endpoint-name metricsui 
```

表示されたエンドポイントには、クラスターのユーザー名とパスワードを使用してログインできます。 

![Grafana ダッシュボード](media/big-data-cluster-monitor-apps/grafana-dashboard-endpoint.png)

`nodeMetricsUrl` と `sqlMetricsUrl` の値は、Kubernetes ノードのメトリックとビッグ データ クラスターのサービス メトリックを監視するための Grafana ダッシュボードにリンクされています。

![grafana ダッシュボード](./media/view-cluster-status/grafana-dashboard.png)

![SQL](./media/view-cluster-status/grafana-sql-status.png)



## <a name="next-steps"></a>次のステップ

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]の詳細については、「[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]とは](big-data-cluster-overview.md)」を参照してください。