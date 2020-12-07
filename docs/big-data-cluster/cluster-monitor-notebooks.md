---
title: Jupyter ノートブックと Azure Data Studio を使用してクラスターを監視する
titleSuffix: SQL Server Big Data Clusters
description: SQL Server 2019 ビッグ データ クラスター上での Jupyter ノートブックと Azure Data Studio を使用したクラスターの監視。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 10/01/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 516b1bb461e5927ff52f0cee79e48d9945e6da21
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92378504"
---
# <a name="monitoring-cluster-with-notebooks"></a>ノートブックを使用したクラスターの監視

このページは、SQL Server ビッグ データ クラスター用のノートブックのインデックスです。 これらの実行可能ノートブック (.ipynb) は、ビッグ データ クラスターの監視に役立つように SQL Server 2019 向けに設計されています。

各ノートブックは、独自の依存関係を確認するように設計されています。 **[Run all cells]\(すべてのセルを実行\)** を使用すると、正常に完了するか、例外が発生し、欠落している依存関係を解決するための別のノートブックにハイパーリンクされたヒントが示されます。 後続のノートブックへのヒント ハイパーリンクに従い、 **[Run all cells]\(すべてのセルを実行\)** をクリックし、成功した場合は元のノートブックに戻り、 **[Run all cells]\(すべてのセルを実行\)** をクリックします。

すべての依存関係がインストールされていても、 **[Run all cells]\(すべてのセルを実行\)** に失敗した場合は、各ノートブックを使用して結果を分析し、可能であれば、問題の解決にさらに役立つように別のノートブックにハイパーリンクされたヒントを生成します。


## <a name="monitoring-kubernetes"></a>Kubernetes の監視

このセクションには、`azdata` コマンド ライン インターフェイス (CLI) を使用して SQL Server ビッグ データ クラスターに関する情報と状態を取得するのに役立つ一連のノートブックが含まれています。

|名前 |説明 |
|---|---|---|---|
|TSG006 - システム ポッドの状態を取得する|すべてのシステム ポッドの状態を表示します。 |
|TSG007 - BDC ポッドの状態を取得する|ビッグ データ クラスター ポッドの状態を表示します。|
|TSG008 - バージョン情報を取得する (Kubernetes)|Kubernetes クラスター情報を取得します。|
|TSG009 - ノードの取得 (Kubernetes)|kubernetes コンテキストを取得します。 |
|TSG010 - 構成コンテキストを取得する|DMV クエリを使用して、クエリ プロセッサの内部エラーに関する詳細情報を取得します。|
|TSG015 - BDC サービスを表示する (Kubernetes)|Kubernetes クラスターにデプロイされている BDC クラスターのサービスの状態を取得します。 |
|TSG016 - BDC ポッドの説明|Kubernetes クラスターにデプロイされている BDC のポッドの状態を取得します。 |
|TSG020 - ノードを説明する (Kubernetes)|kubectl コマンド ライン インターフェイスを使用して BDC クラスターのノード情報を取得します。 |
|TSG021 - クラスター情報を取得する (Kubernetes)|Kubernetes クラスター情報を取得します。 |
|TSG022 - kubeadm ホストの外部 IP アドレスを取得する|kubeadm のホストの外部 IP アドレスを取得します。 |
|TSG023 - すべての BDC オブジェクトを取得する (Kubernetes)|システム名前空間とビッグ データ クラスター名前空間のすべての Kubernetes リソースの概要を取得します。 |
|TSG042 - ノード名およびデータとログの PVC の外部マウントを取得する|データとログの外部マウントと共に、ポッドをホストするノード名を取得します。 |
|TSG063 - ストレージ クラスを取得する (Kubernetes)|このノートブックを使用して、Kubernetes ストレージ クラスを取得します。 |
|TSG064 - BDC 永続ボリューム要求を取得する|ビッグ データ クラスターの永続ボリューム要求 (PVC) を表示します。 |
|TSG065 - BDC シークレットを取得する (Kubernetes)|ビッグ データ クラスターのシークレットを表示します。 |
|TSG066 - BDC イベントを取得する (Kubernetes)|ビッグ データ クラスターのイベントを表示します。|
|TSG072 - 永続ボリュームを取得する (Kubernetes)|Kubernetes クラスターの永続ボリューム (PV) を表示します。 永続ボリュームは、非名前空間オブジェクトです。 |
|TSG081 - 名前空間を取得する (Kubernetes)|kubernetes 名前空間を取得します。 |
|TSG089 - BDC の実行されていないポッドの説明|Kubernetes クラスターの実行されていない BDC ポッドを示します。 |
|TSG097 - BDC のステートフル セットを取得する (Kubernetes)|Kubernetes クラスターの BDC statefulset を表示します。 |
|TSG098 - BDC replicaset を取得する (Kubernetes)|Kubernetes クラスターの BDC statefulset を示します。 |
|TSG099 - BDC daemonset の取得 (Kubernetes)|Kubernetes クラスターの BDC daemonset を示します。 |


## <a name="monitor-big-data-cluster-bdc"></a>ビッグ データ クラスター (BDC) の監視

このセクションには、SQL Server ビッグ データ クラスター (BDC) をホストしている Kubernetes クラスターに関する情報と状態を取得するのに役立つ一連のノートブックが含まれています。

|名前 |説明 |
|---|---|---|---|
|TSG003 - BDC Spark セッションを表示する|BDC Spark セッションを表示します。 |
|TSG004 - BDC アプリを表示する|BDC クラスターで稼働しているアプリを表示します。|
|TSG012 - BDC の状態を表示する|BDC クラスターのさまざまなコンポーネントの現在の状態を取得します。|
|TSG013 - 記憶域プール (HDFS) のファイル一覧を表示する|記憶域プール (HDFS) のファイル一覧を取得します。 |
|TSG014 - BDC エンドポイントを表示する|BDC クラスターで使用可能なすべてのエンドポイントを取得します。|
|TSG017 - BDC 構成を表示する|BDC 構成を取得します。 |
|TSG033 - BDC SQL の状態を表示する|Kubernetes クラスターにデプロイされている BDC の SQL Server の状態を取得します。 |
|TSG049 - BDC コントローラーの状態を表示する|Kubernetes クラスターにデプロイされている BDC のコントローラーの状態を取得します。 |
|TSG068 - BDC HDFS の状態を表示する|Kubernetes クラスターにデプロイされている BDC の HDFS の状態を取得します。 |
|TSG069 - ビッグ データ クラスターのゲートウェイの状態を表示する|Kubernetes クラスターにデプロイされている BDC のゲートウェイの状態を取得します。 |
|TSG070 - SQL マスター プールに対してクエリを実行する| マスター インスタンスで SQL クエリを実行します。 |

## <a name="next-steps"></a>次のステップ

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]の詳細については、「[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]とは](big-data-cluster-overview.md)」を参照してください。
