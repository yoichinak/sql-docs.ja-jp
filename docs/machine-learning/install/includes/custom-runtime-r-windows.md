---
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 02/08/2021
ms.topic: include
author: dphansen
ms.author: davidph
ms.openlocfilehash: 2a156ab122f0eadce71da9f4fcaf9e99584c8e32
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100072769"
---
## <a name="prerequisites"></a>前提条件

R カスタム ランタイムをインストールする前に、次のものをインストールします。

+ 既存の SQL Server インスタンスを使用する場合は、SQL Server 2019 の[累積的な更新プログラム (CU) 3 以降](../../../database-engine/install-windows/latest-updates-for-microsoft-sql-server.md)をインストールします。

## <a name="install-language-extensions"></a>言語拡張をインストールする

> [!NOTE]
> SQL Server 2019 に [Machine Learning Services](../../sql-server-machine-learning-services.md) がインストールされている場合は、言語拡張機能が既にインストールされているため、この手順は省略できます。

以下の手順のようにして、[SQL Server 言語拡張機能](../../../language-extensions/language-extensions-overview.md)をインストールします。これは、R カスタム ランタイムに使用されます。

1. SQL Server 2019 のセットアップ ウィザードを開始します。
  
1. **[インストール]** タブで、 **[SQL Server の新規スタンドアロン インストールを実行するか、既存のインストールに機能を追加します]** を選択します。

1. **[機能の選択]** ページで、次のオプションを選択します。
  
    + **データベース エンジン サービス**
  
        SQL Server で言語拡張を使用するには、データベース エンジンのインスタンスをインストールする必要があります。 新規または既存のインスタンスのいずれかを使用できます。
  
    + **Machine Learning Services および言語の拡張**

        **[Machine Learning Services および言語の拡張]** を選択します。 後でカスタム R ランタイムをインストールするので、R は選択しないでください。

        :::image type="content" source="../media/2019-setup-language-extensions.png" alt-text="SQL Server 2019 言語拡張機能のセットアップ。":::

1. **[インストールの準備完了]** ページで、以下が選択されていることを確認した後、 **[インストール]** を選択します。
  
    + データベース エンジン サービス
    + Machine Learning Services および言語の拡張

1. セットアップが完了した後、確認のメッセージが表示されたらコンピューターを再起動します。

> [!IMPORTANT]
> 言語拡張機能を使用して SQL Server 2019 の新規インスタンスをインストールする場合は、次の手順に進む前に、[累積的な更新プログラム (CU) 3 以降](../../../database-engine/install-windows/latest-updates-for-microsoft-sql-server.md)をインストールしてください。

## <a name="install-r"></a>R のインストール

カスタム ランタイムとして使用する R のバージョンをダウンロードしてインストールします。 R バージョン 3.3 以降がサポートされています。

