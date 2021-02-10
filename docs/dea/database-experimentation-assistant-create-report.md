---
title: 分析レポートの作成
description: Database Experimentation Assistant (DEA) で分析レポートを生成します。 分析レポートは、提案された変更のパフォーマンスへの影響に関する洞察を提供します。
ms.date: 01/24/2020
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: pochiraju
ms.author: rajpo
ms.reviewer: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 931e013a84cd808d75a50edafdcf73d105f51827
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100045112"
---
# <a name="create-analysis-reports-in-database-experimentation-assistant-sql-server"></a>Database Experimentation Assistant で分析レポートを作成する (SQL Server)

両方の対象サーバーでソーストレースを再生した後、Database Experimentation Assistant (DEA) で分析レポートを生成できます。 分析レポートは、提案された変更のパフォーマンスへの影響についての洞察を得るのに役立ちます。

## <a name="create-an-analysis-report"></a>分析レポートを作成する

1. DEA で、リストアイコンを選択し、サーバー名と認証の種類を指定して、シナリオに応じて [ **接続の暗号化** ] と [ **サーバー証明書の信頼** ] チェックボックスをオンまたはオフにし、[ **接続**] を選択します。

   ![トレースファイルを使用したサーバーへの接続](./media/database-experimentation-assistant-create-report/dea-connect-to-server-with-trace-files.png)

2. [ **分析レポート** ] 画面で、[ **新しい分析レポート**] を選択します。

   ![新しい分析レポートの作成](./media/database-experimentation-assistant-create-report/dea-create-an-analysis-report.png)

3. [ **新しい分析レポート** ] 画面で、レポートの名前、ストレージの場所、ターゲット1とターゲット2のトレースファイルのパスを指定し、[ **開始**] を選択します。

   ![新しい分析レポートの詳細を指定します](./media/database-experimentation-assistant-create-report/dea-new-analysis-report-details.png)

   入力した情報が有効な場合は、分析レポートが作成されます。

   ![新しく作成された分析レポート](./media/database-experimentation-assistant-create-report/dea-newly-created-analysis-report.png)

      > [!NOTE]
      > 入力した情報のいずれかが無効な場合は、正しくない情報を含むテキストボックスが赤色で強調表示されます。 必要に応じて修正を行い、もう一度 [ **開始** ] を選択します。

## <a name="frequently-asked-questions-about-analysis-reports"></a>分析レポートに関してよく寄せられる質問

**Q: 私の分析レポートにはどのような情報が表示されるのですか。**

DEA は、統計テストを使用してワークロードを分析し、各クエリがターゲット1からターゲット2にどのように実行されたかを判断します。 各クエリのパフォーマンスの詳細が表示されます。 DEA の詳細については、「 [はじめ](database-experimentation-assistant-get-started.md)に」を参照してください。

**Q: 別のレポートを生成しているときに、新しい分析レポートを作成することはできますか。**

いいえ。  現時点では、競合を防ぐために一度に生成できるレポートは1つだけです。 ただし、複数のキャプチャと再生を同時に実行することはできます。

**Q: コマンドプロンプトを使用して分析レポートを生成することはできますか。**

はい。 分析レポートは、コマンドプロンプトで生成できます。 その後、UI でレポートを表示できます。 詳細については、「 [コマンドプロンプトでの実行](database-experimentation-assistant-run-command-prompt.md)」を参照してください。

## <a name="troubleshoot-analysis-reports"></a>分析レポートのトラブルシューティング

**Q: サーバーで分析レポートを生成して表示するには、どのようなセキュリティアクセス許可が必要ですか。**

DEA にログインしているユーザーには、分析サーバーの sysadmin 権限が必要です。 ユーザーがグループに属している場合は、グループに sysadmin 権限があることを確認します。

|考えられるエラー|解決策|  
|---|---|  
|データベースに接続できません。 レポートを分析および表示するための sysadmin 権限を持っていることを確認します。|サーバーまたはデータベースに対するアクセス権または sysadmin 権限を持っていない可能性があります。 ログイン権限を確認してから、操作をやり直してください。|  
|サーバー **サーバー名** に **レポート名** を生成できません。 詳細については、 **レポート名** レポートを確認してください。|新しいレポートを生成するために必要な sysadmin 権限を持っていない可能性があります。 詳細なエラーを表示するには、エラーが発生したレポートを選択し、% temp% dea でログを確認し \\ ます。|  
|現在のユーザーには、操作を実行するために必要なアクセス許可がありません。 トレースを実行し、レポートを分析するための sysadmin 権限を持っていることを確認します。|新しいレポートを生成するために必要な sysadmin 権限がありません。|  

**Q: を実行しているコンピューターに接続できません SQL Server**

- SQL Server を実行しているコンピューターの名前が有効であることを確認します。 確認するには、SQL Server Management Studio (SSMS) を使用してサーバーに接続してみてください。
- ファイアウォール構成で SQL Server を実行しているコンピューターへの接続がブロックされていないことを確認します。
- ユーザーが必要なユーザー権限を持っていることを確認します。

