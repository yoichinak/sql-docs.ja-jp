---
title: pip を使用して Azure Data CLI (azdata) をインストールする
titleSuffix: ''
description: pip で azdata ツールをインストールする方法について説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4aa52ebe56cbe4af3d2983a9ed800ebbc1538971
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257455"
---
# <a name="install-azure-data-cli-azdata-with-pip"></a>[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] の `pip` でのインストール

[!INCLUDE[azdata](../../includes/applies-to-version/azdata.md)]

この記事では、`pip` を使用して Windows、Linux、または macOS/OS X 用の [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] ツールをインストールする方法について説明します。

> [!TIP]
> よりシンプルなエクスペリエンスのために、Windows、Linux (Ubuntu、Debian、RHEL、CentOS、openSUSE、SLE の各ディストリビューション) と macOS 用の [パッケージ マネージャー](./deploy-install-azdata.md)を使用して `azdata` をインストールすることができます。

## <a name="prerequisites"></a><a id="prerequisites"></a> 前提条件

`azdata` は Python で記述されたコマンドライン ユーティリティです。クラスター管理者はこれを使用すると、REST API 経由でデータ リソースをブートストラップし、管理できるようになります。 最低限必要な Python バージョンは v3.5 です。 `pip` は、`azdata` ツールをダウンロードしてインストールするために必要です。 以下の手順では、Windows、Linux (Ubuntu)、macOS/OS X の例を示します。他のプラットフォーム上での Python のインストールする方法については、[Python のドキュメント](https://wiki.python.org/moin/BeginnersGuide/Download)を参照してください。 さらに、最新バージョンの `requests` Python パッケージをインストールして更新します。

```bash
pip3 install -U requests
```

## <a name="windows-azdata-installation"></a><a id="windows"></a> Windows `azdata` のインストール

1. Windows クライアントで、[https://www.python.org/downloads/](https://www.python.org/downloads/) から必要な Python パッケージをダウンロードします。 Python 3.5.3 以降では、Python をインストールするときに pip3 もインストールされます。

   > [!TIP]
   > Python3 をインストールするときに、`PATH` に Python を追加することを選択します。 そうしない場合は、後で pip3 が配置されている場所を見つけて、`PATH` に手動で追加することができます。

1. 新しい Windows PowerShell セッションを開き、Python で最新のパスを取得します。

1. SQL Server 2019 CU5 リリース以降では、azdata にサーバーから独立したセマンティック バージョンがあります。 これより前のリリースの `azdata` がインストールされている場合は、まずそれをアンインストールしてから最新バージョンをインストールすることが重要です。

   たとえば、2019-cu4 の場合は、次のコマンドを実行します。

   ```powershell
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-cu4/requirements.txt
   ```

  > [!NOTE]
  > 前の例では、`2019-cu6` を `azdata` の実際のインストールのバージョンと CU に置き換えます。 

1. `azdata`をインストールする。

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

## <a name="linux-azdata-installation"></a><a id="linux"></a> Linux `azdata` のインストール

Linux では、Python 3.5 をインストールしてから、pip をアップグレードする必要があります。 次の例は、Ubuntu で動作するコマンドを示しています。 その他の Linux プラットフォームについては、[Python のドキュメント](https://wiki.python.org/moin/BeginnersGuide/Download)を参照してください。

1. 必要な Python パッケージをインストールします。

   ```bash
   sudo apt-get update && \
   sudo apt-get install -y python3 && \
   sudo apt-get install -y python3-pip && \
   sudo apt-get install -y libkrb5-dev && \
   sudo apt-get install -y libsqlite3-dev && \
   sudo apt-get install -y unixodbc-dev
   ```

1. pip3 をアップグレードします。

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. SQL Server 2019 CU5 リリース以降では、azdata にサーバーから独立したセマンティック バージョンがあります。 これより前のリリースの `azdata` がインストールされている場合は、まずそれをアンインストールしてから最新バージョンをインストールすることが重要です。

   たとえば、`2019-cu6` の場合は、次のコマンドを実行します。

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-cu6/requirements.txt
   ```

  > [!NOTE]
  > 前の例では、`2019-cu6` を `azdata` の実際のインストールのバージョンと CU に置き換えます。

1. `azdata`をインストールする。

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!NOTE]
   > `--user` スイッチを指定すると、`azdata` が Python ユーザー インストール ディレクトリにインストールされます。 通常、Linux 上ではこれは `~/.local/bin` です。 このディレクトリをパスに追加するか、ユーザー インストール ディレクトリに移動して、そこから `./azdata` を実行します。

## <a name="install-azdata-on-macos-or-os-x"></a><a id="macOSX"></a> macOS または OS X に `azdata` をインストールする

macOS または OS X に `azdata` をインストールするには、次の手順を実行します。 各ステップでは、ターミナルで例を実行します。

1. macOS クライアント上で、[Homebrew](https://brew.sh) をインストールします (まだインストールしていない場合)。

   ```bash
   /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   ```

1. Python と pip、最小バージョン 3.0 をインストールします。

   ```bash
   brew install python3
   ```

1. 依存関係をインストールします。

   ```bash
   pip3 install -U requests
   brew install freetds
   ```

1. SQL Server 2019 CU5 リリース以降では、azdata にサーバーから独立したセマンティック バージョンがあります。 これより前のリリースの `azdata` がインストールされている場合は、まずそれをアンインストールしてから最新バージョンをインストールすることが重要です。 たとえば、次のコマンドを使用すると、`azdata` の RC1 バージョンが削除されます。

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. Azure Data CLI をインストールする。

   ```bash
   pip3 install -r https://aka.ms/azdata
   ```

## <a name="next-steps"></a>次のステップ

ビッグ データ クラスターの詳細については、「[[!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]とは](../../big-data-cluster/big-data-cluster-overview.md)」を参照してください。

[Azure Arc 対応データ サービス](/azure/azure-arc/data/)で azdata を使用する
