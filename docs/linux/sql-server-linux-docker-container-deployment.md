---
title: SQL Server Docker コンテナーをデプロイして接続する
description: SQL Server を Docker コンテナーにデプロイする方法と、コンテナーの内外から SQL Server に接続するさまざまなツールについて説明します
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.custom: contperfq1
ms.date: 09/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
zone_pivot_groups: cs1-command-shell
ms.openlocfilehash: 380fa9b4cb6941b438d0308be38956659862ce50
ms.sourcegitcommit: 22102f25db5ccca39aebf96bc861c92f2367c77a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2020
ms.locfileid: "92115463"
---
# <a name="deploy-and-connect-to-sql-server-docker-containers"></a>SQL Server Docker コンテナーをデプロイして接続する

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

この記事では、SQL Server Docker コンテナーをデプロイして接続する方法について説明します。

その他の展開シナリオは次のとおりです。

- [Windows](../database-engine/install-windows/install-sql-server.md)
- [Linux](../linux/sql-server-linux-setup.md)
- [Kubernetes - ビッグ データ クラスター](../big-data-cluster/deploy-get-started.md)

> [!NOTE]
> この記事では特に mssql-server-linux イメージを使用することに焦点を当てます。 Windows イメージについては言及しませんが、[msmssql-server-windows Docker Hub ページ](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/)で詳細を確認できます。

> [!IMPORTANT]
> 運用環境のユース ケースで SQL Server コンテナーを実行する前に、[SQL Server コンテナーのサポート ポリシー](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)を読み、サポートされる構成で実行していることを確認してください。

この 6 分間のビデオでは、コンテナーでの SQL Server の実行について説明します。

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2019-in-Containers/player?WT.mc_id=dataexposed-c9-niner]

## <a name="pull-and-run-the-container-image"></a>コンテナー イメージのプルと実行

SQL Server 2017 および SQL Server 2019 用の Docker コンテナー イメージをプルして実行するには、次のクイックスタートの前提条件と手順に従います。

- [Docker を使用して SQL Server 2017 コンテナー イメージを実行する](quickstart-install-connect-docker.md?view=sql-server-2017)
- [Docker を使用して SQL Server 2019 コンテナー イメージを実行する](quickstart-install-connect-docker.md?view=sql-server-ver15)

この構成記事では、以下のセクションで追加の使用シナリオを示します。

## <a name="connect-and-query"></a>接続とクエリ

コンテナーの外部またはコンテナーの内部から、コンテナー内の SQL Server に接続してクエリを実行できます。 次のセクションでは、両方のシナリオについて説明します。

### <a name="tools-outside-the-container"></a>コンテナーの外部のツール

SQL 接続をサポートする外部の Linux、Windows、macOS ツールから、Docker マシン上の SQL Server インスタンスに接続することができます。 いくつかの一般的なツールを次に示します。

- [Azure Data Studio](../azure-data-studio/quickstart-sql-server.md)
- [sqlcmd](sql-server-linux-setup-tools.md)
- [Visual Studio Code](../tools/visual-studio-code/sql-server-develop-use-vscode.md)
- [Windows の SQL Server Management Studio (SSMS)](sql-server-linux-manage-ssms.md)

次の例では、**sqlcmd** を使用して、Docker コンテナー内で実行されている SQL Server に接続します。 接続文字列内の IP アドレスは、コンテナーを実行しているホスト マシンの IP アドレスです。

::: zone pivot="cs1-bash"
```bash
sqlcmd -S 10.3.2.4 -U SA -P '<YourPassword>'
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
sqlcmd -S 10.3.2.4 -U SA -P "<YourPassword>"
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
sqlcmd -S 10.3.2.4 -U SA -P "<YourPassword>"
```
::: zone-end

既定の **1433** ではないホスト ポートをマップした場合は、そのポートを接続文字列に追加します。 たとえば、`docker run` コマンド内で `-p 1400:1433` を指定した場合は、ポート 1400 を明示的に指定して接続します。

::: zone pivot="cs1-bash"
```bash
sqlcmd -S 10.3.2.4,1400 -U SA -P '<YourPassword>'
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
sqlcmd -S 10.3.2.4,1400 -U SA -P "<YourPassword>"
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
sqlcmd -S 10.3.2.4,1400 -U SA -P "<YourPassword>"
```
::: zone-end

### <a name="tools-inside-the-container"></a>コンテナーの内部のツール

SQL Server 2017 以降では、[SQL Server のコマンドライン ツール](sql-server-linux-setup-tools.md)がコンテナー イメージに含まれています。 対話型のコマンド プロンプトを使用してイメージにアタッチすると、ツールをローカルで実行できます。

