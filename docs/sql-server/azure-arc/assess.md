---
title: Azure Arc 対応 SQL Server インスタンスでオンデマンド SQL Assessment を構成する
description: Azure Arc 対応 SQL Server インスタンスでオンデマンド SQL Assessment を構成する
author: anosov1960
ms.author: sashan
ms.reviewer: mikeray
ms.date: 09/10/2020
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: c6f2a0989cb13253ef4a6a26e013a6b8c7a84ded
ms.sourcegitcommit: f888ac94c7b5f6b6f138ab75719dadca04e8284a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93294377"
---
# <a name="configure-sql-assessment-on-an-azure-arc-enabled-sql-server-instance"></a>Azure Arc 対応 SQL Server インスタンスで SQL Assessment を構成する

SQL Assessment には、SQL Server の構成を評価するためのメカニズムが用意されています。 この記事では、Azure Arc 対応 SQL Server インスタンスで SQL Assessment を使用する手順について説明します。

## <a name="prerequisites"></a>前提条件

* SQL Server インスタンスが Azure Arc に接続されていること。手順については、「[SQL Server を Azure Arc に接続する](connect.md)」の記事をご覧ください。

* マシンに Microsoft Monitoring Agent (MMA) 拡張機能がインストールされ、構成されていること。 手順については、[MMA のインストール](configure-advanced-data-security.md#install-microsoft-monitoring-agent-mma)に関する記事をご覧ください。 [Log Analytics エージェント](/azure/azure-monitor/platform/log-analytics-agent)に関する記事からも詳細情報を入手することができます。

* SQL Server インスタンスで [TCP/IP プロトコルが有効になっていること](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)。

* SQL Server の名前付きインスタンスを操作する場合は、[SQL Server ブラウザー サービス](../../tools/configuration-manager/sql-server-browser-service.md)が実行されていること。

* 「[サービス ハブのオンデマンド評価の前提条件](/services-hub/health/assessment-prereq-docs#on-demand-assessment-prerequisite-documents)」の SQL Server ドキュメントを確認済みであること。

## <a name="run-on-demand-sql-assessment"></a>オンデマンド SQL Assessment を実行する

1. SQL Server - Azure Arc リソースを開き、左側のペインで **[Environment Health]\(環境の正常性\)** を選択します。

   > [!div class="mx-imgBorder"]
   > [ ![SQL Server - Azure Arc リソースの [Environment Health]\(環境の正常性\) 画面が示されているスクリーンショット](media/assess/sql-assessment-heading-sql-server-arc.png) ](media/assess/sql-assessment-heading-sql-server-arc.png#lightbox)

> [!IMPORTANT]
> MMA の拡張機能がインストールされていない場合、オンデマンドでの SQL Assessment は開始できません。

2. [アカウントの種類] を選択します。 管理されたサービス アカウントがある場合は、ポータルから直接 SQL Assessment を開始できます。 アカウント名を指定します。

> [!NOTE]
> " *管理されたサービス アカウント* " を指定すると **[Configure SQL Assessment]** \(SQL Assessment の構成\) ボタンがアクティブになり、 *CustomScriptExtension* を展開してポータルから評価を開始できるようになります。 *CustomScriptExtension* は一度に 1 つしか展開できないため、SQL Assessment のスクリプト拡張機能は実行後に自動的に削除されます。 既に別の *CustomScriptExtension* がホスト コンピューターに展開されている場合、 **[Configure SQL Assessment]** \(SQL Assessment の構成\) ボタンはアクティブになりません。

3. 既定を変更したい場合は、データ コレクション コンピューターで作業ディレクトリを指定します。 既定では `C:\sql_assessment\work_dir` が使用されます。 収集および分析時、データは一時的にそのフォルダーに格納されます。 フォルダーが存在しない場合は、自動的に作成されます。

4. **[Configure SQL Assessment]** \(SQL Assessment の構成\) をクリックしてポータルから SQL Assessment を開始する場合、標準の展開のポップアップが表示されます。

> [!div class="mx-imgBorder"]
   > [ ![CustomScriptExtension の展開を示すスクリーンショット。](media/assess/sql-assessment-custom-script-deployment.png) ](media/assess/sql-assessment-custom-script-deployment.png#lightbox)

5. ターゲット コンピューターから SQL Assessment を開始する場合は、 **[構成スクリプトのダウンロード]** をクリックし、ダウンロードしたスクリプトをターゲット コンピューターにコピーして、 **powershell.exe** の管理者インスタンスで次の 1 つのコード ブロックを実行します。

   * " _ドメイン アカウント_ ": ユーザー アカウントとパスワードの入力を求められます。

      ```powershell
      Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass -Force
      & '.\AddSqlAssessment.ps1'
      ```

   * " _管理されたサービスアカウント (MSA)_ "

      ```powershell
      Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass -Force
      & '.\AddSqlAssessment.ps1' -ManagedServiceAccountName <MSA account name>
      ```

> [!NOTE]
> このスクリプトは、データ収集をトリガーする *SQLAssessment* という名前のタスクをスケジュールします。 このタスクは、スクリプトを実行してから 1 時間以内に実行されます。 その後、7 日ごとに繰り返されます。

> [!TIP]
> タスクは、別の日時に実行されるように変更したり、すぐに実行するように強制したりすることもできます。 タスク スケジューラ ライブラリで、 **Microsoft** > **Operations Management Suite** > **AOI\*\*\***  > **Assessments** > **SQLAssessment** を見つけます。

## <a name="view-sql-assessment-results"></a>SQL Assessment の結果を表示する

* _[Environment Health]\(環境の正常性\)_ ペインで、 **[View SQL Assessment results]\(SQL Assessment の結果を表示\)** ボタンを選択します。

   > [!NOTE]
   > **[View SQL Assessment results]\(SQL Assessment の結果を表示\)** ボタンは、結果が Log Analytics で準備できるまで、無効のままになります。 この処理には、ターゲット マシンでデータ ファイルが処理されてから最大 2 時間かかることがあります。

   > [!div class="mx-imgBorder"]
   > [ ![SQL Assessment の結果が示されているスクリーンショット。](media/assess/sql-assessment-results.png) ](media/assess/sql-assessment-results.png#lightbox)

* 作業フォルダー内のファイルを確認することで、収集マシンでのデータ処理の状態を確認できます。 スケジュールされたタスクが完了すると、 _new._ プレフィックスが付いたいくつかのファイルが作業ディレクトリに表示されます。

   > [!div class="mx-imgBorder"]
   > [ ![作業フォルダーに新しいデータ ファイルが表示されている [ファイル マネージャー] ウィンドウが示されているスクリーンショット。](media/assess/sql-assessment-data-files-ready.png) ](media/assess/sql-assessment-data-files-ready.png#lightbox)

* Microsoft Monitoring Agent によって、15 分ごとに作業フォルダーがスキャンされます。 _new.*_ ファイルが検索され、Log Analytics ワークスペースにデータが送信されます。 MMA によってファイルがアップロードされると、プレフィックスが _new._ から _processed._ に変更されます。

   > [!div class="mx-imgBorder"]
   > ![処理されたデータ ファイルを表示している [ファイル マネージャー] ウィンドウが示されているスクリーンショット。](media/assess/sql-assessment-data-files-processed.png)

## <a name="next-steps"></a>次の手順

* [サービス ハブのオンデマンド評価](/services-hub/health/assessment-prereq-docs#on-demand-assessment-prerequisite-documents)の前提条件のドキュメントを表示して、さらに詳しい情報を入手します。

* オンデマンド SQL Assessment 機能の包括的なサポートを受けるには、Premier または統合のサポート サブスクリプションが必要です。 詳細については、[Azure Premier サポート](https://azure.microsoft.com/support/plans/premier)に関するページをご覧ください。
