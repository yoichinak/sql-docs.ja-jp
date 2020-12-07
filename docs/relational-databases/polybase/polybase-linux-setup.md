---
title: Linux への PolyBase のインストール
titlesuffix: SQL Server
description: Linux に SQL Server PolyBase をインストールする方法について説明します。 PolyBase を使用すると、リモート データ ソースに対して外部クエリを実行することができます。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: dakryze
ms.date: 8/18/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: 6bed37e6fe0451e45e9d99fd9c15d03d12a30a4b
ms.sourcegitcommit: 19ae05bc69edce1e3b3d621d7fdd45ea5f74969d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/18/2020
ms.locfileid: "88564652"
---
# <a name="install-polybase-on-linux"></a>Linux への PolyBase のインストール

[!INCLUDE [sqlserver2019-linux](../../includes/applies-to-version/sqlserver2019-linux.md)]

Linux に [PolyBase](../../relational-databases/polybase/polybase-guide.md) (`mssql-server-polybase` および `mssql-server-polybase-hadoop`) をインストールする手順を以下に示します。 PolyBase を使用すると、リモート データ ソースに対して外部クエリを実行することができます。

>[!NOTE]
> PolyBase をインストールする前に、まず [SQL Server 2019 をインストール](../../linux/sql-server-linux-setup.md#platforms)します。 これにより、`mssql-server-polybase` および `mssql-server-polybase-hadoop` パッケージをインストールするときに使用するキーとリポジトリが構成されます。

>[!NOTE]
>
> - PolyBase は、Linux 上の SQL Server 2017 ではサポートされていません。
> - Linux での PolyBase のスケール アウトは、現在ご利用いただけません。

ご利用のオペレーティング システムに PolyBase をインストールします。

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

## <a name="install-on-rhel"></a><a name="RHEL"></a>RHEL へのインストール

Red Hat Enterprise Linux に `mssql-server-polybase` をインストールするには、次のコマンドを使用します。 

```bash
sudo yum install -y mssql-server-polybase
```

SQL Server インスタンスの再起動を求めるメッセージが表示されます。 これを行うには、次のコマンドを使用します。

```bash
sudo systemctl restart mssql-server
```

>[!NOTE]
>インストール後に、[PolyBase 機能を有効にする](#enable)必要があります。

次のコマンドを使用して `mssql-server-polybase-hadoop` をインストールします。 

```bash
sudo yum install -y mssql-server-polybase-hadoop
```

PolyBase Hadoop パッケージは次のパッケージに依存します。
- `mssql-server`
- `mssql-server-polybase`
- `mssql-server-extensibility`
- `mssql-zulu-jre-11`. 

インストール中に `launchpadd` を再起動するように求めるメッセージが表示されます。 これを行うには、次のコマンドを使用します。

```bash
sudo systemctl restart mssql-launchpadd
```

>[!NOTE]
>インストール後に、[Hadoop 接続レベルを設定する](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md#c-set-hadoop-connectivity)必要があります。

オフライン インストールが必要な場合は、[リリース ノート](../../linux/sql-server-linux-release-notes.md)の PolyBase パッケージのダウンロードを参照してください。 次に、[SQL Server のインストール](../../linux/sql-server-linux-setup.md#offline)の記事で説明されているのと同じオフライン インストール手順を使用します。

## <a name="install-on-ubuntu"></a><a name="ubuntu"></a>Ubuntu へのインストール

Ubuntu に `mssql-server-polybase` をインストールするには、次のコマンドを使用します。 

```bash
sudo apt-get install mssql-server-polybase
```

SQL Server インスタンスの再起動を求めるメッセージが表示されます。 これを行うには、次のコマンドを使用します。

```bash
sudo systemctl restart mssql-server
```

>[!NOTE]
>インストール後に、[PolyBase 機能を有効にする](#enable)必要があります。

オフライン インストールが必要な場合は、[リリース ノート](../../linux/sql-server-linux-release-notes.md)の PolyBase パッケージのダウンロードを参照してください。 次に、[SQL Server のインストール](../../linux/sql-server-linux-setup.md#offline)の記事で説明されているのと同じオフライン インストール手順を使用します。

次のコマンドを使用して `mssql-server-polybase-hadoop` をインストールします。 

```bash
sudo apt-get install mssql-server-polybase-hadoop
```

PolyBase Hadoop パッケージは次のパッケージに依存します。
- `mssql-server`
- `mssql-server-polybase`
- `mssql-server-extensibility`
- `mssql-zulu-jre-11`. 

インストール中に `launchpadd` を再起動するように求めるメッセージが表示されます。 これを行うには、次のコマンドを使用します。

```bash
sudo systemctl restart mssql-launchpadd
```

>[!NOTE]
>インストール後に、[Hadoop 接続レベルを設定する](../../relational-databases/polybase/polybase-configure-hadoop.md#configure-hadoop-connectivity)必要があります。

## <a name="install-on-sles"></a><a name="SLES"></a>SLES へのインストール

SUSE Linux Enterprise Server に `mssql-server-polybase` をインストールするには、次のコマンドを使用します。 

```bash
sudo zypper install mssql-server-polybase
```

SQL Server インスタンスの再起動を求めるメッセージが表示されます。 これを行うには、次のコマンドを使用します。

```bash
sudo systemctl restart mssql-server
```

>[!NOTE]
>インストール後に、[PolyBase 機能を有効にする](#enable)必要があります。

オフライン インストールが必要な場合は、[リリース ノート](../../linux/sql-server-linux-release-notes.md)の PolyBase パッケージのダウンロードを参照してください。 次に、[SQL Server のインストール](../../linux/sql-server-linux-setup.md#offline)の記事で説明されているのと同じオフライン インストール手順を使用します。


## <a name="enable-polybase"></a><a name="enable"></a> PolyBase を有効にする

インストールが完了したら、PolyBase を有効にしてその機能にアクセスできるようにする必要があります。 インストールされている SQL Server インスタンスに接続し、次の Transact-SQL コマンドを使用して有効にします。

```sql
exec sp_configure @configname = 'polybase enabled', @configvalue = 1;
RECONFIGURE WITH OVERRIDE;
```

## <a name="update-polybase"></a>PolyBase を更新する

`mssql-server-polybase` が既にインストールされている場合、次のコマンドを使用して最新バージョンに更新できます。

### <a name="rhel"></a>RHEL

```bash
sudo yum remove -y mssql-server-polybase-hadoop
sudo yum remove -y mssql-server-polybase
sudo yum check-update
sudo yum install -y mssql-server-polybase
sudo yum install -y mssql-server-polybase-hadoop
```

SQL Server インスタンスの再起動を求めるメッセージが表示されます。 これを行うには、次のコマンドを使用します。

```
sudo systemctl restart mssql-server
```

### <a name="ubuntu"></a>Ubuntu

```bash
sudo apt-get remove mssql-server-polybase-hadoop
sudo apt-get remove mssql-server-polybase
sudo apt-get update 
sudo apt-get install mssql-server-polybase
sudo apt-get remove mssql-server-polybase-hadoop
```

SQL Server インスタンスの再起動を求めるメッセージが表示されます。 これを行うには、次のコマンドを使用します。

```
sudo systemctl restart mssql-server
```

### <a name="sles"></a>SLES

```bash
sudo zypper remove mssql-server-polybase
sudo zypper refresh
sudo zypper install mssql-server-polybase
```

SQL Server インスタンスの再起動を求めるメッセージが表示されます。 これを行うには、次のコマンドを使用します。

```
sudo systemctl restart mssql-server
```

>[!NOTE]
>インストール後に、[PolyBase 機能を有効にする](#enable)必要があります。

## <a name="next-steps"></a>次のステップ

Linux 上の PolyBase は、次のデータ ソースにアクセスできます。 PolyBase が有効になっているこれらのソースから外部テーブルを作成する方法の詳細については、提供されているリンクを参照してください。 

- [SQL Server、SQL Database、Azure Synapse Analytics)](../../relational-databases/polybase/polybase-configure-sql-server.md)
- [Hadoop](../../relational-databases/polybase/polybase-configure-hadoop.md)
- [Azure Blob Storage](../../relational-databases/polybase/polybase-configure-azure-blob-storage.md)
- [Oracle](../../relational-databases/polybase/polybase-configure-oracle.md)
- [Teradata](../../relational-databases/polybase/polybase-configure-teradata.md)
- [MongoDB (& Cosmos DB)](../../relational-databases/polybase/polybase-configure-mongodb.md)

これを使用する方法について詳しくは、[CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) に関する Transact-SQL 参照記事をご覧ください。
