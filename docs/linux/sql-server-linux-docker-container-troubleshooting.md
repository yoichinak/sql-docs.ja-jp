---
title: SQL Server Docker コンテナーのトラブルシューティング
description: Linux Docker コンテナーで SQL Server イメージを使用する場合に発生する一般的なエラーを解決するさまざまなトラブルシューティングの方法について説明します
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.custom: contperfq1
ms.date: 09/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
zone_pivot_groups: cs1-command-shell
ms.openlocfilehash: 0a58ad0e4271833c7aef24333b14a61ef80a16c9
ms.sourcegitcommit: 678f513b0c4846797ba82a3f921ac95f7a5ac863
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2020
ms.locfileid: "89511585"
---
# <a name="troubleshooting-sql-server-docker-containers"></a>SQL Server Docker コンテナーのトラブルシューティング

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

この記事では SQL Server Docker コンテナーをデプロイして使用するときに発生する一般的なエラーおよび、その問題の解決に役立つトラブルシューティング方法について説明します。

## <a name="docker-command-errors"></a>Docker コマンドのエラー

いずれかの `docker` コマンドでエラーが発生した場合は、docker サービスが実行されていることを確認し、高度な権限を使用して実行してみてください。

たとえば、Linux 上では、`docker` コマンドの実行時に次のエラーが表示される場合があります。

```output
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

Linux 上でこのエラーが発生した場合は、前に `sudo` を付けて同じコマンドを実行してみてください。 これが失敗した場合は、docker サービスが実行されていることを確認し、必要に応じて開始します。

```bash
sudo systemctl status docker
sudo systemctl start docker
```

Windows では、PowerShell またはコマンド プロンプトを管理者として起動していることを確認します。

## <a name="sql-server-container-startup-errors"></a>SQL Server コンテナーのスタートアップ エラー

SQL Server コンテナーの実行に失敗する場合は、次のテストを試してください。

- `failed to create endpoint CONTAINER_NAME on network bridge. Error starting proxy: listen tcp 0.0.0.0:1433 bind: address already in use.` などのエラーが表示される場合、既に使用されているポートにコンテナー ポート 1433 をマップしようとしています。 これは、ホスト マシン上で SQL Server をローカルに実行している場合に発生する可能性があります。 また、2 つの SQL Server コンテナーを開始し、両方を同じホスト ポートにマップしようとした場合にも発生する可能性があります。 この状況が発生した場合は、`-p` パラメーターを使用して、コンテナー ポート 1433 を別のホスト ポートにマップします。 次に例を示します。 

    <!--SQL Server 2017 on Linux -->
    ::: moniker range="= sql-server-linux-2017 || = sql-server-2017"
    
    ::: zone pivot="cs1-bash"
    ```bash
    docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d mcr.microsoft.com/mssql/server:2017-latest`.
    ```
    ::: zone-end
    
    ::: zone pivot="cs1-powershell"
    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2017-latest`.
    ```
    ::: zone-end
    
    ::: zone pivot="cs1-cmd"
    ```cmd
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2017-latest`.
    ```
    ::: zone-end
    
    ::: moniker-end
    
    <!--SQL Server 2019 on Linux-->
    ::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"
    
    ::: zone pivot="cs1-bash"
    ```bash
    docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-latest`.
    ```
    ::: zone-end
    
    ::: zone pivot="cs1-powershell"
    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-latest`.
    ```
    ::: zone-end
    
    ::: zone pivot="cs1-cmd"
    ```cmd
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-latest`.
    ```
    ::: zone-end
    
    ::: moniker-end

- コンテナーを起動しようとしたときに `Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.30tdout=1&tail=all: dial unix /var/run/docker.sock: connect: permission denied` のようなエラーが表示される場合、Ubuntu の docker グループに自分のユーザーを追加します。 その後、この変更が新しいセッションに影響するため、ログアウトしてもう一度ログインします。 

   ```bash
    usermod -aG docker $USER
   ```

- コンテナーからのエラー メッセージがあるかどうかを確認します。

   ```bash
   docker logs e69e056c702d
   ```

- クイックスタートの記事の「[前提条件](quickstart-install-connect-docker.md#requirements)」セクションで指定されている最小メモリおよびディスク要件を満たしていることを確認します。

- コンテナー管理ソフトウェアを使用している場合は、ルートとして実行されているコンテナー プロセスがサポートされていることを確認します。 コンテナー内の sqlservr プロセスは、ルートとして実行されます。

- お使いの SQL Server Docker コンテナーが開始した直後に終了する場合は、お使いの docker のログを確認します。 Windows の PowerShell で `docker run` コマンドを使用する場合、単一引用符ではなく二重引用符を使用します。 PowerShell Core では、単一引用符を使用します。

- 「[SQL Server のセットアップ ログとエラー ログ](#errorlogs)」を確認してください。

## <a name="enable-dump-captures"></a>ダンプ キャプチャを有効にする

SQL Server プロセスがコンテナーの内部で失敗している場合は、**SYS_PTRACE** が有効になった新しいコンテナーを作成する必要があります。 これにより、プロセスをトレースするための Linux 機能が追加されます。これは、例外発生時にダンプ ファイルを作成するために必要です。 ダンプ ファイルは、問題のトラブルシューティングを支援するためにサポートによって使用できます。 次の docker run コマンドを使用すると、この機能が有効になります。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

::: zone pivot="cs1-bash"
```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -e 'MSSQL_PID=Developer' --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

