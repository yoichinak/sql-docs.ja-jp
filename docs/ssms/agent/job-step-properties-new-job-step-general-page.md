---
description: ジョブ ステップのプロパティ - [新しいジョブ ステップ] \([全般] ページ)
title: 新しいジョブ ステップのプロパティ ([全般] ページ)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.stepgeneral.f1
ms.assetid: 8d1885ba-4386-4528-8f2b-68c16852720c
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c7575152ff23cec3096c9f5e1e22f1f0ea1a8094
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036560"
---
# <a name="job-step-properties---new-job-step-general-page"></a>ジョブ ステップのプロパティ - [新しいジョブ ステップ] \([全般] ページ)

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 現在、[Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance) によって、すべてではありませんが、ほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、[Azure SQL Managed Instance と SQL Server の T-SQL の相違点](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)に関するページを参照してください。

このページでは、[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブ ステップのプロパティを表示または変更します。新しいジョブ ステップを定義することもできます。  
  
このページに移動するには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のオブジェクト エクスプローラーで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを展開します。次に **[ジョブ]** を右クリックし、 **[新しいジョブ]** をクリックして **[ステップ]** ページを選択し、 **[新規作成]** をクリックします。 または、オブジェクト エクスプローラーでジョブを右クリックし、 **[プロパティ]** をクリックして **[ステップ]** ページを選択し、 **[新規作成]**、 **[挿入]**、または **[編集]** をクリックします。  
  
## <a name="options"></a>オプション  
**[ステップ名]**  
ジョブ ステップの名前を設定します。  
  
**Type**  
ジョブ ステップが使用するサブシステムを設定します。 選択したサブシステムに基づいて、ジョブ ステップを定義するために表示されるオプションが変更されます。  
  
**[実行するアカウント名]**  
ジョブ ステップのプロキシ アカウントを設定します。 sysadmin 固定サーバー ロールのメンバーは、 **[SQL Server エージェント サービスのアカウント]** を指定することもできます。  
  
**[データベース]**  
ジョブ ステップを実行するデータベースを設定します。 このオプションは、すべてのジョブ ステップの種類で使用できるとは限りません。  
  
**コマンド**  
ジョブ ステップが実行するコマンドを設定します。  
  
## <a name="options-for-transact-sql-job-steps"></a>Transact-SQL ジョブ ステップのオプション  
**[ファイル]**  
コマンドをファイルから読み込みます。  
  
**[すべて選択]**  
コマンドのテキストを選択します。  
  
**コピー**  
選択されたテキストをクリップボードにコピーします。  
  
**貼り付け**  
クリップボードの内容を貼り付けます。  
  
**Parse**  
コマンドの構文をチェックします。  
  
## <a name="options-for-activex-script-job-steps"></a>ActiveX スクリプト ジョブ ステップのオプション  
  
> [!IMPORTANT]
> ActiveX スクリプティング サブシステムは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の将来のバージョンで [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェントから削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。  
  
**[VBScript]**  
[!INCLUDE[msCoName](../../includes/msconame_md.md)] Visual Basic Scripting Edition をジョブ ステップの言語として指定します。  
  
**JScript**  
JScript をジョブ ステップの言語として指定します。  
  
**その他**  
別のスクリプト言語で記述されたジョブ ステップの言語の名前を入力します。  
  
**[ファイル]**  
コマンドをファイルから読み込みます。  
  
**[すべて選択]**  
コマンドのテキストを選択します。  
  
**コピー**  
選択したテキストをコピーします。  
  
**貼り付け**  
クリップボードの内容を貼り付けます。  
  
## <a name="options-for-operating-system-cmdexec-job-steps"></a>オペレーティング システム (CmdExec) ジョブ ステップのオプション  
**[コマンド成功時のプロセス終了コード]**  
成功を示すためにコマンドが返す終了コードを入力します。  
  
**[ファイル]**  
コマンドをファイルから読み込みます。  
  
**[すべて選択]**  
コマンドのテキストを選択します。  
  
**コピー**  
選択したテキストをコピーします。  
  
**貼り付け**  
クリップボードの内容を貼り付けます。  
  
## <a name="options-for-powershell-job-steps"></a>PowerShell ジョブ ステップのオプション  
**[ファイル]**  
ファイルからスクリプトを読み込みます。  
  
**[すべて選択]**  
スクリプトのテキストを選択します。  
  
**コピー**  
選択したテキストをコピーします。  
  
**貼り付け**  
クリップボードの内容を貼り付けます。  
  
## <a name="options-for-replication-distributor-job-steps"></a>レプリケーション ディストリビューター ジョブ ステップのオプション  
**[すべて選択]**  
コマンドのテキストを選択します。  
  
**コピー**  
選択したテキストをコピーします。  
  
**貼り付け**  
クリップボードの内容を貼り付けます。  
  
## <a name="options-for-replication-merge-job-steps"></a>レプリケーション マージ ジョブ ステップのオプション  
**[すべて選択]**  
コマンドのテキストを選択します。  
  
**コピー**  
選択したテキストをコピーします。  
  
**貼り付け**  
クリップボードの内容を貼り付けます。  
  
## <a name="options-for-replication-queue-reader-job-steps"></a>レプリケーション キュー リーダーのジョブ ステップのオプション  
**[データベース]**  
ジョブ ステップに使用するデータベースです。  
  
**[すべて選択]**  
コマンドのテキストを選択します。  
  
**コピー**  
選択したテキストをコピーします。  
  
**貼り付け**  
クリップボードの内容を貼り付けます。  
  
## <a name="options-for-replication-snapshot-job-steps"></a>レプリケーション スナップショット ジョブ ステップのオプション  
**[すべて選択]**  
コマンドのテキストを選択します。  
  
**コピー**  
選択したテキストをコピーします。  
  
**貼り付け**  
クリップボードの内容を貼り付けます。  
  
## <a name="options-for-replication-transaction-log-reader-job-steps"></a>レプリケーション トランザクション ログ リーダー ジョブ ステップのオプション  
**[すべて選択]**  
コマンドのテキストを選択します。  
  
**コピー**  
選択したテキストをコピーします。  
  
**貼り付け**  
クリップボードの内容を貼り付けます。  
  
## <a name="options-for-sql-server-analysis-services-command-job-steps"></a>SQL Server Analysis Services コマンド ジョブ ステップのオプション  
**サーバー**  
ジョブ ステップを実行するサーバーを選択します。  
  
**[ファイル]**  
コマンドをファイルから読み込みます。  
  
**[すべて選択]**  
コマンドのテキストを選択します。  
  
**コピー**  
選択したテキストをコピーします。  
  
**貼り付け**  
クリップボードの内容を貼り付けます。  
  
## <a name="options-for-sql-server-analysis-services-query-job-steps"></a>SQL Server Analysis Services クエリ ジョブ ステップのオプション  
**サーバー**  
ジョブ ステップを実行するサーバーを選択します。  
  
**[データベース]**  
ジョブ ステップに使用するデータベースです。  
  
**[ファイル]**  
コマンドをファイルから読み込みます。  
  
**[すべて選択]**  
コマンドのテキストを選択します。  
  
**コピー**  
選択したテキストをコピーします。  
  
**貼り付け**  
クリップボードの内容を貼り付けます。  
  
## <a name="options-for-integration-services-package-execution-job-steps"></a>Integration Services パッケージ実行ジョブ ステップのオプション  
  
### <a name="general-tab"></a>全般タブ  
[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ([!INCLUDE[ssIS](../../includes/ssis_md.md)]) パッケージの場所と、使用する認証方法を指定します。 このタブを選択するとき、次のオプションを利用できます。  
  
**[パッケージ ソース]**  
[!INCLUDE[ssIS](../../includes/ssis_md.md)] パッケージが格納されている場所を指定します。 次のいずれかを選択します。  
  
-   **SQL Server**  
  
-   **ファイル システム**  
  
-   **[SSIS パッケージ ストア]**  
  
**[サーバー]**  
[!INCLUDE[ssIS](../../includes/ssis_md.md)] パッケージが格納されているサーバーの名前を入力します。 このオプションは、 **[パッケージ ソース]** に **[SQL Server]** または **[SSIS パッケージ ストア]** が指定されている場合のみ使用できます。  
  
**[Windows 認証を使用する]**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] へのログインに [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows 認証を使用します。  
  
**[SQL Server 認証を使用する]**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] へのログインに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用します。 この認証方法を選択した場合は、適切な **[ユーザー名]** および **[パスワード]** を入力してください。  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証は旧バージョンとの互換性を維持するために提供されます。 セキュリティを向上させるためには、可能な限り、Windows 認証を使用してください。  
  
**パッケージ**  
パッケージの場所を入力します。  
  
> [!IMPORTANT]  
> パスワードで保護された [!INCLUDE[ssIS](../../includes/ssis_md.md)] パッケージについては、 **[構成]** タブをクリックし、 **[パッケージ パスワード]** ダイアログ ボックスにパスワードを入力します。 入力しないと、パスワードで保護されたパッケージを実行する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブは失敗します。  
  
### <a name="configurations-tab"></a>[構成] タブ  
[!INCLUDE[ssIS](../../includes/ssis_md.md)] パッケージの構成オプションを指定します。 このタブを選択すると、次のオプションを使用できます。  
  
**構成ファイル**  
パッケージの構成ファイルを一覧表示します。  
  
**追加**  
パッケージの構成ファイルを追加します。  
  
**Remove**  
パッケージの構成ファイルを削除します。  
  
**[上へ移動]**  
選択された構成ファイルを上へ移動します。  
  
**[下へ移動]**  
選択された構成ファイルを下へ移動します。  
  
### <a name="command-files-tab"></a>[コマンド ファイル] タブ  
パッケージのコマンド ファイルを選択します。 コマンド ファイルは、一覧に表示されている順番で処理されます。 このタブを選択するとき、次のオプションを利用できます。  
  
**[コマンド ファイル]**  
パッケージのコマンド ファイルを一覧表示します。  
  
**追加**  
コマンド ファイルを追加します。  
  
**Remove**  
選択されたコマンド ファイルを削除します。  
  
**[上へ移動]**  
選択されたコマンド ファイルを上へ移動します。  
  
**[下へ移動]**  
選択されたコマンド ファイルを下へ移動します。  
  
### <a name="data-sources-tab"></a>[データ ソース] タブ  
パッケージの指定されたデータ ソースを表示します。  
  
**接続マネージャー**  
データ ソースの名前を表示します。  
  
**説明**  
データ ソースの記述を表示します。  
  
**接続文字列**  
データ ソースの接続文字列を表示します。  
  
### <a name="execution-options-tab"></a>[実行オプション] タブ  
パッケージの実行オプションを表示または変更します。  
  
**[検証時に警告が発生したらパッケージを失敗とする]**  
このオプションをオンにした場合、検証時に警告が発生するとパッケージの実行は失敗となります。  
  
**[パッケージを実行せずに検証する]**  
このオプションをジョブ ステップに設定すると、パッケージは検証されますが実行されません。  
  
**[同時実行するファイルの最大数]**  
一度に実行できる実行ファイルの最大数です。  
  
**[パッケージのチェックポイントを有効にする]**  
このオプションをジョブ ステップに設定すると、パッケージのチェックポイントが使用されます。  
  
**[チェックポイント ファイル]**  
パッケージ チェックポイント ファイルの名前を入力します。  
  
**...**  
パッケージ チェックポイント ファイルを参照して指定します。  
  
**[再開オプションをオーバーライドする]**  
このオプションをオンにすると、このジョブ ステップに対して、パッケージに指定された再開オプションと異なる再開オプションを指定できます。  
  
**[再開オプション]**  
パッケージを再開するときに実行するアクションを選択します。  
  
### <a name="logging-tab"></a>[ログ記録] タブ  
パッケージのログ プロバイダーを表示または変更します。  
  
**[ログ プロバイダー]**  
ログ プロバイダーの ClassID を選択します。  
  
**[構成文字列]**  
ログ プロバイダーの構成文字列を入力します。  
  
**Remove**  
ログ プロバイダーを削除します。  
  
### <a name="set-values-tab"></a>[値の設定] タブ  
パッケージのプロパティ値を表示または変更します。  
  
**[プロパティのパス]**  
プロパティのパスを表示または変更します。  
  
**Value**  
プロパティの値を表示または変更します。  
  
**Remove**  
プロパティを削除します。  
  
### <a name="verification-tab"></a>[検証] タブ  
ジョブ ステップの検証オプションを選択します。  
  
**[署名付きパッケージのみ実行する]**  
署名されたパッケージのみ実行します。 このオプションがオンになっていると、パッケージが署名されていない場合はジョブ ステップが失敗します。  
  
**[パッケージのビルドを検証する]**  
特定のビルド番号のパッケージのみを実行します。 このオプションがオンになっていると、パッケージのビルド番号が指定された番号と異なる場合は、ジョブ ステップが失敗します。  
  
**ビルド**  
パッケージのビルド番号を入力します。  
  
**[パッケージ ID を確認する]**  
特定の ID を持つパッケージのみ実行します。 このオプションがオンになっていると、パッケージの ID が指定の ID と異なる場合は、ジョブ ステップが失敗します。  
  
**[パッケージ ID]**  
パッケージ ID を入力します。  
  
**[バージョン ID を確認する]**  
特定のバージョン ID を持つパッケージのみ実行します。 このオプションがオンになっていると、パッケージのバージョン ID が指定の ID と異なる場合は、ジョブ ステップが失敗します。  
  
**バージョン ID**  
バージョン ID を入力します。  
  
### <a name="command-line-tab"></a>[コマンド ライン] タブ  
パッケージのコマンド ライン オプションを指定します。 このタブを選択すると、次のオプションを使用できます。  
  
**[元のオプションを復元する]**  
このダイアログで設定したコマンド ライン オプションを指定します。  
  
**[コマンド ラインを手動で編集する]**  
コマンド ライン ウィンドウでオプションを指定します。  
  
**コマンド ライン**  
このパッケージに使用するコマンド ライン オプションを入力します。  
  
## <a name="see-also"></a>参照  
[ジョブ ステップの管理](../../ssms/agent/manage-job-steps.md)  
[パッケージに対する SQL Server エージェント ジョブ](../../integration-services/packages/sql-server-agent-jobs-for-packages.md)  
[レプリケーション エージェントの管理](../../relational-databases/replication/agents/replication-agent-administration.md)  
