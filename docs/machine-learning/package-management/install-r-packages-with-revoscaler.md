---
title: RevoScaleR を使用して R パッケージをインストールする
description: RevoScaleR 関数を使用して、Machine Learning Services または R Services を使って SQL Server に R パッケージをインストールする方法について説明します。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/20/2019
ms.topic: how-to
author: garyericson
ms.author: garye
monikerRange: =sql-server-2016||=sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: 1526f1c9eaaf4924ec248b523bd44148398e031b
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870116"
---
# <a name="use-revoscaler-to-install-r-packages"></a>RevoScaleR を使用して R パッケージをインストールする

[!INCLUDE [SQL Server 2016 and 2017 only](../../includes/applies-to-version/sqlserver2016-2017-only.md)]

この記事では、[RevoScaleR](../r/ref-r-revoscaler.md) (バージョン 9.0.1 以降) 関数を使用して、Machine Learning Services または R Services を使って SQL Server に R パッケージをインストールする方法について説明します。 RevoScaleR 関数を使用すると、リモートの管理者以外のユーザーが、サーバーに直接アクセスせずに SQL Server にパッケージをインストールできます。

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
> [!NOTE]
> SQL Server R Services のお客様が RevoScaleR パッケージ管理機能を利用するには、[コンポーネントをアップグレード](../install/upgrade-r-and-python.md)する必要があります。 パッケージのバージョンと内容を取得する方法については、「[R パッケージ情報の取得](../package-management/r-package-information.md)」を参照してください。
::: moniker-end

## <a name="revoscaler-functions-for-package-management"></a>パッケージ管理の RevoScaleR 関数

次の表では、R パッケージのインストールと管理に使用される関数について説明します。

| Function | 説明 |
|----------|-------------|
| [rxSqlLibPaths](/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) | リモート SQL Server のインスタンス ライブラリのパスを特定します。 |
| [rxFindPackage](/machine-learning-server/r-reference/revoscaler/rxfindpackage) | リモート SQL Server にある 1 つ以上のパッケージのパスを取得します。 |
| [rxInstallPackages](/machine-learning-server/r-reference/revoscaler/rxinstallpackages) | リモートの R クライアントからこの関数は呼び出して、指定したリポジトリから、またはローカルに保存されている zip 形式のパッケージを読み取ることで、SQL Server 計算コンテキストにパッケージをインストールします。 この関数では、依存関係をチェックして、ローカル計算コンテキストでの R パッケージのインストールなど、関連するパッケージを SQL Server にインストールできることを確認します。 このオプションを使用するには、サーバーとデータベースでパッケージ管理が有効になっている必要があります。 クライアント環境とサーバー環境の両方に、同じバージョンの RevoScaleR が必要です。 |
| [rxInstalledPackages](/machine-learning-server/r-reference/revoscaler/rxinstalledpackages) | 指定した計算コンテキストにインストールされているパッケージの一覧を取得します。 |
| [rxSyncPackages](/machine-learning-server/r-reference/revoscaler/rxsyncpackages) | 指定した計算コンテキストについて、ファイル システムとデータベースの間にあるパッケージ ライブラリに関する情報をコピーします。 |
| [rxRemovePackages](/machine-learning-server/r-reference/revoscaler/rxremovepackages) | 指定した計算コンテキストからパッケージを削除します。 また、依存関係を計算し、SQL Server の他のパッケージで使用されなくなったパッケージが削除されていることを確認して、リソースを解放します。 |

## <a name="prerequisites"></a>前提条件

+ SQL Server でリモート管理が有効になっている。 詳細については、[SQL Server でのリモート R パッケージ管理の有効化](r-package-how-to-enable-or-disable.md)に関する記事をご覧ください。

+ クライアント環境とサーバー環境の両方に、同じバージョンの RevoScaleR がある。 詳細については、「[R パッケージ情報の取得](../package-management/r-package-information.md)」を参照してください。

