---
title: SQL Server エージェントでの Windows PowerShell ステップの実行
description: SQL Server エージェント ジョブで Windows PowerShell の手順を行う方法について説明します。
ms.prod: sql
ms.technology: sql-server-powershell
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: matteot, drskwier
ms.custom: seo-lt-2019
ms.date: 03/16/2017
ms.openlocfilehash: 8029d18dee3dd49342c3c029fc78992900394ed4
ms.sourcegitcommit: 9413ddd8071da8861715c721b923e52669a921d8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "101839407"
---
# <a name="run-windows-powershell-steps-in-sql-server-agent"></a>SQL Server エージェントでの Windows PowerShell ステップの実行

[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]

SQL Server エージェントを使用して、スケジュールされた時刻に SQL Server PowerShell スクリプトを実行します。

[!INCLUDE[sql-server-powershell-version](../includes/sql-server-powershell-version.md)]

[!INCLUDE[sql-server-powershell-no-sqlps](../includes/sql-server-powershell-no-sqlps.md)]

## <a name="to-run-powershell-from-sql-server-agent"></a>SQL Server エージェントから PowerShell を実行するには

SQL Server エージェントのジョブ ステップにはいくつかの種類があります。 それぞれの種類は、レプリケーション エージェントやコマンド プロンプト環境など、特定の環境を実装するサブシステムに関連付けられています。 Windows PowerShell スクリプトのコードを作成した後、SQL Server エージェントを使用して、スケジュールされた時刻に実行されるジョブや SQL Server イベントに応答して実行されるジョブにそのスクリプトを含めることができます。 コマンド プロンプト ジョブ ステップまたは PowerShell ジョブ ステップを使用して、Windows PowerShell スクリプトを実行できます。

- PowerShell ジョブ ステップを使用して SQL Server エージェント サブシステムに **sqlps** ユーティリティを実行させます。このユーティリティは、PowerShell 2.0 を起動し、**sqlps** モジュールをインポートします。 SQL Server 2019 以降を実行している場合は、SQL Agent のジョブステップで **[SqlServer](sql-server-powershell.md#sql-server-agent)** モジュールを使用することをお勧めします。

- コマンド プロンプト ジョブ ステップを使用して PowerShell.exe を実行し、 **sqlps** モジュールをインポートするスクリプトを指定します。

### <a name="caution-about-memory-consumption"></a><a name="LimitationsRestrictions"></a> メモリ使用量に関する注意

**sqlps** モジュールで PowerShell を実行する SQL Server エージェント ジョブのステップごとに、約 **20 MB** のメモリを消費するプロセスが起動されます。 大量の Windows PowerShell ジョブ ステップを同時実行すると、パフォーマンスに悪影響が及びます。

## <a name="create-a-powershell-job-step"></a><a name="PShellJob"></a> PowerShell ジョブ ステップの作成

### <a name="to-create-a-powershell-job-step"></a>PowerShell ジョブ ステップを作成するには

1. **[SQL Server エージェント]** を展開し、新しいジョブを作成するか、既存のジョブを右クリックして **[プロパティ]** を選択します。 ジョブの作成に関する詳細については、「 [ジョブの作成](../ssms/agent/create-jobs.md)」を参照してください。

2. **[ジョブのプロパティ]** ダイアログで **[ステップ]** ページを選択し、 **[新規作成]** を選択します。

3. **[新しいジョブ ステップ]** ダイアログの **[ステップ名]** ボックスにジョブ ステップ名を入力します。

4. **[種類]** ボックスの一覧で、 **[PowerShell]** を選択します。

5. **[実行するアカウント名]** ボックスの一覧で、ジョブで使用する資格情報を備えたプロキシ アカウントをクリックします。

6. **[コマンド]** ボックスに、ジョブ ステップで実行する PowerShell スクリプト構文を入力します。 または、 **[開く]** を選択してスクリプト構文が記述されたファイルを選択します。

7. **[詳細設定]** ページを選択して、ジョブ ステップのオプションのうち、ジョブ ステップが成功または失敗した場合のアクション、SQL Server エージェントによるジョブ ステップの再試行回数、および再試行間隔を設定します。

## <a name="create-a-command-prompt-job-step"></a><a name="CmdExecJob"></a> コマンド プロンプト ジョブ ステップの作成

### <a name="to-create-a-cmdexec-job-step"></a>CmdExec ジョブ ステップを作成するには

1. **[SQL Server エージェント]** を展開し、新しいジョブを作成するか、既存のジョブを右クリックして **[プロパティ]** を選択します。 ジョブの作成に関する詳細については、「 [ジョブの作成](../ssms/agent/create-jobs.md)」を参照してください。

2. **[ジョブのプロパティ]** ダイアログで **[ステップ]** ページを選択し、 **[新規作成]** を選択します。

3. **[新しいジョブ ステップ]** ダイアログの **[ステップ名]** ボックスにジョブ ステップ名を入力します。

4. **[種類]** ボックスの一覧の **[オペレーティング システム (CmdExec)]** をクリックします。

5. **[実行するアカウント名]** ボックスの一覧で、ジョブで使用する資格情報を備えたプロキシ アカウントをクリックします。 既定では、CmdExec ジョブ ステップは SQL Server エージェント サービス アカウントのコンテキストで実行されます。

6. **[コマンド成功時のプロセス終了コード]** ボックスに、0 ～ 999999 の値を入力します。

7. **[コマンド]** ボックスに、実行する PowerShell スクリプトを指定するパラメーターと共に powershell.exe を入力します。

8. **[詳細設定]** ページを選択して、ジョブが成功または失敗した場合の操作、SQL Server エージェントによるジョブ ステップ実行の試行回数、SQL Server エージェントでジョブ ステップの出力を書き込むファイルなど、ジョブ ステップのオプションを設定します。 **sysadmin** 固定サーバー ロールのメンバーだけが、オペレーティング システム ファイルにジョブ ステップの出力を書き込むことができます。

## <a name="see-also"></a>参照

- [SQL Server PowerShell](sql-server-powershell.md)
- [PowerShell を使用した SQL Server エージェント](sql-server-powershell.md#sql-server-agent)