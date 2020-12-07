---
title: SQL Server 2016 R Services のインストール
titleSuffix: ''
description: Windows に SQL Server 2016 R Services をインストールする方法について説明します。 R Services を使用すると、データベース内で R スクリプトを実行できます。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 08/06/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: contperfq4
monikerRange: =sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 1aa6fee67871e705f915f72a178ee4d0e4c562e6
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2020
ms.locfileid: "91956771"
---
# <a name="install-sql-server-2016-r-services"></a>SQL Server 2016 R Services のインストール

[!INCLUDE[SQL Server 2016 only](../../includes/applies-to-version/sqlserver2016-only.md)]

Windows に SQL Server 2016 R Services をインストールする方法について説明します。 R Services を使用すると、データベース内で R スクリプトを実行できます。

> [!NOTE]
> SQL Server 2017 以降で、R は Python と共に [Machine Learning Services](../sql-server-machine-learning-services.md) に含まれています。 R が必要な場合、SQL Server 2017 以降をお持ちの場合は、[SQL Server Machine Learning Services のインストール](sql-machine-learning-services-windows-install.md)に関するページを参照して、この機能を追加してください。

<a name="bkmk_prereqs"></a>

## <a name="pre-install-checklist"></a>インストール前のチェックリスト

+ データベース エンジンのインスタンスが必要です。 R だけをインストールすることはできませんが、既存のインスタンスに段階的に追加することはできます。

+ ビジネス継続性のために、R Services では [Always On 可用性グループ](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)がサポートされています。 各ノードに R Services をインストールし、パッケージを構成する必要があります。

+ SQL Server Always On フェールオーバー クラスター インスタンス (FCI) に R Services をインストールしないでください。 R プロセスを分離に使用されるセキュリティ上のメカニズムは、SQL Server Always On フェールオーバー クラスター インスタンス (FCI) 環境との互換性がありません。

+ R Services はドメイン コントローラーにはインストールしないでください。 セットアップの R Services の部分が失敗します。

+ **共有機能** > **R Server (スタンドアロン)** を、データベース内インスタンスを実行しているのと同じコンピューターにインストールしないでください。

+ R の他のバージョンとのサイドバイサイド インストールはサポートされていますが、推奨されません。 これがサポートされているのは、SQL Server インスタンスでは、オープンソースの R ディストリビューションの独自のコピーが使用されるからです。 しかし、SQL Server の外部の SQL Server コンピューターで R を使用するコードを実行すると、さまざまな問題が発生する可能性があります。

  + SQL Server で実行しているときとは異なるライブラリと実行可能ファイルを使用すると、異なる結果になります。
  + 外部ライブラリで実行されている R スクリプトは、SQL Server で管理できないため、リソースの競合が発生します。
  
> [!IMPORTANT]
> セットアップが完了したら、この記事で説明されている追加の構成後の手順を必ず完了してください。 これらの手順には、SQL Server で外部スクリプトを使用できるようにすることや、ユーザーに代わって SQL Server が R ジョブを実行するために必要なアカウントを追加することが含まれます。 通常、構成を変更するには、インスタンスを再起動するか、Launchpad サービスを再起動する必要があります。

## <a name="get-the-installation-media"></a>インストール メディアを入手する

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

<a name="bkmk_ga_instalpatch"></a>

### <a name="install-patch-requirement"></a>インストールのパッチ要件

SQL Server の前提条件としてインストールされる特定のバージョンの Microsoft VC++ 2013 ランタイム バイナリに問題が見つかりました。 VC ランタイム バイナリに対するこの更新プログラムをインストールしないと、特定のシナリオにおいて、SQL Server で安定性の問題が発生する可能性があります。 SQL Server をインストールする前に、「[SQL Server リリース ノート](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch)」にある手順に従って、ご使用のコンピューターに VC ランタイム バイナリのパッチが必要かどうかを確認してください。  

<a name="bkmk2016top"></a>

## <a name="run-setup"></a>セットアップを実行する

ローカル インストールの場合は、セットアップを管理者として実行する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をリモート共有からインストールする場合は、そのリモート共有に対する読み取り権限と実行権限を持つドメイン アカウントを使用する必要があります。

1. SQL Server 2016 のセットアップ ウィザードを開始します。