1. 実行中のコンテナー内で対話型の Bash シェルを開始するには、`docker exec -it` コマンドを使用します。 次の例では、`e69e056c702d` はコンテナー ID です。

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > 常にコンテナー ID 全体を指定する必要はありません。 一意に識別するのに十分な文字を指定するだけでかまいません。 したがって、この例では、完全な ID ではなく `e6` または `e69` を使用すれば十分な可能性があります。 コンテナー ID を確認するには、`docker ps -a` コマンドを実行します。

2. コンテナー内では sqlcmd とローカル接続してください。 既定では sqlcmd はパスにないため、完全なパスを指定する必要があります。

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
    ```

3. sqlcmd が終了したら、「`exit`」と入力します。

4. 対話型コマンド プロンプトでの操作が完了したら、「`exit`」と入力します。 コンテナーは、対話型の Bash シェルを終了した後も引き続き実行されます。

## <a name="check-the-container-version"></a><a id="version"></a> コンテナーのバージョンを確認する

実行中の docker コンテナー内の SQL Server のバージョンを知りたい場合は、次のコマンドを実行して表示します。 `<Container ID or name>` はターゲット コンテナーの ID または名前で置き換えます。 `<YourStrong!Passw0rd>` は SA ログインの SQL Server パスワードで置き換えます。

::: zone pivot="cs1-bash"
```bash
sudo docker exec -it <Container ID or name> /opt/mssql-tools/bin/sqlcmd \
-S localhost -U SA -P '<YourStrong!Passw0rd>' \
-Q 'SELECT @@VERSION'
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker exec -it <Container ID or name> /opt/mssql-tools/bin/sqlcmd `
-S localhost -U SA -P "<YourStrong!Passw0rd>" `
-Q "SELECT @@VERSION"
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker exec -it <Container ID or name> /opt/mssql-tools/bin/sqlcmd ^
-S localhost -U SA -P "<YourStrong!Passw0rd>" ^
-Q "SELECT @@VERSION"
```
::: zone-end

ターゲットの docker コンテナー イメージの SQL Server バージョンとビルド番号を特定することもできます。 次のコマンドでは、**mcr.microsoft.com/mssql/server:2017-latest** イメージの SQL Server バージョンとビルド情報が表示されます。 これは、環境変数 **PAL_PROGRAM_INFO=1** を使用して新しいコンテナーを実行することで行われます。 結果のコンテナーはすぐに終了し、`docker rm` コマンドによって削除されます。

::: zone pivot="cs1-bash"
```bash
sudo docker run -e PAL_PROGRAM_INFO=1 --name sqlver \
-ti mcr.microsoft.com/mssql/server:2019-latest && \
sudo docker rm sqlver
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker run -e PAL_PROGRAM_INFO=1 --name sqlver `
-ti mcr.microsoft.com/mssql/server:2019-latest; `
docker rm sqlver
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker run -e PAL_PROGRAM_INFO=1 --name sqlver ^
-ti mcr.microsoft.com/mssql/server:2019-latest && ^
docker rm sqlver
```
::: zone-end

上記のコマンドでは、次の出力のようなバージョン情報が表示されます。

```output
sqlservr
  Version 15.0.4063.15
  Build ID 8a3bb4cca325e1d0b3071b3a193f6a1d74b440fbd95d2fb18881651a5b9ec8e8
  Build Type release
  Git Version 0335c462
  Built at Fri Aug 28 04:50:27 GMT 2020

PAL
  Build ID cc5ceea1b3d294f7d0166f99932f98c7eacfaaa81bcd7cf23c6a89f785829b63
  Build Type release
  Git Version ae9d66dff
  Built at Fri Aug 28 04:46:48 GMT 2020

Packages
  system.security                         6.2.9200.10,unset,
  system.certificates                     6.2.9200.10,unset,
  secforwarderxplat                       15.0.4063.15
  sqlservr                                15.0.4063.15
  system.common                           10.0.17134.1246.202005133
  system.netfx                            4.7.2.461814
  system                                  6.2.9200.10,unset,
  sqlagent                                15.0.4063.15
