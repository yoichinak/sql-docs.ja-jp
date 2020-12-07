---
description: " の各エディションとサポートされる機能[!INCLUDE[sssqlv15-md](../includes/sssqlv15-md.md)]"
title: SQL Server 2019 の各エディションとサポートされている機能 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- Enterprise Edition [SQL Server]
- Developer Edition [SQL Server]
- 32-bit vs. 64-bit editions [SQL Server]
- default components
- Workgroup Edition [SQL Server]
- Internet servers [SQL Server]
- installing SQL Server, components
- Setup [SQL Server], components
- SQL Server, editions
- SQL Server, components
- client/server applications [SQL Server]
- editions [SQL Server]
- versions [SQL Server]
- Setup [SQL Server], editions
- SQL Server Installation Wizard
- components [SQL Server]
- Standard Edition [SQL Server]
- 64-bit edition [SQL Server]
- IIS [SQL Server]
- installing SQL Server, editions
- editions [SQL Server], about edition options
- Setup [SQL Server]
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 9601deea339bbbc8875bbb593a4efef42cdd070d
ms.sourcegitcommit: 9774e2cb8c07d4f6027fa3a5bb2852e4396b3f68
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2020
ms.locfileid: "92257769"
---
# <a name="editions-and-supported-features-of-sssqlv15-md"></a> の各エディションとサポートされる機能[!INCLUDE[sssqlv15-md](../includes/sssqlv15-md.md)]

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx](../includes/applies-to-version/sqlserver.md)]

このトピックでは、[!INCLUDE[sssqlv15-md](../includes/sssqlv15-md.md)] のさまざまなエディションでサポートされている機能の詳細を説明します。

以前のバージョンについては、以下を参照してください。

* [SQL Server 2017](editions-and-components-of-sql-server-2017.md)
* [SQL Server 2016](editions-and-components-of-sql-server-2016.md)

インストールの前提条件は、アプリケーションのニーズによって異なります。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] にはさまざまなエディションがあり、組織や個人の独自のパフォーマンス、ランタイム、および価格に関する要件に対応できます。 インストールする [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] コンポーネントは、ユーザーの特定の要件によっても異なります。 この後のセクションでは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の最適なエディションおよびコンポーネントを選択する方法について説明します。

180 日の試用期間中、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Evaluation Edition をご利用いただけます。

最新のリリース ノートと新機能については、以下の情報を参照してください。

* [[!INCLUDE[sssqlv15-md](../includes/sssqlv15-md.md)] リリース ノート](../sql-server/sql-server-version-15-release-notes.md)
* [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2019 の新機能](../sql-server/what-s-new-in-sql-server-ver15.md)