1. **[インストール]** タブで、 **[SQL Server の新規スタンドアロン インストールを実行するか、既存のインストールに機能を追加します]** を選択します。

    ![R Services (データベース内) のインストール](media/2016-setup-installation-rsvcs.png "R Services を使用してデータベース エンジンのインストールを開始する")

1. **[機能の選択]** ページで、次のオプションを選択します。

    + **[データベース エンジン サービス]** を選択します。 機械学習を使用する各インスタンスには、データベース エンジンが必要です。
    + **[R Services (データベース内)]** を選択します。 R のデータベース内での使用のサポートがインストールされます。

    ![R Services 機能の選択](media/2016setup-rsvcs-features.png "データベース内の R Services の機能を選択する")

    > [!IMPORTANT]
    > R Server と R Services を同時にインストールしないでください。 

1. **[Microsoft R オープンのインストールに同意する]** ページで、 **[同意する]** をクリックします。
  
    このライセンス契約は、Microsoft R Open をダウンロードするために必要です。これには、オープンソース R 基本パッケージとツール、Microsoft 開発チームから提供された R パッケージおよび接続プロバイダーのディストリビューションが含まれています。
  
1. ライセンス契約に同意した後、インストーラーが準備されるまで少し時間がかかります。 **[次へ]** ボタンが使用可能になったら、クリックします。

1. **[インストールの準備完了]** ページで、次の項目が選択されていることを確認した後、 **[インストール]** を選択します。

    + データベース エンジン サービス
    + R Services (データベース内)

1. セットアップが完了し、コンピューターの再起動を求めるメッセージが表示されたら、再起動してください。 セットアップが完了した時点で、インストール ウィザードによるメッセージを確認することが重要です。 詳細については、「 [SQL Server セットアップ ログ ファイルの表示と読み取り](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)」を参照してください。

## <a name="set-environment-variables"></a>環境変数の設定

R 機能の統合のみの場合、**MKL_CBWR** 環境変数を設定して、Intel Math Kernel Library (MKL) 計算からの[一貫した出力を保証](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)する必要があります。

1. コントロール パネルで、 **[システムとセキュリティ]**  >  **[システム]**  >  **[システムの詳細設定]**  >  **[環境変数]** の順にクリックします。

1. 新しいユーザー変数またはシステム変数を作成します。

    + 変数名を `MKL_CBWR` に設定する
    + 変数値を `AUTO` に設定する

この手順では、サーバーを再起動する必要があります。 すべての構成作業が完了するまで再起動を遅らせることができます。

<a name="bkmk_enableFeature"></a>

##  <a name="enable-script-execution"></a>スクリプトの実行を有効にする

1. [SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md) または [Azure Data Studio](../../azure-data-studio/what-is.md) を開きます。

1. R Services をインストールしたインスタンスに接続し、 **[新しいクエリ]** をクリックしてクエリ ウィンドウを開き、次のコマンドを実行します。

   ```sql
   sp_configure
   ```

    プロパティ `external scripts enabled` の値は、この時点では **0** であることが必要です。 これは、機能が既定で無効になっているためです。 この機能は、R スクリプトを実行する前に、管理者が明示的に有効にする必要があります。

1. 外部スクリプト機能を有効にするには、次のステートメントを実行します。
  
    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
## <a name="restart-the-service"></a>サービスを再起動します。

インストールが完了したら、次のスクリプトの実行を有効にする前に、データベース エンジンを再起動します。

サービスを再起動すると、関連する [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] サービスも自動的に再起動されます。

サービスの再起動は、SSMS でインスタンスの **[再起動]** コマンドを右クリックするか、[SQL Server 構成マネージャー](../../relational-databases/sql-server-configuration-manager.md)を使って行うことができます。

## <a name="verify-installation"></a>インストールの確認

次の手順に従って、外部スクリプトの起動に使用されるすべてのコンポーネントが実行されていることを確認します。

1. SQL Server Management Studio で、新しい [クエリ] ウィンドウを開き、次のコマンドを実行します。

    ```sql
    EXEC sp_configure 'external scripts enabled'
    ```

    この時点で、**run_value** が 1 に設定されている必要があります。

