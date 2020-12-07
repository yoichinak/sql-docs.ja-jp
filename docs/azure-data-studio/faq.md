---
title: Azure Data Studio に関する FAQ
description: "\"これは何をするものなのか?\"、\"これは誰が使うものなのか?\"、\"これはいくらするのか?\" など、Azure Data Studio に関してよく寄せられる質問の回答を用意しました。"
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.reviewer: alayu, maghan
ms.custom: seodec18
ms.date: 10/28/2020
ms.openlocfilehash: 212115d87f747d1ee35bc4d9445833daee5d25e5
ms.sourcegitcommit: 9c6130d498f1cfe11cde9f2e65c306af2fa8378d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93035938"
---
# <a name="azure-data-studio-faq"></a>Azure Data Studio に関する FAQ

## <a name="what-is-azure-data-studio"></a>Azure Data Studio とは

[Azure Data Studio](what-is-azure-data-studio.md) とは、Windows、macOS、Linux 上でオンプレミスおよびクラウド データ プラットフォームの Azure Data ファミリを使用するデータ プロフェッショナルを対象にした、オープン ソースのクロスプラットフォーム デスクトップ環境です。 SQL Operations Studio というプレビュー名で以前にリリースされていた Azure Data Studio では、非常に高速な IntelliSense、コード スニペット、ソース管理の統合、統合されたターミナルを含む最新のエディター エクスペリエンスが提供されています。 これは、データ プラットフォームのユーザーを念頭に置いて設計されており、クエリ結果セットのグラフ化機能とカスタマイズ可能なダッシュボードが組み込まれています。

調査によると、ユーザーはクエリの編集作業に、SQL Server Management Studio でのその他の作業よりもはるかに多くの時間を費やしています。 そのため、Azure Data Studio は、最も使用されている機能に重点を置いて設計されていて、オプションの拡張機能として利用できるようにしたエクスペリエンスが製品に追加されています。 すべてのユーザーは最も頻繁に使用しているワークフローに合わせて自分の環境をカスタマイズできます。

## <a name="how-much-does-azure-data-studio-cost"></a>Azure Data Studio にはどれくらいのコストがかかりますか?

Azure Data Studio は、私的利用または商用利用で無料です。

## <a name="who-should-use-azure-data-studio"></a>どのような人が Azure Data Studio を使用すべきですか

だれでも Azure Data Studio を使用できます。 ただし、データベース開発者、データベース管理者、システム管理者、および独立系ソフトウェア ベンダーによって実行されるタスクを簡素化するように設計されています。

## <a name="what-can-i-do-with-azure-data-studio"></a>Azure Data Studio で何ができますか?

Azure Data Studio は Visual Studio Code の上に構築されていて、SQL Server、Azure SQL Database、Azure Synapse Analytics を操作する際に、キーボードに重点を置いた簡易な最新のコード ワークフロー エクスペリエンスを利用できます。 Azure Data Studio では、ご自分が日々依存しているコア エクスペリエンスが、複数のタブ ウィンドウ、充実した SQL エディター、IntelliSense、キーワード補完、コード スニペットとコード ナビゲーション、ソース管理の統合 (Git と TFS) などの組み込み機能によってシンプルで使いやすくなっています。 オンデマンドでのクエリの実行、テキスト、JSON、または Excel としての結果の表示と保存、データの編集、お気に入りのデータベース接続の整理と管理、馴染みのあるオブジェクト閲覧エクスペリエンスでのデータベース オブジェクトの参照を行うことができます。

Azure Data Studio ユーザー インターフェイス内の [統合ターミナル] ウィンドウにあるお気に入りのコマンドライン ツール (Bash、PowerShell、sqlcmd、bcp、psql、ssh など) を使用できます。 開発目的またはテスト目的でご利用のデータベースのコピーを作成するために、データベース オブジェクトに対して CREATE および INSERT スクリプトを簡単に生成および実行することができます。 データベースおよびデータベース オブジェクト (テーブル、ビュー、ストアド プロシージャ、ユーザー、ログイン、ロールなど) を新規に作成したり、既存のデータベース オブジェクトを更新したりする場合に、スマートなコード スニペットや充実したグラフィカル エクスペリエンスを使用することで生産性を高めることができます。 充実したカスタマイズ可能なダッシュボードを使用することで、オンプレミスのデータベースや、Azure または任意のクラウド内のデータベースでのパフォーマンスに関するボトルネックを監視し、そのトラブルシューティングを迅速に行うことができます。

