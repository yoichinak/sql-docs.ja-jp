---
title: SQL Server アップグレードの分析レポートの表示
description: Database Experimentation Assistant (DEA) でパフォーマンスに関する洞察の分析レポートを表示して理解する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 02/04/2020
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: pochiraju
ms.author: rajpo
ms.reviewer: mathoma
ms.openlocfilehash: d1666d4ba2279623065dd3c0d8faf5e0653de82e
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100065947"
---
# <a name="view-analysis-reports-in-database-experimentation-assistant"></a>Database Experimentation Assistant で分析レポートを表示する

Database Experimentation Assistant (DEA) を使用して [分析レポートを作成](database-experimentation-assistant-create-report.md)した後、実行した A/B テストに基づいて、パフォーマンスの洞察をレポートで確認できます。

## <a name="open-an-existing-analysis-report"></a>既存の分析レポートを開く

1. DEA で、リストアイコンを選択し、サーバー名と認証の種類を指定して、シナリオに応じて [ **接続の暗号化** ] と [ **サーバー証明書の信頼** ] チェックボックスをオンまたはオフにし、[ **接続**] を選択します。

   ![レポートを使用してサーバーに接続する](./media/database-experimentation-assistant-view-report/dea-connect-to-server-with-report-files.png)

2. [ **分析レポート** ] 画面の左側で、表示するレポートのエントリを選択します。

   ![既存のレポートファイルを開く](./media/database-experimentation-assistant-view-report/dea-select-report-to-view.png)

## <a name="view-and-understand-the-analysis-report"></a>分析レポートを表示して理解する

このセクションでは、分析レポートについて説明します。

レポートの最初のページには、実験が実行された対象サーバーのバージョンとビルド情報に関する情報が表示されます。 しきい値を使用すると、A/B テスト分析の感度や許容範囲を調整できます。 既定では、しきい値は 5%; に設定されます。パフォーマンスの向上 (>= 5%) は、"向上" として分類されます。  ドロップダウンリストを使用すると、パフォーマンスしきい値が異なるレポートを評価できます。

レポート内のデータを CSV ファイルにエクスポートするには、[ **エクスポート** ] ボタンを選択します。  分析レポートの任意のページで [ **印刷** ] を選択すると、その時点で画面に表示される内容を印刷できます。

### <a name="query-distribution"></a>クエリの配布

- 円グラフのさまざまなスライスを選択すると、そのカテゴリに属するクエリのみが表示されます。

   ![カテゴリを円スライスとしてレポートする](./media/database-experimentation-assistant-view-report/dea-view-report-pie-slices.png)

  - **低下**: ターゲット2で、ターゲット1よりも悪化したクエリ。
  - **エラー**: 少なくとも1つのターゲットに対して少なくとも1回エラーを示したクエリ。
  - **改善**: ターゲット2でより適切に実行されたクエリがターゲット1よりも優れています。
  - **評価できません**: サンプルサイズが小さすぎるクエリは、統計分析に使用できません。 A/B テスト分析の場合、DEA では、各ターゲットで同じクエリに対して少なくとも15回の実行が必要です。
  - **同じ**: ターゲット1とターゲット2の間に統計的な差がないクエリ。

  エラークエリ (存在する場合) は、別のグラフに表示されます。エラーを種類別に分類し、円グラフでエラーをエラー ID 別に分類する棒グラフ。

   ![エラークエリのグラフ](./media/database-experimentation-assistant-view-report/dea-error-query-charts.png)

  次の4種類のエラーが考えられます。

  - [**既存のエラー**]: ターゲット1とターゲット2の両方に存在するエラー。
  - **新しいエラー**: ターゲット2の新しいエラー。
  - **解決済みのエラー**: ターゲット1に存在するが、ターゲット2で解決されるエラー。
  - **アップグレードブロッカー**: 対象サーバーへのアップグレードをブロックするエラー。

  グラフの横棒または円のセクションをクリックすると、カテゴリにドリルダウンされ、[ **評価できません** ] カテゴリの場合でも、パフォーマンスメトリックが表示されます。

  さらに、ダッシュボードには、パフォーマンスの概要をすばやく向上させるために、上位5つの改善および低下したクエリが表示されます。

### <a name="individual-query-drill-down"></a>個々のクエリのドリルダウン

クエリテンプレートのリンクを選択すると、特定のクエリに関する詳細情報を確認できます。

![特定のクエリにドリルダウンする](./media/database-experimentation-assistant-view-report/dea-query-drill-down-report.png)

- 特定のクエリを選択すると、関連する比較の概要が表示されます。

   ![比較の概要](./media/database-experimentation-assistant-view-report/dea-view-report-comparison-summary.png)

   実行回数、平均期間、平均 CPU、平均読み取り/書き込み数、エラー数など、そのクエリの概要統計情報を確認できます。  クエリがエラークエリの場合、エラーの詳細が [ **エラー情報** ] タブに表示されます。  [ **クエリプラン情報** ] タブでは、ターゲット1とターゲット2でクエリに使用されるクエリプランに関する情報を確認できます。

   > [!NOTE]
   > 拡張イベントを分析している場合 (の場合)。XEL) ファイル、クエリプラン情報は収集されず、ユーザーのコンピューターのメモリ負荷が制限されます。

## <a name="see-also"></a>関連項目

- コマンドプロンプトで分析レポートを生成する方法については、「 [コマンドプロンプトでの実行](database-experimentation-assistant-run-command-prompt.md)」を参照してください。