```

## <a name="run-a-specific-sql-server-container-image"></a><a id="tags"></a> 特定の SQL Server コンテナー イメージを実行する

> [!NOTE]
> SQL Server 2019 CU3 以降では、Ubuntu 18.04 がサポートされています。 mssql/server で使用可能なタグの一覧は、<https://mcr.microsoft.com/v2/mssql/server/tags/list> でご確認ください。

最新の SQL Server コンテナー イメージを使用したくないシナリオもあります。 特定の SQL Server コンテナー イメージを実行するには、次の手順を使用します。

1. 使用するリリースの Docker **タグ**を特定します。 利用可能なタグを表示するには、[mssql-server-linux Docker Hub ページ](https://hub.docker.com/_/microsoft-mssql-server)を参照してください。

2. タグを使用して SQL Server コンテナー イメージをプルします。 たとえば、2019-CU7-ubuntu-18.04 イメージをプルするには、次のコマンドの `<image_tag>` を `2019-CU7-ubuntu-18.04` に置き換えます。

   ```bash
   docker pull mcr.microsoft.com/mssql/server:<image_tag>
   ```

3. そのイメージを使用して新しいコンテナーを実行するには、`docker run` コマンド内でタグ名を指定します。 次のコマンド内の `<image_tag>` を、実行するバージョンに置き換えます。

   ::: zone pivot="cs1-bash"
   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```
   ::: zone-end