+ サーバーとデータベースに接続して、R コマンドを実行する権限がある。 また、データベース ロールのメンバーで、指定したインスタンスとデータベースにパッケージをインストールできる。

  + **共有スコープ** のパッケージは、指定したデータベースの `rpkgs-shared` ロールに属しているユーザーがインストールできます。 このロールのユーザーはすべて、共有パッケージをアンインストールできます。

  + **非公開スコープ** のパッケージは、データベースの `rpkgs-private` ロールに属しているすべてのユーザーがインストールできます。 ただし、ユーザーが表示およびアンインストールできるのは自分のパッケージのみです。

  + データベース所有者は、共有または非公開パッケージを操作できます。

## <a name="client-connections"></a>クライアント接続

同じネットワーク上にある [Microsoft R Client](/machine-learning-server/r-client/install-on-windows) または [Microsoft Machine Learning Server](/machine-learning-server/install/machine-learning-server-windows-install) (データ サイエンティストは無料の Developer エディションを使用することが多い) を、クライアント ワークステーションにできます。

リモート R クライアントからパッケージ管理関数を呼び出すときは、[RxInSqlServer](/machine-learning-server/r-reference/revoscaler/rxinsqlserver) 関数を使用して、最初に計算コンテキスト オブジェクトを作成する必要があります。 その後、使用するパッケージ管理関数それぞれに、計算コンテキストを引数として渡します。

ユーザー ID は、通常、計算コンテキストを設定するときに指定されます。 計算コンテキストを作成するときにユーザー名とパスワードを指定しない場合は、R コードを実行しているユーザーの ID が使用されます。

1. R コマンド ラインで、インスタンスとデータベースへの接続文字列を定義します。
2. 接続文字列を使用して、[RxInSqlServer](/machine-learning-server/r-reference/revoscaler/rxinsqlserver) コンストラクターを使って、SQL Server 計算コンテキストを定義します。

    ```R
    sqlcc <- RxInSqlServer(connectionString = myConnString, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```
3. インストールするパッケージの一覧を作成し、その一覧を文字列変数に保存します。

    ```R
    packageList <- c("e1071", "mice")
    ```

4. [rxInstallPackages](/machine-learning-server/r-reference/revoscaler/rxinstallpackages) を呼び出し、計算コンテキストと、パッケージ名を含む文字列変数を渡します。

    ```R
    rxInstallPackages(pkgs = packageList, verbose = TRUE, computeContext = sqlcc)
    ```

    依存パッケージが必要な場合は、そのパッケージも、クライアントでインターネット接続が利用できることを前提としてインストールされます。
    
    パッケージは、接続を確立しているユーザーの資格情報を使用して、そのユーザーの既定のスコープでインストールされます。

## <a name="call-package-management-functions-in-stored-procedures"></a>ストアド プロシージャでパッケージ管理関数を呼び出す

パッケージ管理関数は `sp_execute_external_script` 内で実行できます。 その場合、関数は、ストアド プロシージャ呼び出し元のセキュリティ コンテキストを使用して実行されます。

## <a name="examples"></a>例

このセクションでは、計算コンテキストとして SQL Server インスタンスまたはデータベースに接続するときに、リモート クライアントからこれらの関数を使用する方法の例を示します。

すべての例で、接続文字列、または接続文字列を必要とする計算コンテキストを指定する必要があります。 この例は、SQL Server の計算コンテキストを作成する方法の 1 つを示しています。

```R
instance_name <- "computer-name/instance-name";
database_name <- "TestDB";
sqlWait= TRUE;
sqlConsoleOutput <- TRUE;
connString <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
sqlcc <- RxInSqlServer(connectionString = connString, wait = sqlWait, consoleOutput = sqlConsoleOutput, numTasks = 4);
```

サーバーが配置されている場所とセキュリティ モデルによっては、接続文字列にドメインとサブネットの仕様を指定するか、SQL ログインを使用することが必要になる場合があります。 次に例を示します。

```R
connStr <- "Driver=SQL Server;Server=myserver.financeweb.contoso.com;Database=Finance;Uid=RUser1;Pwd=RUserPassword"
```

### <a name="get-package-path-on-a-remote-sql-server-compute-context"></a>リモート SQL Server 計算コンテキストにあるパッケージ パスを取得する

