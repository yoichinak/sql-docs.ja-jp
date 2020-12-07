---
title: R カスタム ランタイムをインストールする
description: SQL Server 用の R カスタム ランタイムをインストールする方法について説明します。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 09/20/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2b058fe7aa723eddcdcf97158d19a053bf2b062b
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870053"
---
# <a name="install-an-r-custom-runtime-for-sql-server"></a>SQL Server 用の R カスタム ランタイムをインストールする

[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

この記事では、SQL Server で R スクリプトを実行するためのカスタム ランタイムをインストールする方法について説明します。 カスタム ランタイムによって、外部コードを実行するための機能拡張フレームワーク上に構築された言語拡張テクノロジが使用されます。 R 用のカスタム ランタイムは、次のシナリオで使用できます。

+ 機能拡張フレームワークを使用する SQL Server のインストール。

+ SQL Server 2019 での Machine Learning Services のインストール。 いくつかの追加構成手順を完了した後、言語拡張機能を [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) で使用できます。

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

> [!NOTE]
> この記事では、Windows に R 用のカスタム ランタイムをインストールする方法について説明します。 Linux にインストールするには、[SQL Server on Linux 用の R カスタム ランタイムのインストール](custom-runtime-r.md?view=sql-server-linux-ver15&preserve-view=true)に関するページを参照してください

## <a name="pre-install-checklist"></a>インストール前のチェックリスト

R カスタム ランタイムをインストールする前に、次のものをインストールします。

+ [Windows 用 SQL Server 2019 (累積的な更新プログラム 3 以降)](../../database-engine/install-windows/install-sql-server.md)。

+ [機能拡張フレームワークのある Windows への SQL Server 言語拡張機能](../../language-extensions/install/windows-java.md)。

+ [R バージョン 3.3 以降](https://cran.r-project.org/)。

## <a name="add-sql-server-language-extensions-for-windows"></a>Windows 用の SQL Server 言語拡張機能を追加する

> [!NOTE]
> SQL Server 2019 に Machine Learning Services がインストールされている場合は、Launchpad サービスを含む言語拡張機能用の機能拡張フレームワークが既にインストールされているため、この手順は省略できます。

言語拡張機能では、外部コードの実行に機能拡張フレームワークが使用されます。 コードの実行はコア エンジン プロセスから分離されていますが、SQL Server のクエリ実行と完全に統合されています。

1. SQL Server 2019 のセットアップ ウィザードを開始します。

1. **[インストール]** タブで、 **[SQL Server の新規スタンドアロン インストールを実行するか、既存のインストールに機能を追加します]** を選択します。

    ![SQL Server 2019 インストール CU3 以降](../install/media/2019setup-installation-page-mlsvcs.png)

1. **[機能の選択]** ページで、次のオプションを選択します。

    - **データベース エンジン サービス**

        SQL Server で言語拡張を使用するには、データベース エンジンのインスタンスをインストールする必要があります。 既定のインスタンスまたは名前付きインスタンスを使用できます。

    - **Machine Learning Services および言語の拡張**

       **[Machine Learning Services および言語の拡張]** を選択します。 R を選択する必要はありません。

    ![SQL Server 2019 CU3 以降のインストール機能](../install/media/sql-feature-selection.png)

1. **[インストールの準備完了]** ページで、以下が選択されていることを確認した後、 **[インストール]** を選択します。

    + データベース エンジン サービス
    + Machine Learning Services および言語の拡張

1. セットアップが完了し、コンピューターの再起動を求めるメッセージが表示されたら、再起動してください。 セットアップが完了した時点で、インストール ウィザードによるメッセージを確認することが重要です。 詳細については、「 [SQL Server セットアップ ログ ファイルの表示と読み取り](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)」を参照してください。

## <a name="install-r"></a>R のインストール

> [!NOTE]
>SQL Machine Learning Services の場合、R は、SQL Server インスタンスの **R_SERVICES** フォルダーに既にインストールされています。 たとえば、"C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\R_SERVICES" などです。 このパスを R_HOME として引き続き使用する場合は、次の手順にスキップして Rcpp をインストールしてください。 それ以外で、R の別のランタイムを使用する場合は、引き続きそれをインストールします。

[R (3.3 以降)](https://cran.r-project.org/bin/windows/base/) をインストールし、インストールされているパスを記録しておきます。 このパスは **R_HOME** です。 たとえば、ここで示すように、R_HOME は "C:\Program Files\R\R-4.0.2" です

![カスタム R をインストールする](../install/media/custom-r-installation.png)

> [!NOTE]
>次の手順で、%R_HOME% は R のインストールへのパスであり、実際の値に置き換える必要があります。

## <a name="install-rcpp-package"></a>Rcpp パッケージをインストールする

+ %R_HOME%\bin で R の実行可能ファイルを見つけます。 既定では、`C:\Program Files\R\R-4.0.2\bin` にあります。

+ "*管理者特権*" のコマンド プロンプトから、R を開始します。

```CMD
%R_HOME%\bin\R.exe
```

この "*管理者特権*" の R プロンプト (%R_HOME%\bin\R.exe) で、次のスクリプトを実行して、Rcpp パッケージを %R_HOME%\library フォルダーにインストールします。

```R
install.packages("Rcpp", lib="%R_HOME%/library");
```

## <a name="update-the-system-environment-variables"></a>システム環境変数を更新する

1. システム環境変数として **R_HOME** を追加または変更します。
    + Windows の検索ボックスに「環境」と入力し、 **[Edit the system environment variables]\(システム環境変数の編集\)** を選択します。
    + **[詳細設定]** タブの **[環境変数]** を選択します。

    + **[システム変数]** で **[新規]** を選択して、R_HOME を作成します。
    変更するには、 **[編集]** を選択して変更します。 その値を変更して、カスタム R インストールのパスを指定します。

    ![R_HOME システム環境変数を作成します。](../install/media/sys-env-r-home.png)

2. **PATH** 環境変数を更新します。
    **R.dll** へのパスを、システム環境変数 **PATH** に追加します。 **PATH** を選択してから **[編集]** を選択して、パスの一覧に `%R_HOME%\bin\x64` を追加します。

    ![PATH システム環境変数に追加します。](../install/media/sys-env-path-r.png)

3. **[OK]** を選択して、残りのウィンドウを閉じます。

    別の方法として、"*管理者特権*" のコマンド プロンプトからこれらの環境変数を設定するには、次のコマンドを実行します。 必ずカスタム R インストールのパスを使用してください。

```CMD
setx /m R_HOME "path\to\installation\of\R"
setx /m PATH "path\to\installation\of\R\bin\x64;%PATH%"
```

## <a name="grant-access-to-the-custom-r-installation-folder"></a>カスタム R インストール フォルダーへのアクセスを許可する

> [!NOTE]
>既定の場所である **C:\Program Files\R\R-version** に R をインストールした場合は、この手順を省略できます。

新しい "*管理者特権*" のコマンド プロンプトから **icacls** コマンドを実行して、READ および EXECUTE のアクセス権を、**SQL Server Launchpad サービスのユーザー名** と SID **S-1-15-2-1** (**すべてのアプリケーション パッケージ**) に付与します。 Launchpad サービスのユーザー名は、`NT Service\MSSQLLAUNCHPAD$INSTANCENAME` という形式です。`INSTANCENAME` は、SQL Server のインスタンス名です。

そのコマンドでは、指定したディレクトリ パスの下にあるすべてのファイルとフォルダーへのアクセス権が再帰的に許可されます。

インスタンス名を `MSSQLLAUNCHPAD` に追加します (`MSSQLLAUNCHPAD$INSTANCENAME`)。 この例では、`INSTANCENAME` は既定のインスタンス `MSSQLSERVER` です。

1. **SQL Server Launchpad サービスのユーザー名** にアクセス許可を付与します

    ```cmd
    icacls "%R_HOME%" /grant "NT Service\MSSQLLAUNCHPAD$MSSQLSERVER":(OI)(CI)RX /T
    ```
2. **SID S-1-15-2-1** にアクセス許可を付与します

    ```cmd
    icacls "%R_HOME%" /grant *S-1-15-2-1:(OI)(CI)RX /T

>[!NOTE]
>The preceding command grants permissions to the computer **SID S-1-15-2-1**, which is equivalent to ALL APPLICATION PACKAGES on an English version of Windows. Alternatively, you can use `icacls "%R_HOME%" /grant "ALL APPLICATION PACKAGES":(OI)(CI)RX /T` on an English version of Windows.

## Restart SQL Server Launchpad service

From an *elevated* command prompt, run the following commands. Replace "MSSQLSERVER" with the name of your SQL Server instance.


```CMD
net stop MSSQLLAUNCHPAD$MSSQLSERVER
net start MSSQLLAUNCHPAD$MSSQLSERVER
```

別の方法として、システムの **[サービス]** アプリで SQL Server Launchpad サービスを右クリックし、 **[再起動]** コマンドを選択します。 または、[SQL Server 構成マネージャー](../../relational-databases/sql-server-configuration-manager.md)を使用して、サービスを再起動します。

## <a name="download-r-language-extension"></a>R 言語拡張機能をダウンロードする

[Windows 用 R 言語拡張機能が含まれている zip ファイル](https://github.com/microsoft/sql-server-language-extensions/releases)をダウンロードします。 運用環境ではリリース バージョンを使用することをお勧めします。 開発またはテストではデバッグ バージョンを使用します。エラーを調査するための詳細なログ情報が提供されるためです。

## <a name="register-external-language"></a>外部言語を登録する

拡張機能を使用するデータベースごとに、[CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md) でこの R 言語拡張機能を登録します。 [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download-azure-data-studio) を使用して SQL Server に接続し、次の T-SQL コマンドを実行します。
このステートメントのパスを変更して、ダウンロードした言語拡張機能の zip ファイル (R-lang-extension.zip) の場所を反映します。

> [!NOTE]
>**R** は予約語です。 外部言語には別の名前を使用します (たとえば "myR")。

```sql
CREATE EXTERNAL LANGUAGE [myR]
FROM (CONTENT = N'/path/to/R-lang-extension.zip', FILE_NAME = 'libRExtension.dll');
GO
```

::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

SQL Server は、Red Hat Enterprise Linux (RHEL)、SUSE Linux Enterprise Server (SLES)、および Ubuntu にインストールできます。 詳細については、[「SQL Server on Linux のインストール ガイド」の「サポートされているプラットフォーム」](../../linux/sql-server-linux-setup.md#supportedplatforms)を参照してください。

> [!NOTE]
> この記事では、Linux に R 用のカスタム ランタイムをインストールする方法について説明します。 Windows にインストールするには、[SQL Server on Windows 用 R カスタムのインストール](custom-runtime-r.md?view=sql-server-ver15&preserve-view=true)に関するページを参照してください

## <a name="pre-install-checklist"></a>インストール前のチェックリスト

R カスタム ランタイムをインストールする前に、次のものをインストールします。

+ [Linux 用 SQL Server 2019 (累積的な更新プログラム 3 以降)](../../linux/sql-server-linux-setup.md)。
SQL Server on Linux をインストールする前に、Microsoft リポジトリを構成する必要があります。 詳細については、[リポジトリの構成](../../linux/sql-server-linux-change-repo.md)に関するページを参照してください。

+ [機能拡張フレームワークのある Linux への SQL Server 言語拡張機能](../../linux/sql-server-linux-setup-language-extensions-java.md)。

+ [R バージョン 3.3 以降](https://cran.r-project.org/)。

## <a name="add-sql-server-language-extensions-for-linux"></a>Linux 用の SQL Server 言語拡張機能を追加する

> [!NOTE]
> SQL Server 2019 に Machine Learning Services がインストールされている場合は、言語拡張機能用の **mssql-server-extensibility** パッケージが既にインストールされているため、この手順は省略できます。

言語拡張機能では、外部コードの実行に機能拡張フレームワークが使用されます。 コードの実行はコア エンジン プロセスから分離されていますが、SQL Server のクエリ実行と完全に統合されています。

Linux のバージョンに応じて、次のコマンドを使用して言語拡張機能をインストールします。

### <a name="ubuntu"></a>Ubuntu
> [!Tip]
> 可能であれば、`sudo apt-get update` を使用して、インストールの前にシステム上のパッケージを更新しておきます。 Ubuntu には、https apt transport オプションがない可能性があります。 インストールするには、`sudo apt-get install apt-transport-https` を使用します。

```bash
# Install as root or sudo
sudo apt-get install mssql-server-extensibility
```

### <a name="red-hat"></a>Red Hat
```bash
# Install as root or sudo
sudo yum install mssql-server-extensibility
```

### <a name="suse"></a>Suse
```bash
# Install as root or sudo
sudo zypper install mssql-server-extensibility
```

## <a name="install-r"></a>R のインストール

>[!NOTE]
>SQL Machine Learning Services の場合、R は `/opt/microsoft/ropen/3.5.2/lib64/R` に既にインストールされています。 このパスを R_HOME として引き続き使用する場合は、次の手順にスキップして **Rcpp をインストール** してください。 

R の別のランタイムを使用する場合は、新しいバージョンのインストールを続ける前に、まず `microsoft-r-open-mro` を削除する必要があります。 Ubuntu の例:

```bash
sudo apt remove microsoft-r-open-mro-3.5.2
```

[手順](https://cran.r-project.org/bin/linux/)に従って、それぞれの Linux プラットフォームに対する R (3.3 以降) のインストールを完了します。 既定では、R は **/usr/lib/R** にインストールされます。 このパスは **R_HOME** です。 R を別の場所にインストールする場合は、R_HOME としてそのパスを記録しておきます。

Ubuntu の手順例。 お使いの R のバージョンに応じて、次のリポジトリの URL を変更します。

```bash
export DEBIAN_FRONTEND=noninteractive
sudo apt-get update
sudo apt-get --no-install-recommends -y install curl zip unzip apt-transport-https libstdc++6

# Add R CRAN repository. This repository works for R 4.0.x.
#
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
sudo add-apt-repository 'deb https://cloud.r-project.org/bin/linux/ubuntu xenial-cran40/'
sudo apt-get update

# Install R runtime.
#
sudo apt-get -y install r-base-core
```

## <a name="install-rcpp-package"></a>Rcpp パッケージをインストールする

次の手順で、${R_HOME} は R のインストールへのパスです。 

+ ${R_HOME}/bin で R のバイナリを見つけます。 既定では、 **/usr/lib/R/bin** にあります。

+ R を開始する

  ```bash
  sudo ${R_HOME}/bin/R
  ```

+ この "*管理者特権*" の R プロンプト (${R_HOME}/bin/R) で、次のスクリプトを実行して、**Rcpp** パッケージを ${R_HOME}/library フォルダーにインストールします。

  ```R
  install.packages("Rcpp", lib = "${R_HOME}/library");
  ```

## <a name="using-a-custom-installation-of-r"></a>R のカスタム インストールを使用する

> [!NOTE]
>R を既定の場所である **/usr/lib/R** にインストールした場合は、このセクションを省略できます。

### <a name="update-the-environment-variables"></a>環境変数を更新する

1. mssql-launchpadd サービスを編集して、R_HOME 環境変数を `/etc/systemd/system/mssql-launchpadd.service.d/override.conf` ファイルに追加します

    ```bash
    sudo systemctl edit mssql-launchpadd
    ```

    + 開かれた `/etc/systemd/system/mssql-launchpadd.service.d/override.conf` ファイルに、次のテキストを挿入します。 R_HOME の値を、カスタム R のインストール パスに設定します。

    ```text
    [Service]
    Environment="R_HOME=/path/to/installation/of/R"
    ```

    + 保存して閉じます。

2. **libR.so** を読み込めることを確認します。

    + **/etc/ld.so.conf.d** にカスタム custom-r.conf ファイルを作成します。

    ```bash
    sudo vi /etc/ld.so.conf.d/custom-r.conf
    ```

    + 開かれたファイルで、カスタム R のインストールから **libR.so** へのパスを追加します。

    ```vi editor
    /path/to/installation/of/R/lib
    ```

    + 新しいファイルを保存して閉じます。

    + `ldconfig` を実行し、次のコマンドを実行することで **libR.so** を読み込めることを確認し、すべての依存ライブラリが見つかることを確認します。

    ```bash
    sudo ldconfig
    ldd /path/to/installation/of/R/lib/libR.so
    ```

### <a name="grant-access-to-the-custom-r-installation-folder"></a>カスタム R インストール フォルダーへのアクセスを許可する

/var/opt/mssql/mssql.conf ファイルの extensibility セクションにある `datadirectories` オプションを、カスタム R のインストールに設定します。

```bash
sudo /opt/mssql/bin/mssql-conf set extensibility.datadirectories /path/to/installation/of/R
```

### <a name="restart-mssql-launchpadd-service"></a>mssql-launchpadd サービスを再起動する

> [!NOTE]
>R を既定の場所である **/usr/lib/R** にインストールした場合は、この手順を省略できます。

```bash
sudo systemctl restart mssql-launchpadd
```

## <a name="download-r-language-extension"></a>R 言語拡張機能をダウンロードする

[Linux 用 R 言語拡張機能が含まれている zip ファイル](https://github.com/microsoft/sql-server-language-extensions/releases)をダウンロードします。 運用環境ではリリース バージョンを使用することをお勧めします。 開発またはテストではデバッグ バージョンを使用します。エラーを調査するための詳細なログ情報が提供されるためです。

## <a name="register-external-language"></a>外部言語を登録する

拡張機能を使用するデータベースごとに、[CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md) でこの R 言語拡張機能を登録します。 [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download-azure-data-studio) を使用して SQL Server に接続し、次の T-SQL コマンドを実行します。 
このステートメントのパスを変更して、ダウンロードした言語拡張機能の zip ファイル (r-lang-extension.zip) の場所を反映します。


> [!NOTE]
>**R** は予約語です。 外部言語には別の名前を使用します (たとえば "myR")。

```sql
CREATE EXTERNAL LANGUAGE [myR]
FROM (CONTENT = N'/path/to/R-lang-extension.zip', FILE_NAME = 'libRExtension.so.1.0');
GO
```

::: moniker-end

## <a name="enable-external-script-execution-in-sql-server"></a>SQL Server で外部スクリプトの実行を有効にする

R の外部スクリプトは、ストアド プロシージャ [sp_execute_external スクリプト](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)を SQL Server に対して実行することによって実行できます。 

外部スクリプトを有効にするには、SQL Server に接続されている [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download-azure-data-studio) を使用して、次の SQL コマンドを実行します。

```sql
sp_configure 'external scripts enabled', 1;
RECONFIGURE WITH OVERRIDE;
```

## <a name="verify-language-extension-installation"></a>言語拡張機能のインストールを確認する

この SQL スクリプトを使用して、カスタム R 言語拡張機能が正常にインストールされたことを確認します。 このスクリプトの出力では、R_HOME、R へのパス、およびカスタム R ランタイムのバージョンが表示されます。 スクリプトでカスタム ランタイムが使用されていることを確認します。

```sql
EXEC sp_execute_external_script
    @language =N'myR',
    @script=N'
print(R.home());
print(file.path(R.home("bin"), "R"));
print(R.version);
print("Hello RExtension!");'
```

## <a name="verify-parameters-and-datasets-of-different-data-types"></a>さまざまなデータ型のパラメーターとデータセットを検証する

このスクリプトを使用して、入力と出力のパラメーターおよびデータセットのさまざまなデータ型をテストします。

```sql
DECLARE @sumVal INT = 12;
DECLARE @charVal VARCHAR(30) = N'Hello';
EXEC sp_execute_external_script
    @language =N'myR',
    @script=N'
print(sumVal);
print(charVal);
sumVal <- sumVal + 300;
OutputDataSet <- InputDataSet;'
    ,@input_data_1 = N'select 1, cast(1.4 as real), ''Hi'', cast(''1'' as bit)'
    ,@params = N'@sumVal int OUTPUT, @charVal VARCHAR(30)'
    ,@sumVal = @sumVal OUTPUT
    ,@charVal =  @charVal
WITH RESULT SETS ((intCol INT, doubleCol REAL, charCol CHAR(2), logicalCol BIT));
PRINT @sumVal;
```

## <a name="see-also"></a>関連項目

+ [SQL Server の機能拡張フレームワーク](../concepts/extensibility-framework.md)
+ [言語拡張機能の概要](../../language-extensions/language-extensions-overview.md)