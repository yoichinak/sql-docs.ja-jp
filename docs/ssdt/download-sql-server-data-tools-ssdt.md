---
title: SQL Server Data Tools (SSDT) のダウンロード
description: SQL Server Data Tools (SSDT) について説明します。 Visual Studio 2019 と Visual Studio 2017 を使用してこのデータベース開発ツール セットをインストールする方法を確認します。
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssdt
ms.topic: conceptual
keywords: ssdt のインストール, ssdt のダウンロード, 最新の ssdt
ms.assetid: b0fc4987-d260-4d0a-9dd1-98099835b361
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan
ms.custom: seo-lt-2019
ms.date: 02/20/2020
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 39f1f79701a0a3fd871b2b273a48197b8b42187b
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "92005889"
---
# <a name="download-sql-server-data-tools-ssdt-for-visual-studio"></a>SQL Server Data Tools (SSDT) for Visual Studio のダウンロード

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md.md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

**SQL Server Data Tools (SSDT)** は、SQL Server リレーショナル データベース、Azure SQL のデータベース、Analysis Services (AS) データ モデル、Integration Services (IS) パッケージ、Reporting Services (RS) レポートをビルドするための、最新の開発ツールです。 SSDT では、Visual Studio でアプリケーションを開発する場合と同じくらい簡単に、SQL Server のコンテンツの種類を設計および展開できます。

## <a name="ssdt-for-visual-studio-2019"></a>SSDT for Visual Studio 2019

### <a name="changes-in-ssdt-for-visual-studio-2019"></a>SSDT for Visual Studio 2019 の変更点

データベース プロジェクトを作成するための SSDT のコア機能が Visual Studio にとって不可欠な機能であることに変わりはありません。

Visual Studio 2019 では、Analysis Services、Integration Services、Reporting Services のプロジェクトを有効にするために必要な機能がそれぞれの Visual Studio (VSIX) 拡張機能に移行されただけです。

> [!NOTE]
> Visual Studio 2019 用の SSDT スタンドアロン インストーラはありません。

### <a name="install-ssdt-with-visual-studio-2019"></a>Visual Studio 2019 で SSDT をインストールする

