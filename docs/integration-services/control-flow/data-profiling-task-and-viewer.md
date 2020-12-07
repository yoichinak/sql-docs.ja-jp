---
description: データ プロファイル タスクとビューアー
title: データ プロファイル タスクとビューアー | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling task [Integration Services], about data profiling
- data profiling
- profiling data
ms.assetid: 756840e3-aa09-45cd-9951-1a17af4b5925
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ad5a2f88c170477095627a5f6da33b089424dcc4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495992"
---
# <a name="data-profiling-task-and-viewer"></a>データ プロファイル タスクとビューアー

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  データ プロファイル タスクを使用すると、データの抽出、変換、および読み込みを行うプロセス内でデータのプロファイルを実行できます。 データ プロファイル タスクを使用することによって、次のような利点があります。  
  
-   ソース データをより効果的に分析できます。  
  
-   ソース データに関する理解を深めることができます。  
  
-   データ ウェアハウスに読み込まれる前にデータ品質の問題を回避できます。  
  
> [!IMPORTANT]  
>  データ プロファイル タスクは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に格納されているデータでのみ機能します。 サードパーティまたはファイル ベースのデータ ソースでは機能しません。  
  
## <a name="data-profiling-overview"></a>データ プロファイルの概要  
 データ品質は、すべてのビジネスにとって重要です。 企業はトランザクション システム上に分析システムおよびビジネス インテリジェンス システムを構築するので、主要業績評価指標とデータ マイニング予測の信頼性は、基になるデータの有効性に完全に依存します。 ただし、ビジネス上の意思決定における有効なデータの重要性は高まっていますが、このデータの有効性を確保することも難しくなっています。 データはさまざまなシステムやソースおよび多くのユーザーから企業に絶えず流れ込んできています。  
  
 データ品質の基準はドメインまたはアプリケーションに固有であるため、定義が困難な場合があります。 データ品質を定義する一般的な方法の 1 つとして、データのプロファイルが挙げられます。  
  
 データ プロファイルは、次のようなデータに関する集計統計のコレクションです。  
  
-   Customer テーブルの行数。  
  
-   State 列の個別の値の数。  
  
-   Zip 列の NULL 値または不足値の数。  
  
-   City 列の値の分布。  
  
-   Zip 列に対する State 列の機能依存の強さ。つまり、都道府県は特定の郵便番号の値に対して常に同じである必要があります。  
  
 データ プロファイルに示される統計によって、ソース データを使用することで生じる可能性がある品質の問題を効果的に最小限に抑えるために必要な情報を得ることができます。  
  
## <a name="integration-services-and-data-profiling"></a>Integration Services とデータ プロファイル  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]におけるデータのプロファイル処理は、次の手順で構成されています。  
  
 **手順 1 : データ プロファイル タスクの設定**  
 データ プロファイル タスクは、計算するプロファイルを構成するために使用するタスクです。 データ プロファイル タスクが含まれているパッケージを実行して、プロファイルを計算します。 このタスクによって、XML 形式のプロファイル出力がファイルまたはパッケージ変数に保存されます。  
  
 **詳細情報:** [データ プロファイル タスクのセットアップ](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)  
  
 **手順 2 : データ プロファイル タスクで計算されたプロファイルの確認**  
 データ プロファイル タスクで計算されたデータ プロファイルを表示するには、出力をファイルに送信して Data Profile Viewer を使用します。 このビューアーは、サマリ形式とオプションのドリル ダウン機能を使用した詳細形式の両方でプロファイル出力を表示するスタンドアロンのユーティリティです。  
  
 **詳細情報:** [Data Profile Viewer](../../integration-services/control-flow/data-profile-viewer.md)  
  
### <a name="addition-of-conditional-logic-to-the-data-profiling-workflow"></a>データ プロファイル ワークフローへの条件ロジックの追加  
 データ プロファイル タスクには、プロファイルの出力に基づいてこのタスクを下流のタスクに接続するための条件ロジックを使用できるようにする機能が組み込まれていません。 ただし、スクリプト タスクで少量のプログラミングを行って、このロジックを簡単に追加することができます。 たとえば、スクリプト タスクでは、データ プロファイル タスクの出力ファイルに対して XPath クエリを実行できます。 このクエリによって、特定の列の NULL 値の比率が特定のしきい値を超えていないかどうかを判断できます。 比率がしきい値を超えている場合は、パッケージを中断し、ソース データの問題を解決してから続行することができます。 詳細については、「 [パッケージ ワークフローでデータ プロファイル タスクを使用する](../../integration-services/control-flow/incorporate-a-data-profiling-task-in-package-workflow.md)」をご覧ください。  
  
## <a name="related-content"></a>関連コンテンツ  
 [Data Profiler スキーマ](https://go.microsoft.com/fwlink/?LinkId=251524)  
  
  