これらの手順は、既存のコンテナーをダウングレードするためにも使用できます。 たとえば、実行中のコンテナーをロールバックまたはダウングレードして、トラブルシューティングやテストを行うことができます。 実行中のコンテナーをダウングレードするには、データ フォルダーの永続化手法を使用する必要があります。 [アップグレードのセクション](#upgrade)で説明したのと同じ手順に従いますが、新しいコンテナーを実行するときに、古いバージョンのタグ名を指定します。

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a name="run-rhel-based-container-images"></a><a id="rhel"></a> RHEL ベースのコンテナー イメージを実行する

SQL Server Linux コンテナー イメージに関するドキュメントは、Ubuntu ベースのコンテナーを指しています。 SQL Server 2019 以降では、Red Hat Enterprise Linux (RHEL) に基づくコンテナーを使用できます。 RHEL のイメージの例は、**mcr.microsoft.com/mssql/rhel/server:2019-CU1-rhel-8** のようになります。

たとえば、次のコマンドでは、RHEL 8 を使用する SQL Server 2019 コンテナー用 Cumulative Update 1 をプルします。

::: zone pivot="cs1-bash"
```bash
sudo docker pull mcr.microsoft.com/mssql/rhel/server:2019-CU1-rhel-8
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker pull mcr.microsoft.com/mssql/rhel/server:2019-CU1-rhel-8
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker pull mcr.microsoft.com/mssql/rhel/server:2019-CU1-rhel-8
```
::: zone-end

::: moniker-end

## <a name="run-production-container-images"></a><a id="production"></a> 実稼働のコンテナー イメージを実行する

前のセクションの[クイックスタート](quickstart-install-connect-docker.md)では、Docker Hub から SQL Server の無償の Developer エディションが実行されます。 Enterprise Edition、Standard Edition、Web Edition などの実稼働のコンテナー イメージを実行する場合でも、ほとんどの情報が適用されます。 しかし、違う点もいくつかあります。それをここで概説します。

- 有効なライセンスを持っている場合にのみ、運用環境内で SQL Server を使用できます。 無償の SQL Server Express 運用ライセンスは[こちら](https://go.microsoft.com/fwlink/?linkid=857693)で入手できます。 SQL Server Standard Edition と Enterprise Edition のライセンスは、[Microsoft ボリューム ライセンス](https://www.microsoft.com/licensing/default.aspx)を通じて入手できます。

- Developer コンテナー イメージは、実稼働エディションを実行するように構成することもできます。 実稼働エディションを実行するには、次の手順に従います。

要件を確認し、[クイックスタート](quickstart-install-connect-docker.md)の手順を実行します。 **MSSQL_PID** 環境変数を使用して、実稼働エディションを指定する必要があります。 次の例は、Enterprise Edition 用の最新の SQL Server 2017 コンテナー イメージを実行する方法を示しています。

::: zone pivot="cs1-bash"
```bash
docker run --name sqlenterprise \
-e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=<YourStrong!Passw0rd>' \
-e 'MSSQL_PID=Enterprise' -p 1433:1433 \
-d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker run --name sqlenterprise `
-e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong!Passw0rd>" `
-e "MSSQL_PID=Enterprise" -p 1433:1433 `
-d "mcr.microsoft.com/mssql/server:2019-latest"
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker run --name sqlenterprise `
-e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong!Passw0rd>" ^
-e "MSSQL_PID=Enterprise" -p 1433:1433 ^
-d "mcr.microsoft.com/mssql/server:2019-latest"
```
::: zone-end

> [!IMPORTANT]
> 値 **Y** を環境変数 **ACCEPT_EULA** に渡し、エディション値を **MSSQL_PID** に渡すことによって、使用する予定の SQL Server のエディションとバージョンに対して有効な既存のライセンスがあることを示しています。 また、Docker コンテナー イメージ内で実行されている SQL Server ソフトウェアの使用は SQL Server ライセンスの条項によって管理されることに同意します。

> [!NOTE]
> **MSSQL_PID** に使用できる値の完全な一覧については、「[Linux 上の SQL Server の設定を環境変数で構成する](sql-server-linux-configure-environment-variables.md)」を参照してください。

## <a name="run-multiple-sql-server-containers"></a><a id="multiple"></a>複数の SQL Server コンテナーを実行する

Docker には、同じホスト マシン上で複数の SQL Server コンテナーを実行する方法が用意されています。 このアプローチは、同じホスト上に複数の SQL Server インスタンスを必要とするシナリオで使用します。 各コンテナーは、異なるポート上で公開される必要があります。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

次の例では、2 つの SQL Server 2017 コンテナーを作成して、ホスト マシン上のポート **1401** と **1402** にマップします。

::: zone pivot="cs1-bash"
```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

次の例では、2 つの SQL Server 2019 コンテナーを作成して、ホスト マシン上のポート **1401** と **1402** にマップします。

::: zone pivot="cs1-bash"
```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-latest
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-latest
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-latest
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: moniker-end

これで、SQL Server の 2 つのインスタンスが別々のコンテナー内で実行されるようになりました。 クライアントは、Docker ホストの IP アドレスとコンテナーのポート番号を使用して、各 SQL Server インスタンスに接続できます。

::: zone pivot="cs1-bash"
```bash
sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
sqlcmd -S 10.3.2.4,1402 -U SA -P '<YourPassword>'
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
sqlcmd -S 10.3.2.4,1402 -U SA -P "<YourPassword>"
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
sqlcmd -S 10.3.2.4,1402 -U SA -P "<YourPassword>"
```
::: zone-end

## <a name="upgrade-sql-server-in-containers"></a><a id="upgrade"></a> コンテナー内の SQL Server をアップグレードする

Docker を使用してコンテナー イメージをアップグレードするには、まず、アップグレードするリリースのタグを特定します。 `docker pull` コマンドを使用して、このバージョンをレジストリからプルします。

```command
docker pull mcr.microsoft.com/mssql/server:<image_tag>
```

これにより、作成した新しいコンテナーの SQL Server イメージが更新されますが、実行中のコンテナー内で SQL Server は更新されません。 これを行うには、最新の SQL Server コンテナー イメージを使用して新しいコンテナーを作成し、その新しいコンテナーにデータを移行する必要があります。

1. 既存の SQL Server コンテナーに対して[データの保持手法](sql-server-linux-docker-container-configure.md#persist)の 1 つを使用していることを確認します。 これにより、同じデータを使用して新しいコンテナーを開始できます。

1. `docker stop` コマンドを使用して SQL Server コンテナーを停止します。

1. `docker run` を使用して新しい SQL Server コンテナーを作成し、マップされたホスト ディレクトリまたはデータ ボリューム コンテナーを指定します。 SQL Server のアップグレードには、必ず特定のタグを使用してください。 新しいコンテナーでは、新しいバージョンの SQL Server が既存の SQL Server データと共に使用されるようになります。

   > [!IMPORTANT]
   > 現時点では、アップグレードは RC1、RC2、GA の間でのみサポートされます。

1. 新しいコンテナー内のデータベースとデータを確認します。

1. 必要に応じて、`docker rm` を使用して古いコンテナーを削除します。

## <a name="next-steps"></a>次のステップ

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

- [クイックスタート](quickstart-install-connect-docker.md?view=sql-server-2017)に従って、Docker 上で SQL Server 2017 のコンテナー イメージを開始する

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

- [クイックスタート](quickstart-install-connect-docker.md?view=sql-server-ver15)に従って、Docker 上で SQL Server 2019 のコンテナー イメージを開始する

::: moniker-end

- [Docker コンテナーに追加できる構成とカスタマイズを確認する](sql-server-linux-docker-container-configure.md)

- リソース、フィードバック、既知の問題について、[mssql-docker GitHub リポジトリ](https://github.com/Microsoft/mssql-docker)を参照する

- [SQL Server Docker コンテナーのトラブルシューティング](sql-server-linux-docker-container-troubleshooting.md)

- [SQL Server のコンテナー用の可用性グループを調べる](sql-server-linux-container-ha-overview.md)

- [SQL Server Docker コンテナーをセキュリティで保護する](sql-server-linux-docker-container-security.md)