---
title: Upgrade Python および R ランタイムをアップグレードする (バインド)
description: SQL Server Machine Learning Services または SQL Server R Services で、sqlbindr.exe を使用した Machine Learning Server へのバインドにより、Python および R ランタイムをアップグレードします。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 09/30/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: =sql-server-2016||=sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: 3263723e04834e5b0a6bad86455f281fe643e083
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870460"
---
# <a name="upgrade-python-and-r-runtime-with-binding-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services でバインドを使用して Python および R ランタイムをアップグレードする
[!INCLUDE [SQL Server 2016 and 2017](../../includes/applies-to-version/sqlserver2016-2017-only.md)]

この記事では **バインド** と呼ばれるインストール プロセスを使用して、[SQL Server 2016 R Services](../r/sql-server-r-services.md) または [SQL Server 2017 Machine Learning Services](../sql-server-machine-learning-services.md) で R または Python ランタイムをアップグレードする方法について説明します。 [Microsoft Machine Learning Server](/machine-learning-server) に "*バインドする*" ことで、[より新しいバージョンの Python および R](#version-map) を入手できます。

> [!IMPORTANT]
> この記事では、*バインド* と呼ばれる、R および Python ランタイムをアップグレードする古い方法について説明します。 **SQL Server 2016 Services Pack (SP) 2 の累積的な更新プログラム (CU) 14 以降** または **SQL Server 2017 の累積的更新プログラム (CU) 22 以降** をインストールしている場合は、代わりに [既定の R または Python 言語ランタイムを新しいバージョンに変更する](change-default-language-runtime-version.md)方法をご覧ください。

## <a name="what-is-binding"></a>バインドとは

バインドは、**R_SERVICES** と **PYTHON_SERVICES** のフォルダーの内容を、[Microsoft Machine Learning Server](/machine-learning-server) の新しい実行可能ファイル、ライブラリ、およびツールを使用して交換するインストール プロセスです。

サービス モデルに付属するアップロード済みのコンポーネントが変更されました。 サービスの更新は、[モダン ライフサイクル](https://support.microsoft.com/help/30881/modern-lifecycle-policy)の [Microsoft R Server および Machine Learning Server のサポート タイムライン](/machine-learning-server/resources-servicing-support)と一致します。

コンポーネントのバージョンとサービスの更新を除き、バインドによってインストールの基本が変更されることはありません。

- Python および R の統合は、引き続きデータベース エンジンのインスタンスの一部です。
- ライセンスは変更されません (バインドに関連する追加コストはありません)。
- SQL Server サポート ポリシーは、データベース エンジンに対して引き続き維持されます。

この記事の残りの部分では、バインド メカニズムと SQL Server の各バージョンでの動作について説明します。

> [!NOTE]
> バインドは、SQL Server のインスタンスにバインドされている、データベース内インスタンスにのみ適用されます。 この場合、スタンドアロン インストールにはバインドは必要ありません。

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
**SQL Server 2016 のバインドに関する考慮事項**

SQL Server 2016 R Services のお客様の場合は、バインドによって次が提供されます。

- 更新された R パッケージ。
- 元のインストールに含まれていない新しいパッケージ ([MicrosoftML](/machine-learning-server/r-reference/microsoftml/microsoftml-package))
- 感情分析と画像検出用の事前トレーニング済みの機械学習[モデル](/machine-learning-server/install/microsoftml-install-pretrained-models)。

[Microsoft Machine Learning Server](/machine-learning-server/index) の新しいメジャー リリースとマイナー リリースごとに、すべてのバインドをさらに更新することができます。
::: moniker-end

## <a name="version-map"></a>バージョン マップ

以下の表は、バージョン マップです。 各マップには、リリース間でのパッケージ バージョンが示されています。 Microsoft Machine Learning Server (Machine Learning Server 9.2.1 からの Python サポートの追加以前は、R Server と呼ばれていました) にバインドする際のアップグレード パスを確認できます。

バインドを行っても、最新バージョンの R または Anaconda は保証されません。 Microsoft Machine Learning Server にバインドすると、セットアップを通じてインストールされる R または Python のバージョンを入手できますが、これは Web 上で入手できる最新バージョンではない可能性があります。

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
[**SQL Server 2016 R Services**](../install/sql-r-services-windows-install.md)

コンポーネント |最初のリリース | [Microsoft R Server 9.0.1](/machine-learning-server/install/r-server-install-windows) | [Microsoft R Server 9.1](/machine-learning-server/install/r-server-install-windows) | [Machine Learning Server 9.2.1](/machine-learning-server/install/machine-learning-server-windows-install) | [Machine Learning Server 9.3](/machine-learning-server/install/machine-learning-server-windows-install) |  [Machine Learning Server 9.4.7](/machine-learning-server/install/machine-learning-server-windows-install)
----------|----------------|----------------|--------------|---------|-------|-------|
R 上の Microsoft R Open (MRO) | R 3.2.2     | R 3.3.2   |R 3.3.3   | R 3.4.1  | R 3.4.3 | R 3.5.2
[RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) | 8.0.3  | 9.0.1 |  9.1 |  9.2.1 |  9.3 |  9.4.7 |
[MicrosoftML](/machine-learning-server/r-reference/microsoftml/microsoftml-package)| 該当なし | 9.0.1 |  9.1 |  9.2.1 |  9.3 | 9.4.7 |
[事前トレーニング済みモデル](/machine-learning-server/install/microsoftml-install-pretrained-models)| 該当なし | 9.0.1 |  9.1 |  9.2.1 |  9.3 | 9.4.7 |
[sqlrutils](/machine-learning-server/r-reference/sqlrutils/sqlrutils)| 該当なし | 1.0 |  1.0 |  1.0 |  1.0 | 1.0 |
[olapR](/machine-learning-server/r-reference/olapr/olapr) | 該当なし | 1.0 |  1.0 |  1.0 |  1.0 | 1.0 |
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
[**SQL Server 2017 Machine Learning Services**](../install/sql-machine-learning-services-windows-install.md)

コンポーネント |最初のリリース | Machine Learning Server 9.3 | Machine Learning Server 9.4.7 |
----------|----------------|---------|---------|
R 上の Microsoft R Open (MRO) | R 3.3.3 | R 3.4.3 | R 3.5.2 |
[RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) |   9.2 |  9.3 | 9.4.7 |
[MicrosoftML](/machine-learning-server/r-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| 9.4.7 |
[sqlrutils](/machine-learning-server/r-reference/sqlrutils/sqlrutils)| 1.0 |  1.0 | 1.0 |
[olapR](/machine-learning-server/r-reference/olapr/olapr) | 1.0 |  1.0 | 1.0 |
Python 3.5 上の Anaconda 4.2  | 4.2/3.5.2 | 4.2/3.5.2 |
[revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2  | 9.3| 9.4.7 |
[microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| 9.4.7 |
[事前トレーニング済みモデル](/machine-learning-server/install/microsoftml-install-pretrained-models) | 9.2 | 9.3| 9.4.7 |
::: moniker-end

## <a name="how-component-upgrade-works"></a>コンポーネントのアップグレードのしくみ

実行可能ファイル、Python、および R のライブラリは、Python および R の既存のインストールを Machine Learning Server にバインドするときにアップグレードされます。

バインドは、Python および R が統合された既存の SQL Server データベース エンジンのインスタンスでセットアップを実行するときに、[Microsoft Machine Learning Server のインストーラー](/machine-learning-server/install/machine-learning-server-windows-install)によって実行されます。 

セットアップによって既存の機能が検出され、Machine Learning Server に再バインドするように求めるメッセージが表示されます。

バインド中に、`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES` と `\PYTHON_SERVICES` の内容が、`C:\Program Files\Microsoft\ML Server\R_SERVER` と `\PYTHON_SERVER` の新しい実行可能ファイルとライブラリで上書きされます。

バインドは Python および R の機能にのみ適用されます。 Python および R のオープンソース パッケージは、次のもので構成されます。

- Anaconda
- Microsoft R Open
- 専用パッケージ RevoScaleR
- Revoscalepy

バインドによって、データベース エンジンのインスタンスのサポート モデルや SQL Server のバージョンが変更されることはありません。

バインドは元に戻すことができます。 [インスタンスのバインドを解除し](#bkmk_Unbind)、SQL Server データベース エンジンのインスタンスを修復することによって、SQL Server サービスに戻すことができます。

<a name="bkmk_BindWizard"></a>

## <a name="bind-to-machine-learning-server-using-setup"></a>セットアップを使用して Machine Learning Server にバインドする

セットアップを使用して SQL Server を Microsoft Machine Learning Server にバインドするには、次の手順に従います。 

1. SSMS で `SELECT @@version` を実行して、サーバーが最小ビルド要件を満たしていることを確認します。

   SQL Server 2016 R Services の場合、最小値は [Service Pack 1](https://www.microsoft.com/download/details.aspx?id=54276) および [CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1)です。

1. R ベース と RevoScaleR パッケージのバージョンを確認して、既存のバージョンが、それを置き換える予定のものよりも古いことを確認します。 

    ```sql
    EXECUTE sp_execute_external_script
    @language=N'R'
    ,@script = N'str(OutputDataSet);
    packagematrix <- installed.packages();
    Name <- packagematrix[,1];
    Version <- packagematrix[,3];
    OutputDataSet <- data.frame(Name, Version);'
    , @input_data_1 = N''
    WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
    ```

1. SSMS と、SQL Server への接続が開いている他のツールをすべて閉じます。 バインドは、プログラム ファイルを上書きします。 SQL Server が開いているセッションがある場合、バインドが失敗し、バインド エラー コード 6 が表示されます。

1. アップグレードするインスタンスがあるコンピューターに Microsoft Machine Learning Server をダウンロードします。 [最新のバージョン](/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer)をお勧めします。

1. フォルダーを解凍し、MLSWIN93 の下にある ServerSetup.exe を起動します。

1. **インストールを構成する** で、アップグレードするコンポーネントを確認して、互換性のあるインスタンスの一覧をレビューします。

1. **[ライセンス契約]** ページで、 **[次の使用条件に同意します]** を選択して Machine Learning Server のライセンス使用条件に同意します。 

1. 連続するページで、Microsoft R Open や Python Anaconda のディストリビューションなど、選択したオープンソース コンポーネントの追加のライセンス条件に同意します。

1. **[完了まであと少しです]** のページで、インストール フォルダーをメモしておきます。 既定のフォルダーは、\Program Files\Microsoft\ML Server です。

    インストール フォルダーを変更する場合は、 **[詳細]** を選択して、ウィザードの最初のページに戻ります。 ただし、前の選択をすべて繰り返す必要があります。

アップグレードに失敗した場合、詳細については、[SqlBindR エラーコード](#sqlbindr-error-codes)を確認してください。

## <a name="offline-binding-no-internet-access"></a>オフラインバインド (インターネットアクセスなし)

インターネットに接続されていないシステムでは、インストーラーと .cab ファイルをインターネットに接続されたコンピューターにダウンロードして、分離されたサーバーにファイルを転送できます。

インストーラー (ServerSetup.exe) には、Microsoft のパッケージ (RevoScaleR、MicrosoftML、olapR、sqlRUtils) が含まれています。 .Cab ファイルには、他のコア コンポーネントが用意されています。 たとえば、"SRO" cab は R Open (Microsoft の配布するオープンソース R) を提供します。

次の手順では、オフライン インストール用のファイルを配置する方法について説明します。

1. MLSWIN93 インストーラーをダウンロードします。 1つの zip 形式のファイルとしてダウンロードします。 [最新バージョン](/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer)をお勧めしますが、[以前のバージョン](/machine-learning-server/install/r-server-install-windows-offline#download-required-components)をインストールすることもできます。

1. .Cab ファイルをダウンロードします。 9\.3 リリースのリンクは次のとおりです。 以前のバージョンが必要な場合は [Microsoft R Server 9.1](/machine-learning-server/install/r-server-install-windows-offline#download-required-components) に追加のリンクがあります。 Python/Anaconda は SQL Server Machine Learning Services のインスタンスにのみ追加できることに注意してください。 事前トレーニング済みのモデルは、Python と R の両方に対して存在します。.cab では、ご利用の言語でのモデルが提供されます。

    | 機能 | ダウンロード |
    |---------|----------|
    | R       | [SRO_3.4.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=867186&clcid=1033) |
    | Python  | [SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054) | 
    | トレーニング済みモデル | [MLM_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859053) |

1. .Zip ファイルと .cab ファイルをターゲット サーバーに転送します。

1. サーバーで、Run コマンドに `%temp%` と入力して、一時ディレクトリの物理的な場所を取得します。 物理パスはマシンによって異なりますが、通常は `C:\Users\<your-user-name>\AppData\Local\Temp` です。

1. .Cab ファイルを % temp% フォルダーに配置します。

1. インストーラーを実行します。

1. ServerSetup.exe を実行し、画面の指示に従ってインストールを完了します。

## <a name="command-line-operations"></a><a name="bkmk_BindCmd"></a>コマンド ライン操作


> [!TIP]
> SqlBindR が見つかりませんか。 セットアップを実行していない可能性があります。
> SqlBindR は Machine Learning Server のセットアップを実行した後にのみ使用できます。

1. 管理者としてコマンド プロンプトを開き、sqlbindr.exe を含むフォルダーに移動します。 既定の場所は、C:\Program Files\Microsoft\MLServer\Setup です

2. 次のコマンドを入力して、使用可能なインスタンスの一覧を表示します。 `SqlBindR.exe /list`
  
   一覧表示されている完全なインスタンス名をメモしておきます。 たとえば、既定のインスタンスの場合、インスタンス名は MSSQL14.MSSQLSERVER または SERVERNAME.MYNAMEDINSTANCE のようになります。

3. */bind* 引数を指定して **SqlBindR.exe** コマンドを実行します。 前の手順で返されたインスタンス名を使用して、アップグレードするインスタンスの名前を指定します。

   たとえば、既定のインスタンスをアップグレードするには、次のように入力します。  `SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. アップグレードが完了したら、変更されたインスタンスに関連付けられているスタート パッド サービスを再起動します。

## <a name="revert-or-unbind-an-instance"></a><a name="bkmk_Unbind"></a>インスタンスを元に戻す、またはバインド解除する

バインドされたインスタンスを、SQL Server セットアップによって確立された Python および R コンポーネントの初期インストールに復元できます。 SQL Server サービスに戻すには、3つの部分があります。

+ [ステップ 1:Microsoft Machine Learning Server からのバインド解除](#step-1-unbind)
+ [手順 2:インスタンスを元の状態に復元する](#step-2-restore)
+ [ステップ 3:インストールに追加したパッケージを再インストールする](#step-3-reinstall-packages)

<a name="step-1-unbind"></a> 

### <a name="step-1-unbind"></a>手順 1:バインドの解除

バインドをロールバックするには、2 つのオプションがあります。セットアップを再実行するか、SqlBindR コマンド ライン ユーティリティを使用します。

#### <a name="unbind-using-setup"></a><a name="bkmk_wizunbind"></a> セットアップを使用してバインドを解除する

1. Machine Learning Server のインストーラーを見つけます。 インストーラーを削除した場合は、もう一度ダウンロードしたり、別のコンピューターからコピーしたりすることが必要になる場合があります。
2. バインドを解除するインスタンスがあるコンピューターで、インストーラーを実行してください。
2. インストーラーによって、バインド解除の候補となるローカル インスタンスが識別されます。
3. 元の構成に戻すインスタンスの横にあるチェックボックスをオフにします。
4. すべてのライセンス契約に同意します。
5. **[完了]** を選択します。 処理には時間がかかります。

#### <a name="unbind-using-the-command-line"></a><a name="bkmk_cmdunbind"></a> コマンド ラインを使用したバインド解除

1. コマンド プロンプトを開き、前のセクションで説明したように **sqlbindr.exe** が含まれているフォルダーに移動します。

2. **SqlBindR.exe** コマンドを実行し、" */unbind*" 引数でインスタンスを指定します。

   次のコマンド ラインは既定のインスタンスを元に戻します。
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

<a name="step-2-restore"></a> 

###  <a name="step-2-repair-the-sql-server-instance"></a>手順 2:SQL Server のインスタンスを修復する

SQL Server セットアップを実行して、Python および R の機能を備えたデータベース エンジンのインスタンスを修復します。 既存の更新プログラムは保持されます。 次の手順は、Python および R パッケージに対するサービス更新プログラムの更新が実行されなかった場合に適用されます。

代替ソリューション:データベース エンジンのインスタンスを完全にアンインストールしてから再インストールし、すべてのサービス更新プログラムを適用します。

<a name="step-3-reinstall-packages"></a> 

### <a name="step-3-add-any-third-party-packages"></a>手順 3:サードパーティ製のパッケージを追加する

パッケージ ライブラリに、他のオープンソースまたはサードパーティのパッケージを追加している場合もあるでしょう。 バインドを逆にすると、既定のパッケージ ライブラリの保存先が切り替わります。そのため、現在 Python および R で使用されているライブラリにパッケージを再インストールする必要があります。 詳細については、「[R パッケージ情報](../package-management/r-package-information.md)」と「[インストール](../package-management/install-additional-r-packages-on-sql-server.md)」、および「[Python パッケージ情報](../package-management/python-package-information.md)および[インストール](../package-management/install-additional-python-packages-on-sql-server.md)」を参照してください。

## <a name="sqlbindrexe-command-syntax"></a>sqlbindr.exe コマンドの構文

### <a name="usage"></a>使用法

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>パラメーター

|名前|説明|
|------|------|
|*list*| 現在のコンピューター上にあるすべての SQL Server インスタンスの ID を一覧表示します|
|*bind*| 指定した SQL Server インスタンスを R Server の最新バージョンにアップグレードし、インスタンスが R Server の今後のアップグレードを自動的に取得するようにします|
|*unbind*|指定した SQL Server インスタンスから R Server の最新バージョンをアンインストールし、R Server の今後のアップグレードがインスタンスに影響を与えないようにします|

<a name="sqlbindr-error-codes"><a/>

## <a name="binding-errors"></a>バインド エラー

Machine Learning Server のインストーラーと SqlBindR の両方で、次のエラー コードとメッセージが返されます。

|エラー コード  | Message           | 詳細               |
|------------|-------------------|-----------------------|
|バインド エラー 0 | Ok (成功) | バインドがエラーなしで渡されました。 |
|バインド エラー 1 | 引数が無効です | 構文エラー。 |
|バインド エラー 2 | 無効なアクション | 構文エラー。 |
|バインド エラー 3 | 無効なインスタンス | インスタンスは存在しますが、バインドには無効です。 |
|バインド エラー 4 | バインドできません | |
|バインド エラー 5 | 既にバインドされています | *bind* コマンドを実行しましたが、指定したインスタンスは既にバインドされています。 |
|バインド エラー 6 | バインドに失敗しました | インスタンスのバインド解除中にエラーが発生しました。 このエラーは、機能を選択せずに Machine Learning Server のインストーラーを実行した場合に発生する可能性があります。 インスタンスが SQL Server 2017 であると仮定した場合、バインドでは、MSSQL インスタンスと Python および R の両方を選択する必要があります。 このエラーは、SqlBindR がプログラム ファイル フォルダーに書き込むことができなかった場合にも発生します。 オープン セッションまたは SQL Server のハンドルによって、このエラーが発生します。 このエラーが発生した場合は、新しいセッションを開始する前に、コンピューターを再起動し、バインドの手順をやり直してください。|
|バインド エラー 7 | バインドされていません | データベース エンジンのインスタンスには、R Services または SQL Server Machine Learning Services があります。 インスタンスは Microsoft Machine Learning Server にバインドされていません。 |
|バインド エラー 8 | バインド解除の失敗 | インスタンスのバインド解除中にエラーが発生しました。 |
|バインド エラー 9 | No instances found (インスタンスが見つかりませんでした) | このコンピューターにはデータベース エンジンのインスタンスが見つかりませんでした。 |

## <a name="known-issues"></a>既知の問題

ここでは、SqlBindR.exe のユーティリティ使用に関する固有の問題、または Machine Learning Server のアップグレード時に SQL Server のインスタンスに影響する可能性があるものについて説明します。

### <a name="restoring-packages-that-were-previously-installed"></a>以前にインストールされたパッケージの復元

Microsoft R Server 9.0.1 にアップグレードすると、SqlBindR.exe による元のパッケージまたは R コンポーネントの復元が失敗します。 インスタンスに対して SQL Server の修復を使用し、すべてのサービス リリースを適用してください。 インスタンスを再起動してください。

新しいバージョンの SqlBindR では、元の R 機能が自動的に復元されるため、R コンポーネントを再インストールしたり、サーバーに再び修正プログラムを適用したりする必要がなくなります。 ただし、初期インストール後に追加された可能性のある R パッケージの更新プログラムをインストールする必要があります。

R コマンドを使い、データベース内のレコードを使用して、インストールされているパッケージをファイル システムに同期します。 詳細については、「[SQL Server の R パッケージ管理](../package-management/install-additional-r-packages-on-sql-server.md)」を参照してください。

### <a name="problems-with-overwritten-sqlbinrini-file-in-sql-server"></a>SQL Server での sqlbinr.ini ファイルの上書きに関する問題

シナリオ:この問題は Machine Learning Server 9.4.7 を SQL Server 2017 にバインドした場合に発生します。  Python が更新され、バインドされた場合、またはお客様が新しい CU に更新した場合、Python がバインドされていることは認識されず、ファイルが上書きされます。 R に関する既知の問題はありません。

回避策として、PYTHON_SERVICES ディレクトリに空ではない `sqlbindr.ini` ファイルを作成します。 その内容がファイルの機能に影響を与えることはありません。

**9.4.7.82** を含む `sqlbindr.ini` ファイルを作成し、次の場所に保存します。  

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>SQL Server からの複数のアップグレードに関する問題

シナリオ:以前に 9.0.1 にアップグレードされた SQL Server 2016 R Services のインスタンス。 Microsoft R Server 9.1.0 の新しいインストーラーを実行しました。 インストーラーによって、すべての有効なインスタンスの一覧が表示されます。
既定では、インストーラーによって以前にバインドされたインスタンスが選択されます。 続行すると、バインド済みのインスタンスはバインド解除されます。 結果として、以前の 9.0.1 インストールと関連するパッケージは削除されますが、新しいバージョンの Microsoft R Server (9.1.0) はインストールされません。

この回避策として、既存の Microsoft R Server のインストールを次のように変更できます。
1. [コントロール] パネルで **[プログラムの追加と削除]** を開きます。
2. Microsoft R Server を見つけて、 **[変更]** を選択します。
3. インストーラーが開始されたら、9.1.0 にバインドするインスタンスを選択します。

Microsoft Machine Learning Server 9.2.1 と 9.3 ではこの問題は発生しません。

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>バインドまたはバインド解除によって、複数の一時フォルダーが残される

インストールの完了後に、一時フォルダーを削除してください。

> [!NOTE]
> インストールが完了するまでお待ちください。 1 つのバージョンに関連付けられている R ライブラリを削除してから、新しい R ライブラリを追加するには、長い時間がかかることがあります。 操作が完了すると、一時フォルダーが削除されます。

## <a name="see-also"></a>関連項目

+ [既定の R または Python 言語ランタイム バージョンを変更する](./change-default-language-runtime-version.md)
+ [Windows 用 Machine Learning Server のインストール (インターネット接続あり)](/machine-learning-server/install/machine-learning-server-windows-install)
+ [Windows 用 Machine Learning Server のインストール (オフライン)](/machine-learning-server/install/machine-learning-server-windows-offline)
+ [Machine Learning Server の既知の問題](/machine-learning-server/resources-known-issues)
+ [以前にリリースされた Microsoft R Server の機能に関するお知らせ](/r-server/whats-new-in-r-server)
+ [機能の非推奨、サポート終了、または変更](/machine-learning-server/resources-deprecated-features)