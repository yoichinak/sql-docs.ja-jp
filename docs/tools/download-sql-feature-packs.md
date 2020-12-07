---
title: SQL Server の拡張機能とツールのダウンロード
description: この記事では、 Microsoft が SQL Server に付加価値を与えるために提供するさまざまなダウンロードおよびスタンドアロン パッケージについて簡単に説明します。
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
keywords: Feature Pack
author: markingmyname
ms.author: maghan
ms.reviewer: mikeray
ms.custom: seo-lt-2019
ms.date: 12/15/2019
ms.openlocfilehash: 44d46bd260b1f59b9d1bcffd4a7bfb6ea46c248c
ms.sourcegitcommit: a9f16d7819ed0e2b7ad8f4a7d4d2397437b2bbb2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2020
ms.locfileid: "88713750"
---
# <a name="download-sql-server-extended-features-and-tools"></a>SQL Server の拡張機能とツールのダウンロード

[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

この記事では、 Microsoft が SQL Server に付加価値を与えるために提供するさまざまなダウンロードおよびスタンドアロン パッケージについて簡単に説明します。

## <a name="analysis-services"></a>Analysis Services

| 機能 | 説明 |
|----|-----|
| [Analysis Services クライアント ライブラリ](https://go.microsoft.com/fwlink/?LinkID=853574) |Microsoft Analysis Services クライアント ライブラリは、アプリケーション プログラミング インターフェイス (API) をカプセル化して、Microsoft SQL Server Analysis Services 2005 以降、Microsoft Azure Analysis Services、Microsoft Power BI との間で要求と応答の認証と交換を行います。<br><br> Microsoft Analysis Services クライアント ライブラリには、次のセットアップ パッケージが含まれます。 </br> Microsoft Analysis Services ADOMD.NET </br> Microsoft Analysis Services OLE DB プロバイダー (MSOLAP) </br> Microsoft 分析管理オブジェクト (AMO) |
| [NuGetAnalysisSrvs](https://www.nuget.org/profiles/NuGetAnalysisSrvs) | Analysis Services 用 NuGet |
|||

## <a name="azure"></a>Azure

| 機能 | 説明 |
|----|-----|
| [SQL Server Backup to Windows Azure Tool](https://go.microsoft.com/fwlink/?LinkID=391033) | Microsoft SQL Server Backup to Windows Azure Tool は、Windows Azure BLOB ストレージへのバックアップを可能にし、ローカルまたはクラウドに格納される SQL Server バックアップを圧縮します。 |
|||

## <a name="command-line-programming-and-t-sql"></a>コマンド ライン、プログラミング、T-SQL

| 機能 | 説明 |
|----|-----|
| [SQL Server 用 Command Line Utilities](https://www.microsoft.com/download/details.aspx?id=52680) | SQLCMD ユーティリティを使用すると、SQL Server インスタンスに接続でき、これらのインスタンスから Transact-SQL バッチを送信したり、行セット情報を出力したりできます。 |
| [SQL Server 用 Drivers for PHP](https://aka.ms/downloadmsphpsql) | Microsoft SQL Server 用 Drivers for PHP は PHP 拡張機能であり、これによって PHP スクリプトから SQL Server データの読み取りおよび書き込みが可能になります。 |
| [JDBC Driver for SQL Server](https://aka.ms/downloadmssqljdbc) | Microsoft JDBC Driver for SQL Server を使用すると、任意の Java アプリケーション、アプリケーション サーバー、Java 対応アプレットから、SQL Server にアクセスできます。|
| [SQL Server Data-Tier Application Framework](https://www.microsoft.com/download/details.aspx?id=56508) | SQL Server Data-tier Application (DAC) Framework は、.NET Framework をベースにしたコンポーネントであり、データベースの開発と管理に必要なアプリケーション ライフサイクル サービスを提供します。 |
| [SQL Server セマンティック言語統計](../relational-databases/search/install-and-configure-semantic-search.md) | セマンティック言語統計データベースは、Microsoft SQL Server の統計的セマンティック検索機能に必要なコンポーネントです。 |
| [SQL Server 共有管理オブジェクト](../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md) | SQL Server 管理オブジェクト (SMO) は .NET Framework のオブジェクト モデルです。ソフトウェア開発者は SMO を使用して、SQL Server のオブジェクトおよびサービスを管理するクライアント側アプリケーションを作成できます。 |
| [System CLR Types](https://go.microsoft.com/fwlink/?linkid=2108808) | SQL Server System CLR Types パッケージには、SQL Server の geometry 型、geography 型、および階層 ID 型を実装するコンポーネントが含まれています。 **注: このコンポーネントを使用するには、[Windows インストーラー 4.5](https://go.microsoft.com/fwlink/?LinkId=123373) も必要です**。 |
| [Windows PowerShell Extensions for Microsoft SQL Server](../database-engine/install-windows/install-sql-server-powershell.md?view=sql-server-2017) | Microsoft Windows PowerShell Extensions for SQL Server には、SQL Server インスタンスの管理用 PowerShell スクリプトを管理者および開発者が作成するためのプロバイダーとコマンドレットのセットが含まれています。 |
|||

## <a name="database-engine"></a>データベース エンジン

| 機能 | 説明 |
|----|-----|
| [SQL Server 用 Command Line Utilities](https://www.microsoft.com/download/details.aspx?id=52680) | SQLCMD ユーティリティを使用すると、SQL Server インスタンスに接続でき、これらのインスタンスから Transact-SQL バッチを送信したり、行セット情報を出力したりできます。 |
| [リモート BLOB ストア](https://go.microsoft.com/fwlink/?linkid=2109005) | SQL Server リモート BLOB ストアは、構造化されていないデータの BLOB を外部の連想データ ストアに保存する方法です。 コンポーネントは、ユーザー アプリケーションにリンクされるクライアント側の DLL と、SQL Server 上にインストールされるストアド プロシージャのセットで構成されます。 |
| [SQL Server Upgrade Advisor](../database-engine/install-windows/supported-version-and-edition-upgrades-version-15.md) | Microsoft Upgrade Advisor を使用すると、SQL Server へアップグレードするための準備として、SQL Server のインスタンスを分析できます。 |
|||

## <a name="integration-services"></a>Integration Services

| 機能 | 説明 |
|----|-----|
| [Integration Services Feature Pack for Azure](../integration-services/azure-feature-pack-for-integration-services-ssis.md) | Microsoft Integration Services Feature Pack for Azure には、IS を使用して Azure Stack に接続するためのツールが用意されています。 |
| [最新の SQL Server 用の Integration Services Feature Pack](https://www.microsoft.com/download/details.aspx?id=100303) | これらのスタンドアロン パッケージは、最新の Microsoft SQL Server Integration Services に付加価値を提供します。 |
|||

## <a name="kerberos"></a>Kerberos

| 機能 | 説明 |
|----|-----|
| [Kerberos Configuration Manager for Microsoft SQL Server](https://www.microsoft.com/download/details.aspx?id=39046) | Kerberos 認証は、ネットワーク上のクライアント エンティティおよびサーバー エンティティ (セキュリティ プリンシパル) を認証するための安全性の高い方法を提供します。 |
|||

## <a name="master-data-services"></a>マスター データ サービス

| 機能 | 説明 |
|----|-----|
| [Microsoft Excel 用マスター データ サービス アドイン](https://go.microsoft.com/fwlink/?LinkID=390972) | Microsoft Excel 用 マスター データ サービス (MDS) アドインは、容易かつ効率的にマスター データを管理するための豊富な機能を提供するデータ管理ツールです。 |
|||

## <a name="providers-and-drivers"></a>プロバイダーおよびドライバー

| 機能 | 説明 |
|----|-----|
| [SQL Server 用 Microsoft ODBC ドライバー](https://go.microsoft.com/fwlink/?LinkID=852531) | Microsoft ODBC Drivers for SQL Server によって、Windows および Unix から Microsoft SQL Server および Microsoft Azure SQL Database へのネイティブな接続が提供されます。 |
| [OLEDB Provider for DB2 for Microsoft SQL Server](/host-integration-server/db2oledbv/installing-data-provider-version-6-0) | Microsoft OLE DB Provider for DB2 v5.0 は、IBM の DB2 データベースに保存されている重要なデータを新しいソリューションと統合するためのテクノロジおよびツール一式を提供します。 SQL Server の開発者および管理者は、Integration Services、Analysis Services、レプリケーション、Reporting Services、および分散クエリ プロセッサでこのデータ プロバイダーを使用できます。 製品ドキュメント (オンラインで閲覧するか、ダウンロードします) に記載されている、データ プロバイダーのインストールに関するセクションを参照してください。 |
|||

## <a name="reporting-services"></a>Reporting Services

| 機能 | 説明 |
|----|-----|
| [レポート ビルダー](https://www.microsoft.com/download/details.aspx?id=53613) | レポート ビルダーは、IT プロフェッショナルおよびパワー ユーザーを対象に、生産性に優れたレポート作成環境を提供します。 SQL Server Reporting Services の完全な運用レポート機能がサポートされています。 |
| [Microsoft SharePoint 用 Reporting Services アドイン](../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)| Microsoft SharePoint テクノロジ用 Reporting Services アドインを使用すると、Reporting Services 機能を SharePoint でのコラボレーションに統合できます。 |
| [ASP.NET Web Forms アプリ用レポート ビューアー コントロール](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.WebForms/) | このレポート ビューアー コントロールを使用すると、SQL Server Reporting Services でページ設定されたレポートを、ASP.NET Web Forms アプリに埋め込むことができます。 |
| [Windows フォーム アプリ用レポート ビューアー コントロール](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Winforms/) | このレポート ビューアー コントロールを使用すると、SQL Server Reporting Services でページ設定されたレポートを、Windows フォーム アプリに埋め込むことができます。 |
|||

## <a name="sql-server-data-tools"></a>SQL Server Data Tools

| 機能 | 説明 |
|----|-----|
| [SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)| SQL Server Data Tools は、SQL Server リレーショナル データベース、Azure SQL データベース、Analysis Services (AS) データ モデル、Integration Services (IS) パッケージ、Reporting Services (RS) レポートをビルドするための、最新の開発ツールです。 SSDT では、Visual Studio でアプリケーションを開発する場合と同じくらい簡単に、SQL Server のコンテンツの種類を設計および展開できます。|
|||

## <a name="see-also"></a>参照

- [SQL Server Management Studio のドキュメント](../ssms/download-sql-server-management-studio-ssms.md)
- [Azure Data Studio](../azure-data-studio/download-azure-data-studio.md?view=sql-server-ver15)
- [追加の更新プログラムとサービス パック](../database-engine/install-windows/latest-updates-for-microsoft-sql-server.md?view=sql-server-ver15)
- [SQL Server Data Tools (SSDT) のダウンロード](../ssdt/download-sql-server-data-tools-ssdt.md)

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]