1. SQL Server 構成マネージャーを開き、**SQL Server Launchpad サービス**が実行されていることを確認します。 R がインストールされているすべてのデータベース エンジンのインスタンスに対して 1 つのサービスがある必要があります。 サービスの詳細については、[機能拡張フレームワーク](../concepts/extensibility-framework.md)に関するページを参照してください。

1. Launchpad が実行されている場合は、外部スクリプト ランタイムが SQL Server と通信できることを確認するため、単純な R を実行できる必要があります。

    [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または Azure Data Studio で新しい **[クエリ]** ウィンドウを開き、次のようなスクリプトを実行します。

    ```sql
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    スクリプトの実行には、最初に外部スクリプト ランタイムが読み込まれるときに少し時間がかかります。 結果は次のようになります。

    | hello |
    |----|
    | 1|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>更新プログラムの適用

最新の Service Pack と累積的な更新プログラムをデータベース エンジンと機械学習コンポーネントの両方に適用することが推奨されます。

インターネットに接続されているデバイスでは、通常、累積的な更新プログラムは Windows Update によって適用されますが、管理された更新には、次の手順を使用することもできます。 データベース エンジンに更新プログラムを適用すると、同じインスタンスにインストールした R ライブラリの累積更新プログラムがセットアップによってプルされます。 

接続されていないサーバーでは、追加の手順が必要です。 詳細については、[インターネット アクセスなしでコンピューターにインストールする > 累積的な更新プログラムを適用する](sql-ml-component-install-without-internet-access.md#apply-cu)を参照してください。

1. 既にインストールされているベースライン インスタンスを使用して開始します: SQL Server 2016 初回リリース、SQL Server 2016 SP 1、または SQL Server 2016 SP 2。

1. 累積的な更新プログラムの一覧に移動します: [Microsoft SQL Server の最新の更新プログラム](../../database-engine/install-windows/latest-updates-for-microsoft-sql-server.md)

1. 最新の Service Pack (ベースライン インスタンスとしてまだインストールされていない) と累積更新プログラムを選択します。 実行可能ファイルがダウンロードされ、自動的に抽出されます。

1. セットアップを実行します。 ライセンス条項に同意し、[機能の選択] ページで、累積的な更新プログラムが適用される機能を確認します。 R Services を含む、現在のインスタンスにインストールされているすべての機能が表示されます。 セットアップにより、すべての機能を更新するために必要な CAB ファイルがダウンロードされます。

1. ウィザードを続行し、R ディストリビューションのライセンス条項に同意します。

> [!NOTE]
> SQL Server 2016 SP2 の累積的な更新プログラム (CU) 14 以降には、より新しいバージョンの R ランタイムが含まれています。 詳細については、[既定の言語ランタイム バージョンの変更](change-default-language-runtime-version.md)に関するページを参照してください。

<a name="bkmk_FollowUp"></a>

## <a name="additional-configuration"></a>追加構成

外部スクリプトの検証手順が成功した場合は、SQL Server Management Studio、Azure Data Studio、または T-SQL ステートメントをサーバーに送信できる他の任意のクライアントから、R コマンドを実行できます。

コマンドの実行中にエラーが発生した場合は、このセクションの追加の構成手順を確認してください。 場合によっては、サービスまたはデータベースに対して追加の適切な構成を行う必要があります。

インスタンス レベルでは、追加の構成には次のものが含まれます。

* [SQL Server Machine Learning Services のファイアウォール構成](../../machine-learning/security/firewall-configuration.md)。
* [追加のネットワーク プロトコルの有効化](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)。
* [リモート接続の有効化](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)。
* ディスク領域を消費するタスクを外部スクリプトで実行しないようにするための[ディスク クォータの管理](/windows/desktop/fileio/managing-disk-quotas)。

<a name="bkmk_configureAccounts"></a>
<a name="bkmk_AllowLogon"></a>

データベースでは、次の構成の更新が必要になる場合があります。

* [SQL Server Machine Learning Services にユーザー アクセス許可を付与する](../../machine-learning/security/user-permission.md)
* [データベース ユーザーとしての SQLRUserGroup の追加](../../machine-learning/security/create-a-login-for-sqlrusergroup.md)

> [!NOTE]
> リストされたすべての変更が必要となるとは限りません。すべて不必要な場合もあります。 必要となるかどうかは、SQL Server をインストールしたセキュリティ スキーマと、ユーザーをどのようにデータベースに接続して外部スクリプトを実行させるかによって異なります。 インストールに関するその他のガイダンスについては、次を参照してください。[SQL Server Machine Learning Services のインストール](../install/sql-machine-learning-services-windows-install.md)

## <a name="suggested-optimizations"></a>推奨される最適化

R で機械学習をサポートするようにサーバーを最適化したり、事前トレーニング済みのモデルをインストールしたりすることもできます。

### <a name="add-more-worker-accounts"></a>ワーカー アカウントを追加する

R を多く使うと思われる場合、または多くのユーザーが同時にスクリプトを実行する場合は、スタート パッド サービスに割り当てられるワーカー アカウントの数を増やすことができます。 詳細については、「[SQL Server Machine Learning Services での外部スクリプトの同時実行のスケーリング](../administration/scale-concurrent-execution-external-scripts.md)」を参照してください。

<a name="bkmk_optimize"></a>

### <a name="optimize-the-server-for-external-script-execution"></a>外部スクリプトの実行用にサーバーを最適化する

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップの既定の設定は、データベース エンジンによってサポートされているさまざまなサービスに対してサーバーのバランスを最適化することを目的としています。サービスには、抽出、変換、および読み込み (ETL) プロセス、レポート、監査、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データを使うアプリケーションなどが含まれます。 そのため、既定の設定では、場合によっては機械学習用のリソースが制限または調整されることがあります (特に、メモリを大量に使用する操作の場合)。

確実に機械学習ジョブの優先順位が適切に設定され、リソースが提供されるようにするには、SQL Server Resource Governor を使って外部リソース プールを構成することをお勧めします。 また、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース エンジンに割り当てられるメモリの量を変更したり、[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] サービスで実行するアカウントの数を増やしたりすることもできます。

- 外部リソースを管理するためのリソース プールを構成するには、[CREATE EXTERNAL RESOURCE POOL](../../t-sql/statements/create-external-resource-pool-transact-sql.md) に関するページを参照してください。
  
- データベース用に予約されているメモリの量を変更するには、「[サーバー メモリの構成オプション](../../database-engine/configure-windows/server-memory-server-configuration-options.md)」を参照してください。
  
- [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] によって開始できる R アカウントの数を変更するには、「[SQL Server Machine Learning Services での外部スクリプトの同時実行のスケーリング](../administration/scale-concurrent-execution-external-scripts.md)」を参照してください。

Standard Edition を使用していて、Resource Governor がない場合は、動的管理ビュー (DMV) と拡張イベントに加え、Windows イベント監視を使用して、R によって使用されるサーバー リソースを管理できます。

### <a name="install-additional-r-packages"></a>追加の R パッケージをインストールする

SQL Server 用に作成する R ソリューションでは、基本 R 関数、SQL Server と共にインストールされた専用パッケージの関数、SQL Server によってインストールされたオープンソースの R のバージョンと互換性のあるサードパーティ製の R パッケージを呼び出すことができます。

SQL Server で使用するパッケージは、インスタンスによって使用される既定のライブラリにインストールする必要があります。 コンピューター上に R の別のインストールがある場合、またはパッケージをユーザー ライブラリにインストールした場合は、これらのパッケージを T-SQL から使用できません。

R パッケージのインストールと管理のプロセスは、SQL Server 2016 と SQL Server 2017 で異なります。 SQL Server 2016 では、データベース管理者は、ユーザーが必要とする R パッケージをインストールする必要があります。 SQL Server 2017 では、ユーザー グループを設定してデータベース レベルでパッケージを共有するか、ユーザーが独自のパッケージをインストールできるようにデータベース ロールを構成します。 詳細については、「[R ツールを使用してパッケージをインストールする](../package-management/install-r-packages-standard-tools.md)」をご覧ください。

## <a name="next-steps"></a>次のステップ

R 開発者はいくつかの簡単な例を試して、SQL Server での R の動作方法の基本を確認できます。 次の手順については、以下のリンクを参照してください。

+ [クイック スタート: T-SQL での R の実行](../tutorials/quickstart-r-create-script.md)
+ [SQL 機械学習用の R チュートリアル](../tutorials/r-tutorials.md)
+ [SQL の機械学習のドキュメント](../index.yml)