::: zone pivot="cs1-bash"
```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -e 'MSSQL_PID=Developer' --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: moniker-end

## <a name="sql-server-connection-failures"></a>SQL Server 接続の失敗

コンテナー内で実行されている SQL Server インスタンスに接続できない場合は、次のテストを試してください。

- `docker ps -a` 出力の **STATUS** 列を参照して、SQL Server コンテナーが実行されていることを確認します。 そうでない場合は、`docker start <Container ID>` を使用して開始します。

- (1433 ではなく) 既定以外のホスト ポートにマップした場合は、接続文字列内でポートを指定していることを確認してください。 ポート マッピングは、`docker ps -a` 出力の **PORTS** 列に表示されます。 たとえば、次のコマンドでは、sqlcmd をポート 1401 上でリッスンしているコンテナーに接続します。

    ::: zone pivot="cs1-bash"
    ```bash
    sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
    ```
    ::: zone-end

    ::: zone pivot="cs1-powershell"
    ```PowerShell
    sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
    ```
    ::: zone-end

    ::: zone pivot="cs1-cmd"
    ```cmd
    sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
    ```
    ::: zone-end

- 既存のマップ済みデータ ボリュームまたはデータ ボリューム コンテナーと共に `docker run` を使用した場合、SQL Server では `SA_PASSWORD` の値が無視されます。 代わりに、事前に構成された SA ユーザーのパスワードが、データ ボリュームまたはデータ ボリューム コンテナー内の SQL Server データから使用されます。 アタッチ先のデータに関連付けられている SA パスワードを使用していることを確認します。

- 「[SQL Server のセットアップ ログとエラー ログ](#errorlogs)」を確認してください。

## <a name="sql-server-availability-groups"></a>SQL Server の可用性グループ

SQL Server の可用性グループと共に Docker を使用している場合は、2 つの追加要件があります。

- レプリカ通信に使用されるポートをマップします (既定値は 5022)。 たとえば、`docker run` コマンドの一部として `-p 5022:5022` を指定します。

- `docker run` コマンドの `-h YOURHOSTNAME` パラメーターを使用して、コンテナーのホスト名を明示的に設定します。 このホスト名は、可用性グループを構成するときに使用されます。 `-h` を使用して指定しない場合、既定の**コンテナー ID** となります。

## <a name="sql-server-setup-and-error-logs"></a><a id="errorlogs"></a> SQL Server のセットアップ ログとエラー ログ

SQL Server のセットアップ ログとエラー ログは、 **/var/opt/mssql/log** 内で確認できます。 コンテナーが実行されていない場合は、まずコンテナーを開始します。 次に、対話型のコマンド プロンプトを使用して、ログを検査します。 コンテナー ID は、`docker ps` コマンドの実行で取得できます。

```bash
docker start <ContainerID>
docker exec -it <ContainerID> "bash"
```

コンテナーの内部の bash セッションから、次のコマンドを実行します。

```bash
cd /var/opt/mssql/log
cat setup*.log
cat errorlog
```

> [!TIP]
> コンテナーの作成時にホスト ディレクトリを **/var/opt/mssql** にマウントした場合は、代わりに、ホスト上のマップされたパスにある **log** サブディレクトリを調べることができます。

## <a name="execute-commands-in-a-container"></a>コンテナー内でコマンドを実行する

実行中のコンテナーがある場合は、ホスト ターミナルからコンテナー内でコマンドを実行できます。

コンテナー ID を取得するには、次のように実行します。

```bash
docker ps -a
```

コンテナー内で bash ターミナルを開始するには、次のように実行します。

```bash
docker exec -it <Container ID> /bin/bash
```

これで、コンテナーの内部のターミナルで実行する場合と同じようにコマンドを実行できるようになりました。 終わったら、`exit` と入力します。 これにより対話型コマンド セッションが終了しますが、コンテナーは引き続き実行されます。

## <a name="next-steps"></a>次のステップ

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

- [クイックスタート](quickstart-install-connect-docker.md?view=sql-server-2017)に従って、Docker 上で SQL Server 2017 のコンテナー イメージを開始します。

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

- [クイックスタート](quickstart-install-connect-docker.md?view=sql-server-ver15)に従って、Docker 上で SQL Server 2019 のコンテナー イメージを開始する。

::: moniker-end

- [SQL Server Docker コンテナーをデプロイして接続する](sql-server-linux-docker-container-deployment.md)

- [Docker コンテナーに追加できる構成とカスタマイズを確認する](sql-server-linux-docker-container-configure.md)

- [SQL Server Docker コンテナーをセキュリティで保護する](sql-server-linux-docker-container-security.md)