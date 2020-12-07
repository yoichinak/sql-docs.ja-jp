---
title: Jupyter ノートブックと Azure Data Studio を使用したログの収集と分析
titleSuffix: SQL Server Big Data Clusters
description: SQL Server 2019 ビッグ データ クラスター上での Jupyter ノートブックと Azure Data Studio を使用したクラスターのログ。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 09/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5efb20db2b0f5e3d3509715a8711ce32414fa9ee
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92378408"
---
# <a name="gathering-and-analyzing-logs-in-the-cluster-with-notebooks"></a>ノートブックを使用したクラスター内のログの収集と分析

このページは、SQL Server ビッグ データ クラスター用のノートブックのインデックスです。 これらの実行可能ノートブック (.ipynb) は、ビッグ データ クラスターのログに役立つように SQL Server 2019 向けに設計されています。

各ノートブックは、独自の依存関係を確認するように設計されています。 **[Run all cells]\(すべてのセルを実行\)** を使用すると、正常に完了するか、例外が発生し、欠落している依存関係を解決するための別のノートブックにハイパーリンクされたヒントが示されます。 後続のノートブックへのヒント ハイパーリンクに従い、 **[Run all cells]\(すべてのセルを実行\)** をクリックし、成功した場合は元のノートブックに戻り、 **[Run all cells]\(すべてのセルを実行\)** をクリックします。

すべての依存関係がインストールされていても、 **[Run all cells]\(すべてのセルを実行\)** に失敗した場合は、各ノートブックを使用して結果を分析し、可能であれば、問題の解決にさらに役立つように別のノートブックにハイパーリンクされたヒントを生成します。

## <a name="gathering-logs-from-big-data-cluster-bdc"></a>ビッグ データ クラスター (BDC) からのログの収集

このセクションには、SQL Server ビッグ データ クラスター(BDC) からのログ取得に役立つ一連のノートブックが含まれています。

| 名前 | 説明 |
|--|--|
| TSG001 - azdata copy-logs を実行する | azdata コマンド ライン インターフェイスを使用して、BDC クラスターのデータをコピーします。 |
| TSG061 - BDC 名前空間内にあるポッドのすべてのコンテナー ログの末尾を取得する | 名前空間の BDC クラスターからポッドのすべてのコンテナー ログを取得します。 |
| TSG062 - BDC 名前空間内にあるポッドのすべての以前のコンテナー ログの末尾を取得する | 名前空間の BDC クラスターからポッドの以前のすべてのコンテナー ログを取得します。 |
| TSG083 - kubectl cluster-info dump を実行する | kubetl コマンド ライン インターフェイスを使用して、BDC クラスター関連の情報をダンプします。 |
| TSG084 - 内部クエリ プロセッサ エラー | DMV クエリを使用して、クエリ プロセッサの内部エラーに関する詳細情報を取得します。 |
| TSG091 - azdata CLI ログを取得する | ローカル コンピューターから azdata ログを取得します。 |



## <a name="analyse-logs-from-big-data-clusters-bdc"></a>ビッグ データ クラスター (BDC) からのログを分析する

SQL Server ビッグ データ クラスターからログを収集して分析するための一連のノートブック。  分析プロセスによって、ログで見つかった既知の問題に対して実行する追加のノートブックが提案されます。

|名前|説明 |
|---|---|
|TSG030 - SQL Server のエラー ログ ファイル|SQL Server errorlog ファイルを取得し、ログ エントリを分析して、さらに関連するトラブルシューティング ガイドを提案します。 |
|TSG031 - SQL Server PolyBase ログ|SQL Server PolyBase ログを取得し、ログ エントリを分析して、さらに関連するトラブルシューティング ガイドを提案します。|
|TSG034 - Livy ログ|Livy ログを取得し、ログ エントリを分析して、さらに関連するトラブルシューティング ガイドを提案します。|
|TSG035 -Spark History ログ|Spark History ログを取得し、ログ エントリを分析して、さらに関連するトラブルシューティング ガイドを提案します。|
|TSG036 - コントローラー ログ|コントローラー ログの最後の 'n' 時間を取得し、ログ エントリを分析して、関連するトラブルシューティング ガイドをさらに提案します。|
|TSG046 - Knox ゲートウェイ ログ|Knox によってクライアントに 500 エラーが返され、根本的な問題の原因を示す詳細 (スタック) が削除されます。 そのため、このノートブックを使って、クラスターから Knox ログを取得します。 Knox ゲートウェイ ログを取得し、ログ エントリを分析して、さらに関連するトラブルシューティング ガイドを提案します。|
|TSG073 - InfluxDB ログ|InfluxDB ログを取得し、ログ エントリを分析して、さらに関連するトラブルシューティング ガイドを提案します。|
|TSG076 - Elastic Search ログ|Elastic Search ログを取得し、ログ エントリを分析して、さらに関連するトラブルシューティング ガイドを提案します。|
|TSG077 - Kibana ログ|Kibana ログを取得し、ログ エントリを分析して、さらに関連するトラブルシューティング ガイドを提案します。|
|TSG088 - Hadoop datanode ログ|Hadoop datanode ログを取得し、ログ エントリを分析して、さらに関連するトラブルシューティング ガイドを提案します。|
|TSG090 - Yarn nodemanager ログ|Yarn nodemanager ログを取得し、ログ エントリを分析して、さらに関連するトラブルシューティング ガイドを提案します。|
|TSG092 - BDC 内のすべてのコンテナーの Supervisord ログの末尾|BDC 内のすべてのコンテナーの Supervisord ログの末尾を取得し、ログ エントリを分析して、さらに関連するトラブルシューティング ガイドを提案します。|
|TSG093 - BDC 内のすべてのコンテナーのエージェント ログの末尾|BDC 内のすべてのコンテナーのエージェント ログの末尾を取得し、ログ エントリを分析して、さらに関連するトラブルシューティング ガイドを提案します。|
|TSG094 - Grafana ログ|Grafana ログを取得し、ログ エントリを分析して、さらに関連するトラブルシューティング ガイドを提案します。|
|TSG095 - Hadoop namenode ログ|Hadoop namenode ログを取得し、ログ エントリを分析して、さらに関連するトラブルシューティング ガイドを提案します。|
|TSG096 - Zookeeper ログ|Zookeeper ログを取得し、ログ エントリを分析して、さらに関連するトラブルシューティング ガイドを提案します。|

## <a name="next-steps"></a>次のステップ

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]の詳細については、「[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]とは](big-data-cluster-overview.md)」を参照してください。