1. [R バージョン 3.3 以降](https://cran.r-project.org/bin/windows/base/)をダウンロードします。

1. R のセットアップを実行します。

1. R がインストールされたパスを記録しておきます。 たとえば、この記事では `C:\Program Files\R\R-4.0.3` です。

    :::image type="content" source="../media/r-setup-path.png" alt-text="R のセットアップ":::

## <a name="update-system-environment-variable"></a>システム環境変数を更新する

以下の手順のようにして、**PATH** システム環境変数を変更します。

1. Windows の検索ボックスで「**システム環境変数の編集**」を検索して開きます。

1. **[詳細設定]** の **[環境変数]** を選択します。

1. **PATH** システム環境変数を変更します。

    **PATH** を選択して、 **[編集]** をクリックします。

    **[新規]** を選択して、R インストール パスの `\bin\x64` フォルダーへのパスを追加します。 たとえば、「 `C:\Program Files\R\R-4.0.3\bin\x64` 」のように入力します。

## <a name="install-rcpp-package"></a>Rcpp パッケージをインストールする

以下の手順のようにして、**Rcpp** パッケージをインストールします。

1. "*管理者特権*" でのコマンド プロンプトを開始します (管理者として実行)。

1. コマンド プロンプトから R を起動します。 R インストール パスのフォルダーで `\bin\R.exe` を実行します。 たとえば、「 `C:\Program Files\R\R-4.0.3\bin\R.exe` 」のように入力します。

    ```CMD
    "C:\Program Files\R\R-4.0.3\bin\R.exe"
    ```

1. 次のスクリプトを実行して、R インストール パスの `\library` フォルダーに Rcpp パッケージをインストールします。 たとえば、「 `C:\Program Files\R\R-4.0.3\library` 」のように入力します。

    ```R
    install.packages("Rcpp", lib="C:\Program Files\R\R-4.0.3\library");
    ```

## <a name="grant-access-to-r-folder"></a>R フォルダーへのアクセス権を付与する

> [!NOTE]
> R を既定の場所である `C:\Program Files\R\R-version` (`C:\Program Files\R\R-4.0.3` など) にインストールした場合は、この手順を省略できます。

新しい "*管理者特権*" でのコマンド プロンプトから次の **icacls** コマンドを実行して、**読み取りと実行** のアクセス権を、**SQL Server Launchpad サービスのユーザー名** と SID **S-1-15-2-1** (**ALL APPLICATION PACKAGES**) に付与します。 Launchpad サービスのユーザー名は、`NT Service\MSSQLLAUNCHPAD$INSTANCENAME` という形式です。`INSTANCENAME` は、SQL Server のインスタンス名です。

そのコマンドでは、指定したディレクトリ パスの下にあるすべてのファイルとフォルダーへのアクセス権が再帰的に許可されます。

1. **SQL Server Launchpad サービスのユーザー名** に、R インストール パスへのアクセス許可を付与します。 たとえば、「 `C:\Program Files\R\R-4.0.3` 」のように入力します。

    ```cmd
    icacls "C:\Program Files\R\R-4.0.3" /grant "NT Service\MSSQLLAUNCHPAD":(OI)(CI)RX /T
    ```

    名前付きインスタンスの場合、**SQL01** というインスタンスに対するコマンドは `icacls "C:\Program Files\R\R-4.0.3" /grant "NT Service\MSSQLLAUNCHPAD$SQL01":(OI)(CI)RX /T` になります。

2. **SID S-1-15-2-1** に、R インストール パスへのアクセス許可を付与します。 たとえば、「 `C:\Program Files\R\R-4.0.3` 」のように入力します。

    ```cmd
    icacls "C:\Program Files\R\R-4.0.3" /grant *S-1-15-2-1:(OI)(CI)RX /T
    ```

    上記のコマンドを実行すると、コンピューター SID **S-1-15-2-1** にアクセス許可が付与されます。これは、英語版の Windows における **ALL APPLICATION PACKAGES** と同等です。 または、英語版の Windows で `icacls "C:\Program Files\R\R-4.0.3" /grant "ALL APPLICATION PACKAGES":(OI)(CI)RX /T` を使用することもできます。

## <a name="restart-sql-server-launchpad"></a>SQL Server Launchpad を再起動する

SQL Server Launchpad サービスを再起動するには、次の手順に従います。

1. [[SQL Server 構成マネージャー]](../../../relational-databases/sql-server-configuration-manager.md) を開きます。

1. **[SQL Server サービス]** で **[SQL Server Launchpad (MSSQLSERVER)]** を右クリックして、 **[再起動]** を選択します。 名前付きインスタンスを使用している場合は、 **(MSSQLSERVER)** の代わりにインスタンス名が表示されます。

## <a name="register-language-extension"></a>言語拡張機能を登録する

次の手順のようにして、R カスタム ランタイムに使用される R 言語拡張機能をダウンロードして登録します。

1. [SQL Server 言語拡張機能の GitHub リポジトリ](https://github.com/microsoft/sql-server-language-extensions/releases)から **R-lang-extension-windows-release.zip** ファイルをダウンロードします。

    開発環境やテスト環境では、代わりにデバッグ バージョン (**R-lang-extension-windows-debug.zip**) を使用できます。 デバッグ バージョンでは、エラーを調査するための詳細なログ情報が提供されます。これは運用環境では推奨されません。

1. [Azure Data Studio](../../../azure-data-studio/what-is-azure-data-studio.md) を使用してお使いの SQL Server インスタンスに接続し、次の T-SQL コマンドを実行して、[CREATE EXTERNAL LANGUAGE](../../../t-sql/statements/create-external-language-transact-sql.md) で R 言語拡張機能を登録します。

    このステートメントのパスを変更して、ダウンロードした言語拡張機能の zip ファイルの場所 (**R-lang-extension-windows-release.zip**) と R インストールの場所 (`C:\\Program Files\\R\\R-4.0.3`) を反映します。

    ```sql
    CREATE EXTERNAL LANGUAGE [myR]
    FROM (CONTENT = N'C:\path\to\R-lang-extension-windows-release.zip', 
        FILE_NAME = 'libRExtension.dll',
        ENVIRONMENT_VARIABLES = N'{"R_HOME": "C:\\Program Files\\R\\R-4.0.3"}'););
    GO
    ```

    R 言語拡張機能を使用するデータベースごとに、このステートメントを実行します。

    > [!NOTE]
    > **R** は予約語であり、新しい外部言語の名前として使用することはできません。 別の名前を使用してください。 たとえば、上記のステートメントでは **myR** が使用されています。
