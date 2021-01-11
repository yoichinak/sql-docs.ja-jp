---
title: Python カスタム ランタイムをインストールする
description: 言語拡張機能を使用して SQL Server 用の Python カスタム ランタイムをインストールする方法について説明します。 Python カスタム ランタイムは機械学習に使用できます。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/30/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
zone_pivot_groups: python-custom-runtime-platform
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15'
ms.openlocfilehash: 91aace4333b4496338b782344e64cdfea2b886bd
ms.sourcegitcommit: 5b2c47ce88f7e56552fd415c32b319009d043b56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/29/2020
ms.locfileid: "97804332"
---
# <a name="install-a-python-custom-runtime-for-sql-server"></a>SQL Server 用の Python カスタム ランタイムをインストールする
[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

この記事では、SQL Server で外部 Python スクリプトを実行するための Python カスタム ランタイムをインストールする方法について説明します。 このカスタム ランタイムは、[SQL Server 言語拡張機能](../../language-extensions/language-extensions-overview.md)を使用するもので、機械学習スクリプトの実行に使用できます。

Python カスタム ランタイムを使用すると、[SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) と共にインストールされる既定のランタイム バージョンではなく、独自のバージョンの Python ランタイムを SQL Server と共に使用することができます。

::: zone pivot="python-custom-runtime-windows"

## <a name="prerequisites"></a>前提条件

Python カスタム ランタイムをインストールする前に、次のものをインストールします。

+ SQL Server 2019 の[累積的な更新プログラム (CU) 3 以降](../../database-engine/install-windows/latest-updates-for-microsoft-sql-server.md)をインストールします。

+ [Python 3.7](https://www.python.org/downloads/) をサーバーにインストールします。

    カスタム Python ランタイムに使用される Python 言語拡張機能は、現在、Python 3.7 のみをサポートしています。 別のバージョンの Python を使用する場合は、[Python 言語拡張機能の GitHub リポジトリ](https://github.com/microsoft/sql-server-language-extensions/tree/master/language-extensions/python)の指示に従って、拡張機能を変更し、再構築してください。

    > [!IMPORTANT]
    > Python のインストール時には、 **[Add Python 3.7 to PATH]\(Python 3.7 を PATH に追加\)** をオンにしてください。

## <a name="install-language-extensions"></a>言語拡張をインストールする

> [!NOTE]
> SQL Server 2019 に [Machine Learning Services](../sql-server-machine-learning-services.md) がインストールされている場合は、言語拡張機能が既にインストールされているため、この手順は省略できます。

[SQL Server 言語拡張機能](../../language-extensions/language-extensions-overview.md) (Python カスタム ランタイムに使用されるもの) をインストールするには、次の手順に従います。

1. SQL Server 2019 のセットアップ ウィザードを開始します。
  
1. **[インストール]** タブで、 **[SQL Server の新規スタンドアロン インストールを実行するか、既存のインストールに機能を追加します]** を選択します。

1. **[機能の選択]** ページで、次のオプションを選択します。
  
    + **データベース エンジン サービス**
  
        SQL Server で言語拡張を使用するには、データベース エンジンのインスタンスをインストールする必要があります。 新規または既存のインスタンスのいずれかを使用できます。
  
    + **Machine Learning Services および言語の拡張**

        **[Machine Learning Services および言語の拡張]** を選択します。 後でカスタム Python ランタイムをインストールするので、Python は選択しないでください。

        :::image type="content" source="media/2019-setup-language-extensions.png" alt-text="SQL Server 2019 言語拡張機能のセットアップ。":::

1. **[インストールの準備完了]** ページで、以下が選択されていることを確認した後、 **[インストール]** を選択します。
  
    + データベース エンジン サービス
    + Machine Learning Services および言語の拡張

1. セットアップが完了した後、確認のメッセージが表示されたらコンピューターを再起動します。

> [!IMPORTANT]
> 言語拡張機能を使用して SQL Server 2019 の新規インスタンスをインストールする場合は、次の手順に進む前に、[累積的な更新プログラム (CU) 3 以降](../../database-engine/install-windows/latest-updates-for-microsoft-sql-server.md)をインストールしてください。

## <a name="install-pandas"></a>pandas をインストールする

"*管理者特権*" でのコマンド プロンプトから、Python 用 [pandas](https://pandas.pydata.org/) パッケージをインストールします。

```bash
python.exe -m pip install pandas
```

## <a name="add-environment-variable"></a>環境変数を追加する

システム環境変数 **PYTHONHOME** を追加または変更します。

1. Windows の検索ボックスに「*環境*」と入力し、 **[Edit the system environment variables]\(システム環境変数の編集\)** を選択します。
1. **[詳細設定]** タブの **[環境変数]** を選択します。
1. **[システム変数]** で **[新規]** を選択し、Python 3.7 のインストール場所を指す **PYTHONHOME** を作成します。 PYTHONHOME が既に存在する場合は、 **[編集]** を選択し、Python 3.7 のインストール場所を指定します。
1. **[OK]** をクリックして、すべてのウィンドウを閉じます。

    :::image type="content" source="media/pythonhome-env-variable.png" alt-text="PYTHON HOME 環境変数。":::

## <a name="grant-access-to-python-folder"></a>Python フォルダーへのアクセスを許可する

新しい "*管理者特権*" でのコマンド プロンプトから次の **icacls** コマンドを実行して、**PYTHONHOME** に対する **READ および EXECUTE** のアクセス権を、**SQL Server Launchpad サービス** と SID **S-1-15-2-1** (**ALL_APPLICATION_PACKAGES**) に付与します。

1. **SQL Server Launchpad サービスのユーザー名** にアクセス許可を付与します。

    ```cmd
    icacls "%PYTHONHOME%" /grant "NT Service\MSSQLLAUNCHPAD":(OI)(CI)RX /T
    ```

    名前付きインスタンスの場合、**SQL01** というインスタンスに対するコマンドは `icacls "%PYTHONHOME%" /grant "NT Service\MSSQLLAUNCHPAD$SQL01":(OI)(CI)RX /T` になります。

2. **SID S-1-15-2-1** にアクセス許可を付与します。

    ```cmd
    icacls "%PYTHONHOME%" /grant *S-1-15-2-1:(OI)(CI)RX /T
    ```

    上記のコマンドを実行すると、コンピューター SID **S-1-15-2-1** にアクセス許可が付与されます。これは、英語版の Windows における **ALL APPLICATION PACKAGES** と同等です。 または、英語版の Windows で `icacls "%R_HOME%" /grant "ALL APPLICATION PACKAGES":(OI)(CI)RX /T` を使用することもできます。

## <a name="restart-sql-server-launchpad"></a>SQL Server Launchpad を再起動する

SQL Server Launchpad サービスを再起動するには、次の手順に従います。

1. [[SQL Server 構成マネージャー]](../../relational-databases/sql-server-configuration-manager.md) を開きます。

1. **[SQL Server サービス]** で **[SQL Server Launchpad (MSSQLSERVER)]** を右クリックして、 **[再起動]** を選択します。 名前付きインスタンスを使用している場合は、 **(MSSQLSERVER)** の代わりにインスタンス名が表示されます。

## <a name="register-language-extension"></a>言語拡張機能を登録する

Python 言語拡張機能 (Python カスタム ランタイムに使用されるもの) をダウンロードして登録するには、次の手順に従います。

1. [SQL Server 言語拡張機能の GitHub リポジトリ](https://github.com/microsoft/sql-server-language-extensions/releases)から **python-lang-extension-windows.zip** ファイルをダウンロードします。

    開発環境やテスト環境では、デバッグ バージョン (**python-lang-extension-windows-debug.zip**) を使用することもできます。 デバッグ バージョンでは、エラーを調査するための詳細なログ情報が提供されます。これは運用環境では推奨されません。

1. [Azure Data Studio](../../azure-data-studio/what-is-azure-data-studio.md) を使用して SQL Server インスタンスに接続し、次の T-SQL コマンドを実行して、Python 言語拡張機能を [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md) に登録します。 

    このステートメントのパスを変更して、ダウンロードした言語拡張機能の zip ファイル (**python-lang-extension-windows.zip**) の場所を反映します。

    ```sql
    CREATE EXTERNAL LANGUAGE [myPython]
    FROM (CONTENT = N'/path/to/python-lang-extension-windows.zip', FILE_NAME = 'pythonextension.dll');
    GO
    ```

    Python 言語拡張機能を使用するデータベースごとに、このステートメントを実行します。

    > [!NOTE]
    > **Python** は予約語であり、新しい外部言語の名前として使用することはできません。 別の名前を使用してください。 たとえば、上記のステートメントでは **myPython** が使用されています。

::: zone-end

::: zone pivot="python-custom-runtime-linux"

## <a name="prerequisites"></a>前提条件

Python カスタム ランタイムをインストールする前に、次のものをインストールします。

+ Linux 用 SQL Server 2019 をインストールします。 SQL Server は、Red Hat Enterprise Linux (RHEL)、SUSE Linux Enterprise Server (SLES)、および Ubuntu にインストールできます。 詳細については、[SQL Server on Linux のインストール ガイダンス](../../linux/sql-server-linux-setup.md)を参照してください。

+ SQL Server 2019 の累積的な更新プログラム (CU) 3 以降にアップグレードします。 次の手順に従います。
    1. 累積的な更新プログラムのリポジトリを構成します。 詳細については、「[SQL Server on Linux のインストールとアップグレードを行うためのリポジトリを構成する](../../linux/sql-server-linux-change-repo.md)」を参照してください。

    1. **mssql-server** パッケージを、最新の累積更新プログラムに更新します。 詳細については、[「SQL Server on Linux のインストール ガイド」の「SQL Server の更新またはアップグレード」](../../linux/sql-server-linux-setup.md#upgrade)を参照してください。

+ [Python 3.7](https://www.python.org/downloads/) をサーバーにインストールします。

    カスタム Python ランタイムに使用される Python 言語拡張機能は、現在、Python 3.7 のみをサポートしています。 別のバージョンの Python を使用する場合は、[Python 言語拡張機能の GitHub リポジトリ](https://github.com/microsoft/sql-server-language-extensions/tree/master/language-extensions/python)の指示に従って、拡張機能を変更し、再構築してください。

## <a name="install-language-extensions"></a>言語拡張をインストールする

> [!NOTE]
> SQL Server 2019 に [Machine Learning Services](../sql-server-machine-learning-services.md) がインストールされている場合は、言語拡張機能用の **mssql-server-extensibility** パッケージが既にインストールされているため、この手順は省略できます。

[SQL Server 言語拡張機能](../../language-extensions/language-extensions-overview.md) (Python カスタム ランタイムに使用されるもの) を Linux にインストールするには、以下のコマンドに従います。

#### <a name="ubuntu"></a>[Ubuntu](#tab/ubuntu)

1. 可能であれば、次のコマンドを実行して、インストールの前にシステム上のパッケージを更新しておきます。

    ```bash
    # Install as root or sudo
    sudo apt-get update
    ```

1. Ubuntu には、https apt transport オプションがない可能性があります。 これをインストールするには、次のコマンドを実行します。

    ```bash
    # Install as root or sudo
    apt-get install apt-transport-https
    ```

1. 次のコマンドを使用して **mssql-server-extensibility** をインストールします。

    ```bash
    # Install as root or sudo
    sudo apt-get install mssql-server-extensibility
    ```

#### <a name="red-hat-enterprise-linux-rhel"></a>[Red Hat Enterprise Linux (RHEL)](#tab/rhel)

```bash
# Install as root or sudo
sudo yum install mssql-server-extensibility
```

#### <a name="suse-linux-enterprise-server-sles"></a>[SUSE Linux Enterprise Server (SLES)](#tab/sles)

```bash
# Install as root or sudo
sudo zypper install mssql-server-extensibility
```

---

## <a name="install-python-37-and-pandas"></a>Python 3.7 と pandas をインストールする

Python 3.7、libpython3.7 ライブラリ、および pandas パッケージをインストールします。 

Ubuntu のコマンドの例を次に示します。

```bash
# Install python3.7 and the corresponding library:
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt-get update
sudo apt-get install python3.7 python3-pip libpython3.7

# Install pandas to /usr/lib:
sudo python3.7 -m pip install pandas -t /usr/lib/python3.7/dist-packages
```

## <a name="custom-installation-of-python"></a>Python のカスタム インストール

> [!NOTE]
> `/usr/lib/python3.7` の既定の場所に Python 3.7 がインストールされている場合は、このセクションをスキップし、「[言語拡張機能を登録する](#register-language-extension-linux)」セクションに進むことができます。

独自のバージョンの Python 3.7 をビルドした場合は、次のコマンドを使用して、SQL Server にカスタム インストールを把握させます。

### <a name="add-environment-variable"></a>環境変数を追加する

まず、**mssql-launchpadd** サービスを編集して、**PYTHONHOME** 環境変数を `/etc/systemd/system/mssql-launchpadd.service.d/override.conf` ファイルに追加します

1. systemctl を使用してファイルを開きます

    ```bash
    sudo systemctl edit mssql-launchpadd
    ```

1. 開かれた `/etc/systemd/system/mssql-launchpadd.service.d/override.conf` ファイルに、次のテキストを挿入します。 **PYTHONHOME** の値をカスタムの Python インストール パスに設定します。

    ```
    [Service]
    Environment="PYTHONHOME=/path/to/installation/of/python3.7"
    ```

1. ファイルを保存して、エディターを閉じます。

次に、`libpython3.7m.so.1.0` を読み込めることを確認します。

1. `/etc/ld.so.conf.d` 内に custom-python.conf ファイルを作成します。

    ```bash
    sudo vi /etc/ld.so.conf.d/custom-python.conf
    ```

1. 開かれたファイルに、カスタムの Python インストールから **libpython3.7m.so.1.0** へのパスを追加します。

    ```
    /path/to/installation/of/python3.7/lib
    ```

1. 新しいファイルを保存し、エディターを閉じます。

1. `ldconfig` を実行し、次のコマンドを実行することで `libpython3.7m.so.1.0` を読み込めることを確認し、すべての依存ライブラリが見つかることを確認します。

    ```bash
    sudo ldconfig
    ldd /path/to/installation/of/python3.7/lib/libpython3.7m.so.1.0
    ```

### <a name="grant-access-to-python-folder"></a>Python フォルダーへのアクセスを許可する

/var/opt/mssql/mssql.conf ファイルの extensibility セクションにある `datadirectories` オプションを、カスタム Python のインストールに設定します。

```bash
sudo /opt/mssql/bin/mssql-conf set extensibility.datadirectories /path/to/installation/of/python3.7
```

### <a name="restart-mssql-launchpadd"></a>Mssql-launchpadd を再起動する

```bash
sudo systemctl restart mssql-launchpadd
```

<a name="register-language-extension-linux"></a>

## <a name="register-language-extension"></a>言語拡張機能を登録する

Python 言語拡張機能 (Python カスタム ランタイムに使用されるもの) をダウンロードして登録するには、次の手順に従います。

1. [SQL Server 言語拡張機能の GitHub リポジトリ](https://github.com/microsoft/sql-server-language-extensions/releases)から **python-lang-extension-linux.zip** ファイルをダウンロードします。

    開発環境やテスト環境では、デバッグ バージョン (**python-lang-extension-linux-debug.zip**) を使用することもできます。 デバッグ バージョンでは、エラーを調査するための詳細なログ情報が提供されます。これは運用環境では推奨されません。

1. [Azure Data Studio](../../azure-data-studio/what-is-azure-data-studio.md) を使用して SQL Server インスタンスに接続し、次の T-SQL コマンドを実行して、Python 言語拡張機能を [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md) に登録します。 

    このステートメントのパスを変更して、ダウンロードした言語拡張機能の zip ファイル (**python-lang-extension-linux.zip**) の場所を反映します。

    ```sql
    CREATE EXTERNAL LANGUAGE [myPython]
    FROM (CONTENT = N'/path/to/python-lang-extension-linux.zip', FILE_NAME = 'libPythonExtension.so.1.0');
    GO
    ```

    Python 言語拡張機能を使用するデータベースごとに、このステートメントを実行します。

    > [!NOTE]
    > **Python** は予約語であり、新しい外部言語の名前として使用することはできません。 別の名前を使用してください。 たとえば、上記のステートメントでは **myPython** が使用されています。

::: zone-end

## <a name="enable-external-script"></a>外部スクリプトを有効にする

Python 外部スクリプトは、ストアド プロシージャ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) を使用して実行できます。

外部スクリプトを有効にするには、[Azure Data Studio](../../azure-data-studio/what-is-azure-data-studio.md) を使用して次のステートメントを実行します。

```sql
sp_configure 'external scripts enabled', 1;
RECONFIGURE WITH OVERRIDE;  
```

## <a name="verify-installation"></a>インストールの確認

Python カスタム ランタイムのインストールと機能を確認するには、次の SQL スクリプトを使用します。

```sql
EXEC sp_execute_external_script
@language =N'myPython',
@script=N'
import sys
print(sys.path)
print(sys.version)
print(sys.executable)'
```

## <a name="next-steps"></a>次のステップ

+ [SQL Server 用の R カスタム ランタイムをインストールする](custom-runtime-r.md)
+ [SQL Server の機能拡張フレームワーク](../concepts/extensibility-framework.md)
+ [言語拡張機能の概要](../../language-extensions/language-extensions-overview.md)