**[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] をお試しください。[Evaluation Center から [!INCLUDE[sssqlv15-md](../includes/sssqlv15-md.md)] をダウンロードしてください](https://www.microsoft.com//evalcenter/evaluate-sql-server)**

## <a name="ssnoversion-editions"></a>[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] のエディション

次の表で、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のエディションについて説明します。

|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エディション|定義|
|---------------------------------------|----------------|
|Enterprise|プレミアム製品である [!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Enterprise Edition は、非常に優れたパフォーマンス、無制限の仮想化<sup>1</sup>、およびエンド ツー エンドのビジネス インテリジェンスを備えた包括的なハイエンド データセンター機能を提供することで、ミッション クリティカルなワークロードに高水準のサービス レベルを実現し、エンド ユーザーがデータの分析情報を入手できるようにしています。|
|Standard|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Standard Edition は、企業部門や小規模組織がアプリケーションを実行するための基本的なデータ管理/ビジネス インテリジェンス データベースを提供し、内部設置型およびクラウド用の一般的な開発ツールをサポートすることで、最小限の IT リソースでデータベースを効果的に管理することを可能にします。|
|Web|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Web Edition は、大小さまざまな規模の Web 資産に対応できるスケーラビリティ、経済性、および管理性を備えた、Web ホスティング企業および Web VAP 向けの総保有コストの低いオプションです。|
|Developer|開発者は、[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Developer Edition を使用して、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]上で動作するあらゆる種類のアプリケーションを開発できます。 このエディションには Enterprise Edition の機能がすべて含まれていますが、実稼動サーバーとして使用するのではなく、開発およびテスト システムとしての利用に対してライセンスが供与されます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Developer は、アプリケーションを作成し、テストするユーザーに適しています。|
|Express Edition|Express Edition はエントリレベルの無料のデータベースで、学習や、デスクトップおよび小規模サーバー データ ドリブン アプリケーションの構築などに適しています。 このエディションは、独立系ソフトウェア ベンダー、開発者、クライアント アプリケーションを趣味で開発する開発者などに最適です。 さらに高度なデータベース機能が必要な場合には、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express を [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の他の上位バージョンにシームレスにアップグレードできます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express LocalDB は、Express の簡易バージョンです。Express のプログラミング機能をすべて備えており、ユーザー モードで実行され、前提条件が少なく構成不要の高速インストールが可能です。|

<sup>1</sup> 無制限の仮想化は、[ソフトウェア アシュアランス](https://www.microsoft.com/licensing/licensing-programs/software-assurance-default)がある Enterprise Edition のお客様が利用できます。 デプロイは、ライセンス ガイドに準拠している必要があります。 詳細については、価格とライセンスのページを参照してください。

## <a name="using-ssnoversion-with-clientserver-applications"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] とクライアント/サーバー アプリケーションの使用

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のクライアント コンポーネントだけを、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のインスタンスに直接接続するクライアント/サーバー アプリケーションを実行するコンピューターにインストールできます。 クライアント コンポーネントをインストールすることは、データベース サーバー上にある [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスを管理する場合、または [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] アプリケーションを開発しようとしている場合にも適切なオプションです。

クライアント ツールをインストールするオプションを選択すると、下位互換コンポーネント、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 、接続コンポーネント、管理ツール、ソフトウェア開発キット、 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]オンライン ブック コンポーネントなどの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 機能がインストールされます。 詳細については、[[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインストール](../database-engine/install-windows/install-sql-server.md)に関するページを参照してください。

### <a name="running-with-iis"></a>IIS での実行

インターネット インフォメーション サービス (IIS) を実行するサーバーなどのインターネット サーバーによって、一般に [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] クライアント ツールがインストールされます。 クライアント ツールには、アプリケーションが [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のインスタンスに接続する際に使用するクライアント接続コンポーネントが含まれています。

>[!NOTE]
>IIS を実行しているコンピューターに [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスをインストールすることは可能ですが、通常はサーバー コンピューターが 1 台の小規模 Web サイトの場合に行います。 ほとんどの Web サイトでは、その中層 IIS システムが 1 つまたはクラスター構成の複数サーバーに配置され、データベースは 1 つの独立したサーバーまたは連合構成の複数サーバーに配置されます。

## <a name="deciding-among-ssnoversion-components"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] コンポーネントの決定

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインストールに含めるコンポーネントを選択するには、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]インストール ウィザードの [機能の選択] ページを使用します。 既定では、ツリーの中に、選択されている機能はありません。

以下の表の情報を参照し、ニーズに最も合う機能を判断してください。

|サーバー コンポーネント|説明|
|-----------------------|-----------------|
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] には[!INCLUDE[ssDE](../includes/ssde-md.md)]が含まれています。これは、データの格納、処理、およびセキュリティ保護、レプリケーション、フルテキスト検索、リレーショナルおよび XML データを管理するツール、データベース内分析機能の統合、および Hadoop とその他の異種データ ソースにアクセスするための PolyBase 統合、およびリレーショナル データで Python および R スクリプトを実行するための Machine Learning Services 用のコア サービスです。|
|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] には、オンライン分析処理 (OLAP) アプリケーションおよびデータ マイニング アプリケーションを作成および管理するためのツールが含まれます。|
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] には、表形式、マトリックス形式、グラフィカル形式、および自由形式のレポートを作成、管理、配置するためのサーバー コンポーネントとクライアント コンポーネントが含まれます。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] は、レポート アプリケーション開発用の拡張可能プラットフォームとしても使用できます。|
|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] は、データを移動、コピー、変換するためのグラフィカル ツールおよびプログラミング可能なオブジェクトのセットです。 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] 用の [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)](DQS) コンポーネントも含まれています。|
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (MDS) は、マスター データ管理のための [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ソリューションです。 MDS は、あらゆるドメイン (製品、顧客、アカウント) を管理するように構成できます。MDS には、データの管理に使用できる [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] のほかに、階層、きめ細かいセキュリティ、トランザクション、データのバージョン管理、およびビジネス ルールが含まれています。|
|Machine Learning Services (データベース内)|Machine Learning Services (データベース内) は、エンタープライズ データ ソースを使用する分散型のスケーラブルな機械学習ソリューションをサポートします。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2016 では、R 言語がサポートされていました。 [!INCLUDE[sssqlv15-md](../includes/sssqlv15-md.md)] では、R と Python がサポートされています。|
|Machine Learning Server (スタンドアロン)|Machine Learning Server (スタンドアロン) では、Linux や Hadoop などの複数のエンタープライズ データ ソースを使用する分散型のスケーラブルな機械学習ソリューションを複数のプラットフォームに配置できます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2016 では、R 言語がサポートされていました。 [!INCLUDE[sssqlv15-md](../includes/sssqlv15-md.md)] では、R と Python がサポートされています。|

|管理ツール|説明|
|----------------------|-----------------|
|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] (SSMS) は、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のコンポーネントを構成、管理、開発し、それらのコンポーネントへアクセスするための統合環境です。 SSMS を使用すると、すべてのスキル レベルの開発者と管理者が [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] を使用できます。 最新エディションの SSMS を使用すると SMO が更新され、それには [SQL Assessment API](../tools/sql-assessment-api/sql-assessment-api-overview.md) が含まれます。<br /><br/> ダウンロードしてインストールする <br />「[[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Studio のダウンロード](https://msdn.microsoft.com/library/mt238290.aspx)」から [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]|
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャー|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーを使用して、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] サービス、サーバー プロトコル、クライアント プロトコル、およびクライアントの別名に関する基本的な構成管理を行います。|
|[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]|[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] には、 [!INCLUDE[ssDE](../includes/ssde-md.md)] または [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]のインスタンスを監視するためのグラフィカル ユーザー インターフェイスが備わっています。|
|[!INCLUDE[ssDE](../includes/ssde-md.md)] チューニング アドバイザー|[!INCLUDE[ssDE](../includes/ssde-md.md)] チューニング アドバイザーは、最適なインデックスのセット、インデックス付きビュー、およびパーティションの作成に役立ちます。|
|Data Quality クライアント|DQS サーバーに接続し、データ クレンジング操作を実行するための、非常にシンプルで直感的なグラフィカル ユーザー インターフェイスを備えています。 データ クレンジング操作の際に行われるさまざまな処理を一元的に監視することもできます。|
|[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]|[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] は、ビジネス インテリジェンス コンポーネント ( [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]) のソリューションをビルドするための IDE です。<br /><br /> (以前の Business Intelligence Development Studio)。<br /><br /> [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] には、Visual Studio 内で [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] プラットフォーム (社内および社外の両方) のデータベース設計を行うデータベース開発者用の統合環境である "データベース プロジェクト" も含まれます。 データベース開発者は、強化された Visual Studio のサーバー エクスプローラーを使用して、データベース オブジェクトおよびデータの作成または編集、クエリの実行を簡単に行うことができます。|
|接続コンポーネント|クライアントとサーバー間の通信用コンポーネント、および DB-Library、ODBC、OLE DB 用のネットワーク ライブラリをインストールします。|

|ドキュメント|説明|
|-------------------|-----------------|
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] オンライン ブック|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の主要マニュアル。|

