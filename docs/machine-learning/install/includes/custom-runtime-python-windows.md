---
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 02/08/2021
ms.topic: include
author: dphansen
ms.author: davidph
ms.openlocfilehash: 9f58ddf6b58e32d40b2962b47255aba2e553acca
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100072955"
---
## <a name="prerequisites"></a>前提条件

Python カスタム ランタイムをインストールする前に、次のものをインストールします。

+ 既存の SQL Server インスタンスを使用する場合は、SQL Server 2019 の[累積的な更新プログラム (CU) 3 以降](../../../database-engine/install-windows/latest-updates-for-microsoft-sql-server.md)をインストールします。

## <a name="install-language-extensions"></a>言語拡張をインストールする

> [!NOTE]
> SQL Server 2019 に [Machine Learning Services](../../sql-server-machine-learning-services.md) がインストールされている場合は、言語拡張機能が既にインストールされているため、この手順は省略できます。

[SQL Server 言語拡張機能](../../../language-extensions/language-extensions-overview.md) (Python カスタム ランタイムに使用されるもの) をインストールするには、次の手順に従います。

1. SQL Server 2019 のセットアップ ウィザードを開始します。
  
1. **[インストール]** タブで、 **[SQL Server の新規スタンドアロン インストールを実行するか、既存のインストールに機能を追加します]** を選択します。

1. **[機能の選択]** ページで、次のオプションを選択します。
  
    + **データベース エンジン サービス**
  
        SQL Server で言語拡張を使用するには、データベース エンジンのインスタンスをインストールする必要があります。 新規または既存のインスタンスのいずれかを使用できます。
  
    + **Machine Learning Services および言語の拡張**

        **[Machine Learning Services および言語の拡張]** を選択します。 後でカスタム Python ランタイムをインストールするので、Python は選択しないでください。

        :::image type="content" source="../media/2019-setup-language-extensions.png" alt-text="SQL Server 2019 言語拡張機能のセットアップ。":::

1. **[インストールの準備完了]** ページで、以下が選択されていることを確認した後、 **[インストール]** を選択します。
  
    + データベース エンジン サービス
    + Machine Learning Services および言語の拡張

1. セットアップが完了した後、確認のメッセージが表示されたらコンピューターを再起動します。

> [!IMPORTANT]
> 言語拡張機能を使用して SQL Server 2019 の新規インスタンスをインストールする場合は、次の手順に進む前に、[累積的な更新プログラム (CU) 3 以降](../../../database-engine/install-windows/latest-updates-for-microsoft-sql-server.md)をインストールしてください。

## <a name="install-python"></a>Python のインストール