Azure Data Studio では、ご利用のデータベースをバックアップおよび復元するための一貫したエクスペリエンスが提供されています。 SQL Server Always On 可用性グループの計画的なサポートにより、ご利用のミッションクリティカルな SQL Server データベース用の AG の構成、監視、トラブルシューティングを容易に行うことができ、障害発生時にはセカンダリ データベースに迅速にフェールオーバーすることができます。 Azure Data Studio は、任意のオペレーティングシステム上で選択したデータベースの DevOps ライフサイクルにおいて生産性が向上するように設計されています。 その結果、常に管理状態に置かれるので、リスクを軽減し、問題を迅速に解決し、顧客の期待を超える価値を継続的に提供することができます。

## <a name="is-azure-data-studio-open-source"></a>Azure Data Studio はオープンソースですか?

Azure Data Studio とそのデータ プロバイダーのソース コードは、GitHub で入手できます。 フロントエンド [Azure Data Studio](https://github.com/microsoft/azuredatastudio) のソースコード (Visual Studio Code に基づく) は、ソース コード EULA の下で利用できます。この EULA では、ソフトウェアを変更および使用する権利が提供されますが、ソフトウェアを再配布したりクラウド サービス内でホストしたりすることはできません。 データ プロバイダーのソース コードは、MIT ライセンス ([https://github.com/Microsoft/sqltoolsservice](https://github.com/Microsoft/sqltoolsservice)) の下で利用できます。

## <a name="do-we-plan-to-open-source-ssms"></a>オープンソースの SSMS を計画していますか?

いいえ。

ただし、次世代のマルチ OS CLI および GUI ツールはオープンソースです。 たとえば、VS Code、mssql-scripter、および msql CLI の mssql 拡張機能はすべて、GitHub のオープン ソースです。 Azure Data Studio のソース コードは、GitHub で入手できます。  

## <a name="now-that-theres-azure-data-studio-does-microsoft-plan-to-deprecate-ssms-and-ssdt"></a>Azure Data Studio があるので、Microsoft は SSMS と SSDT を廃止する予定ですか? 

いいえ。

主力の Windows ツール (SSMS、SSDT、PowerShell) への投資は、次世代のマルチ OS とマルチ DB CLI および GUI ツールに加えて継続されます。 目標は、お客様が自身のシナリオに合わせて選択したプラットフォーム上で希望するツールを選択できるようにすることです。 Azure Data Studio は、クエリの編集とデータ開発に関するエクスペリエンスにより重点を置いています。これらは、調査によれば、SQL Server Management Studio において桁違いに最も使用度の高い機能です。 Azure Data Studio では、拡張機能として、バックアップ、復元、エージェント ジョブ管理、サーバー プロファイリングなどのその他の重要度の高い管理機能を使用することもできます。 Azure Data Studio はクロスプラットフォームでもあるので、ユーザーは自分の選んだプラットフォームで作業を行うことができます。 ただし、SQL Server Management Studio では引き続き最も広範な管理機能が提供しており、これはプラットフォーム管理タスク用の主力ツールであり続けています。 

## <a name="when-should-i-use-azure-data-studio-or-sql-server-management-studio"></a>Azure Data Studio または SQL Server Management Studio は、どのような場合に使用する必要がありますか?

*Azure Data Studio は次のような場合に使用します。*

- 主にクエリの編集または実行を行っている。
- 結果セットをすばやくグラフ化して視覚化する機能が必要である。
- sqlcmd または PowerShell を使用して統合ターミナル経由でほとんどの管理タスクを実行することができる。
- ウィザードのエクスペリエンスが最小限必要である。
- 詳細な管理またはプラットフォームに関連する構成を行う必要はない。
- macOS または Linux 上で実行する必要がある。

*SQL Server Management Studio は次の場合に使用します。*

- 複雑な管理またはプラットフォームの構成を行っている。
- ユーザー管理、脆弱性評価、セキュリティ機能の構成など、セキュリティ管理を行っている。
- パフォーマンス チューニング アドバイザーとダッシュボードを使用する必要がある。
- データベース ダイアグラムとテーブル デザイナーを使用する。
- 登録済みサーバーへのアクセスが必要である。
- ライブ クエリ統計、またはクライアント統計を利用する。

## <a name="feature-comparison"></a>機能の比較

Azure Data Studio と SQL Server Management Studio (SSMS) の相違点の詳細については、「[Azure Data Studio とは](what-is-azure-data-studio.md#feature-comparison-with-sql-server-management-studio-ssms)」を参照してください。


## <a name="what-if-azure-data-studio-is-missing-a-feature-that-is-in-ssmsssdt"></a>Azure Data Studio で、SSMS/SSDT にある機能が見つからない場合は、どうなりますか?

それは、シナリオと顧客/ビジネス ニーズによって決まります。 優先順位を付けるために、[GitHub](https://github.com/microsoft/azuredatastudio/issues) に提案を提出し、既存のものに投票します。

## <a name="i-understand-azure-data-studio-and-the-mssql-extension-for-vs-code-are-powered-by-a-new-tools-service-that-uses-smo-apis-under-the-covers-is-smo-available-on-linux-and-macos"></a>Azure Data Studio と VS Code 用の mssql 拡張機能は、内部的に SMO API を使用する新しいツール サービスによって強化されていると理解しています。 SMO は Linux と macOS 上で利用できますか?

SMO API は、Linux または macOS に対してまだ使いやすい方法で提供されていません。 Microsoft は Azure Data Studio で必要としていて、ロードマップの一環として拡張する予定である SMO API のサブセットを .NET Core に移植済みです。 SQL Tools Service は GitHub 上の次の場所にあります: [https://github.com/Microsoft/sqltoolsservice](https://github.com/Microsoft/sqltoolsservice)。

## <a name="do-you-plan-to-port-the-dacfx-apis-andor-sqlpackageexe-andor-ssdt-to-linux-and-macos"></a>DACFx API、sqlpackage.exe、SSDT を Linux や macOS に移植する予定はありますか?

はい。

[SqlPackage.exe](../tools/sqlpackage-download.md) が、Windows、macOS、および Linux 用の .NET Core で使用できるようになりました。  SQL プロジェクト (SSDT) の機能は、[SQL Database プロジェクトの拡張機能](extensions/sql-database-project-extension.md)の Azure Data Studio で有効になっています。

## <a name="will-sql-powershell-cmdlets-be-available-on-linux-and-macos"></a>SQL PowerShell コマンドレットは、Linux および macOS 上で利用できますか?

SQL PowerShell は、現在 PowerShell ギャラリーで入手できます。これを Windows 上で使用すれば、Linux 上の SQL など、あらゆる場所で実行されている SQL Server を操作できます。 Linux および macOS 用の SQL PowerShell コマンドレットを提供することは、ロードマップにあります。 優先順位を付けるために、[GitHub](https://github.com/microsoft/azuredatastudio/issues) に提案を提出してください。

## <a name="who-usually-uses-azure-data-studio"></a>通常、だれが Azure Data Studio を使用しますか?

開発者と DBA が通常は、Azure Data Studio のユーザーです。

## <a name="does-azure-data-studio-integrate-with-azure-synapse-analytics"></a>Azure Data Studio は Azure Synapse Analytics に統合されますか?

はい。

Azure Synapse Analytics に対する Azure Data Studio のサポートは、Azure SQL Managed Instance および SQL Server 2019 ビッグ データと共に、現在プレビュー段階にあります。

## <a name="why-is-azure-data-studio-important-for-big-data-scenarios"></a>ビッグ データのシナリオで Azure Data Studio が重要なのはなぜですか?

SQL Server ではその機能が Big Data 領域にまで拡張されているので、それらのユースケースをサポートするために新しいツールが必要とされています。 そのため、Azure Data Studio によって SQL Server ビッグ データの新しいエクスペリエンスが提供されています。これには、SQL Server ツールセットのノートブック エクスペリエンスや、リモート SQL Server および Oracle インスタンスからのデータへのアクセスを簡単かつ高速にする新しい外部テーブルの作成ウィザードが含まれます。

## <a name="can-i-use-visual-studio-code-vs-code-extensions-with-azure-data-studio"></a>Azure Data Studio で Visual Studio Code (VS Code) 拡張機能を使用できますか?

はい。

ただし、VS Code のすべての拡張機能が Azure Data Studio に変換されるわけではありません。

## <a name="next-steps"></a>次の手順
- [Azure Data Studio とは](what-is-azure-data-studio.md)
- [Azure Data Studio のダウンロード](download-azure-data-studio.md)