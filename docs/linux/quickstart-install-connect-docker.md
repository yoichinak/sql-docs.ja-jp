---
title: Docker:SQL Server on Linux 用のコンテナーのインストール
description: このクイック スタートでは、Docker を使用して SQL Server 2017 および 2019 のコンテナー イメージを実行する方法を示します。 その次に、sqlcmd でデータベースを作成し、クエリを実行します。
ms.custom: seo-lt-2019, contperfq1
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.date: 09/07/2020
ms.topic: quickstart
ms.prod: sql
ms.technology: linux
ms.prod_service: linux
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
zone_pivot_groups: cs1-command-shell
ms.openlocfilehash: 8e87ca7630fca5e72daf2a3e4eedfd38d50482fd
ms.sourcegitcommit: 22102f25db5ccca39aebf96bc861c92f2367c77a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2020
ms.locfileid: "92115665"
---
# <a name="quickstart-run-sql-server-container-images-with-docker"></a>クイック スタート:Docker を使用して SQL Server コンテナー イメージを実行する
[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

> [!NOTE]
> 次に示す例では、docker.exe の使用を示していますが、これらのコマンドの多くは Podman でも機能します。 Docker コンテナー エンジンと同様の CLI が提供されています。 Podman の詳細は、[こちら](http://docs.podman.io/en/latest)をご覧ください。

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

このクイック スタートでは、Docker を使用して SQL Server 2017 コンテナー イメージ [mssql-server-linux](https://hub.docker.com/_/microsoft-mssql-server) をプルして実行します。 次に、**sqlcmd** と接続して最初のデータベースを作成し、クエリを実行します。

> [!TIP]
> SQL Server 2019 のコンテナーを実行する場合は、[この記事の SQL Server 2019 バージョン](quickstart-install-connect-docker.md?view=sql-server-linux-ver15)を参照してください。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

> [!NOTE]
> SQL Server 2019 CU3 以降では、Ubuntu 18.04 がサポートされています。

このクイック スタートでは、Docker を使用して SQL Server 2019 コンテナー イメージ [mssql-server-linux](https://hub.docker.com/r/microsoft/mssql-server) をプルして実行します。 次に、**sqlcmd** と接続して最初のデータベースを作成し、クエリを実行します。

> [!TIP]
> このクイック スタートでは、SQL Server 2019 のコンテナーを作成します。 SQL Server 2017 のコンテナーを作成する場合は、[この記事の SQL Server 2017 バージョン](quickstart-install-connect-docker.md?view=sql-server-linux-2017)を参照してください。

::: moniker-end

このイメージは、Ubuntu 18.04 に基づく Linux で実行されている SQL Server で構成されます。 イメージは Linux の Docker エンジン 1.8+ または Mac/Windows 用 Docker で使用することができます。 このクイックスタートでは特に、**Linux** イメージで SQL Server を使用することを中心に取り上げます。 Windows イメージについては言及しませんが、[mssql-server-windows-developer Docker Hub ページ](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/)で詳細を確認できます。

## <a name="prerequisites"></a><a id="requirements"></a> 前提条件

- サポートされているいずれかの Linux ディストリビューションの Docker エンジン 1.8+ または Mac/Windows 用 Docker。 詳細については、「[Install Docker](https://docs.docker.com/engine/installation/)」(Docker をインストールする) を参照してください。
- Docker **overlay2** ストレージ ドライバー。 ほとんどのユーザーでは、これが既定値です。 このストレージ プロバイダーを利用しておらず、変更する必要がある場合、[overlay2 の構成に関する docker ドキュメント](https://docs.docker.com/storage/storagedriver/overlayfs-driver/#configure-docker-with-the-overlay-or-overlay2-storage-driver)を参照してください。
- 2 GB 以上のディスク領域。
- 2 GB 以上の RAM。
- [SQL Server on Linux のシステム要件](sql-server-linux-setup.md#system)。

<!--The following H2 is versioned for 2017 and 2019. Much of the content is duplicated, so
any changes to one section should be duplicated in the other-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a name="pull-and-run-the-2017-container-image"></a><a id="pullandrun2017"></a> 2017 コンテナー イメージをプルし、実行する

次の手順を開始する前に、この記事で上述した推奨シェル (bash、PowerShell、または cmd) を選択していることを確認してください。

1. Microsoft コンテナー レジストリから SQL Server 2017 Linux コンテナー イメージをプルします。

   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```
   ::: zone-end

   > [!TIP]
   > SQL Server 2019 のコンテナーを実行する場合は、[この記事の SQL Server 2019 バージョン](quickstart-install-connect-docker.md?view=sql-server-linux-ver15#pullandrun2019)を参照してください。

   前のコマンドから、最新の SQL Server 2017 コンテナー イメージがプルされます。 特定のイメージをプルしたい場合、コロンとタグ名 (たとえば `mcr.microsoft.com/mssql/server:2017-GA-ubuntu`) を追加します。 利用可能なすべてのイメージを表示するには、[mssql-server Docker Hub のページ](https://hub.docker.com/r/microsoft/mssql-server)を参照してください。

   ::: zone pivot="cs1-bash"
   この記事の bash コマンドには、`sudo` が使用されています。 macOS では、`sudo` が不要な場合があります。 Linux では、`sudo` を使用して Docker を実行したくない場合は、**docker** グループを構成して、そのグループにユーザーを追加できます。 詳細については、「[Linux でのインストール後の手順](https://docs.docker.com/install/linux/linux-postinstall/)」を参照してください。

   ::: zone-end

2. Docker でコンテナー イメージを実行する場合は、Bash シェル (Linux/macOS) または管理者特権での PowerShell コマンド プロンプトから次のコマンドを使用することができます。

   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong@Passw0rd>" \
      -p 1433:1433 --name sql1 -h sql1 \
      -d \
      mcr.microsoft.com/mssql/server:2017-latest
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   
   > [!NOTE]
   > PowerShell Core を使用している場合、二重引用符を一重引用符に置換します。
   
   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong@Passw0rd>" `
      -p 1433:1433 --name sql1 -h sql1 `
      -d `
      mcr.microsoft.com/mssql/server:2017-latest
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong@Passw0rd>" `
      -p 1433:1433 --name sql1 -h sql1 `
      -d `
      mcr.microsoft.com/mssql/server:2017-latest
   ```
   ::: zone-end

   > [!NOTE]
   > パスワードは SQL Server の既定のパスワード ポリシーに従う必要があります。従わない場合、コンテナーで SQL Server をセットアップできず、動作が停止します。 既定で、パスワードは 8 文字以上の長さにする必要があり、次の 4 つのセットのうち 3 つから文字を含める必要があります。大文字、小文字、10 進数、記号です。 [docker ログ](https://docs.docker.com/engine/reference/commandline/logs/) コマンドを実行することでエラー ログを調査することができます。
   >
   > 既定では、これにより SQL Server 2017 Developer Edition のコンテナーが作成されます。 コンテナーで実稼働エディションを実行するためのプロセスは若干異なります。 詳細については、「[Run production container images](./sql-server-linux-docker-container-deployment.md#production)」(実稼働のコンテナー イメージを実行する) を参照してください。

   次の表は、前の `docker run` の例のパラメーターについて説明しています。

   | パラメーター | 説明 |
   |-----|-----|
   | **-e "ACCEPT_EULA=Y"** |  **ACCEPT_EULA** 変数を任意の値に設定し、[使用許諾契約書](https://go.microsoft.com/fwlink/?linkid=857698)の承諾を確定します。 SQL Server イメージの設定が必要です。 |
   | **-e "SA_PASSWORD=\<YourStrong@Passw0rd\>"** | 8 文字以上の、[SQL Server のパスワード要件](../relational-databases/security/password-policy.md)を満たす強力なパスワードを指定します。 SQL Server イメージの設定が必要です。 |
   | **-p 1433:1433** | ホスト環境の TCP ポート (最初の値) とコンテナーの TCP ポート (2 番目の値) をマップします。 この例では、SQL Server がコンテナー内の TCP 1433 上でリッスンしており、これがホスト上のポート 1433 に公開されています。 |
   | **--name sql1** | ランダムに生成された名前ではなく、コンテナーのカスタム名を指定します。 複数のコンテナーを実行する場合は、この同じ名前を再利用することはできません。 |
   | **-h sql1** | コンテナーのホスト名を指定していない場合にこれを明示的に設定するために使用されます。既定では、ランダムに生成されたシステム GUID であるコンテナー ID に設定されています。 |
   | **-d** | コンテナーをバックグラウンド (デーモン) で実行します |
   | **mcr.microsoft.com/mssql/server:2017-latest** | SQL Server 2017 Linux コンテナー イメージ。 |

3. Docker コンテナーを表示するには、`docker ps` コマンドを使用します。


   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker ps -a
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker ps -a
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker ps -a
   ```
   ::: zone-end

   次のスクリーンショットのような出力が表示されます。

   ![Docker ps コマンドの出力](./media/sql-server-linux-setup-docker/docker-ps-command.png)

4. **[STATUS]** 列に **[Up]** の状態が表示されている場合、SQL Server はコンテナーで実行されており、 **[PORTS]** 列に指定されたポートでリッスンしています。 SQL Server コンテナーの **[STATUS]** 列に **[Exited]** と表示されている場合は、[構成ガイドのトラブルシューティングのセクション](./sql-server-linux-docker-container-troubleshooting.md)を参照してください。

前述の `-h` (ホスト名) パラメーターは、コンテナーの内部名をカスタム値に変更します。 これは、次の Transact-SQL クエリで返される名前です。

```sql
SELECT @@SERVERNAME,
    SERVERPROPERTY('ComputerNamePhysicalNetBIOS'),
    SERVERPROPERTY('MachineName'),
    SERVERPROPERTY('ServerName')
```

ターゲット コンテナーを特定しやすくするため、`-h` と `--name` を同じ値に設定することをお勧めします。

5. 最後の手順として、`SA_PASSWORD` が `ps -eax` 出力に表示され、同じ名前の環境変数に格納されるため、SA パスワードを変更します。 以下の手順を参照してください。

::: moniker-end
<!--End of 2017 "Pull and run" section-->

<!--This is the 2019 version of the "Pull and run" section-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a name="pull-and-run-the-2019-container-image"></a><a id="pullandrun2019"></a> 2019 コンテナー イメージをプルし、実行する

次の手順を開始する前に、この記事で上述した推奨シェル (bash、PowerShell、または cmd) を選択していることを確認してください。

1. Microsoft コンテナー レジストリから SQL Server 2019 Linux コンテナー イメージをプルします。

   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker pull mcr.microsoft.com/mssql/server:2019-latest
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   
   > [!NOTE]
   > PowerShell Core を使用している場合、二重引用符を一重引用符に置換します。
   
   ```PowerShell
   docker pull mcr.microsoft.com/mssql/server:2019-latest
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker pull mcr.microsoft.com/mssql/server:2019-latest
   ```
   ::: zone-end

   > [!TIP]
   > このクイック スタートでは、SQL Server 2019 の Docker イメージを使用します。 SQL Server 2017 のイメージを実行する場合は、[この記事の SQL Server 2017 バージョン](quickstart-install-connect-docker.md?view=sql-server-linux-2017#pullandrun2017)を参照してください。

   上記のコマンドでは、Ubuntu に基づいて SQL Server 2019 のコンテナー イメージをプルします。 代わりに RedHat に基づくコンテナーイメージを使用するには、[RHEL ベースのコンテナー イメージの実行](./sql-server-linux-docker-container-deployment.md#rhel)に関するページを参照してください。 利用可能なすべてのイメージを表示する方法は、[mssql-server-linux Docker Hub ページ](https://hub.docker.com/_/microsoft-mssql-server)を参照してください。

   ::: zone pivot="cs1-bash"
   この記事の bash コマンドには、`sudo` が使用されています。 macOS では、`sudo` が不要な場合があります。 Linux では、`sudo` を使用して Docker を実行したくない場合は、**docker** グループを構成して、そのグループにユーザーを追加できます。 詳細については、「[Linux でのインストール後の手順](https://docs.docker.com/install/linux/linux-postinstall/)」を参照してください。
   ::: zone-end

2. Docker でコンテナー イメージを実行する場合は、Bash シェル (Linux/macOS) または管理者特権での PowerShell コマンド プロンプトから次のコマンドを使用することができます。

   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong@Passw0rd>" \
      -p 1433:1433 --name sql1 -h sql1 \
      -d mcr.microsoft.com/mssql/server:2019-latest
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong@Passw0rd>" `
      -p 1433:1433 --name sql1 -h sql1 `
      -d mcr.microsoft.com/mssql/server:2019-latest
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong@Passw0rd>" `
      -p 1433:1433 --name sql1 -h sql1 `
      -d mcr.microsoft.com/mssql/server:2019-latest
   ```
   ::: zone-end

   > [!NOTE]
   > パスワードは SQL Server の既定のパスワード ポリシーに従う必要があります。従わない場合、コンテナーで SQL Server をセットアップできず、動作が停止します。 既定で、パスワードは 8 文字以上の長さにする必要があり、次の 4 つのセットのうち 3 つから文字を含める必要があります。大文字、小文字、10 進数、記号です。 [docker ログ](https://docs.docker.com/engine/reference/commandline/logs/) コマンドを実行することでエラー ログを調査することができます。
   >
   > 既定では、これにより SQL Server 2019 Developer Edition のコンテナーが作成されます。

   次の表は、前の `docker run` の例のパラメーターについて説明しています。

   | パラメーター | 説明 |
   |-----|-----|
   | **-e "ACCEPT_EULA=Y"** |  **ACCEPT_EULA** 変数を任意の値に設定し、[使用許諾契約書](https://go.microsoft.com/fwlink/?LinkId=746388)の承諾を確定します。 SQL Server イメージの設定が必要です。 |
   | **-e "SA_PASSWORD=\<YourStrong@Passw0rd\>"** | 8 文字以上の、[SQL Server のパスワード要件](../relational-databases/security/password-policy.md)を満たす強力なパスワードを指定します。 SQL Server イメージの設定が必要です。 |
   | **-p 1433:1433** | ホスト環境の TCP ポート (最初の値) とコンテナーの TCP ポート (2 番目の値) をマップします。 この例では、SQL Server がコンテナー内の TCP 1433 上でリッスンしており、これがホスト上のポート 1433 に公開されています。 |
   | **--name sql1** | ランダムに生成された名前ではなく、コンテナーのカスタム名を指定します。 複数のコンテナーを実行する場合は、この同じ名前を再利用することはできません。 |
   | **-h sql1** | コンテナーのホスト名を指定していない場合にこれを明示的に設定するために使用されます。既定では、ランダムに生成されたシステム GUID であるコンテナー ID に設定されています。 |
   | **mcr.microsoft.com/mssql/server:2019-latest** | SQL Server 2019 Ubuntu Linux コンテナー イメージ。 |

3. Docker コンテナーを表示するには、`docker ps` コマンドを使用します。

   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker ps -a
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker ps -a
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker ps -a
   ```
   ::: zone-end

   次のスクリーンショットのような出力が表示されます。

   ![Docker ps コマンドの出力](./media/sql-server-linux-setup-docker/docker-ps-command.png)

4. **[STATUS]** 列に **[Up]** の状態が表示されている場合、SQL Server はコンテナーで実行されており、 **[PORTS]** 列に指定されたポートでリッスンしています。 SQL Server コンテナーの **[STATUS]** 列に **[Exited]** と表示されている場合、「[SQL Server Docker コンテナーのトラブルシューティング](sql-server-linux-docker-container-troubleshooting.md)」を参照してください。

前述の `-h` (ホスト名) パラメーターは、コンテナーの内部名をカスタム値に変更します。 これにより、コンテナーの内部名がカスタム値に変更されます。 これは、次の Transact-SQL クエリで返される名前です。

```sql
SELECT @@SERVERNAME,
    SERVERPROPERTY('ComputerNamePhysicalNetBIOS'),
    SERVERPROPERTY('MachineName'),
    SERVERPROPERTY('ServerName')
```

ターゲット コンテナーを特定しやすくするため、`-h` と `--name` を同じ値に設定することをお勧めします。


5. 最後の手順として、`SA_PASSWORD` が `ps -eax` 出力に表示され、同じ名前の環境変数に格納されるため、SA パスワードを変更します。 以下の手順を参照してください。


::: moniker-end
<!--End of 2019 "Pull and run" section-->



## <a name="change-the-sa-password"></a><a id="sapassword"></a> SA パスワードの変更

<!-- This section was pasted in from includes/sql-server-linux-change-docker-password.md, to better support zone pivots. 2019/02/11 -->

**SA** アカウントは、セットアップ時に作成される SQL Server インスタンスのシステム管理者です。 SQL Server のコンテナーを作成した後、そのコンテナーで `echo $SA_PASSWORD` を実行すると、指定した環境変数 `SA_PASSWORD` が検索できるようになります。 セキュリティのため、SA のパスワードを変更してください。

1. SA ユーザーに使用する強力なパスワードを選択します。

1. `docker exec` を使用して **sqlcmd** を実行し、Transact-SQL でパスワードを変更します。 次の例では、古いパスワード `<YourStrong!Passw0rd>` と新しいパスワード `<YourNewStrong!Passw0rd>` を実際のパスワード値に置き換えます。

   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P "<YourStrong@Passw0rd>" \
      -Q 'ALTER LOGIN SA WITH PASSWORD="<YourNewStrong@Passw0rd>"'
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourStrong@Passw0rd>" `
      -Q "ALTER LOGIN SA WITH PASSWORD='<YourNewStrong@Passw0rd>'"
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourStrong!Passw0rd>" `
      -Q "ALTER LOGIN SA WITH PASSWORD='<YourNewStrong@Passw0rd>'"
   ```
   ::: zone-end

## <a name="connect-to-sql-server"></a>SQL Server への接続

次の手順では、SQL Server コマンドライン ツールの [**sqlcmd**](../tools/sqlcmd-utility.md) をコンテナー内で使用し、SQL Server に接続します。

1. 実行中のコンテナー内で対話型の Bash シェルを開始するには、`docker exec -it` コマンドを使用します。 次の例の `sql1` は、コンテナーを作成したときに `--name` パラメーターによって指定された名前です。

   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker exec -it sql1 "bash"
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker exec -it sql1 "bash"
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker exec -it sql1 "bash"
   ```
   ::: zone-end

2. コンテナー内では sqlcmd とローカル接続してください。 既定では sqlcmd はパスにないため、完全なパスを指定する必要があります。

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P "<YourNewStrong@Passw0rd>"
   ```

   > [!TIP]
   > コマンド ラインでパスワードを省略すると、入力を求められます。

3. 成功すると、**sqlcmd** コマンド プロンプト `1>` が表示されます。

## <a name="create-and-query-data"></a>データの作成とクエリ

後続のセクションでは **sqlcmd** と Transact-SQL to を使用し、新しいデータベースを作成し、データを追加し、クエリを実行します。

### <a name="create-a-new-database"></a>新しいデータベースの作成

次の手順では、`TestDB` という名前の新しいデータベースを作成します。

1. **sqlcmd** のコマンド プロンプトに次の Transact-SQL コマンドを貼り付け、テスト データベースを作成します。

   ```sql
   CREATE DATABASE TestDB
   ```

2. 次の行に、サーバー上のすべてのデータベースの名前を返すクエリを記述します。

   ```sql
   SELECT Name from sys.Databases
   ```

3. 前の 2 つのコマンドは、すぐに実行されていません。 新しい行に「`GO`」と入力し、前のコマンドを実行します。

   ```sql
   GO
   ```

### <a name="insert-data"></a>データの挿入

次に、新しいテーブル `Inventory` を作成し、2 つの新しい行を挿入します。

1. **sqlcmd** のコマンド プロンプトで、コンテキストを新しい `TestDB` データベースに切り替えます。

   ```sql
   USE TestDB
   ```

2. `Inventory` という名前の新しいテーブルを作成します。

   ```sql
   CREATE TABLE Inventory (id INT, name NVARCHAR(50), quantity INT)
   ```

3. 新しいテーブルにデータを挿入します。

   ```sql
   INSERT INTO Inventory VALUES (1, 'banana', 150); INSERT INTO Inventory VALUES (2, 'orange', 154);
   ```

4. 「`GO`」と入力して前のコマンドを実行します。

   ```sql
   GO
   ```

### <a name="select-data"></a>データの選択

ここで、`Inventory` テーブルからデータを返すクエリを実行します。

1. **sqlcmd** のコマンド プロンプトで、数量が 152 より大きい`Inventory` テーブルから行を返すクエリを入力します。

   ```sql
   SELECT * FROM Inventory WHERE quantity > 152;
   ```

2. 次のコマンドを実行します。

   ```sql
   GO
   ```

### <a name="exit-the-sqlcmd-command-prompt"></a>sqlcmd コマンド プロンプトの終了

1. **sqlcmd** セッションを終了するには、「`QUIT`」と入力します。

   ```sql
   QUIT
   ```

2. コンテナー内で対話型のコマンド プロンプトを終了するには、`exit` と入力します。 コンテナーは、対話型の Bash シェルを終了した後も引き続き実行されます。

## <a name="connect-from-outside-the-container"></a><a id="connectexternal"></a> コンテナーの外からの接続

SQL 接続をサポートする外部の Linux、Windows、macOS ツールから、Docker コンピューターの SQL Server インスタンスに接続することもできます。

次の手順ではコンテナーの外で **sqlcmd** を使用して、コンテナーで実行されている SQL Server に接続します。 この手順は、コンテナーの外に SQL Server コマンド ライン ツールがインストール済みであることを前提としています。 他のツールを使用する場合にも同じ原則が適用されますが、接続するプロセスはツールごとに固有です。

1. コンテナーをホストしているコンピューターの IP アドレスを探します。 Linux の場合、 **ifconfig** または **ip addr** を使用します。Windows の場合、**ipconfig** を使用します。

1. この例では、**sqlcmd** ツールをクライアント マシン上にインストールします。 詳細については、[Windows 上での sqlcmd のインストール](../tools/sqlcmd-utility.md)または [Linux 上での sqlcmd のインストール](sql-server-linux-setup-tools.md)に関するページを参照してください。

1. コンテナーのポート 1433 にマップされた IP アドレスとポートを指定して sqlcmd を実行します。 この例では、ホスト マシン上の同じポート 1433 です。 ホスト マシン上でマップされた別のポートを指定した場合は、ここにそれを使用します。 ファイアウォールで適切な受信ポートを開き、接続を許可する必要もあります。

   ::: zone pivot="cs1-bash"
   ```bash
   sqlcmd -S <ip_address>,1433 -U SA -P "<YourNewStrong@Passw0rd>"
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   sqlcmd -S <ip_address>,1433 -U SA -P "<YourNewStrong@Passw0rd>"
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   sqlcmd -S <ip_address>,1433 -U SA -P "<YourNewStrong@Passw0rd>"
   ```
   ::: zone-end

1. Transact-SQL コマンドを実行します。 終わったら、`QUIT` と入力します。

SQL Server に接続するその他の一般的なツールは次のとおりです。

- [Visual Studio Code](../tools/visual-studio-code/sql-server-develop-use-vscode.md)
- [Windows の SQL Server Management Studio (SSMS)](sql-server-linux-manage-ssms.md)
- [Azure Data Studio](../azure-data-studio/what-is.md)
- [mssql-cli (プレビュー)](https://github.com/dbcli/mssql-cli/blob/master/doc/usage_guide.md)
- [PowerShell Core](sql-server-linux-manage-powershell-core.md)

## <a name="remove-your-container"></a>コンテナーの削除

このチュートリアルで使用した SQL Server のコンテナーを削除する場合は、次のコマンドを実行します。

::: zone pivot="cs1-bash"
```bash
sudo docker stop sql1
sudo docker rm sql1
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker stop sql1
docker rm sql1
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker stop sql1
docker rm sql1
```
::: zone-end

> [!WARNING]
> コンテナーを完全に停止して削除すると、コンテナー内のすべての SQL Server データが削除されます。 データを保持する必要がある場合は、[コンテナーからバックアップ ファイルを作成してコピーする](tutorial-restore-backup-in-sql-server-container.md)か、[コンテナー データを永続化する手法](sql-server-linux-docker-container-configure.md#persist)を使用します。

## <a name="docker-demo"></a>Docker のデモ

Docker の SQL Server コンテナー イメージを使用すると、開発とテストの改善のためにどのように Docker を使用できるかを知りたくなるかもしれません。 次のビデオは、継続的インテグレーションと展開シナリオでどのように Docker を使用できるかを説明しています。

> [!VIDEO https://channel9.msdn.com/Events/Connect/2017/T152/player]

## <a name="next-steps"></a>次のステップ

データベース バックアップファイルをコンテナーに復元する方法については、「[Restore a SQL Server database in a Linux Docker container](tutorial-restore-backup-in-sql-server-container.md)」(Linux の Docker コンテナーで SQL Server データベースを復元する) を参照してください。 [複数のコンテナー](sql-server-linux-docker-container-deployment.md#multiple)の実行、[データ永続化](sql-server-linux-docker-container-configure.md#persist)、[トラブルシューティング](sql-server-linux-docker-container-troubleshooting.md)など、その他のシナリオを試してください。

リソース、フィードバック、既知の問題について、[mssql-docker GitHub リポジトリ](https://github.com/Microsoft/mssql-docker)も参照してください。