この例では、計算コンテキスト **にある** RevoScaleR`sqlcc` パッケージのパスを取得します。

```R
sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlcc)
print(sqlPackagePaths)
```

**結果**

"C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/RevoScaleR"

> [!TIP]
> SQL コンソール出力を表示するオプションを有効にした場合は、`print` ステートメントの前にある関数から状態メッセージが表示されることがあります。 コードのテストが完了したら、計算コンテキスト コンストラクターで `consoleOutput` を FALSE に設定して、メッセージを削除します。

### <a name="get-locations-for-multiple-packages"></a>複数のパッケージの場所を取得する

次の例では、計算コンテキスト **にある** RevoScaleR **および** lattice`sqlcc` パッケージのパスを取得します。 複数のパッケージに関する情報を取得するには、パッケージ名を含む文字列ベクトルを渡します。

```R
packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlcc)
print(packagePaths)
```

### <a name="get-package-versions-on-a-remote-compute-context"></a>リモート計算コンテキストにあるパッケージのバージョンを取得する

このコマンドを R コンソールから実行して、計算コンテキスト *sqlServer* にインストールされているパッケージのビルド番号とバージョン番号を取得します。

```R
sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer)
```

### <a name="install-a-package-on-sql-server"></a>SQL Server にパッケージをインストールする

この例では、**forecast** パッケージとその依存関係を計算コンテキストにインストールします。

  ```R
  pkgs <- c("forecast")
  rxInstallPackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
  ```

### <a name="remove-a-package-from-sql-server"></a>パッケージを SQL Server から削除する

この例では、**forecast** パッケージとその依存関係を計算コンテキストから削除します。

  ```R
  pkgs <- c("forecast")
  rxRemovePackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
  ```

### <a name="synchronize-packages-between-database-and-file-system"></a>データベースとファイル システムの間でパッケージを同期する

次の例では、データベース **TestDB** をチェックして、すべてのパッケージがファイル システムにインストールされているかどうかを確認します。 不足しているパッケージがある場合は、そのパッケージがファイル システムにインストールされます。

```R
# Instantiate the compute context
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

# Synchronize the packages in the file system for all scopes and users
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

パッケージの同期は、データベースごと、およびユーザーごとに実行されます。 詳細については、「[SQL Server の R パッケージ同期](package-install-uninstall-and-sync.md)」を参照してください。

### <a name="use-a-stored-procedure-to-list-packages-in-sql-server"></a>ストアド プロシージャを使用して SQL Server にあるパッケージの一覧を表示する

Management Studio または T-SQL をサポートする他のツールから次のコマンドを実行し、ストアド プロシージャで `rxInstalledPackages` を使用して、現在のインスタンスにインストールされているパッケージの一覧を取得します。

```sql
EXEC sp_execute_external_script 
  @language=N'R', 
  @script=N'
    myPackages <- rxInstalledPackages();
    OutputDataSet <- as.data.frame(myPackages);
    '
```

`rxSqlLibPaths` 関数を使用すると、SQL Server Machine Learning Services によって使用されているアクティブなライブラリを特定できます。 このスクリプトは、現在のサーバーのライブラリ パスのみを返すことができます。 

```sql
declare @instance_name nvarchar(100) = @@SERVERNAME, @database_name nvarchar(128) = db_name();
exec sp_execute_external_script 
  @language = N'R',
  @script = N'
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    .libPaths(rxSqlLibPaths(connStr));
    print(.libPaths());
  ', 
  @input_data_1 = N'', 
  @params = N'@instance_name nvarchar(100), @database_name nvarchar(128)',
  @instance_name = @instance_name, 
  @database_name = @database_name;
```

## <a name="see-also"></a>参照

+ [リモートの R パッケージ管理を有効にする](r-package-how-to-enable-or-disable.md)
+ [R パッケージの同期](package-install-uninstall-and-sync.md)
+ [R パッケージを使用するためのヒント](tips-for-using-r-packages.md)
+ [R パッケージ情報の取得](../package-management/r-package-information.md)