---
title: Linux 上の SQL Server 2019 のリリース ノート
description: この記事には、Linux で実行されている SQL Server 2019 のリリース ノートとサポートされている機能が含まれています。 リリース ノートは、最新のリリースと以前のいくつかのリリースに含まれています。
author: VanMSFT
ms.author: vanto
ms.date: 10/01/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 00e2e11f83fb282bbc674f2fdba91810986c69bd
ms.sourcegitcommit: 32135463a8494d9ed1600a58f51819359e3c09dc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2020
ms.locfileid: "91833653"
---
# <a name="release-notes-for-sql-server-2019-on-linux"></a>Linux 上の SQL Server 2019 のリリース ノート

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx-linuxonly.md](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-linuxonly.md)]

次のリリース ノートは、Linux で実行されている SQL Server 2019 に適用されます。 この記事は、リリースごとのセクションに分けられています。 各リリースには、Linux パッケージのダウンロードへのリンクに加えて、CU の変更について説明するサポート記事へのリンクが含まれています。

> [!TIP]
> SQL Server 2019 の Linux 新機能の詳細については、[SQL Server 2019 の新機能](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15#sql-server-on-linux)に関するページを参照してください。

[!INCLUDE [linux-supported-platfoms-2019](../includes/linux-supported-platfoms-2019.md)]

## <a name="tools"></a>ツール

SQL Server を対象とする既存のクライアント ツールの多くは、Linux で実行されている SQL Server をシームレスにターゲットにすることができます。 一部のツールには、Linux で適切に動作させるための特定のバージョン要件がある場合があります。 SQL Server ツールの完全な一覧については、[SQL Server 用の SQL ツールとユーティリティ](../tools/overview-sql-tools.md)に関するページを参照してください。

## <a name="release-history"></a>リリース履歴

SQL Server 2019 のリリース履歴の一覧を次の表に示します。

| Release                   | Version       | リリース日 |
|---------------------------|---------------|--------------|
| [CU8](#cu8)               | 15.0.4073.23  | 2020-10-07   |
| [CU7 (削除済み)](https://support.microsoft.com/help/4570012)     | 15.0.4063.15  | 2020-09-02   |
| [CU6](#cu6)               | 15.0.4053.23  | 2020-08-04   |
| [CU5](#cu5)               | 15.0.4043.16  | 2020-06-22   |
| [CU4](#cu4)               | 15.0.4033.1   | 2020-03-31   |
| [CU3](#cu3)               | 15.0.4023.6   | 2020-03-12   |
| [CU2](#cu2)               | 15.0.4013.40  | 2020-02-13   |
| [CU1](#cu1)               | 15.0.4003.23  | 2020-01-07   |
| [GA](#ga)                 | 15.0.2000.5   | 2019-11-04   |
| [リリース候補](#rc)  | 15.0.1900.25  | 2019-08-21   |

## <a name="how-to-install-updates"></a><a id="cuinstall"></a>更新プログラムのインストール方法

CU リポジトリ (mssql-server-2019) を構成済みの場合は、新規インストールを実行すると、SQL Server パッケージの最新の CU を取得します。 Docker コンテナー イメージが必要な場合は、[Docker エンジン用の Microsoft SQL Server on Linux](https://hub.docker.com/r/microsoft/mssql-server/) の公式イメージを参照してください。 リポジトリ構成の詳細については、[SQL Server on Linux 用のリポジトリの構成](sql-server-linux-change-repo.md)に関するページを参照してください。

既存の SQL Server パッケージを更新する場合は、パッケージごとに適切な更新コマンドを実行して、最新の CU を取得します。 各パッケージの特定の更新手順については、次のインストール ガイドを参照してください。

- [SQL Server パッケージのインストール](sql-server-linux-setup.md#upgrade)
- [フルテキスト検索パッケージのインストール](sql-server-linux-setup-full-text-search.md)
- [SQL Server Integration Services のインストール](sql-server-linux-setup-ssis.md)
- [Linux への SQL Server 2019 Machine Learning Services R および Python のサポートのインストール](sql-server-linux-setup-machine-learning.md)
- [PolyBase パッケージのインストール](../relational-databases/polybase/polybase-linux-setup.md)
- [SQL Server エージェントの有効化](sql-server-linux-setup-sql-agent.md)

## <a name="cu8-september-2020"></a><a id="cu8"></a> CU8 (2020 年 9 月)

これは SQL Server 2019 (15.x) の Cumulative Update 8 (CU8) リリースです。 このリリースの SQL Server データベース エンジンのバージョンは、15.0.4073.23 です。 修正プログラムと機能強化の詳細については、<https://support.microsoft.com/help/4577194> を参照してください。

### <a name="package-details"></a>パッケージの詳細

手動またはオフラインのパッケージ インストールの場合は、次の表の情報を使用して RPM と Debian のパッケージをダウンロードすることができます。

> [!NOTE]
> CU1 以降では、Red Hat 用のオフライン パッケージのインストール リンクが RHEL 8 パッケージを指しています。 RHEL 7 パッケージをお探しの場合は、ダウンロード パス <https://packages.microsoft.com/rhel/7/mssql-server-2019/> を参照してください。
>
> **Ubuntu 18.04** は、CU3 以降の SQL Server 2019 でサポートされるようになりました。 Ubuntu 用のオフライン パッケージのインストール リンクは、Ubuntu 18.04 パッケージを指しています。 Ubuntu 16.04 パッケージをお探しの場合は、ダウンロード パス <https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/> を参照してください。

| Package | パッケージ バージョン | ダウンロード |
|-----|-----|-----|
| Red Hat RPM パッケージ | 15.0.4073.23-4 | [エンジン RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-15.0.4073.23-4.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-ha-15.0.4073.23-4.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-fts-15.0.4073.23-4.x86_64.rpm)</br>[拡張機能 RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-extensibility-15.0.4073.23-4.x86_64.rpm)</br>[Java 拡張機能 RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-extensibility-java-15.0.4073.23-4.x86_64.rpm)</br>[PolyBase RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-polybase-15.0.4073.23-4.x86_64.rpm)|
| SLES RPM パッケージ | 15.0.4073.23-4 | [mssql-server エンジン RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-15.0.4073.23-4.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-ha-15.0.4073.23-4.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-fts-15.0.4073.23-4.x86_64.rpm)</br>[拡張機能 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-15.0.4073.23-4.x86_64.rpm)</br>[Java 拡張機能 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-java-15.0.4073.23-4.x86_64.rpm)</br>[PolyBase RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-polybase-15.0.4073.23-4.x86_64.rpm)|
| Ubuntu 18.04 Debian パッケージ | 15.0.4073.23-4 | [エンジン Debian パッケージ](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server/mssql-server_15.0.4073.23-4_amd64.deb)</br>[高可用性 Debian パッケージ](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.4073.23-4_amd64.deb)</br>[フルテキスト検索 Debian パッケージ](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.4073.23-4_amd64.deb)</br>[拡張機能 Debian パッケージ](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.4073.23-4_amd64.deb)</br>[Java 拡張機能 Debian パッケージ](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.4073.23-4_amd64.deb)</br>[PolyBase RPM パッケージ](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.4073.23-4_amd64.deb)|

## <a name="cu6-july-2020"></a><a id="cu6"></a> CU6 (2020 年 7 月)

これは SQL Server 2019 (15.x) の Cumulative Update 6 (CU6) リリースです。 このリリースの SQL Server データベース エンジンのバージョンは、15.0.4053.23 です。 修正プログラムと機能強化の詳細については、<https://support.microsoft.com/help/4563110> を参照してください。

### <a name="package-details"></a>パッケージの詳細

手動またはオフラインのパッケージ インストールの場合は、次の表の情報を使用して RPM と Debian のパッケージをダウンロードすることができます。

> [!NOTE]
> CU1 以降では、Red Hat 用のオフライン パッケージのインストール リンクが RHEL 8 パッケージを指しています。 RHEL 7 パッケージをお探しの場合は、ダウンロード パス <https://packages.microsoft.com/rhel/7/mssql-server-2019/> を参照してください。
>
> **Ubuntu 18.04** は、CU3 以降の SQL Server 2019 でサポートされるようになりました。 Ubuntu 用のオフライン パッケージのインストール リンクは、Ubuntu 18.04 パッケージを指しています。 Ubuntu 16.04 パッケージをお探しの場合は、ダウンロード パス <https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/> を参照してください。

| Package | パッケージ バージョン | ダウンロード |
|-----|-----|-----|
| Red Hat RPM パッケージ | 15.0.4053.23-2 | [エンジン RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-15.0.4053.23-2.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-ha-15.0.4053.23-2.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-fts-15.0.4053.23-2.x86_64.rpm)</br>[拡張機能 RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-extensibility-15.0.4053.23-2.x86_64.rpm)</br>[Java 拡張機能 RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-extensibility-java-15.0.4053.23-2.x86_64.rpm)</br>[PolyBase RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-polybase-15.0.4053.23-2.x86_64.rpm)|
| SLES RPM パッケージ | 15.0.4053.23-2 | [mssql-server エンジン RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-15.0.4053.23-2.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-ha-15.0.4053.23-2.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-fts-15.0.4053.23-2.x86_64.rpm)</br>[拡張機能 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-15.0.4053.23-2.x86_64.rpm)</br>[Java 拡張機能 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-java-15.0.4053.23-2.x86_64.rpm)</br>[PolyBase RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-polybase-15.0.4053.23-2.x86_64.rpm)|
| Ubuntu 18.04 Debian パッケージ | 15.0.4053.23-2 | [エンジン Debian パッケージ](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server/mssql-server_15.0.4053.23-2_amd64.deb)</br>[高可用性 Debian パッケージ](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.4053.23-2_amd64.deb)</br>[フルテキスト検索 Debian パッケージ](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.4053.23-2_amd64.deb)</br>[拡張機能 Debian パッケージ](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.4053.23-2_amd64.deb)</br>[Java 拡張機能 Debian パッケージ](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.4053.23-2_amd64.deb)</br>[PolyBase RPM パッケージ](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.4053.23-2_amd64.deb)|

## <a name="cu5-june-2020"></a><a id="cu5"></a> CU5 (2020 年 6 月)

これは SQL Server 2019 (15.x) の Cumulative Update 5 (CU5) リリースです。 このリリースの SQL Server データベース エンジンのバージョンは、15.0.4043.16 です。 修正プログラムと機能強化の詳細については、<https://support.microsoft.com/help/4552255> を参照してください。

### <a name="package-details"></a>パッケージの詳細

手動またはオフラインのパッケージ インストールの場合は、次の表の情報を使用して RPM と Debian のパッケージをダウンロードすることができます。

> [!NOTE]
> CU1 以降では、Red Hat 用のオフライン パッケージのインストール リンクが RHEL 8 パッケージを指しています。 RHEL 7 パッケージをお探しの場合は、ダウンロード パス <https://packages.microsoft.com/rhel/7/mssql-server-2019/> を参照してください。
>
> **Ubuntu 18.04** は、CU3 以降の SQL Server 2019 でサポートされるようになりました。 Ubuntu 用のオフライン パッケージのインストール リンクは、Ubuntu 18.04 パッケージを指しています。 Ubuntu 16.04 パッケージをお探しの場合は、ダウンロード パス <https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/> を参照してください。

| Package | パッケージ バージョン | ダウンロード |
|-----|-----|-----|
| Red Hat RPM パッケージ | 15.0.4043.16-4 | [エンジン RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-15.0.4043.16-4.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-ha-15.0.4043.16-4.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-fts-15.0.4043.16-4.x86_64.rpm)</br>[拡張機能 RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-extensibility-15.0.4043.16-4.x86_64.rpm)</br>[Java 拡張機能 RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-extensibility-java-15.0.4043.16-4.x86_64.rpm)</br>[PolyBase RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-polybase-15.0.4043.16-4.x86_64.rpm)|
| SLES RPM パッケージ | 15.0.4043.16-4 | [mssql-server エンジン RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-15.0.4043.16-4.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-ha-15.0.4043.16-4.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-fts-15.0.4043.16-4.x86_64.rpm)</br>[拡張機能 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-15.0.4043.16-4.x86_64.rpm)</br>[Java 拡張機能 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-java-15.0.4043.16-4.x86_64.rpm)</br>[PolyBase RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-polybase-15.0.4043.16-4.x86_64.rpm)|
| Ubuntu 18.04 Debian パッケージ | 15.0.4043.16-4 | [エンジン Debian パッケージ](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server/mssql-server_15.0.4043.16-4_amd64.deb)</br>[高可用性 Debian パッケージ](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.4043.16-4_amd64.deb)</br>[フルテキスト検索 Debian パッケージ](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.4043.16-4_amd64.deb)</br>[拡張機能 Debian パッケージ](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.4043.16-4_amd64.deb)</br>[Java 拡張機能 Debian パッケージ](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.4043.16-4_amd64.deb)</br>[PolyBase RPM パッケージ](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.4043.16-4_amd64.deb)|

## <a name="cu4-april-2020"></a><a id="cu4"></a> CU4 (2020 年 4 月)

これは SQL Server 2019 (15.x) の Cumulative Update 4 (CU4) リリースです。 このリリースの SQL Server データベース エンジンのバージョンは、15.0.4033.1 です。 修正プログラムと機能強化の詳細については、<https://support.microsoft.com/help/4548597> を参照してください。

### <a name="package-details"></a>パッケージの詳細

手動またはオフラインのパッケージ インストールの場合は、次の表の情報を使用して RPM と Debian のパッケージをダウンロードすることができます。

> [!NOTE]
> CU1 以降では、Red Hat 用のオフライン パッケージのインストール リンクが RHEL 8 パッケージを指しています。 RHEL 7 パッケージをお探しの場合は、ダウンロード パス <https://packages.microsoft.com/rhel/7/mssql-server-2019/> を参照してください。
>
> **Ubuntu 18.04** は、CU3 以降の SQL Server 2019 でサポートされるようになりました。 Ubuntu 用のオフライン パッケージのインストール リンクは、Ubuntu 18.04 パッケージを指しています。 Ubuntu 16.04 パッケージをお探しの場合は、ダウンロード パス <https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/> を参照してください。

| Package | パッケージ バージョン | ダウンロード |
|-----|-----|-----|
| Red Hat RPM パッケージ | 15.0.4033.1-2 | [エンジン RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-15.0.4033.1-2.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-ha-15.0.4033.1-2.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-fts-15.0.4033.1-2.x86_64.rpm)</br>[拡張機能 RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-extensibility-15.0.4033.1-2.x86_64.rpm)</br>[Java 拡張機能 RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-extensibility-java-15.0.4033.1-2.x86_64.rpm)</br>[PolyBase RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-polybase-15.0.4033.1-2.x86_64.rpm)|
| SLES RPM パッケージ | 15.0.4033.1-2 | [mssql-server エンジン RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-15.0.4033.1-2.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-ha-15.0.4033.1-2.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-fts-15.0.4033.1-2.x86_64.rpm)</br>[拡張機能 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-15.0.4033.1-2.x86_64.rpm)</br>[Java 拡張機能 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-java-15.0.4033.1-2.x86_64.rpm)</br>[PolyBase RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-polybase-15.0.4033.1-2.x86_64.rpm)|
| Ubuntu 18.04 Debian パッケージ | 15.0.4033.1-2 | [エンジン Debian パッケージ](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server/mssql-server_15.0.4033.1-2_amd64.deb)</br>[高可用性 Debian パッケージ](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.4033.1-2_amd64.deb)</br>[フルテキスト検索 Debian パッケージ](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.4033.1-2_amd64.deb)</br>[拡張機能 Debian パッケージ](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.4033.1-2_amd64.deb)</br>[Java 拡張機能 Debian パッケージ](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.4033.1-2_amd64.deb)</br>[PolyBase RPM パッケージ](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.4033.1-2_amd64.deb)|

## <a name="cu3-march-2020"></a><a id="cu3"></a> CU3 (2020 年 3 月)

これは SQL Server 2019 (15.x) の Cumulative Update 3 (CU3) リリースです。 このリリースの SQL Server Database エンジンのバージョンは、15.0.4023.6 です。 修正プログラムと機能強化の詳細については、<https://support.microsoft.com/help/4538853> を参照してください。

### <a name="package-details"></a>パッケージの詳細

手動またはオフラインのパッケージ インストールの場合は、次の表の情報を使用して RPM と Debian のパッケージをダウンロードすることができます。

> [!NOTE]
> CU1 以降では、Red Hat 用のオフライン パッケージのインストール リンクが RHEL 8 パッケージを指しています。 RHEL 7 パッケージをお探しの場合は、ダウンロード パス <https://packages.microsoft.com/rhel/7/mssql-server-2019/> を参照してください。
>
> **Ubuntu 18.04** は、CU3 以降の SQL Server 2019 でサポートされるようになりました。 Ubuntu 用のオフライン パッケージのインストール リンクは、Ubuntu 18.04 パッケージを指しています。 Ubuntu 16.04 パッケージをお探しの場合は、ダウンロード パス <https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/> を参照してください。

| Package | パッケージ バージョン | ダウンロード |
|-----|-----|-----|
| Red Hat RPM パッケージ | 15.0.4023.6-2 | [エンジン RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-15.0.4023.6-2.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-ha-15.0.4023.6-2.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-fts-15.0.4023.6-2.x86_64.rpm)</br>[拡張機能 RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-extensibility-15.0.4023.6-2.x86_64.rpm)</br>[Java 拡張機能 RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-extensibility-java-15.0.4023.6-2.x86_64.rpm)</br>[PolyBase RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-polybase-15.0.4023.6-2.x86_64.rpm)|
| SLES RPM パッケージ | 15.0.4023.6-2 | [mssql-server エンジン RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-15.0.4023.6-2.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-ha-15.0.4023.6-2.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-fts-15.0.4023.6-2.x86_64.rpm)</br>[拡張機能 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-15.0.4023.6-2.x86_64.rpm)</br>[Java 拡張機能 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-java-15.0.4023.6-2.x86_64.rpm)</br>[PolyBase RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-polybase-15.0.4023.6-2.x86_64.rpm)|
| Ubuntu 18.04 Debian パッケージ | 15.0.4023.6-2 | [エンジン Debian パッケージ](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server/mssql-server_15.0.4023.6-2_amd64.deb)</br>[高可用性 Debian パッケージ](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.4023.6-2_amd64.deb)</br>[フルテキスト検索 Debian パッケージ](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.4023.6-2_amd64.deb)</br>[拡張機能 Debian パッケージ](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.4023.6-2_amd64.deb)</br>[Java 拡張機能 Debian パッケージ](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.4023.6-2_amd64.deb)</br>[PolyBase RPM パッケージ](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.4023.6-2_amd64.deb)|

## <a name="cu2-february-2020"></a><a id="cu2"></a> CU2 (2020 年 2 月)

これは SQL Server 2019 (15.x) の Cumulative Update 2 (CU2) リリースです。 このリリースの SQL Server データベース エンジンのバージョンは、15.0.4013.40 です。 修正プログラムと機能強化の詳細については、<https://support.microsoft.com/help/4536075> を参照してください。

### <a name="package-details"></a>パッケージの詳細

手動またはオフラインのパッケージ インストールの場合は、次の表の情報を使用して RPM と Debian のパッケージをダウンロードすることができます。

> [!NOTE]
> CU1 以降では、Red Hat 用のオフライン パッケージのインストール リンクが RHEL 8 パッケージを指しています。 RHEL 7 パッケージをお探しの場合は、ダウンロード パス <https://packages.microsoft.com/rhel/7/mssql-server-2019/> を参照してください。

| Package | パッケージ バージョン | ダウンロード |
|-----|-----|-----|
| Red Hat RPM パッケージ | 15.0.4013.40-8 | [エンジン RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-15.0.4013.40-8.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-ha-15.0.4013.40-8.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-fts-15.0.4013.40-8.x86_64.rpm)</br>[拡張機能 RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-extensibility-15.0.4013.40-8.x86_64.rpm)</br>[Java 拡張機能 RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-extensibility-java-15.0.4013.40-8.x86_64.rpm)</br>[PolyBase RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-polybase-15.0.4013.40-8.x86_64.rpm)|
| SLES RPM パッケージ | 15.0.4013.40-8 | [mssql-server エンジン RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-15.0.4013.40-8.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-ha-15.0.4013.40-8.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-fts-15.0.4013.40-8.x86_64.rpm)</br>[拡張機能 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-15.0.4013.40-8.x86_64.rpm)</br>[Java 拡張機能 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-java-15.0.4013.40-8.x86_64.rpm)</br>[PolyBase RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-polybase-15.0.4013.40-8.x86_64.rpm)|
| Ubuntu 16.04 Debian パッケージ | 15.0.4013.40-8 | [エンジン Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server/mssql-server_15.0.4013.40-8_amd64.deb)</br>[高可用性 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.4013.40-8_amd64.deb)</br>[フルテキスト検索 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.4013.40-8_amd64.deb)</br>[拡張機能 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.4013.40-8_amd64.deb)</br>[Java 拡張機能 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.4013.40-8_amd64.deb)</br>[PolyBase RPM パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.4013.40-8_amd64.deb)|

## <a name="cu1-january-2020"></a><a id="cu1"></a> CU1 (2020 年 1 月)

これは SQL Server 2019 (15.x) の Cumulative Update 1 (CU1) リリースです。 このリリースに対する SQL Server データベース エンジンのバージョンは 15.0.4003.23 です。 このリリースでの修正プログラムと機能強化の詳細については、<https://support.microsoft.com/en-us/help/4527376> を参照してください。

### <a name="package-details"></a>パッケージの詳細

手動またはオフラインのパッケージ インストールの場合は、次の表の情報を使用して RPM と Debian のパッケージをダウンロードすることができます。

> [!NOTE]
> CU1 以降では、Red Hat 用のオフライン パッケージのインストール リンクが RHEL 8 パッケージを指しています。 RHEL 7 パッケージをお探しの場合は、ダウンロード パス <https://packages.microsoft.com/rhel/7/mssql-server-2019/> を参照してください。

| Package | パッケージ バージョン | ダウンロード |
|-----|-----|-----|
| Red Hat RPM パッケージ | 15.0.4003.23-3 | [エンジン RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-15.0.4003.23-3.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-ha-15.0.4003.23-3.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-fts-15.0.4003.23-3.x86_64.rpm)</br>[拡張機能 RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-extensibility-15.0.4003.23-3.x86_64.rpm)</br>[Java 拡張機能 RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-extensibility-java-15.0.4003.23-3.x86_64.rpm)</br>[PolyBase RPM パッケージ](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-polybase-15.0.4003.23-3.x86_64.rpm)|
| SLES RPM パッケージ | 15.0.4003.23-3 | [mssql-server エンジン RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-15.0.4003.23-3.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-ha-15.0.4003.23-3.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-fts-15.0.4003.23-3.x86_64.rpm)</br>[拡張機能 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-15.0.4003.23-3.x86_64.rpm)</br>[Java 拡張機能 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-java-15.0.4003.23-3.x86_64.rpm)</br>[PolyBase RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-polybase-15.0.4003.23-3.x86_64.rpm)|
| Ubuntu 16.04 Debian パッケージ | 15.0.4003.23-3 | [エンジン Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server/mssql-server_15.0.4003.23-3_amd64.deb)</br>[高可用性 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.4003.23-3_amd64.deb)</br>[フルテキスト検索 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.4003.23-3_amd64.deb)</br>[拡張機能 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.4003.23-3_amd64.deb)</br>[Java 拡張機能 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.4003.23-3_amd64.deb)</br>[PolyBase RPM パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.4003.23-3_amd64.deb)|

## <a name="ga-november-2019"></a><a id="ga"></a> GA (2019 年 11 月)

これは SQL Server 2019 (15.x) の一般提供 (GA) リリースです。 このリリースに対する SQL Server データベース エンジンのバージョンは 15.0.2000.5 です。

### <a name="package-details"></a>パッケージの詳細

手動またはオフラインのパッケージ インストールの場合は、次の表の情報を使用して RPM と Debian のパッケージをダウンロードすることができます。

| Package | パッケージ バージョン | ダウンロード |
|-----|-----|-----|
| Red Hat RPM パッケージ | 15.0.2000.5-5 | [エンジン RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2019/mssql-server-15.0.2000.5-5.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2019/mssql-server-ha-15.0.2000.5-5.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2019/mssql-server-fts-15.0.2000.5-5.x86_64.rpm)</br>[拡張機能 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2019/mssql-server-extensibility-15.0.2000.5-5.x86_64.rpm)</br>[Java 拡張機能 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2019/mssql-server-extensibility-java-15.0.2000.5-5.x86_64.rpm)</br>[PolyBase RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-2019/mssql-server-polybase-15.0.2000.5-5.x86_64.rpm)|
| SLES RPM パッケージ | 15.0.2000.5-5 | [mssql-server エンジン RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-15.0.2000.5-5.x86_64.rpm)</br>[高可用性 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-ha-15.0.2000.5-5.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-fts-15.0.2000.5-5.x86_64.rpm)</br>[拡張機能 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-15.0.2000.5-5.x86_64.rpm)</br>[Java 拡張機能 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-java-15.0.2000.5-5.x86_64.rpm)</br>[PolyBase RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-polybase-15.0.2000.5-5.x86_64.rpm)|
| Ubuntu 16.04 Debian パッケージ | 15.0.2000.5-5 | [エンジン Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server/mssql-server_15.0.2000.5-5_amd64.deb)</br>[高可用性 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.2000.5-5_amd64.deb)</br>[フルテキスト検索 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.2000.5-5_amd64.deb)</br>[拡張機能 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.2000.5-5_amd64.deb)</br>[Java 拡張機能 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.2000.5-5_amd64.deb)</br>[PolyBase RPM パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.2000.5-5_amd64.deb)|

## <a name="release-candidate-august-2019"></a><a id="rc"></a> リリース候補 (2019 年 8 月)

次のセクションでは、リリース候補のパッケージの場所と既知の問題について説明します。 SQL Server 2019 の Linux の新機能の詳細については、[SQL Server 2019 の新機能](../sql-server/what-s-new-in-sql-server-ver15.md)に関するページを参照してください。

### <a name="package-details"></a>パッケージの詳細

手動またはオフラインのパッケージ インストールの場合は、次の表の情報を使用して RPM と Debian のパッケージをダウンロードすることができます。

| Package | パッケージ バージョン | ダウンロード |
|-----|-----|-----|
| Red Hat RPM パッケージ | 15.0.1900.25-1 | [エンジン RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1900.25-1.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1900.25-1.x86_64.rpm)</br>[拡張機能 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1900.25-1.x86_64.rpm)</br>[Java 拡張機能 RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1900.25-1.x86_64.rpm)</br>[PolyBase RPM パッケージ](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1900.25-1.x86_64.rpm)|
| SLES RPM パッケージ | 15.0.1900.25-1 | [mssql-server エンジン RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1900.25-1.x86_64.rpm)</br>[フルテキスト検索 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1900.25-1.x86_64.rpm)</br>[拡張機能 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1900.25-1.x86_64.rpm)</br>[Java 拡張機能 RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1900.25-1.x86_64.rpm)</br>[PolyBase RPM パッケージ](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1900.25-1.x86_64.rpm)|
| Ubuntu 16.04 Debian パッケージ | 15.0.1900.25-1 | [エンジン Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1900.25-1_amd64.deb)</br>[フルテキスト検索 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1900.25-1_amd64.deb)</br>[拡張機能 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1900.25-1_amd64.deb)</br>[Java 拡張機能 Debian パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1900.25-1_amd64.deb)</br>[PolyBase RPM パッケージ](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1900.25-1_amd64.deb)|

## <a name="known-issues"></a>既知の問題

以下のセクションでは、Linux 上の SQL Server 2019 (15.x) の一般提供 (GA) リリースに関する既知の問題について説明します。

### <a name="general"></a>全般

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] がインストールされているホスト名の長さは 15 文字以下でなければなりません。 

    - **解決方法**:/etc/hostname の名前を 15 文字以下に変更します。

- システム時刻を手動で過去の時間に戻して設定すると、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 内の内部システム時刻の更新を停止します。

    - **解決方法**:[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]を再起動します。

- サポートされているのは単一インスタンスのインストールのみです。

    - **解決方法**:特定のホストに複数のインスタンスが必要な場合は、VM または Docker コンテナーの使用を検討してください。 

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager は [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] on Linux には接続できません。

- **sa** ログインの既定の言語は English (英語) です。

    - **解決方法**:**ALTER LOGIN** ステートメントを使用して **sa** ログインの言語を変更します。

- OLEDB プロバイダーによって次の警告がログに記録されます: `Failed to verify the Authenticode signature of 'C:\binn\msoledbsql.dll'. Signature verification of SQL Server DLLs will be skipped. Genuine copies of SQL Server are signed. Failure to verify the Authenticode signature might indicate that this is not an authentic release of SQL Server. Install a genuine copy of SQL Server or contact customer support.`

   - **解決方法**:必要な操作はありません。 OLEDB プロバイダーは SHA256 を使用して署名されています。 SQL Server データベース エンジンでは、署名された .dll は正しく検証されません。

### <a name="databases"></a>データベース

- mssql-conf ユーティリティを使って master データベースを移動することはできません。 他のシステム データベースは mssql-conf で移動できます。

- Windows 上の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] にバックアップされたデータベースを復元する場合は、Transact-SQL ステートメントで **WITH MOVE** 句を使用する必要があります。

- トランスポート層セキュリティ (TLS) の特定のアルゴリズム (暗号スイート) は、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] on Linux では適切に機能しません。 この結果、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] に接続しようとすると接続エラーが発生し、高可用性グループのレプリカ間の接続を確立する際に問題が発生します。

   - **解決方法**:次の手順を実行して、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] on Linux 用の **mssql.conf** 構成スクリプトを変更して、問題のある暗号スイートを無効にします。

      1. /var/opt/mssql/mssql.conf に次の内容を追加します。

          ```
          [network]
          tlsciphers= AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:!ECDHE-RSA-AES128-GCM-SHA256:!ECDHE-RSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES128-GCM-SHA256:!ECDHE-ECDSA-AES256-SHA384:!ECDHE-ECDSA-AES128-SHA256:!ECDHE-ECDSA-AES256-SHA:!ECDHE-ECDSA-AES128-SHA:!ECDHE-RSA-AES256-SHA384:!ECDHE-RSA-AES128-SHA256:!ECDHE-RSA-AES256-SHA:!ECDHE-RSA-AES128-SHA:!DHE-RSA-AES256-GCM-SHA384:!DHE-RSA-AES128-GCM-SHA256:!DHE-RSA-AES256-SHA:!DHE-RSA-AES128-SHA:!DHE-DSS-AES256-SHA256:!DHE-DSS-AES128-SHA256:!DHE-DSS-AES256-SHA:!DHE-DSS-AES128-SHA:!DHE-DSS-DES-CBC3-SHA:!NULL-SHA256:!NULL-SHA
          ```

         > [!NOTE]
         > 上記のコードでは、`!` によって式が否定されています。 これにより、次の暗号スイートを使用しないように OpenSSL に指示されます。  

      1. 次のコマンドを使用して [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] を再起動します。

          ```bash
          sudo systemctl restart mssql-server
          ```

- インメモリ OLTP を使用する Windows 上の [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] データベースは、Linux 上の SQL Server 2019 (15.x) で復元することはできません。 インメモリ OLTP を使用する [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] データベースを復元するには、最初に Windows 上でデータベースを [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]、SQL Server 2017、または SQL Server 2019 にアップグレードしてから、バックアップ/復元またはデタッチ/アタッチを使用して Linux 上の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] に移動します。

- ユーザー権限 **ADMINISTER BULK OPERATIONS** は、現時点で Linux ではサポートされていません。

### <a name="networking"></a>ネットワーク

リンク サーバーや可用性グループなど、sqlservr プロセスからの送信 TCP 接続に関連する機能は、次の両方の条件が満たされている場合は動作しない可能性があります。

1. ターゲット サーバーは、IP アドレスではなくホスト名として指定されます。

1. カーネルでは、ソース インスタンスの IPv6 が無効になっています。 システムのカーネルで IPv6 が有効になっているかどうかを確認するには、次のすべてのテストに合格する必要があります。

   - `cat /proc/cmdline` は、現在のカーネルのブート コマンドラインを出力します。 この出力に `ipv6.disable=1` を含めることはできません。
   - /proc/sys/net/ipv6/ ディレクトリが存在している必要があります。
   - `socket(AF_INET6, SOCK_STREAM, IPPROTO_IP)` を呼び出す C プログラムが成功する必要があります。syscall は、fd! =-1 を返して EAFNOSUPPORT で失敗しない必要があります。

正確なエラーは、機能によって異なります。 リンク サーバーの場合、これはログイン タイムアウト エラーとして現れます。 可用性グループの場合、セカンダリの `ALTER AVAILABILITY GROUP JOIN` DDL は 5 分後に失敗し、ダウンロード構成のタイムアウト エラーが発生します。

この問題を回避するには、次のいずれかのようにします。

1. ホスト名ではなく IP を使用して、TCP 接続のターゲットを指定します。

1. ブート コマンドラインから `ipv6.disable=1` を削除して、カーネルで IPv6 を有効にします。 これを行う方法は、Linux ディストリビューションとブートローダー (grub など) によって異なります。 IPv6 を無効にする場合でも、`sysctl` 構成 (たとえば、`/etc/sysctl.conf`) で `net.ipv6.conf.all.disable_ipv6 = 1` を設定することによって無効にすることもできます。 この場合も、システムのネットワーク アダプターが IPv6 アドレスを取得できませんが、sqlservr の機能を使用できるようになります。

#### <a name="network-file-system-nfs"></a>Network File System (NFS)
運用環境で **Network File System (NFS)** のリモート共有を使用する場合は、次のサポート要件に注意してください。

- NFS バージョン **4.2 以上**を使用してください。 前のバージョンの NFS では、最新のファイル システムに共通する `fallocate` やスパース ファイルの作成などの必要な機能がサポートされていません。
- NFS マウント上の **/var/opt/mssql** ディレクトリのみが検索されます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] システム バイナリなどの他のファイルはサポートされていません。
- リモート共有をマウントするときに NFS クライアントが `nolock` オプションを使用していることを確認してください。

### <a name="localization"></a>ローカリゼーション

- セットアップ時にロケールが英語 (en_us) でない場合は、bash セッション/ターミナルで UTF-8 エンコードを使用する必要があります。 ASCII エンコードを使用すると、次のようなエラーが表示される場合があります。

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   UTF-8 エンコードを使用できない場合は、MSSQL_LCID 環境変数を使用してセットアップを実行し、使用する言語選択を指定します。

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

- mssql-conf セットアップを実行していて、英語以外の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインストールを実行すると、ローカライズされたテキストの後に "SQL Server を構成中..." という不適切な拡張文字が表示されます。 または、ラテン語以外のインストールの場合、文が完全に欠落する可能性があります。 欠落している文には、次のローカライズされた文字列が表示される必要があります。"ライセンス PID は正常に処理されました。 新しいエディションは [\<Name\> edition] です。" この文字列は情報提供のみを目的とした出力であり、次の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 累積更新プログラムでは、すべての言語でこの値に対応します。 これは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の正常なインストールには影響しません。 

#### <a name="full-text-search"></a>フルテキスト検索

- このリリースでは、Office ドキュメントのフィルターを含め、すべてのフィルターが使用できるわけではありません。 サポートされているフィルターの一覧については、[Linux への SQL Server フルテキスト検索のインストール](sql-server-linux-setup-full-text-search.md#filters)に関するページを参照してください。

### <a name="sql-server-integration-services-ssis"></a><a id="ssis"></a> SQL Server Integration Services (SSIS)

- **mssql-server-is** パッケージは、このリリースの SUSE ではサポートされていません。 現時点では、Ubuntu と Red Hat Enterprise Linux (RHEL) でサポートされています。

- Linux CTP 2.1 Refresh 以降の [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] の場合、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージでは、Linux で ODBC 接続を使用できます。 この機能は [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] と MySQL ODBC ドライバーでテストされていますが、ODBC 仕様に準拠するあらゆる Unicode ODBC ドライバーでも動作することが予想されます。 デザイン時、DSN または接続文字列を指定し、ODBC データに接続できます。Windows 認証を使用することもできます。 詳細については、[Linux での ODBC サポートの告知ブログ記事](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)を参照してください。

- Linux 上で SSIS パッケージを実行する場合、このリリースでは次の機能はサポートされていません。
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] カタログ データベース
  - SQL エージェントでスケジュールされたパッケージの実行
  - Windows 認証
  - サードパーティ コンポーネント
  - 変更データ キャプチャ (CDC)
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] スケール アウト
  - SSIS 用の Azure Feature Pack
  - Hadoop と HDFS のサポート
  - Microsoft Connector for SAP BW

現在サポートされていない、または制限付きでサポートされている組み込み SSIS コンポーネントの一覧については、[Linux の SSIS の制限事項と既知の問題](sql-server-linux-ssis-known-issues.md#components)に関するページを参照してください。

Linux の SSIS の詳細については、次の記事を参照してください。
-   [SSIS の Linux サポートをお知らせするブログ記事](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)。
-   [SQL Server Integration Services (SSIS) on Linux をインストールする](sql-server-linux-setup-ssis.md)
-   [SSIS を使用して Linux 上でデータの抽出、変換、読み込みを行う](sql-server-linux-migrate-ssis.md)

### <a name="sql-server-management-studio-ssms"></a><a id="ssms"></a> SQL Server Management Studio (SSMS)

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] on Linux に接続されている Windows の [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] には、次の制限事項が適用されます。

- メンテナンス プランはサポートされていません。

- [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] の管理データ ウェアハウス (MDW) とデータ コレクターはサポートされていません。 

- Windows 認証または Windows イベント ログ オプションを備えた [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] の UI コンポーネントは、Linux では機能しません。 これらの機能は、SQL ログインなどの他のオプションと共に引き続き使用できます。 

- 保持するログ ファイルの数は変更できません。

## <a name="next-steps"></a>次のステップ

作業を開始するには、次のクイック スタートを参照してください。

- [Red Hat Enterprise Linux へのインストール](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server へのインストール](quickstart-install-connect-suse.md)
- [Ubuntu へのインストール](quickstart-install-connect-ubuntu.md)
- [Docker 上での実行](quickstart-install-connect-ubuntu.md)
- [Azure での SQL VM プロビジョニング](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)
- [実行と接続 - クラウド](quickstart-install-connect-clouds.md)

よく寄せられる質問に対する回答については、「[SQL Server on Linux に関する FAQ](sql-server-linux-faq.md)」を参照してください。
