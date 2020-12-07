---
title: パフォーマンス、スナップショット、キャッシュ (Reporting Services) | Microsoft Docs
description: インストールに固有のパフォーマンス要因を理解し、必要な結果を生成するためにベースライン データを取得し、テストを実行する方法について説明します。
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- performance [Reporting Services]
- Reporting Services, performance
ms.assetid: 85afd00f-e8d7-4ef7-9174-2ff84d82f960
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 479347709474b12f84cb451b197a8df323c76e22
ms.sourcegitcommit: 827ad02375793090fa8fee63cc372d130f11393f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2020
ms.locfileid: "89480524"
---
# <a name="performance-snapshots-caching-reporting-services"></a>パフォーマンス、スナップショット、キャッシュ (Reporting Services)
  レポート サーバーのパフォーマンスには、ハードウェア、レポートに同時にアクセスするユーザー数、レポートのデータ量、出力形式など、さまざまな要因が絡み合って影響を与えます。 環境に固有のパフォーマンス要因を把握し、期待した結果を得るための対策を講じるには、ベースライン データを用意し、テストを実行する必要があります。 ツールとガイドラインの詳細については、MSDN の資料「 [Reporting Services のパフォーマンスの最適化](https://docs.microsoft.com/archive/blogs/sqlcat/reporting-services-performance-and-optimization) 」および「 [Visual Studio 2005 を使用した SQL Server 2005 Reporting Services レポート サーバーのロード テスト](https://go.microsoft.com/fwlink/?LinkID=77519)」を参照してください。  
  
 考慮する必要がある一般的な原則は次のとおりです。  
  
-   レポートの処理と表示には、多くのメモリを必要とします。 搭載メモリ量ができるだけ多いコンピューターを選択してください。  
  
-   レポート サーバーとレポート サーバー データベースを別個のコンピューターでホストした方が、1 台のハイエンド コンピューターで両方をホストするよりも、パフォーマンスが高くなる傾向があります。  
  
-   すべてのレポートの処理速度が低下している場合は、複数のレポート サーバー インスタンスで単一のレポート サーバー データベースをサポートするスケールアウト配置を検討します。 最適な結果を得るには、負荷分散ソフトウェアを使用して、配置全体に対して要求を均等に分散させるようにします。  
  
-   ある特定のレポートの処理速度だけが低下しているとき、そのレポートを要求時に実行する場合は、レポート データセット クエリをチューニングします。 また、キャッシュできる共有データセットの使用、レポートのキャッシュ、またはスナップショットとしてのレポートの実行を検討してください。  
  
-   特定の形式のすべてのレポートの処理速度が低下している場合 (PDF 形式で表示している場合など)、ファイル共有配信を検討するか、メモリを増設する、または、異なる形式を選択するようにします。  
  
-   レポート処理の所要時間など、使用状況のメトリックを調べるには、レポート サーバーの実行ログを参照します。 詳細については、「 [レポート サーバー実行ログと ExecutionLog3 ビュー](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)」を参照してください。  
  
-   メモリ管理構成設定をチューニングすることによってパフォーマンスの問題を緩和する方法の詳細については、「 [レポート サーバー アプリケーションで利用可能なメモリの構成](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [レポート サーバーのパフォーマンスの監視](../../reporting-services/report-server/monitoring-report-server-performance.md)  
 サーバー上の処理負荷を追跡する際に使用できるパフォーマンス オブジェクトについて説明します。  
  
 [レポート処理プロパティの設定](../../reporting-services/report-server/set-report-processing-properties.md)  
 要求時にキャッシュから、またはスケジュールに従ってレポート スナップショットとして、実行するレポートを構成する方法を説明します。  
  
 [レポート サーバー アプリケーションで利用可能なメモリの構成](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)  
 既定のメモリ管理動作をオーバーライドする方法を説明します。  
  
 [レポートのキャッシュ (SSRS)](../../reporting-services/report-server/caching-reports-ssrs.md)  
 レポート サーバー上でのレポートのキャッシュの動作を説明します。  
  
 [共有データセットのキャッシュ &#40;SSRS&#41;](../../reporting-services/report-server/cache-shared-datasets-ssrs.md)  
 レポート サーバー上での共有データセットのキャッシュの動作を説明します。  
  
 [サイズの大きなレポートの処理](../../reporting-services/report-server/process-large-reports.md)  
 サイズの大きいレポートを構成および配布する際の推奨事項を記載しています。  
  
 [レポートおよび共有データセット処理のタイムアウト値の設定 &#40;SSRS&#41;](../../reporting-services/report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)  
 クエリとレポート処理にタイムアウトを設定する方法について説明します。  
  
## <a name="see-also"></a>参照  
 [Manage a Running Process](../../reporting-services/subscriptions/manage-a-running-process.md)   
 [レポート実行の確認](../../reporting-services/report-server/verifying-a-report-run.md)  
  
  
