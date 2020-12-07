---
description: SQL Server インポートおよびエクスポート ウィザードを起動する
title: SQL Server インポートおよびエクスポート ウィザードを起動する
titleSuffix: Integration Services (SSIS)
ms.prod: sql
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Import and Export Wizard
- starting SQL Server Import and Export Wizard
- Import and Export Wizard
- starting Import and Export Wizard
ms.assetid: 5fc4f6d1-1f6f-444e-9aeb-827f85e1c405
author: chugugrace
ms.author: chugu
ms.reviewer: ''
ms.custom: ''
ms.date: 11/18/2019
ms.openlocfilehash: 1bf52643a67557e808ccf10a29d82d0e4ed6e9ff
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92195896"
---
# <a name="start-the-sql-server-import-and-export-wizard"></a>SQL Server インポートおよびエクスポート ウィザードを起動する

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

このトピックで説明されているいずれかの方法で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードを起動して、サポートされているデータ ソースからデータをインポートし、サポートされているデータ ソースにデータをエクスポートします。

> [!IMPORTANT]
> このトピックでは、ウィザードの **起動** 方法のみを説明します。 他のものをお探しの場合は、「[関連タスクとコンテンツ](#related-tasks-and-content)」を参照してください。

ウィザードは次の方法で起動できます。

- サポートされているデータ ソースとの間でインポートまたはエクスポートを実行するには、 [スタート メニュー](#start-menu)」を参照してください。
- サポートされているデータ ソースとの間でインポートまたはエクスポートを実行するには、 [コマンド プロンプト](#command-prompt)」を参照してください。
- SQL Server との間でインポートまたはエクスポートするには、 [SQL Server Management Studio (SSMS)](#sql-server-management-studio-ssms)」を参照してください。
- SQL Server との間でインポートまたはエクスポートするには、 [SQL Server Data Tools (SSDT) がインストールされている Visual Studio](#visual-studio)」を参照してください。

## <a name="prerequisite---is-the-wizard-installed-on-your-computer"></a>前提条件 - コンピューターへのウィザードのインストール

ウィザードを実行する必要はあるが、コンピューターに [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールしていない場合は、SQL Server Data Tools (SSDT) をインストールすることで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードをインストールできます。 詳細については、「 [SQL Server Data Tools (SSDT) のダウンロード](../../ssdt/download-sql-server-data-tools-ssdt.md)」を参照してください。

> [!NOTE]
> 64 ビット バージョンの SQL Server インポートおよびエクスポート ウィザードを使用するには、SQL Server をインストールする必要があります。 SQL Server Data Tools (SSDT) および SQL Server Management Studio (SSMS) は 32 ビット アプリケーションであり、32 ビット バージョンのウィザードを含む、32 ビット ファイルのみがインストールされます。

## <a name="start-menu"></a>[スタート] メニュー

### <a name="start-the-sql-server-import-and-export-wizard-from-the-start-menu"></a>[スタート] メニューから SQL Server インポートおよびエクスポート ウィザードを起動する

1. **[スタート]** メニューで、**Microsoft SQL Server 20xx** を見つけて展開します。
2. 以下のいずれかのオプションをクリックします。
    - **SQL Server 20xx データのインポートおよびエクスポート (64 ビット)**
    - **SQL Server 20xx データのインポートおよびエクスポート (32 ビット)**

    データ ソースに 32 ビットのデータ プロバイダーが必要であることがわかっていない限り、64 ビット バージョンのウィザードを実行してください。

    ![ウィザードの起動 (スタート)](../../integration-services/import-export-data/media/start-wizard-start-64.png)

## <a name="command-prompt"></a>コマンド プロンプト

### <a name="start-the-sql-server-import-and-export-wizard-from-the-command-prompt"></a>コマンド プロンプトから SQL Server インポートおよびエクスポート ウィザードを起動する

コマンド プロンプト ウィンドウで、次のいずれかの場所から **DTSWizard.exe** を実行します。

- 64 ビット バージョンの場合、**C:\Program Files\Microsoft SQL Server\140\DTS\Binn**。
  - *140* = SQL Server 2017。  この値は、使用している SQL Server のバージョンによって異なります。

- 32 ビット バージョンの場合、**C:\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn**。
  - *140* = SQL Server 2017。  この値は、使用している SQL Server のバージョンによって異なります。

データ ソースに 32 ビットのデータ プロバイダーが必要であることがわかっていない限り、64 ビット バージョンのウィザードを実行してください。

![ウィザードの起動 (cmd)](../../integration-services/import-export-data/media/start-wizard-cmd.png)
  
## <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)

### <a name="start-the-sql-server-import-and-export-wizard-from-sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS) から SQL Server インポートおよびエクスポート ウィザードを起動する

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。

2. **[データベース]** を展開します。

3. データベースを右クリックします。

4. **[タスク]** にカーソルを合わせます。

5. 以下のいずれかのオプションをクリックします。

   - **データのインポート**

   - **データのエクスポート**  

   ![ウィザードの起動 (SSMS)](../../integration-services/import-export-data/media/start-wizard-ssms.jpg) 

SQL Server をインストールしていない場合、あるいは SQL Server をインストールしているが、SQL Server Management Studio をインストールしていない場合、「 [SQL Server Management Studio (SSMS) のダウンロード](../../ssms/download-sql-server-management-studio-ssms.md)」を参照してください。

## <a name="visual-studio"></a>Visual Studio

### <a name="start-the-sql-server-import-and-export-wizard-from-visual-studio-with-sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT) で Visual Studio から SQL Server インポートおよびエクスポート ウィザードを起動する

 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]がインストールされている Visual Studio で、Integration Services プロジェクトを開いている状態で、次のいずれかを実行します。

- **[プロジェクト]** メニューの **[SSIS インポートおよびエクスポート ウィザード]** をクリックします。

   ![ウィザードの起動 (プロジェクト)](../../integration-services/import-export-data/media/start-wizard-project.png)

   \- - または -

- ソリューション エクスプローラーで、 **[SSIS パッケージ]** フォルダーを右クリックし、 **[SSIS インポートおよびエクスポート ウィザード]** をクリックします。

    ![ウィザードの起動 (パッケージ)](../../integration-services/import-export-data/media/start-wizard-packages.png)

Visual Studio がインストールされていない場合、あるいは Visual Studio がインストールされているが、SQL Server Data Tools がインストールされていない場合、「 [SQL Server Data Tools (SSDT) のダウンロード](../../ssdt/download-sql-server-data-tools-ssdt.md)」を参照してください。

## <a name="get-the-wizard"></a>ウィザードを入手する

ウィザードを実行する必要はあるが、コンピューターに [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールしていない場合は、SQL Server Data Tools (SSDT) をインストールすることで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードをインストールできます。 詳細については、「 [SQL Server Data Tools (SSDT) のダウンロード](../../ssdt/download-sql-server-data-tools-ssdt.md)」を参照してください。

## <a name="get-help-while-the-wizard-is-running"></a>ウィザードの実行中にヘルプを得る

> [!TIP]
> ウィザードのページまたはダイアログ ボックスで F1 キーをタップすると、現在のページの文書が表示されます。   

## <a name="whats-next"></a>次の手順

ウィザードを起動すると、最初のページは **[SQL Server インポートおよびエクスポート ウィザードへようこそ]** になります。 このページでいかなる操作も必要はありません。 詳細については、「 [SQL Server インポートおよびエクスポート ウィザードへようこそ](../../integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)」を参照してください。  
  
## <a name="related-tasks-and-content"></a>関連タスクとコンテンツ

その他の基本的なタスクは次のとおりです。

- **ウィザードのしくみの簡単な例を参照してください。**

  - **スクリーン ショットを参照する場合。** この単純な例を 1 つのページに示した「[簡単な例によるインポートおよびエクスポート ウィザードの概要](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)」をご覧ください。

  - **ビデオを視聴する場合。** ウィザードを実行し、わかりやすく簡単な手順でデータを Excel にエクスポートする方法を説明した YouTube の 4 分間のビデオ「[SQL Server インポートおよびエクスポート ウィザードを使用して Excel にエクスポートする](https://go.microsoft.com/fwlink/?linkid=829049)」 をご覧ください。

  - **ウィザードのしくみについては、以下を参照してください。**

  - **ウィザードの詳細については、以下を参照してください。** ウィザードの概要をお探しの場合は、「 [SQL Server でサポートされるインポートとエクスポートのデータ ソース](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)」を参照してください。

  - **ウィザードの手順について学習する。** ウィザードの手順についての情報を探している場合は、「[SQL Server インポートおよびエクスポート ウィザードの手順](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md)」をご覧ください。 ウィザードのページごとに別のドキュメント ページもあります。

  - **データ ソースおよび変換先に接続する方法を学習する。** データへの接続方法についての情報を探している場合は、「[SQL Server インポートおよびエクスポート ウィザードを使用してデータ ソースに接続する](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md)」の一覧から目的のページを選んでください。 いくつかの一般的に使用されるデータ ソースごとに個別のドキュメントのページがあります。