詳細については、% temp% dea のログを参照してください \\ 。 問題が解決しない場合は、製品チームにお問い合わせください。

**Q: 分析レポートを生成するときにエラーが表示する**

DEA をインストールした後に初めて分析レポートを生成するときは、インターネットアクセスが必要です。 統計分析に必要なパッケージをダウンロードするには、インターネットアクセスが必要です。

レポートの作成中にエラーが発生した場合は、[進行状況] ページに分析の生成に失敗した特定の手順が表示されます。 詳細については、% temp% dea のログを参照してください \\ 。 必要なユーザー権限を持つサーバーへの接続が有効であることを確認してから、再試行してください。 問題が解決しない場合は、製品チームにお問い合わせください。

|考えられるエラー|解決策|  
|---|---|  
|RInterop は起動時にエラーになります。 RInterop ログを確認してから、操作をやり直してください。|DEA は、依存する R パッケージをダウンロードするためにインターネットアクセスを必要とします。 % Temp% rinterop の RInterop ログを確認 \\ し、% temp% dea のログを破棄して \\ ください。 RInterop が正しく初期化されなかった場合、または正しい R パッケージを使用せずに初期化された場合は、DEA ログの初期化前の手順の後に "新しい分析レポートを生成できませんでした" という例外が表示されることがあります。<br><br>RInterop ログには、"jsonlite パッケージが使用できません" というエラーが表示されることもあります。 コンピューターがインターネットにアクセスできない場合は、必要な jsonlite R パッケージを手動でダウンロードできます。<br><br><li>\\コンピューターのファイルシステムの% userprofile% dearpackages フォルダーにアクセスします。 このフォルダーは、DEA で R が使用するパッケージで構成されています。</li><br><li>インストールされているパッケージの一覧に jsonlite フォルダーがない場合は、インターネットにアクセスできるコンピューターで、からの jsonlite1.4.zip のリリースバージョンをダウンロードする必要があり \_ [https://cran.r-project.org/web/packages/jsonlite/index.html](https://cran.r-project.org/web/packages/jsonlite/index.html) ます。</li><br><li>DEA を実行しているコンピューターに .zip ファイルをコピーします。  Jsonlite フォルダーを抽出し、% userprofile% \\ dearpackages にコピーします。 この手順により、自動的に jsonlite パッケージが R にインストールされます。フォルダーは **jsonlite** という名前にする必要があります。コンテンツは、以下の1レベルではなくフォルダー内に直接配置する必要があります。</li><br><li>DEA を閉じて再度開いてから、もう一度分析を試してください。</li><br>RGUI を使用することもできます。 [**パッケージ**] [  >  **zip からインストール**] にアクセスします。 前の手順でダウンロードしたパッケージにアクセスし、をインストールします。<br><br>RInterop が初期化され、正しく設定されている場合は、RInterop ログに "依存する R パッケージ jsonlite をインストールしています" と表示されます。|  
|SQL Server インスタンスに接続できません。サーバー名が正しいことを確認し、ログインしているユーザーに必要なアクセス権があるかどうかを確認してください。|サーバーにアクセス権がないか、サーバー名が正しくない可能性があります。|
|RInterop プロセスがタイムアウトしました。DEA および RInterop ログを確認し、タスクマネージャーで RInterop プロセスを停止してから、操作をやり直してください。<br><br>or<br><br>RInterop は faulted 状態にあります。 タスクマネージャーで RInterop プロセスを停止してから、操作をやり直してください。|% Temp% rinterop でログを確認し \\ て、エラーを確認してください。 タスクマネージャーから RInterop プロセスを削除してから、操作をやり直してください。 問題が解決しない場合は、製品チームにお問い合わせください。|

**Q: レポートが生成されましたが、データが不足しています**

SQL Server を実行している分析コンピューターのデータベースを確認して、データが存在することを確認します。 分析データベースが存在することを確認し、そのテーブルを確認します。 たとえば、TblBatchesA、TblBatchesB、および TblSummaryStats の各テーブルを確認します。

データが存在しない場合は、データが正しくコピーされていないか、データベースが破損している可能性があります。 一部のデータのみが不足している場合は、キャプチャまたは再生で作成されたトレースファイルがワークロードを正確にキャプチャしていない可能性があります。 データがある場合は、% temp% dea のログファイル \\ を調べて、エラーがログに記録されたかどうかを確認してください。 その後、もう一度分析レポートの生成を試みます。

他にも質問やフィードバックがありますか? 左下隅にあるスマイルアイコンをクリックして、DEA ツールを通じてフィードバックを送信します。

## <a name="see-also"></a>関連項目

- 分析レポートを表示する方法については、「 [レポートの表示](database-experimentation-assistant-view-report.md)」を参照してください。
