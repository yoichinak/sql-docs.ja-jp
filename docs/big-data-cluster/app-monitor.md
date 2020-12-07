---
title: azdata と Grafana ダッシュボードでアプリケーションを監視する
titleSuffix: SQL Server Big Data Clusters
description: SQL Server 2019 ビッグ データ クラスターで azdata と Grafana を利用し、アプリケーションを監視する
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 08/16/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1391b88f2762293aa4eebf255682605bf5b6b1e0
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257282"
---
# <a name="monitor-applications-with-azdata-and-grafana-dashboard"></a>azdata と Grafana ダッシュボードでアプリケーションを監視する

Grafana は最良のクラウドネイティブ仮想化ツールの 1 つで、Kubernetes で実行されているアプリケーションのさまざまな監視メトリックを提供する目的で利用できます。  

この記事では、SQL Server ビッグ データ クラスター内でアプリケーションを監視する方法について説明します。

## <a name="prerequisites"></a>前提条件

- [SQL Server 2019 ビッグ データ クラスター](deployment-guidance.md)
- [[!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]](../azdata/install/deploy-install-azdata.md)

## <a name="capabilities"></a>機能

SQL Server 2019 では、アプリケーションの作成、削除、説明、初期化、一覧の実行、更新を行うことができます。 次の表では、**azdata** で使用できるアプリケーションの展開コマンドについて説明します。

|コマンド |説明 |
|:---|:---|
|`azdata bdc endpoint list` | ビッグ データ クラスターのエンドポイントを一覧表示します。 |


次の例を利用し、**Grafana ダッシュボード**のエンドポイントをリストアップできます。

```bash
azdata bdc endpoint list --endpoint-name metricsui 
```

表示されたエンドポイントには、クラスターのユーザー名とパスワードを使用してログインできます。 

![Grafana ダッシュボード](media/big-data-cluster-monitor-apps/grafana-dashboard-endpoint.png)


ダッシュボードを開いたら、 **[Host Apps Metrics]\(ホスト アプリ メトリック)\** に進みます。ここではアプリケーションに関する分析情報がさらに得られ、追跡できます。  

![ホスト アプリ メトリック](media/big-data-cluster-monitor-apps/host-apps-metrics.png)


アプリケーションの 1 ポッドに関する分析情報をさらに得るには (アプリケーションには複数のコピーが存在する場合があります)、 **[Host Apps Metrics]\(ホスト アプリ メトリック)\**   に移動し、ポッドを選択します。メトリックが次のように表示されます。  

![ホスト ポッド メトリック](media/big-data-cluster-monitor-apps/host-pods-metrics.png) 


## <a name="next-steps"></a>次のステップ

その他のサンプルにはついては、[アプリの展開サンプル](https://aka.ms/sql-app-deploy)に関するページを参照してください。

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]の詳細については、「[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]とは](big-data-cluster-overview.md)」を参照してください。