[Visual Studio 2019](/visualstudio/install/install-visual-studio?preserve-view=true&view=vs-2019) が既にインストールされている場合、ワークロードの一覧を編集して SSDT を含めることができます。 Visual Studio 2019 をインストールしていない場合は、[Visual Studio 2019 Community](https://visualstudio.microsoft.com/downloads/) をダウンロードしてインストールできます。

インストール済みの Visual Studio ワークロードを SSDT を含めるように変更するには、Visual Studio インストーラーを使用します。

1. Visual Studio インストーラーを起動します。 Windows の [スタート] メニューで "installer" を検索できます。

   ![Windows の [スタート] メニューの Visual Studio インストーラー (2019)](../ssdt/media/visual-studio-installer.png)

2. インストーラーで SSDT を追加するエディションの Visual Studio を選択し、 **[変更]** を選択します。

3. ワークロードの一覧で **[データの保存と処理]** の下にある **[SQL Server Data Tools]** を選択します。

   ![[データの保存と処理] ワークロード (2019)](../ssdt/media/download-sql-server-data-tools-ssdt/data-workload-2019.png)

Analysis Services、Integration Services、または Reporting Services プロジェクトの場合は、Visual Studio 内から ( **[拡張機能]** 、 **[拡張機能を管理する]** の順に選択する) または [[Marketplace]](https://marketplace.visualstudio.com/search?term=services&target=VS&category=All%20categories&vsVersion=&sortBy=Relevance) から適切な[拡張機能](/visualstudio/ide/finding-and-using-visual-studio-extensions)をインストールできます。

* [Analysis Services](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)
* [統合サービス](https://marketplace.visualstudio.com/items?itemName=SSIS.SqlServerIntegrationServicesProjects)
* [Reporting Services](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio)

## <a name="ssdt-for-visual-studio-2017"></a>SSDT for Visual Studio 2017

### <a name="changes-in-ssdt-for-visual-studio-2017"></a>SSDT for Visual Studio 2017 の変更点

Visual Studio 2017 以降では、データベース プロジェクトの作成機能が Visual Studio のインストールに統合されています。 Core SSDT エクスペリエンス用の SSDT のスタンドアロン インストーラーをインストールする必要はありません。

Analysis Services、Integration Services または Reporting Services のプロジェクトを作成するには、依然として SSDT のスタンドアロン インストーラーが必要です。

### <a name="install-ssdt-with-visual-studio-2017"></a>Visual Studio 2017 で SSDT をインストールする

[Visual Studio インストール](/visualstudio/install/install-visual-studio)中に SSDT をインストールするには、 **[データの保存と処理]** ワークロードを選択し、 **[SQL Server Data Tools]** を選択します。

Visual Studio が既にインストールされている場合、Visual Studio を使用し、インストール済みのワークロードを SSDT を含めるように変更します。

1. Visual Studio インストーラーを起動します。 Windows の [スタート] メニューで "installer" を検索できます。

   ![Windows の [スタート] メニューの Visual Studio インストーラー (2017)](../ssdt/media/visual-studio-installer.png)

2. インストーラーで SSDT を追加するエディションの Visual Studio を選択し、 **[変更]** を選択します。

3. ワークロードの一覧で **[データの保存と処理]** の下にある **[SQL Server Data Tools]** を選択します。

   ![[データの保存と処理] ワークロード (2017)](../ssdt/media/download-sql-server-data-tools-ssdt/data-workload-2017.png)

### <a name="install-analysis-services-integration-services-and-reporting-services-tools"></a>Analysis Services、Integration Services、Reporting Services ツールをインストールする

Analysis Services、Integration Services、Reporting Services プロジェクトのサポートをインストールするには、[SSDT スタンドアロン インストーラー](#ssdt-for-vs-2017-standalone-installer)を実行します。

このインストーラーは、SSDT ツールの追加先となる Visual Studio インスタンスを一覧表示します。 Visual Studio がまだインストールされていない場合、 **[Install a new SQL Server Data Tools instance]\(新しい SQL Server Data Tools インスタンスをインストールする\)** を選択すると、SSDT と最小バージョンの Visual Studio がインストールされます。ただし、最良のエクスペリエンスを得るには、[最新バージョンの Visual Studio](https://www.visualstudio.com/downloads) で SSDT を使用することをお勧めします。

![AS、IS、RS を選択する](../ssdt/media/download-sql-server-data-tools-ssdt/select-services.png)

## <a name="ssdt-for-vs-2017-standalone-installer"></a>SSDT for VS 2017 (スタンドアロン インストーラー)

:::image type="icon" source="media/download.png" border="false"::: **[SSDT for Visual Studio 2017 (15.9.6) のダウンロード](https://go.microsoft.com/fwlink/?linkid=2139376)**

> [!IMPORTANT]
> * SSDT for Visual Studio 2017 (15.9.6) をインストールする前に、*Analysis Services プロジェクト*と *Reporting Services プロジェクト*の拡張機能がインストールされている場合はアンインストールし、すべての VS インスタンスを閉じます。 
> * SQL Server 2017 用の受信トレイ コンポーネント Power Query ソースが削除されました。 すぐに使用できるコンポーネントとして SQL Server 2017 および 2019 用の Power Query ソースを発表しました。これは[こちら](https://www.microsoft.com/download/details.aspx?id=100619)からダウンロードできます。
> * Oracle および Teradata コネクタを使用し、SQL 2019 より前の以前のバージョンの SQL Server をターゲットとするパッケージを設計するには、[SQL 2019 用の Microsoft Oracle Connector](https://www.microsoft.com/download/details.aspx?id=58228) および [SQL 2019 用の Microsoft Teradata Connector](https://www.microsoft.com/download/details.aspx?id=100599) に加えて、対応するバージョンの Microsoft Connector for Oracle and Teradata by Attunity もインストールする必要があります。
>    * [SQL Server 2017 をターゲットとする Microsoft Connector Version 5.0 for Oracle and Teradata by Attunity](https://www.microsoft.com/download/details.aspx?id=55179)
>    * [SQL Server 2016 をターゲットとする Microsoft Connector Version 4.0 for Oracle and Teradata by Attunity](https://www.microsoft.com/download/details.aspx?id=52950)
>    * [SQL Server 2014 をターゲットとする Microsoft Connector Version 3.0 for Oracle and Teradata by Attunity](https://www.microsoft.com/download/details.aspx?id=44582)
>    * [SQL Server 2012 をターゲットとする Microsoft Connector Version 2.0 for Oracle and Teradata by Attunity](https://www.microsoft.com/download/details.aspx?id=29283)

### <a name="release-notes"></a>リリース ノート

すべての変更の一覧については、「[SQL Server Data Tools (SSDT) リリース ノート](release-notes-ssdt.md)」をご覧ください。

### <a name="system-requirements"></a>システム要件

SSDT for Visual Studio 2017 の[システム要件](/visualstudio/productinfo/vs2017-system-requirements-vs)は Visual Studio と同じです。

### <a name="available-languages---ssdt-for-vs-2017"></a>使用できる言語 - SSDT for VS 2017

**SSDT for VS 2017** の今回のリリースは、次の言語でインストールできます。

* [簡体中国語](https://go.microsoft.com/fwlink/?linkid=2139376&clcid=0x804)
* [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2139376&clcid=0x404)
* [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2139376&clcid=0x409)
* [フランス語](https://go.microsoft.com/fwlink/?linkid=2139376&clcid=0x40c)
* [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2139376&clcid=0x407)
* [イタリア語](https://go.microsoft.com/fwlink/?linkid=2139376&clcid=0x410)
* [日本語](https://go.microsoft.com/fwlink/?linkid=2139376&clcid=0x411)
* [韓国語](https://go.microsoft.com/fwlink/?linkid=2139376&clcid=0x412)
* [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2139376&clcid=0x416)
* [ロシア語](https://go.microsoft.com/fwlink/?linkid=2139376&clcid=0x419)
* [スペイン語](https://go.microsoft.com/fwlink/?linkid=2139376&clcid=0x40a)

### <a name="considerations-and-limitations"></a>考慮事項と制限事項

* コミュニティ バージョンをオフラインでインストールすることはできません

* SSDT をアップグレードするには、SSDT のインストールに使用したのと同じパスに従う必要があります。 たとえば、VSIX 拡張機能を使用して SSDT を追加した場合、VSIX 拡張機能を使用してアップグレードする必要があります。 別のインストール経由で SSDT をインストールした場合は、その方法を使用してアップグレードする必要があります。

## <a name="offline-install"></a>オフライン インストール

インターネットに接続されていない状態で SSDT をインストールするには、このセクションの手順に従います。 詳細については、「[Visual Studio 2017 のネットワーク インストールを作成する](/visualstudio/install/create-a-network-installation-of-visual-studio)」を参照してください。

まず、**オンライン**のときに次の手順を完了します。

1. [SSDT スタンドアロン インストーラーをダウンロードします](#ssdt-for-vs-2017-standalone-installer)。

2. [Download vs_sql.exe](https://aka.ms/vs/15/release/vs_sql.exe)。

3. 引き続き、オンラインのときに、次のコマンドのいずれかを実行し、オフライン インストールに必要なすべてのファイルをダウンロードします。 `--layout` オプションの使用がキーとなり、オフライン インストールのために実際のファイルがダウンロードされます。 `<filepath>` はファイルを保存する実際のレイアウトのパスに置き換えます。
   1. 特定の言語には、`vs_sql.exe --layout c:\<filepath> --lang en-us` のようにロケールを渡します (1 つの言語は 1 GB まで)。
   1. すべての言語には、`vs_sql.exe --layout c:\<filepath>` のように `--lang` 引数を省略します (すべての言語は 3.9 GB まで)。

前述の手順を完了したら、以下の手順を**オフライン**で実行できます。

1. `vs_setup.exe --NoWeb` を実行して、VS2017 Shell と SQL Server Data Project をインストールします。

2. レイアウト フォルダーから `SSDT-Setup-ENU.exe /install` を実行し、SSIS/SSRS/SSAS を選択します。
   a. 無人インストールを実行する場合は、`SSDT-Setup-ENU.exe /INSTALLALL[:vsinstances] /passive` を実行します。

利用可能なオプションについては、`SSDT-Setup-ENU.exe /help` を実行します。

> [!NOTE]
> Visual Studio 2017 の完全バージョンを使用する場合は、SSDT 専用のオフライン フォルダーを作成し、この新しく作成したフォルダーから `SSDT-Setup-ENU.exe` を実行します (別の Visual Studio 2017 のオフライン レイアウトに SSDT を追加しないでください)。 既存の Visual Studio のオフライン レイアウトに SSDT レイアウトを追加すると、必要なランタイム コンポーネント (.exe) がそこに作成されません。

## <a name="supported-sql-versions"></a>サポートされる SQL のバージョン

|プロジェクト テンプレート|サポートされている SQL プラットフォーム|
|-------------------|--------------------|
|リレーショナル データベース| SQL Server 2005\* - SQL Server 2017<br> (SSDT 17.x または SSDT for Visual Studio 2017 を使って、[SQL Server on Linux](../linux/sql-server-linux-overview.md) に接続します)<br /><br />Azure SQL データベース<br /><br />Azure Synapse Analytics (クエリのみサポートします。データベース プロジェクトは、まだサポートされていません)<br /><br /> \* SQL Server 2005 のサポートは非推奨とされます。<br /><br /> 正式にサポートされている SQL バージョンに移行します|
|Analysis Services モデル<br /><br />Reporting Services レポート | SQL Server 2008 - SQL Server 2017|
|Integration Services パッケージ| SQL Server 2012 - SQL Server 2019 |

## <a name="dacfx"></a>DacFx

SSDT for Visual Studio 2015 と SSDT for Visual Studio 2017 は、両方とも DacFx 17.4.1 を使用します。[データ層アプリケーション フレームワーク (DacFx) 17.4.1 をダウンロードする](https://www.microsoft.com/download/details.aspx?id=56508)。

## <a name="previous-versions"></a>以前のバージョン

Visual Studio 2015 の SSDT、または古いバージョンの SSDT をダウンロードしてインストールするには、「[SQL Server Data Tools (SSDT と SSDT-BI) の以前のリリース](previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi.md)」を参照してください。

## <a name="see-also"></a>参照

* [SSDT MSDN フォーラム](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt) 

* [SSDT チーム ブログ](/archive/blogs/ssdt/)

* [DACFx API リファレンス](/previous-versions/sql/sql-server-2014/dn645454(v=sql.120))

* [SQL Server Management Studio (SSMS) のダウンロード](../ssms/download-sql-server-management-studio-ssms.md)

## <a name="next-steps"></a>次のステップ

SSDT をインストールした後、次のチュートリアルを参照して、SSDT を使ったデータベース、パッケージ、データ モデル、レポートの作成方法を学ぶことができます。

* [プロジェクト指向のオフライン データベース開発](project-oriented-offline-database-development.md)

* [SSIS チュートリアル:シンプルな ETL パッケージの作成](../integration-services/ssis-how-to-create-an-etl-package.md)

* [Analysis Services チュートリアル](/analysis-services/analysis-services-tutorials-ssas)

* [基本的なテーブル レポートの作成 (SSRS チュートリアル)](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]