**Developer Edition と Evaluation Edition** Developer Edition と Evaluation Edition でサポートされている機能については、下の表に記載されている [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise Edition の機能をご覧ください。

Developer Edition により、引き続き [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 分散再生](../tools/distributed-replay/sql-server-distributed-replay.md)のクライアントが 1 つだけサポートされます。

## <a name="scale-limits"></a><a name="Cross-BoxScaleLimits"></a> スケールの制限

|機能|Enterprise|Standard|Web|Express with<br/>Advanced Services|Express|
|-------|--------:|------:|---:|-------------------------------:|-----:|
|1 つのインスタンスで使用される最大計算容量 - [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]<sup>1</sup>|オペレーティング システムの最大容量|4 ソケットまたは 24 コアのいずれか小さいほうに制限|4 ソケットまたは 16 コアのいずれか小さいほうに制限|1 ソケットまたは 4 コアのいずれか小さいほうに制限|1 ソケットまたは 4 コアのいずれか小さいほうに制限|
|1 つのインスタンスで使用される最大計算容量 - [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] または [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|オペレーティング システムの最大容量|4 ソケットまたは 24 コアのいずれか小さいほうに制限|4 ソケットまたは 16 コアのいずれか小さいほうに制限|1 ソケットまたは 4 コアのいずれか小さいほうに制限|1 ソケットまたは 4 コアのいずれか小さいほうに制限|
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] のインスタンスごとのバッファー プールの最大メモリ|オペレーティング システムの最大容量|128 <nobr/>GB|64 <nobr/>GB|1410 <nobr/>MB|1410<nobr/> MB|
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] のインスタンスごとの列ストア セグメント キャッシュの最大メモリ|メモリ制限なし| 32 <nobr/>GB| 16 <nobr/>GB| 352 <nobr/>MB| 352 <nobr/>MB|
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] のデータベースごとの最大メモリ最適化データ サイズ|メモリ制限なし| 32 <nobr/>GB| 16 <nobr/>GB| 352 <nobr/>MB| 352 <nobr/>MB|
|利用可能な最大メモリ サイズ ( [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]のインスタンスごと)|オペレーティング システムの最大容量|16 <nobr/>GB<sup>2</sup><br /><br /> 64 <nobr/>GB<sup>3</sup>|該当なし|該当なし|該当なし|
|利用可能な最大メモリ サイズ ( [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]のインスタンスごと)|オペレーティング システムの最大容量|64 <nobr/>GB|64 <nobr/>GB|4 <nobr/>GB|該当なし|
|リレーショナル データベースの最大サイズ|524 <nobr/> PB|524 <nobr/> PB|524 <nobr/> PB|10 <nobr/>GB|10 <nobr/>GB|

