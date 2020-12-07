---
title: SQL Server Integration Services on Linux をインストールする
description: この記事では、SQL Server Integration Services (SSIS) on Linux をインストール方法について説明します。 SSIS は、Ubuntu 16.04 および Red Hat Enterprise Linux にインストールできます。
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
ms.date: 01/09/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: a8ec33ad6d3c2bfc9c8f3adab2acad2fdb74ce0d
ms.sourcegitcommit: 3ea082c778f6771b17d90fb597680ed334d3e0ec
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/11/2020
ms.locfileid: "88088772"
---
# <a name="install-sql-server-integration-services-ssis-on-linux"></a>SQL Server Integration Services (SSIS) on Linux をインストールする

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

この記事の手順に従って、SQL Server Integration Services (**mssql-server-is**) on Linux をインストールします。 今回の Linux 用の Integration Services のリリースでサポートされる機能の詳細については、[リリース ノート](sql-server-linux-release-notes.md)を参照してください。

次のプラットフォームに SQL Server Integration Services をインストールできます。

- [Ubuntu 16.04](#ubuntu)
- [Red Hat Enterprise Linux](#RHEL)

## <a name="install-ssis-on-ubuntu"></a><a name="ubuntu"></a> Ubuntu に SSIS をインストールする

Ubuntu 上に **mssql-server-is** パッケージをインストールするには、次の手順を行います。

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. パブリック リポジトリの GPG キーをインポートします。

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. SQL Server Ubuntu リポジトリを登録します。

   ```bash
   sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

1. 次のコマンドを実行して SQL Server Integration Services をインストールします。

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server-is
   ```

1. Integration Services をインストールした後、**ssis-conf** を実行します。 詳細については、「[ssis-conf を使用して SSIS on Linux を構成する](sql-server-linux-configure-ssis.md)」を参照してください。

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

1. 構成が完了したら、PATH 環境変数を設定します。

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. パブリック リポジトリの GPG キーをインポートします。

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. SQL Server Ubuntu リポジトリを登録します。

   ```bash
   sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2019.list)"
   ```

1. 次のコマンドを実行して SQL Server Integration Services をインストールします。

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server-is
   ```

1. Integration Services をインストールした後、**ssis-conf** を実行します。 詳細については、「[ssis-conf を使用して SSIS on Linux を構成する](sql-server-linux-configure-ssis.md)」を参照してください。

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

1. 構成が完了したら、PATH 環境変数を設定します。

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

::: moniker-end

### <a name="update-ssis"></a>SSIS を更新する

既に **mssql-server-is** をインストールしている場合は、次のコマンドを使って最新バージョンに更新します。

```bash
sudo apt-get install mssql-server-is
```

### <a name="remove-ssis"></a>SSIS を削除する

**mssql-server-is** を削除するには、次のコマンドを実行します。

```bash
sudo apt-get remove mssql-server-is
```

## <a name="install-ssis-on-rhel"></a><a name="RHEL"></a> RHEL に SSIS をインストールする
RHEL 上に **mssql-server-is** パッケージをインストールするには、次の手順を行います。

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. SQL Server Red Hat リポジトリ構成ファイルをダウンロードします。

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

1. 次のコマンドを実行して SQL Server Integration Services をインストールします。

   ```bash
   sudo yum install -y mssql-server-is
   ```

1. インストール後に **ssis-conf** を実行します。 詳細については、「[ssis-conf を使用して SSIS on Linux を構成する](sql-server-linux-configure-ssis.md)」を参照してください。

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

1. 構成が完了したら、PATH 環境変数を設定します。

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. SQL Server Red Hat リポジトリ構成ファイルをダウンロードします。

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2019.repo
   ```

1. 次のコマンドを実行して SQL Server Integration Services をインストールします。

   ```bash
   sudo yum install -y mssql-server-is
   ```

1. インストール後に **ssis-conf** を実行します。 詳細については、「[ssis-conf を使用して SSIS on Linux を構成する](sql-server-linux-configure-ssis.md)」を参照してください。

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

1. 構成が完了したら、PATH 環境変数を設定します。

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

::: moniker-end

### <a name="update-ssis"></a>SSIS を更新する

既に **mssql-server-is** をインストールしている場合は、次のコマンドを使って最新バージョンに更新します。

```bash
sudo yum update mssql-server-is
```

### <a name="remove-ssis"></a>SSIS を削除する
**mssql-server-is** を削除するには、次のコマンドを実行します。

```bash
sudo yum remove mssql-server-is
```

## <a name="unattended-installation"></a>自動実行インストール

自動実行インストール形式で **ssis-conf setup** を実行するには、次の手順を行います。

1. **-n** (プロンプトなし) オプションを指定します。
1. 環境変数を設定することで、必要な値を指定します。

次の例では、これらのアクションを実行します。

- SSIS をインストールします
- SSIS_PID 環境変数の値を指定することで、Developer エディションを指定します
- ACCEPT_EULA 環境変数の値を指定して、マイクロソフト ソフトウェア ライセンス条項に同意します
- **-n** (プロンプトなし) オプションを指定して、自動実行インストールを実行します。

```
sudo SSIS_PID=Developer ACCEPT_EULA=Y /opt/ssis/bin/ssis-conf -n setup 
```

### <a name="environment-variables-for-unattended-installation"></a>自動実行インストール用の環境変数

| 環境変数 | 説明 |
|---|---|
| ACCEPT_EULA | "Y" のような値に設定すると、SQL Server ライセンス条項に同意します。|
| SSIS_PID | SQL Server のエディションまたはプロダクト キーを設定します。 可能な値を次に示します。<ul><li>評価</li><li>開発者</li><li>Express</li><li>Web</li><li>Standard</li><li>Enterprise</li><li>プロダクト キー</li></ul>プロダクト キーを指定する場合は、 *#####* - *#####* - *#####* - *#####* - *#####* という形式にします。この *#* は文字または数字です。  |
| | |

## <a name="next-steps"></a>次のステップ

Linux 上で SSIS パッケージを実行するには、「[SSIS を使用して SQL Server on Linux 用のデータの抽出、変換、および読み込みを行う](sql-server-linux-migrate-ssis.md)」を参照してください。

Linux 上で SSIS 設定を追加で構成するには、「[ssis-conf を使用して SQL Server Integration Services on Linux を構成する](sql-server-linux-configure-ssis.md)」を参照してください。

## <a name="related-content-about-ssis-on-linux"></a>Linux 上の SSIS の関連コンテンツ

- [SSIS を使用して Linux 上でデータの抽出、変換、読み込みを行う](sql-server-linux-migrate-ssis.md)
- [ssis-conf を使用して SQL Server Integration Services on Linux を構成する](sql-server-linux-configure-ssis.md)
- [Linux での SSIS に関する制限事項と既知の問題](sql-server-linux-ssis-known-issues.md)
- [cron を使用して Linux 上で SQL Server Integration Services パッケージの実行スケジュールを設定する](sql-server-linux-schedule-ssis-packages.md)
