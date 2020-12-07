---
title: ビッグ データ クラスター (BDC) の管理リソース
titleSuffix: SQL Server
description: この記事では、Azure Data Studio、ノートブック、および Azure Data CLI (azdata) コマンドを使用して、ビッグ データ クラスターの状態を表示する方法について説明します。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 10/20/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5d469d1b8d89b07748485c9df3f7f7905af52099
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358230"
---
# <a name="administration-resources-for-big-data-clusters-bdc"></a>ビッグ データ クラスター (BDC) の管理リソース 

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

この記事では、SQL Server ビッグ データ クラスターを外部から管理する方法について説明します。

## <a name="know-your-architecture"></a>アーキテクチャを理解する

SQL Server 2019 (15.x) 以降、SQL Server ビッグ データ クラスターを使用すると、Kubernetes 上で動作する SQL Server、Spark、および HDFS コンテナーのスケーラブルなクラスターを展開できます。 次の記事では、ビッグ データ クラスターの概要について説明されています。
- [SQL Server ビッグ データ クラスターとは](big-data-cluster-overview.md)

SQL Server ビッグ データ クラスターにより、明確で一貫性のある承認と認証が提供されます。 ビッグ データ クラスターのセキュリティの概要については、次の記事を参照してください。
- [SQL Server ビッグ データ クラスターのセキュリティの概念](concept-security.md)

## <a name="manage-and-operate-with-tools"></a>ツールを使用して管理および操作する

次の記事は、ビッグ データ クラスターを次の方法で管理および操作する方法について説明しています。 

- [Azure Data Studio を使用して SQL Server ビッグ データ クラスターに接続する](connect-to-big-data-cluster.md)
- [SQL Server コントローラー ダッシュボードのビッグ データ クラスターを管理する](manage-with-controller-dashboard.md)
- [Azure Data Studio ノートブックを使用して SQL Server ビッグ データ クラスターを管理する](notebooks-manage-bdc.md)
- [ノートブックを使用してクラスター上でビッグ データ クラスター (BDC) を管理する](cluster-manage-notebooks.md)
- [Spark を使用したサンプル ノートブックの実行](notebooks-tutorial-spark.md)

## <a name="monitor-with-tools"></a>ツールを使用して監視する

次の記事は、ビッグ データ クラスターを次の方法で監視する方法について説明しています。 

- [Azure Data Studio を使用して BDC クラスターを監視する](cluster-monitor-ads.md)
- [Azdata ユーティリティを使用して BDC クラスターを監視する](cluster-monitor-cmdlet.md)
- [Grafana ダッシュボードを使用して BDC クラスターを監視する](cluster-monitor-grafana.md)
- [Jupyter ノートブックと Azure Data Studio を使用して BDC クラスターを監視する](cluster-monitor-notebooks.md)

## <a name="monitor-and-inspect-logs-with-notebooks"></a>ノートブックを使用してログを監視および検査する

次の記事には、Azure Data Studio で使用できる Jupyter ノートブックの多くが一覧表示されています。

- [ノートブックを使用したクラスターの監視](cluster-monitor-notebooks.md)
- [ノートブックを使用したクラスター内のログの収集と分析](cluster-logging-notebooks.md)

## <a name="big-data-clusters-troubleshooting-resources"></a>ビッグ データ クラスターのトラブルシューティングに関するリソース

次の記事では、ビッグ データ クラスターのトラブルシューティングを行う方法が説明されています。

- [kubectl ユーティリティを使用した BDC クラスターのトラブルシューティング](cluster-troubleshooting-commands.md) 
- [Pyspark ノートブックのトラブルシューティング](troubleshoot-pyspark-notebook.md)
- [Jupyter ノートブックと Azure Data Studio (ADS) を使用した BDC クラスターのトラブルシューティング](cluster-troubleshooter-notebooks.md)
- [HDFS のアクセス許可の復元](troubleshoot-hdfs-restore-admin.md)

次の記事では、Active Directory モードで展開されたビッグ データ クラスターのトラブルシューティングを行う方法が説明されています。
- [Active Directory モードでの BDC クラスターのトラブルシューティング](troubleshoot-active-directory.md) 
- [AD モード ログイン失敗のトラブルシューティング](troubleshoot-ad-login-failed-untrusted-domain.md)
- [BDC AD モードのデプロイが停止した場合のトラブルシューティング](troubleshoot-ad-reverse-lookup-zone.md)

## <a name="next-steps"></a>次のステップ

ビッグ データ クラスターの詳細については、[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] とは](big-data-cluster-overview.md)の概要に関するページを参照してください。