<sup>1</sup> Enterprise Edition with Server および Client Access License (CAL) に基づくライセンス (新しい使用許諾契約では利用できません) は、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスあたり最大 20 コアに制限されています。 コアベースのサーバー ライセンス モデルでは、制限はありません。 詳細については、「[[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のエディション別の計算容量制限](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)」を参照してください。

<sup>2</sup> テーブル

<sup>3</sup> MOLAP

## <a name="rdbms-high-availability"></a><a name="RDBMSHA"></a> RDBMS の高可用性

|機能|Enterprise|Standard|Web|Express with<br/>Advanced Services|高速|
|-------|:--------:|:------:|:-:|--------------------------------:|:-----:|
|Server Core サポート<sup>1</sup>|はい|はい|はい|はい|はい|
|ログ配布|はい|はい|はい|いいえ|いいえ|
|データベース ミラーリング|はい|はい<sup>2</sup>|○<sup>3</sup>|○<sup>3</sup>|○<sup>3</sup>|
|バックアップ圧縮|はい|はい|いいえ|いいえ|いいえ|
|データベース スナップショット|はい|はい|はい|はい|はい|
|Always On フェールオーバー クラスター インスタンス<sup>4</sup>|はい|はい|いいえ|いいえ|いいえ|
|Always On 可用性グループ<sup>5</sup>|はい|いいえ|いいえ|いいえ|いいえ|
|基本的な可用性グループ<sup>6</sup>|いいえ|はい|いいえ|いいえ|いいえ|
|自動読み取りおよび書き込み接続の再ルーティング |はい|いいえ|いいえ|いいえ|いいえ|
|オンライン ページおよびファイルの復元|はい|いいえ|いいえ|いいえ|いいえ|
|オンライン インデックスの作成と再構築|はい|いいえ|いいえ|いいえ|いいえ|
|再開可能なオンライン インデックス再構築|はい|いいえ|いいえ|いいえ|いいえ|
|オンラインのスキーマ変更|はい|いいえ|いいえ|いいえ|いいえ|
|高速復旧|はい|いいえ|いいえ|いいえ|いいえ|
|高速データベース復旧|はい|はい|はい|いいえ|いいえ|
|ミラー化バックアップ|はい|いいえ|いいえ|いいえ|いいえ|
|ホット アド メモリと CPU|はい|いいえ|いいえ|いいえ|いいえ|
|データベース復旧アドバイザー|はい|はい|はい|はい|はい|
|暗号化されたバックアップ|はい|はい|いいえ|いいえ|いいえ|
|Windows Azure へのハイブリッド バックアップ (URL へのバックアップ)|はい|はい|はい|いいえ|いいえ|
|クラスターレス可用性グループ <sup>5、6</sup>|はい|はい|いいえ|いいえ|いいえ|
|ディザスター リカバリー用フェールオーバー サーバー<sup>7</sup>|はい|はい|いいえ|いいえ|いいえ|
|高可用性用フェールオーバー サーバー<sup>7</sup>|はい|はい|いいえ|いいえ|いいえ|
|Azure でのディザスター リカバリー用フェールオーバー サーバー<sup>7</sup>|はい|はい|いいえ|いいえ|いいえ|

<sup>1</sup> Server Core への [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインストールの詳細については、「[Server Core への [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインストール](../database-engine/install-windows/install-sql-server-on-server-core.md)」を参照してください。

<sup>2</sup> FULL SAFETY のみ

<sup>3</sup> ミラーリング監視のみ

<sup>4</sup> Enterprise Edition では、ノードの数はオペレーティング システムの最大容量です。 Standard Edition では、2 つのノードがサポートされます。

<sup>5</sup> Enterprise Edition では、5 個の同期セカンダリ レプリカを含む最大 8 個のセカンダリ レプリカがサポートされます。

<sup>6</sup> Standard Edition では、基本的な可用性グループがサポートされます。 基本的な可用性グループは、1 つのデータベースで、2 つのレプリカをサポートします。 基本的な可用性グループの詳細については、「[基本的な可用性グループ](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md)」を参照してください。

<sup>7</sup> [ソフトウェア アシュアランス](https://www.microsoft.com/licensing/licensing-programs/software-assurance-default)が必要です。

## <a name="rdbms-scalability-and-performance"></a><a name="RDBMSSP"></a> RDBMS のスケーラビリティとパフォーマンス

|機能|Enterprise|Standard|Web|Express with<br/>Advanced Services|高速|
|------:|:--------:|:------:|:-:|:-------------------------------:|:------:|
|列ストア<sup>1</sup> <sup>2</sup>|はい|はい|はい|はい|はい|
|クラスター化列ストア インデックス内のラージ オブジェクト バイナリ|はい|はい|はい|はい|はい|
|オンライン非クラスター化列ストア インデックスの再構築|はい|いいえ|いいえ|いいえ|いいえ|
|メモリ内データベース: インメモリ OLTP<sup>1</sup>|はい|はい|はい|○<sup>3</sup>|はい|
|メモリ内データベース: ハイブリッド バッファー プール|はい|はい|いいえ|いいえ|いいえ|
|メモリ内データベース: メモリ最適化 tempdb メタデータ|はい|いいえ|いいえ|いいえ|いいえ|
|メモリ内データベース: 永続メモリのサポート|はい|はい|はい|はい|はい|
|Stretch Database|はい|はい|はい|はい|はい|
|複数インスタンスのサポート|50|50|50|50|50|
|テーブルとインデックスのパーティション分割|はい|はい|はい|はい|はい|
|データ圧縮|はい|はい|はい|はい|はい|
|リソース ガバナー|はい|いいえ|いいえ|いいえ|いいえ|
|パーティション テーブルの並列処理|はい|いいえ|いいえ|いいえ|いいえ|
|複数の Filestream コンテナー|はい|はい|はい|はい|はい|
|NUMA 対応のラージ ページ メモリとバッファー配列の割り当て|はい|いいえ|いいえ|いいえ|いいえ|
|バッファー プール拡張|はい|はい|いいえ|いいえ|いいえ|
|I/O リソース管理|はい|いいえ|いいえ|いいえ|いいえ|
|先行読み取り|はい|いいえ|いいえ|いいえ|いいえ|
|拡張スキャン|はい|いいえ|いいえ|いいえ|いいえ|
|遅延持続性|はい|はい|はい|はい|はい|
|インテリジェント データベース: 自動チューニング|はい|いいえ|いいえ|いいえ|いいえ|
|インテリジェント データベース: 行ストアのバッチ モード <sup>1</sup>|はい|いいえ|いいえ|いいえ|いいえ|
|インテリジェント データベース: 行モード メモリ許可フィードバック|はい|いいえ|いいえ|いいえ|いいえ|
|インテリジェント データベース: 個別の概算数|はい|はい|はい|はい|はい|
|インテリジェント データベース: テーブル変数の遅延コンパイル|はい|はい|はい|はい|はい|
|インテリジェント データベース: スカラー UDF のインライン化|はい|はい|はい|はい|はい|
|バッチ モード アダプティブ結合|はい|いいえ|いいえ|いいえ|いいえ|
|バッチ モード メモリ許可フィードバック|はい|いいえ|いいえ|いいえ|いいえ|
|複数ステートメントのテーブル値関数のインターリーブ実行|はい|はい|はい|はい|はい|
|一括挿入の機能強化|はい|はい|はい|はい|はい|

<sup>1</sup> インメモリ OLTP データ サイズおよび列ストア セグメント キャッシュは、「[スケールの制限](#Cross-BoxScaleLimits)」セクションでエディションごとに指定されているメモリ量に制限されます。 [バッチ モード](../relational-databases/query-processing-architecture-guide.md#batch-mode-execution)操作の並列処理の度合い (DOP) は、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard Edition では 2 DOP、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Web Edition および Express Edition では 1 DOP に制限されます。 これは、ディスク ベース テーブルとメモリ最適化テーブルで作成された列ストア インデックスに当てはまります。

<sup>2</sup> 集計プッシュダウン、文字列述語のプッシュダウン、SIMD の最適化は、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise Edition のスケーラビリティの強化です。 詳細については、「[列ストア インデックス - 新機能](../relational-databases/indexes/columnstore-indexes-what-s-new.md)」を参照してください。

<sup>3</sup> LocalDB のインストール オプションには、この機能は含まれていません。

## <a name="rdbms-security"></a><a name="RDBMSS"></a> RDBMS のセキュリティ

|機能|Enterprise|Standard|Web|Express with<br/>Advanced Services|Express|
|-------|:--------:|:------:|:-:|:-----:|:-----------------------:|:-----:|
|行レベルのセキュリティ|はい|はい|はい|はい|はい|
|Always Encrypted|はい|はい|はい|はい|はい|
|セキュリティで保護されたエンクレーブが設定された Always Encrypted|はい|はい|はい|はい|はい|
|動的データ マスク|はい|はい|はい|はい|はい|
|サーバー監査|はい|はい|はい|はい|はい|
|データベース監査|はい|はい|はい|はい|はい|
|透過的なデータベースの暗号化|はい|はい|はい|いいえ|いいえ|
|拡張キー管理|はい|はい|いいえ|いいえ|いいえ|
|ユーザー定義ロール|はい|はい|はい|はい|はい|
|包含データベース|はい|はい|はい|はい|はい|
|バックアップの暗号化|はい|はい|いいえ|いいえ|いいえ|
|データの分類と監査|はい|はい|はい|はい|はい|

## <a name="replication"></a><a name="Replication"></a> レプリケーション

|機能|Enterprise|Standard|Web|Express with<br/>Advanced Services|高速|
|-------|:---------:|:-------:|:--:|:--------------------------------:|:------:|
|異種サブスクライバー|はい|はい|いいえ|いいえ|いいえ|
|マージ レプリケーション|はい|はい|可<sup>1</sup>|可<sup>1</sup>|可<sup>1</sup>|
|Oracle パブリッシュ|はい|いいえ|いいえ|いいえ|いいえ|
|ピア ツー ピア トランザクション レプリケーション|はい|いいえ|いいえ|いいえ|いいえ|
|スナップショット レプリケーション|はい|はい|可<sup>1</sup>|可<sup>1</sup>|可<sup>1</sup>|
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 変更の追跡|はい|はい|はい|はい|はい|
|トランザクション レプリケーション|はい|はい|可<sup>1</sup>|可<sup>1</sup>|可<sup>1</sup>|
|Azure へのトランザクション レプリケーション|はい|はい|いいえ|いいえ|いいえ|
|トランザクション レプリケーションの更新可能サブスクリプション|はい|はい|いいえ|いいえ|いいえ|

<sup>1</sup> サブスクライバーのみ

## <a name="management-tools"></a><a name="SSMS"></a> 管理ツール

|機能|Enterprise|Standard|Web|Express with Advanced Services|Express|
|-------|:--------:|:------:|:-:|:----------------------------:|:-----:|
|SQL 管理オブジェクト (SMO)|はい|はい|はい|はい|はい|
|SQL Assessment API|はい|はい|はい|はい|はい|
|SQL 脆弱性評価 |はい|はい|はい|はい|はい|
|SQL 構成マネージャー|はい|はい|はい|はい|はい|
|SQL CMD (コマンド プロンプト ツール)|はい|はい|はい|はい|はい|
|分散再生 - 管理ツール|はい|はい|はい|はい|いいえ|
|分散再生 - クライアント|はい|はい|はい|いいえ|いいえ|
|分散再生 - コントローラー|可<sup>1</sup>|はい<sup>2</sup>|はい<sup>2</sup>|いいえ|いいえ|
|SQL Profiler|はい|はい|いいえ<sup>3</sup>|いいえ<sup>3</sup>|いいえ<sup>3</sup>|
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エージェント|はい|はい|はい|いいえ|いいえ|
|Microsoft System Center Operations Manager 管理パック|はい|はい|はい|いいえ|いいえ|
|データベース チューニング アドバイザー (DTA)|はい|はい<sup>4</sup>|はい<sup>4</sup>|いいえ|いいえ|

<sup>1</sup> 最大 16 クライアント

<sup>2</sup> 1 クライアント

<sup>3</sup> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Web、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express with Tools、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express with Advanced Services は、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard および [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise エディションを使用してプロファイルできます。

<sup>4</sup> チューニングは Standard Edition 機能でのみ有効です。

## <a name="rdbms-manageability"></a><a name="RDBMSM"></a> RDBMS の管理の容易性

|機能|Enterprise|Standard|Web|Express with<br/>Advanced Services|高速|
|-------|:--------:|:------:|:-:|:-------------------------------:|:-----:|
|ユーザー インスタンス|いいえ|いいえ|いいえ|はい|はい|
|LocalDB|いいえ|いいえ|いいえ|はい|いいえ|
|専用管理者接続|はい|はい|はい|可<sup>1</sup>|可<sup>1</sup>|
|SysPrep のサポート <sup>2</sup>|はい|はい|はい|はい|はい|
|PowerShell スクリプティングのサポート<sup>3</sup>|はい|はい|はい|はい|はい|
|データ層アプリケーション コンポーネントの操作のサポート - 抽出、配置、アップグレード、削除|はい|はい|はい|はい|はい|
|ポリシー オートメーション (変更時とスケジュールに基づいて確認)|はい|はい|はい|いいえ|いいえ|
|パフォーマンス データ コレクター|はい|はい|はい|いいえ|いいえ|
|複数インスタンス管理でマネージド インスタンスとして登録できる|はい|はい|はい|いいえ|いいえ|
|標準的なパフォーマンス レポート|はい|はい|はい|いいえ|いいえ|
|プラン ガイドおよびプラン ガイドの固定計画|はい|はい|はい|いいえ|いいえ|
|NOEXPAND ヒントを使用したインデックス付きビューの直接クエリ|はい|はい|はい|はい|はい|
|SQL Server Analysis Services の直接クエリ|はい|はい|いいえ|いいえ|はい|
|インデックス付きビューの自動メンテナンス|はい|はい|はい|いいえ|いいえ|
|分散パーティション ビュー|はい|いいえ|いいえ|いいえ|いいえ|
|並列インデックス操作|はい|いいえ|いいえ|いいえ|いいえ|
|クエリ オプティマイザーによる自動的なインデックス付きのビュー使用|はい|いいえ|いいえ|いいえ|いいえ|
|並列整合性チェック|はい|いいえ|いいえ|いいえ|いいえ|
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ユーティリティ コントロール ポイント|はい|いいえ|いいえ|いいえ|いいえ|
|バッファー プール拡張|はい|はい|いいえ|いいえ|いいえ|
|ビッグ データ クラスターのマスター インスタンス|はい|はい|いいえ|いいえ|いいえ|
|互換性証明書|はい|はい|はい|はい|はい|

<sup>1</sup> トレース フラグを使用

<sup>2</sup> 詳細については、「[SysPrep を使用した [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインストールに関する注意点](../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md)」を参照してください。

<sup>3</sup> Linux では、Linux 上の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] をターゲットとする Windows コンピューターから PowerShell スクリプトがサポートされます。

## <a name="development-tools"></a><a name="DevTools"></a> 開発ツール

|機能|Enterprise|Standard|Web|Express with<br/>Advanced Services|高速|
|-------|:--------:|:------:|:-:|:-------------------------------:|:-----:|
|Microsoft Visual Studio の統合|はい|はい|はい|はい|はい|
|Intellisense (Transact-SQL および MDX)|はい|はい|はい|はい|はい|
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools (SSDT)|はい|はい|はい|はい|いいえ|
|MDX 編集、デバッグ、およびデザイン ツール|はい|はい|いいえ|いいえ|いいえ|

## <a name="programmability"></a><a name="Programmability"></a> Programmability

|機能|Enterprise|Standard|Web|Express with<br/>Advanced Services|高速
|-------|:--------:|:------:|:-:|:-------------------------------:|:-----:|
|基本的な R 統合<sup>1</sup>|はい|はい|はい|はい|いいえ|
|高度な R 統合<sup>2</sup>|はい|いいえ|いいえ|いいえ|いいえ|
|基本的な Python 統合|はい|はい|はい|はい|いいえ|
|高度な Python 統合|はい|いいえ|いいえ|いいえ|いいえ|
|Machine Learning Server (スタンドアロン)|はい|いいえ|いいえ|いいえ|いいえ|
|PolyBase コンピューティング ノード|はい|○<sup>3</sup>|○<sup>3</sup>|○<sup>3</sup>|○<sup>3</sup> |
|PolyBase ヘッド ノード<sup>4</sup>|はい|はい|いいえ|いいえ|いいえ|
|JSON|はい|はい|はい|はい|はい|
|クエリ ストア|はい|はい|はい|はい|はい|
|テンポラル|はい|はい|はい|はい|はい|
|共通言語ランタイム (CLR) 統合|はい|はい|はい|はい|はい|
|Java 言語ランタイム統合|はい|はい|はい|はい|はい|
|ネイティブ XML サポート|はい|はい|はい|はい|はい|
|XML インデックスの作成|はい|はい|はい|はい|はい|
|MERGE と UPSERT の機能|はい|はい|はい|はい|はい|
|FILESTREAM のサポート|はい|はい|はい|はい|はい|
|FileTable|はい|はい|はい|はい|はい|
|日付および時刻データ型|はい|はい|はい|はい|はい|
|国際化サポート|はい|はい|はい|はい|はい|
|フルテキストおよびセマンティック検索|はい|はい|はい|はい|いいえ|
|クエリ内の言語指定|はい|はい|はい|はい|いいえ|
|Service Broker (メッセージング)|はい|はい|いいえ<sup>5</sup>|いいえ<sup>5</sup>|いいえ<sup>5</sup>|
|Transact-SQL エンドポイント|はい|はい|はい|いいえ|いいえ|
|グラフ|はい|はい|はい|はい|はい|
|UTF-8 のサポート|はい|はい|はい|はい|はい|

<sup>1</sup> 基本的な統合は 2 コアとメモリ内データ セットに制限されます。

<sup>2</sup> 高度な統合では、使用可能な全てのコアを、ハードウェア制限の対象となるすべてのサイズのデータ セットの並列処理で使用できます。

<sup>3</sup> 複数のコンピューティング ノードでのスケール アウトにはヘッド ノードが必要です。

<sup>4</sup> SQL Server 2019 PolyBase ヘッド ノードより前は、Enterprise Edition が必要です。

<sup>5</sup> クライアントのみ

## <a name="integration-services"></a><a name="IS"></a> Integration Services

[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] の各エディションによってサポートされる [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Integration Services (SSIS) の機能については、「[[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の各エディションがサポートする Integration Services の機能](../integration-services/integration-services-features-supported-by-the-editions-of-sql-server.md)」を参照してください。

## <a name="master-data-services"></a><a name="MDS"></a> Master Data Services

[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] の各エディションによってサポートされる [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] と Data Quality Services の機能については、「[マスター データ サービスと [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のエディションでサポートされるデータ品質サービス機能](../master-data-services/master-data-services-and-data-quality-services-features-support.md)」を参照してください。

## <a name="data-warehouse"></a><a name="DW"></a> データ ウェアハウス

|機能|Enterprise|Standard|Web|Express with<br/>Advanced Services|高速|
|-------|:--------:|:------:|:-:|:-------------------------------:|:-----:|
|自動生成ステージングとデータ ウェアハウス スキーマ|はい|はい|いいえ|いいえ|いいえ|
|変更データ キャプチャ|はい|はい|いいえ|いいえ|いいえ|
|スター結合クエリ最適化|はい|いいえ|いいえ|いいえ|いいえ|
|パーティション テーブルとパーティション インデックスに対する並列クエリ処理|はい|いいえ|いいえ|いいえ|いいえ|
|グローバル バッチ集計|はい|いいえ|いいえ|いいえ|いいえ|

## <a name="analysis-services"></a><a name="SSAS"></a> Analysis Services

[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] の各エディションによってサポートされる Analysis Services の機能については、「[[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の各エディションがサポートする Analysis Services の機能](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)」を参照してください。

## <a name="reporting-services"></a><a name="SSRS"></a> Reporting Services

[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] の各エディションによってサポートされる Reporting Services の機能については、「[[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の各エディションがサポートする Reporting Services の機能](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)」を参照してください。

## <a name="business-intelligence-clients"></a><a name="BIC"></a> Business Intelligence クライアント

[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] の各エディションによってサポートされる Business Intelligence クライアントの機能については、「[[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の各エディションがサポートする Analysis Services の機能](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)」または「[[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の各エディションがサポートする Reporting Services の機能](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)」を参照してください。

## <a name="spatial-and-location-services"></a><a name="SLS"></a> 空間およびロケーション サービス

|機能名|Enterprise|Standard|Web|Express with<br/>Advanced Services|Express|
|-------------|:-------:|:------:|:-:|:-------------------------------:|:-----:|
|空間インデックス|はい|はい|はい|はい|はい|
|平面データ型と測地データ型|はい|はい|はい|はい|はい|
|高度な空間的なライブラリ|はい|はい|はい|はい|はい|
|業界標準の空間データ形式のインポート/エクスポート|はい|はい|はい|はい|はい|

## <a name="additional-database-services"></a><a name="ADS"></a> その他のデータベース サービス

|機能名|Enterprise|Standard|Web|Express with<br/>Advanced Services|高速|
|------------|:--------:|:------:|:-:|:-------------------------------:|:-----:|
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Migration Assistant|はい|はい|はい|はい|はい|
|データベース メール|はい|はい|はい|いいえ|いいえ|

## <a name="other-components"></a><a name="Other"></a> その他のコンポーネント

|機能名|Enterprise|Standard|Web|Express with<br/>Advanced Services|高速|
|------------|:--------:|:------:|:-:|:-------------------------------:|:-----:|
|StreamInsight|StreamInsight Premium Edition|StreamInsight Standard Edition|StreamInsight Standard Edition|いいえ|いいえ|
|StreamInsight HA|StreamInsight Premium Edition|いいえ|いいえ|いいえ|いいえ|

## <a name="next-steps"></a>次のステップ

[[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の製品仕様](https://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb)

[[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインストール](../database-engine/install-windows/installation-for-sql-server-2016.md)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
