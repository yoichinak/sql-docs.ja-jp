---
title: Python カスタム ランタイムをインストールする
description: SQL Server 用の Python カスタム ランタイムをインストールする方法について説明します。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 09/20/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2a37b086804a8fabe3719db0744b49345d69e6b8
ms.sourcegitcommit: 2bf83972036bdbe6a039fb2d1fc7b5f9ca9589d3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/17/2020
ms.locfileid: "94674140"
---
# <a name="install-a-python-custom-runtime-for-sql-server"></a>SQL Server 用の Python カスタム ランタイムをインストールする
[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

この記事では、SQL Server で Python スクリプトを実行するためのカスタム ランタイムをインストールする方法について説明します。 カスタム ランタイムによって、外部コードを実行するための機能拡張フレームワーク上に構築された言語拡張テクノロジが使用されます。 Python 用のカスタム ランタイムは、次のシナリオで使用できます。

+ 機能拡張フレームワークを使用する SQL Server のインストール。

+ SQL Server 2019 での Machine Learning Services のインストール。 いくつかの追加構成手順を完了した後、言語拡張機能を [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) で使用できます。

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

> [!NOTE]
> この記事では、Windows に Python 用のカスタム ランタイムをインストールする方法について説明します。 Linux にインストールするには、[SQL Server on Linux 用の Python カスタム ランタイムのインストール](custom-runtime-python.md?view=sql-server-linux-ver15&preserve-view=true)に関するページを参照してください

## <a name="pre-install-checklist"></a>インストール前のチェックリスト

Python カスタム ランタイムをインストールする前に、次のものをインストールします。

+ [Windows 用の SQL Server 2019 Cumulative Update (CU) 3](../../database-engine/install-windows/install-sql-server.md)。

+ [機能拡張フレームワークのある Windows への SQL Server 言語拡張機能](../../language-extensions/install/windows-java.md)。

+ [Python 3.7]( https://www.python.org/downloads/release/python-379/)。

## <a name="add-sql-server-language-extensions-for-windows"></a>Windows 用の SQL Server 言語拡張機能を追加する

> [!NOTE]
> SQL Server 2019 に Machine Learning Services がインストールされている場合、拡張機能フレームワークは既にインストールされているため、この手順をスキップできます。

言語拡張機能では、外部コードの実行に機能拡張フレームワークが使用されます。 コードの実行はコア エンジン プロセスから分離されていますが、SQL Server のクエリ実行と完全に統合されています。

1. SQL Server 2019 のセットアップ ウィザードを開始します。
  
1. **[インストール]** タブで、 **[SQL Server の新規スタンドアロン インストールを実行するか、既存のインストールに機能を追加します]** を選択します。
    
    ![SQL Server 2019 インストール CU3 以降](../install/media/2019setup-installation-page-mlsvcs.png) 

1. **[機能の選択]** ページで、次のオプションを選択します。
  
    - **データベース エンジン サービス**
  
        SQL Server で言語拡張を使用するには、データベース エンジンのインスタンスをインストールする必要があります。 既定のインスタンスまたは名前付きインスタンスを使用できます。
  
    - **Machine Learning Services および言語の拡張**
   
       **[Machine Learning Services および言語の拡張]** を選択します。 Python を選択する必要はありません。

    ![SQL Server 2019 CU3 以降のインストール機能](../install/media/sql-feature-selection.png) 

1. **[インストールの準備完了]** ページで、以下が選択されていることを確認した後、 **[インストール]** を選択します。
  
    + データベース エンジン サービス
    + Machine Learning Services および言語の拡張

1. セットアップが完了し、コンピューターの再起動を求めるメッセージが表示されたら、再起動してください。 セットアップが完了した時点で、インストール ウィザードによるメッセージを確認することが重要です。 詳細については、「 [SQL Server セットアップ ログ ファイルの表示と読み取り](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)」を参照してください。


## <a name="install-python-37"></a>Python 3.7 をインストールする 

[Python 3.7]( https://www.python.org/downloads/release/python-379/) をインストールし、PATH に追加します。

![Python 3.7 をパスに追加します。](../install/media/python-379.png) 


#### <a name="install-pandas"></a>pandas をインストールする

"*管理者特権*" でのコマンド プロンプトから、Python 用 [pandas](https://pandas.pydata.org/) パッケージをインストールします。

```bash
python.exe -m pip install pandas
```

## <a name="update-the-system-environment-variables"></a>システム環境変数を更新する

システム環境変数として PYTHONHOME を追加または変更します。

+ Windows の検索ボックスに「環境」と入力し、 **[Edit the system environment variables]\(システム環境変数の編集\)** を選択します。
+ **[詳細設定]** タブの **[環境変数]** を選択します。
+ **[システム変数]** で **[新規]** を選択し、Python 3.7 のインストール場所を指す PYTHONHOME を作成します。
PYTHONHOME が既に存在する場合は、 **[編集]** を選択し、Python 3.7 のインストール場所を指定します。
+ **[OK]** を選択して、残りのウィンドウを閉じます。

![PYTHONHOME システム変数を作成します。](../install/media/sys-pythonhome.png)

## <a name="grant-access-to-the-custom-python-installation-folder"></a>カスタム Python インストール フォルダーへのアクセスを許可する

新しい "*管理者特権*" でのコマンド プロンプトから次の **icacls** コマンドを実行して、PYTHONHOME に対する READ および EXECUTE のアクセス権を、**SQL Server Launchpad サービス** と SID **S-1-15-2-1** (**ALL_APPLICATION_PACKAGES**) に付与します。 Launchpad サービスのユーザー名は `NT Service\MSSQLLAUNCHPAD$INSTANCENAME* where INSTANCENAME` はご利用の SQL Server のインスタンス名です。 そのコマンドでは、指定したディレクトリ パスの下にあるすべてのファイルとフォルダーへのアクセス権が再帰的に許可されます。

インスタンス名を `MSSQLLAUNCHPAD` に追加します (`MSSQLLAUNCHPAD$INSTANCENAME`)。 この例では、INSTANCENAME は既定のインスタンス `MSSQLSERVER` です。

1. **SQL Server Launchpad サービスのユーザー名** にアクセス許可を付与します。

    ```cmd
    icacls "%PYTHONHOME%" /grant "NT Service\MSSQLLAUNCHPAD$MSSQLSERVER":(OI)(CI)RX /T

2. Give permissions to **SID S-1-15-2-1**.
    ```cmd
    icacls "%PYTHONHOME%" /grant *S-1-15-2-1:(OI)(CI)RX /T

>[!NOTE]
>The preceding command grants permissions to the computer **SID S-1-15-2-1**, which is equivalent to ALL APPLICATION PACKAGES on an English version of Windows. Alternatively, you can use `icacls "%R_HOME%" /grant "ALL APPLICATION PACKAGES":(OI)(CI)RX /T` on an English version of Windows.

## Restart SQL Server Launchpad service

From an *elevated* command prompt, run the following commands. Replace "MSSQLSERVER" with the name of your SQL Server instance.

```CMD
net stop MSSQLLAUNCHPAD$MSSQLSERVER
net start MSSQLLAUNCHPAD$MSSQLSERVER
```

または、システムの **[サービス]** アプリで SQL Server Launchpad サービスを右クリックし、 **[再起動]** コマンドをクリックします。 または、[SQL Server 構成マネージャー](../../relational-databases/sql-server-configuration-manager.md)を使用して、サービスを再起動します。

## <a name="download-python-language-extension"></a>Python 言語拡張機能をダウンロードする

[Windows 用 Python 言語拡張機能が含まれている zip ファイル](https://github.com/microsoft/sql-server-language-extensions/releases)をダウンロードします。 運用環境ではリリース バージョンを使用することをお勧めします。 開発またはテストではデバッグ バージョンを使用します。エラーを調査するための詳細なログ情報が提供されるためです。

## <a name="register-external-language"></a>外部言語を登録する

拡張機能を使用するデータベースごとに、[CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md) でこの Python 言語拡張機能を登録します。 [Azure Data Studio](../../azure-data-studio/download-azure-data-studio.md) を使用して SQL Server に接続し、次の T-SQL コマンドを実行します。 このステートメントのパスを変更して、ダウンロードした言語拡張機能の zip ファイル (python-lang-extension.zip) の場所を反映します。

> [!NOTE]
> Python は予約語です。 外部言語には別の名前を使用します (たとえば "myPython")。

```sql
CREATE EXTERNAL LANGUAGE [myPython]
FROM (CONTENT = N'/path/to/python-lang-extension.zip', FILE_NAME = 'pythonextension.dll');
GO
```

::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

SQL Server は、Red Hat Enterprise Linux (RHEL)、SUSE Linux Enterprise Server (SLES)、および Ubuntu にインストールできます。 詳細については、[「SQL Server on Linux のインストール ガイド」の「サポートされているプラットフォーム」](../../linux/sql-server-linux-setup.md)を参照してください。

> [!NOTE]
> この記事では、Linux に Python 用のカスタム ランタイムをインストールする方法について説明します。 Windows にインストールするには、[SQL Server on Windows 用 Python カスタム ランタイムのインストール](custom-runtime-python.md?view=sql-server-ver15&preserve-view=true)に関するページを参照してください。

## <a name="pre-install-checklist"></a>インストール前のチェックリスト

Python カスタム ランタイムをインストールする前に、次のものをインストールします。

+ [Linux 用 SQL Server 2019 (累積的な更新プログラム 3 以降)](../../linux/sql-server-linux-setup.md)。
SQL Server on Linux をインストールする場合は、Microsoft リポジトリを構成する必要があります。 詳細については、[リポジトリの構成](../../linux/sql-server-linux-change-repo.md)に関するページを参照してください

  > [!NOTE]
  > Python カスタム ランタイムには、SQL Server 2019 の累積的な更新プログラム (CU) 3 以降が必要です。

+ [機能拡張フレームワークのある Linux への SQL Server 言語拡張機能](../../linux/sql-server-linux-setup-language-extensions-java.md)。

+ [Python 3.7](https://www.python.org/downloads/release/python-379/)。

## <a name="add-sql-server-language-extensions-for-linux"></a>Linux 用の SQL Server 言語拡張機能を追加する

> [!NOTE]
> SQL Server 2019 に Machine Learning Services がインストールされている場合は、言語拡張機能用の **mssql-server-extensibility** パッケージが既にインストールされているため、この手順は省略できます。

言語拡張機能では、外部コードの実行に機能拡張フレームワークが使用されます。 コードの実行はコア エンジン プロセスから分離されていますが、SQL Server のクエリ実行と完全に統合されています。

Linux のバージョンに応じて、次のコマンドを使用して言語拡張機能をインストールします。

### <a name="ubuntu"></a>Ubuntu
> [!TIP]
> 可能であれば、`update` を使用して、インストールの前にシステム上のパッケージを更新しておきます。 Ubuntu には、https apt transport オプションがない可能性があります。 インストールするには、`apt-get install apt-transport-https` を使用します。

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

## <a name="using-a-custom-installation-of-python-37"></a>Python 3.7 のカスタム インストールを使用する

> [!NOTE]
> Python を `/usr/lib/python3.7` の既定の場所にインストールした場合は、[次のセクション](#download-python-linux)にスキップできます。

独自のバージョンの Python 3.7 をビルドした場合は、次のコマンドを使用して、SQL Server でカスタム インストールを見つけて読み込むことができるようにします。

### <a name="update-the-environment-variables"></a>環境変数を更新する

1. mssql-launchpadd サービスを編集して、PYTHONHOME 環境変数を `/etc/systemd/system/mssql-launchpadd.service.d/override.conf` ファイルに追加します

      ```bash
      sudo systemctl edit mssql-launchpadd
      ```

    + 開かれた `/etc/systemd/system/mssql-launchpadd.service.d/override.conf` ファイルに、次のテキストを挿入します。 PYTHONHOME の値をカスタムの Python インストール パスに設定します。

      ```vi
      [Service]
      Environment="PYTHONHOME=/path/to/installation/of/python3.7"
      ```

    + 保存して閉じます。

2. `libpython3.7m.so.1.0` を読み込めることを確認します。

    + `/etc/ld.so.conf.d` 内に custom-python.conf ファイルを作成します。

      ```bash
      sudo vi /etc/ld.so.conf.d/custom-python.conf
      ```

    + 開かれたファイルに、カスタムの Python インストールから **libpython3.7m.so.1.0** へのパスを追加します。

      ```vi
      /path/to/installation/of/python3.7/lib
      ```

    + 新しいファイルを保存して閉じます。

    + `ldconfig` を実行し、次のコマンドを実行することで `libpython3.7m.so.1.0` を読み込めることを確認し、すべての依存ライブラリが見つかることを確認します。

      ```bash
      sudo ldconfig
      ldd /path/to/installation/of/python3.7/lib/libpython3.7m.so.1.0
      ```

### <a name="grant-access-to-the-custom-python-folder"></a>カスタム Python フォルダーへのアクセスを許可する

/var/opt/mssql/mssql.conf ファイルの extensibility セクションにある `datadirectories` オプションを、カスタム Python のインストールに設定します。

```bash
sudo /opt/mssql/bin/mssql-conf set extensibility.datadirectories /path/to/installation/of/python3.7
```

### <a name="restart-the-mssql-launchpadd-service"></a>mssql-launchpadd サービスを再起動する

```bash
sudo systemctl restart mssql-launchpadd
```
## <a name="download-python-language-extension"></a><a name="download-python-linux"></a> Python 言語拡張機能をダウンロードする

[Linux 用 Python 言語拡張機能が含まれている zip ファイル](https://github.com/microsoft/sql-server-language-extensions/releases)をダウンロードします。 運用環境ではリリース バージョンを使用することをお勧めします。 開発またはテストではデバッグ バージョンを使用します。エラーを調査するための詳細なログ情報が提供されるためです。

## <a name="register-external-language"></a>外部言語を登録する

拡張機能を使用するデータベースごとに、[CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md) でこの Python 言語拡張機能を登録します。 [Azure Data Studio](../../azure-data-studio/download-azure-data-studio.md) を使用して SQL Server に接続し、次の T-SQL コマンドを実行します。 
このステートメントのパスを変更して、ダウンロードした言語拡張機能の zip ファイル (python-lang-extension.zip) の場所を反映します。

> [!NOTE]
>Python は予約語です。 外部言語には別の名前を使用します (たとえば "myPython")。

```sql
CREATE EXTERNAL LANGUAGE myPython 
FROM (CONTENT = N'/PATH/TO/python-lang-extension.zip', FILE_NAME = 'libPythonExtension.so.1.0');
GO
```

::: moniker-end

## <a name="enable-external-script-execution-in-sql-server"></a>SQL Server で外部スクリプトの実行を有効にする

Python の外部スクリプトは、ストアド プロシージャ [sp_execute_external スクリプト](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)を SQL Server に対して実行することによって実行できます。 

外部スクリプトを有効にするには、SQL Server に接続されている [Azure Data Studio](../../azure-data-studio/download-azure-data-studio.md) を使用して、次の SQL コマンドを実行します。

```sql
sp_configure 'external scripts enabled', 1;
RECONFIGURE WITH OVERRIDE;  
```

## <a name="verify-language-extension-installation"></a>言語拡張機能のインストールを確認する

この SQL スクリプトでは、インストールされている言語拡張機能をテストします。

```sql
EXEC sp_execute_external_script
@language =N'myPython',
@script=N'
import sys
print(sys.path)
print(sys.version)
print(sys.executable)'
```

## <a name="verify-parameters-and-datasets-of-different-data-types"></a>さまざまなデータ型のパラメーターとデータセットを検証する

このスクリプトを使用して、入力と出力のパラメーターおよびデータセットのさまざまなデータ型をテストします。

```sql
DECLARE @sumVal int = 12;
DECLARE @charVal VARCHAR(30) = N'Hello'

EXEC sp_execute_external_script
@language =N'myPython',
@script=N'
print(sumVal)
print(charVal)
sumVal = sumVal + 300
OutputDataSet = InputDataSet'
,@input_data_1 = N'SELECT 1, CAST(1.4 as real), ''Hi'', CAST(''1'' as bit)'
,@params = N'@sumVal int OUTPUT, @charVal VARCHAR(30)'
,@sumVal = @sumVal OUTPUT
,@charVal = @charVal
WITH RESULT SETS ((intCol int, doubleCol real, charCol char(2), logicalCol bit));

PRINT @sumVal
```

## <a name="next-steps"></a>次の手順

+ [SQL Server の機能拡張フレームワーク](../concepts/extensibility-framework.md)
+ [言語拡張機能の概要](../../language-extensions/language-extensions-overview.md)