カスタム Python ランタイムに使用される Python 言語拡張機能は、現在、Python 3.7 のみをサポートしています。 別のバージョンの Python を使用する場合は、[Python 言語拡張機能の GitHub リポジトリ](https://github.com/microsoft/sql-server-language-extensions/tree/master/language-extensions/python)の指示に従って、拡張機能を変更し、再構築してください。

1. Windows 用の [Python 3.7](https://www.python.org/downloads/windows/) をダウンロードし、サーバーでセットアップを実行します。

1. **[Add Python 3.7 to PATH]\(Python 3.7 を PATH に追加\)** を選択し、 **[インストールをカスタマイズする]** を選択します。

    :::image type="content" source="../media/python-install-add-to-path.png" alt-text="Python 3.7 のインストール - Python 3.7 を PATH に追加する":::

1. **[オプション機能]** は既定値をそのまま使用して、 **[次へ]** を選択します。

1. **[すべてのユーザーに対してインストール]** を選択し、インストールの場所を記録しておきます。

    :::image type="content" source="../media/python-install-for-all-users.png" alt-text="Python 3.7 のインストール - すべてのユーザーに対してインストール":::

1. **[インストール]** を選択します。

## <a name="install-pandas"></a>pandas をインストールする

"*管理者特権*" でのコマンド プロンプトから (管理者として実行)、Python 用の [pandas](https://pandas.pydata.org/) パッケージをインストールします。

```bash
python.exe -m pip install pandas
```

## <a name="grant-access-to-python-folder"></a>Python フォルダーへのアクセスを許可する

新しい "*管理者特権*" でのコマンド プロンプトから次の **icacls** コマンドを実行して、Python のインストール場所への **読み取りと実行** のアクセス権を、**SQL Server Launchpad サービス** と SID **S-1-15-2-1** (**ALL_APPLICATION_PACKAGES**) に付与します。

次の例では、Python のインストール場所として `C:\Program Files\Python37` を使用します。 お使いの場所が異なる場合は、コマンドでそれを変更します。

1. **SQL Server Launchpad サービスのユーザー名** にアクセス許可を付与します。

    ```cmd
    icacls "C:\Program Files\Python37" /grant "NT Service\MSSQLLAUNCHPAD":(OI)(CI)RX /T
    ```

    名前付きインスタンスの場合、**SQL01** というインスタンスに対するコマンドは `icacls "C:\Program Files\Python37" /grant "NT Service\MSSQLLAUNCHPAD$SQL01":(OI)(CI)RX /T` になります。

2. **SID S-1-15-2-1** にアクセス許可を付与します。

    ```cmd
    icacls "C:\Program Files\Python37" /grant *S-1-15-2-1:(OI)(CI)RX /T
    ```

    上記のコマンドを実行すると、コンピューター SID **S-1-15-2-1** にアクセス許可が付与されます。これは、英語版の Windows における **ALL APPLICATION PACKAGES** と同等です。 または、英語版の Windows で `icacls "C:\Program Files\Python37" /grant "ALL APPLICATION PACKAGES":(OI)(CI)RX /T` を使用することもできます。

## <a name="restart-sql-server-launchpad"></a>SQL Server Launchpad を再起動する

SQL Server Launchpad サービスを再起動するには、次の手順に従います。

1. [[SQL Server 構成マネージャー]](../../../relational-databases/sql-server-configuration-manager.md) を開きます。

1. **[SQL Server サービス]** で **[SQL Server Launchpad (MSSQLSERVER)]** を右クリックして、 **[再起動]** を選択します。 名前付きインスタンスを使用している場合は、 **(MSSQLSERVER)** の代わりにインスタンス名が表示されます。

## <a name="register-language-extension"></a>言語拡張機能を登録する

Python 言語拡張機能 (Python カスタム ランタイムに使用されるもの) をダウンロードして登録するには、次の手順に従います。

1. [SQL Server 言語拡張機能の GitHub リポジトリ](https://github.com/microsoft/sql-server-language-extensions/releases)から **python-lang-extension-windows-release.zip** ファイルをダウンロードします。

    開発環境やテスト環境では、デバッグ バージョン (**python-lang-extension-windows-debug.zip**) を使用することもできます。 デバッグ バージョンでは、エラーを調査するための詳細なログ情報が提供されます。これは運用環境では推奨されません。

1. [Azure Data Studio](../../../azure-data-studio/what-is-azure-data-studio.md) を使用して SQL Server インスタンスに接続し、次の T-SQL コマンドを実行して、Python 言語拡張機能を [CREATE EXTERNAL LANGUAGE](../../../t-sql/statements/create-external-language-transact-sql.md) に登録します。

    このステートメントのパスを変更して、ダウンロードした言語拡張機能の zip ファイルの場所 (**python-lang-extension-windows-release.zip**) と Python インストールの場所 (`C:\\Program Files\\Python3.7`) を反映します。

    ```sql
    CREATE EXTERNAL LANGUAGE [myPython]
    FROM (CONTENT = N'C:\path\to\python-lang-extension-windows-release.zip', 
        FILE_NAME = 'pythonextension.dll', 
        ENVIRONMENT_VARIABLES = N'{"PYTHONHOME": "C:\\Program Files\\Python3.7"}');
    GO
    ```

    Python 言語拡張機能を使用するデータベースごとに、このステートメントを実行します。

    > [!NOTE]
    > **Python** は予約語であり、新しい外部言語の名前として使用することはできません。 別の名前を使用してください。 たとえば、上記のステートメントでは **myPython** が使用されています。
