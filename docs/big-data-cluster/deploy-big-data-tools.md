---
title: ビッグ データ ツールをインストールする
titleSuffix: SQL Server big data clusters
description: SQL Server 2019 ビッグ データ クラスターで使用するツールをインストールする方法について説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 27248c9a8ef05b8662f56255cab47e47bd2959f4
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257232"
---
# <a name="install-sql-server-2019-big-data-tools"></a>SQL Server 2019 のビッグ データ ツールをインストールする

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

この記事では、[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]を作成、管理、使用するためにインストールする必要があるクライアント ツールについて説明します。 次のセクションでは、ツールおよびインストール手順へのリンクの一覧を示します。 ビッグ データ クラスターを配置する前に、必須とマークされているツールを Windows または Linux で構成します。

## <a name="big-data-cluster-tools"></a>ビッグ データ クラスターのツール

次の表では、一般的なビッグ データ クラスター ツールとそのインストール方法を示します。

| ツール | 必須 | 説明 | インストール |
|---|---|---|---|
| `python` | はい | Python は、動的なセマンティクスを備えた、インタープリター方式でオブジェクト指向の高水準プログラミング言語です。 SQL Server 用のビッグ データ クラスターの多くの部分で、Python が使われています。 | [Python のインストール](#python)|
| [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] | はい | ビッグ データ クラスターをインストールして管理するためのコマンドライン ツールです。 | [インストール](../azdata/install/deploy-install-azdata.md) |
| `kubectl`<sup>1</sup> | はい | 基になる Kubernetes クラスターを監視するためのコマンドライン ツールです ([詳細情報](https://kubernetes.io/docs/tasks/tools/install-kubectl/))。 | [Windows](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-with-powershell-from-psgallery) \| [Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-using-native-package-management) |
| **Azure Data Studio** | はい | SQL Server のクエリを実行するためのクロスプラットフォーム グラフィック ツールです。 | [インストール](../azure-data-studio/download-azure-data-studio.md) |
| **データ仮想化の拡張機能** | はい | データ仮想化ウィザードを提供する Azure Data Studio の拡張機能。 | [インストール](../azure-data-studio/extensions/data-virtualization-extension.md) |
| **Azure CLI**<sup>2</sup> | AKS の場合 | Azure のサービスを管理するための最新のコマンドライン インターフェイスです。 AKS ビッグ データ クラスターの展開で使われます ([詳細情報](/cli/azure/?view=azure-cli-latest&preserve-view=true))。 | [インストール](/cli/azure/install-azure-cli?view=azure-cli-latest&preserve-view=true) |
| **mssql-cli** | 省略可能 | SQL Server のクエリを実行するための最新のコマンドライン インターフェイスです ([詳細情報](../tools/mssql-cli.md))。 | [Windows](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/windows.md) \| [Linux](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/linux.md) |
| **sqlcmd** | 一部のスクリプトの場合 | SQL Server のクエリを実行するための従来のコマンドライン ツールです ([詳細情報](../tools/sqlcmd-utility.md))。 SQLCMD パッケージをインストールする前に、Microsoft ODBC Driver 11 for SQL Server のインストールが必要になる場合があります。 | [Windows](https://www.microsoft.com/download/details.aspx?id=36433) \| [Linux](../linux/sql-server-linux-setup-tools.md) |
| `curl` <sup>3</sup> | 一部のスクリプトの場合 | URL でデータを転送するためのコマンドライン ツールです。 | [Windows](https://curl.haxx.se/windows/) \| Linux: curl パッケージのインストール |
| `oc` | Red Hat OpenShift と Azure Redhat OpenShift の展開に必要です。 |`oc` は、Open Shift コマンド ライン インターフェイス (CLI) です。 | [CLI のインストール](https://docs.openshift.com/container-platform/4.4/cli_reference/openshift_cli/getting-started-cli.html#installing-the-cli)

<sup>1</sup>`kubectl` バージョン 1.13 以降を使う必要があります。 また、`kubectl` のバージョンは、Kubernetes クラスターより 1 つ上または下のマイナー バージョンにする必要があります。 `kubectl` クライアント上で特定のバージョンをインストールする場合は、[curl を使用した `kubectl` バイナリのインストール](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl)に関するページを参照してください (Windows 10 では、Windows PowerShell ではなく cmd.exe を使って、curl を実行してください)。

> [!TIP]
> Azure Kubernetes Service (AKS) に以前に展開されたクラスターで `kubectl` を使うには、次の Azure CLI コマンドを使ってクラスター コンテキストを設定する必要があります。
>
>    ```azurecli
>    az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>
>    ```

<sup>2</sup> Azure CLI バージョン 2.0.4 以降を使う必要があります。 バージョンを確認する必要がある場合は、`az --version` を実行します。

<sup>3</sup> Windows 10 の場合、cmd プロンプトから実行するときは、`curl` は既に PATH にあります。 他のバージョンの Windows では、リンクを使って `curl` をダウンロードし、PATH に配置します。

## <a name="which-tools-are-required"></a>必要なツール

上の表では、ビッグ データ クラスターで使われる一般的なツールがすべて示されています。 どのツールが必要かは、実際のシナリオによって異なります。 ただし、一般に、クラスターの管理、接続、クエリを行うには、次のツールが最も重要です。

- [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]
- `kubectl`
- **Azure Data Studio**
- **データ仮想化の拡張機能**

残りのツールは、特定のシナリオでのみ必要です。 **Azure CLI** を使って、AKS の展開に関連付けられている Azure サービスを管理できます。 **mssql-cli** は必須ではありませんが便利なツールです。これを使うと、クラスター内の SQL Server マスター インスタンスに接続し、コマンド ラインからクエリを実行できます。 そして、GitHub スクリプトでサンプル データをインストールする予定の場合は、**sqlcmd** と `curl` が必要です。

### <a name="install-python-offline"></a><a id="python"></a> Python をオフラインでインストールする

1. インターネットにアクセスできるコンピューターで、Python が含まれる次のいずれかの圧縮ファイルをダウンロードします。

   | オペレーティング システム | ダウンロード |
   |---|---|
   | Windows | [https://go.microsoft.com/fwlink/?linkid=2074021](https://go.microsoft.com/fwlink/?linkid=2074021) |
   | Linux   | [https://go.microsoft.com/fwlink/?linkid=2065975](https://go.microsoft.com/fwlink/?linkid=2065975) |
   | OSX     | [https://go.microsoft.com/fwlink/?linkid=2065976](https://go.microsoft.com/fwlink/?linkid=2065976) |

1. 圧縮されたファイルをターゲット コンピューターにコピーし、任意のフォルダーに抽出します。

1. Windows の場合にのみ、そのフォルダーから `installLocalPythonPackages.bat` を実行して、パラメーターと同じフォルダーへの完全なパスを渡します。

   ```PowerShell
   installLocalPythonPackages.bat "C:\python-3.6.6-win-x64-0.0.1-offline\0.0.1"
   ```

## <a name="download-and-install-azure-data-studio"></a>Azure Data Studio のダウンロードとインストール

Azure Data Studio には、SQL Server ビッグ データ クラスター専用の機能が用意されています。

[最新の Azure Data Studio を取得します](../azure-data-studio/download-azure-data-studio.md)。

最新リリースに関する詳細については、[リリース ノート](./release-notes-big-data-cluster.md)をご覧ください。

## <a name="next-steps"></a>次のステップ

ツールを構成した後、クラウドまたはオンプレミスの Kubernetes に SQL Server 2019 ビッグ データ クラスターを配置します。 詳しくは、展開に関する次の記事をご覧ください。

- [クイック スタート: Azure Kubernetes Service (AKS) に SQL Server ビッグ データ クラスターを展開する](quickstart-big-data-cluster-deploy.md)
- [Kubernetes に [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] を展開する方法](deployment-guidance.md)

ビッグ データ クラスターの詳細については、「[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]とは](big-data-cluster-overview.md)」を参照してください。