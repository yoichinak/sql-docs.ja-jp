---
title: Machine Learning 拡張機能
description: Azure Data Studio の Machine Learning 拡張機能を使用すると、パッケージの管理、機械学習モデルのインポート、予測の作成、および SQL データベースの実験を実行するためのノートブックの作成を行うことができます。
ms.prod: azure-data-studio
ms.technology: machine-learning
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.reviewer: sstein
ms.custom: ''
ms.date: 05/19/2020
ms.openlocfilehash: 163f5efca97e99609cbdbaae8f713c4576cc4e0b
ms.sourcegitcommit: 9c6130d498f1cfe11cde9f2e65c306af2fa8378d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93035978"
---
# <a name="machine-learning-extension-for-azure-data-studio-preview"></a>Azure Data Studio の Machine Learning 拡張機能 (プレビュー)

[Azure Data Studio](../what-is-azure-data-studio.md) の Machine Learning 拡張機能を使用すると、パッケージの管理、機械学習モデルのインポート、予測の作成、および SQL データベースの実験を実行するためのノートブックの作成を行うことができます。 この拡張機能は、現在プレビューの段階にあります。

## <a name="prerequisites"></a>前提条件

Azure Data Studio を実行するコンピューターには、次の前提条件をインストールする必要があります。

- [Python 3](https://www.python.org/downloads/)。 Python をインストールしたら、[[拡張機能の設定]](#settings) で、Python インストールへのローカル パスを指定する必要があります。 Azure Data Studio で [Python カーネル ノートブック](../notebooks/notebooks-python-kernel.md)を使用したことがある場合は、拡張機能ではノートブックからのパスが既定で使用されます。

- Windows、macOS、または Linux 用の [Microsoft ODBC driver 17 for SQL Server](../../connect/odbc/download-odbc-driver-for-sql-server.md)。

- [R 3.5](https://www.r-project.org/) (省略可能)。 3\.5 以外のバージョンは現在サポートされていません。 R 3.5 をインストールしたら、R を有効にし、[[拡張機能の設定]](#settings) で、R インストールへのローカル パスを指定する必要があります。 これは、データベースで R パッケージを管理する場合にのみ必要です。

### <a name="trouble-installing-python-3-from-within-ads"></a>ADS 内からの Python 3 のインストールで問題が発生した場合

Python 3 をインストールしようとしたときに、TLS/SSL に関するエラーが表示された場合は、次の 2 つのオプションのコンポーネントを追加します。

_エラーのサンプル_
```
$: ~/0.0.1/bin/python3 -m pip install --user "jupyter>=1.0.0" --extra-index-url https://prose-python-packages.azurewebsites.net
WARNING: pip is configured with locations that require TLS/SSL, however the ssl module in Python is not available.
Looking in indexes: https://pypi.org/simple, https://prose-python-packages.azurewebsites.net
Requirement already satisfied: jupyter
```

_次をインストールします_

- [Homebrew](https://brew.sh) (オプション)。 Homebrew をインストールし、その後コマンド ラインから `brew update` を実行します。

- *openssl* (オプション)。 次に、`brew install openssl` を実行します。

## <a name="install-the-extension"></a>拡張機能をインストールする

Azure Data Studio に Machine Learning 拡張機能をインストールするには、次の手順に従います。

1. Azure Data Studio で拡張機能マネージャーを開きます。 拡張機能アイコンを選択するか、[表示] メニューの [拡張機能] を選択できます。

1. **Machine Learning** 拡張機能を選択し、その詳細を表示します。

1. **[インストール]** を選択します。

1. **[再度読み込む]** を選択して拡張機能を有効にします。 これは、拡張機能を初めてインストールするときにのみ必要です。

<a name="settings"></a>

## <a name="extension-settings"></a>拡張機能の設定

Machine Learning 拡張機能の設定を変更するには、次の手順に従います。

1. Azure Data Studio で拡張機能マネージャーを開きます。 拡張機能アイコンを選択するか、[表示] メニューの [拡張機能] を選択できます。

1. **有効化された** 拡張機能の下で、 **Machine Learning** 拡張機能を見つけます。

1. **[管理]** アイコンを選択します。

1. **[拡張機能の設定]** アイコンを選択します。

拡張機能の設定は次のようになります。

:::image type="content" source="media/machine-learning-extension/ml-extension-settings.png" alt-text="Machine Learning 拡張機能の設定":::

### <a name="enable-python"></a>Python の有効化

データベースで Machine Learning 拡張機能と Python パッケージ管理を使用するには、次の手順に従います。

> [!IMPORTANT]
> Machine Learning 拡張機能では、データベース機能で Python パッケージ管理を使用しない場合でも、Python を有効にし、ほとんどの機能が動作するように構成する必要があります。

1. **[Machine Learning: Python の有効化]** が有効になっていることを確認します。 既定では、この設定は有効になっています。

1. 既存の Python インストールへのパスを **[Machine Learning: Python パス]** で指定します。 これには Python の実行可能ファイルまたは実行可能ファイルが格納されているフォルダーへの完全なパスを指定できます。 Azure Data Studio で [Python カーネル ノートブック](../notebooks/notebooks-python-kernel.md)を使用したことがある場合は、拡張機能ではノートブックからのパスが既定で使用されます。

### <a name="enable-r"></a>R の有効化

データベースの R パッケージ管理に Machine Learning 拡張機能を使用するには、次の手順に従います。

1. **[Machine Learning: R の有効化]** が有効になっていることを確認します。 既定では、この設定は無効になっています。

1. 既存の R インストールへのパスを **[Machine Learning: R パス]** で指定します。 これは、R 実行可能ファイルへの完全なパスである必要があります。 

## <a name="use-the-machine-learning-extension"></a>Machine Learning 拡張機能を使用する

Azure Data Studio で Machine Learning 拡張機能を使用するには、次の手順に従います。

1. Azure Data Studio で **[接続]** ビューレットを開きます。

1. ご使用のサーバーを右クリックし、 **[管理]** を選択します。

1. 左側のメニューの **[全般]** の下で **[Machine Learning]** を選択します。

Machine Learning 拡張機能を使用して、パッケージを管理し、予測を行い、データベースにモデルをインポートする方法については、 **次のステップ** の下のリンクを参照してください。

## <a name="next-steps"></a>次のステップ

- [データベースでのパッケージの管理](machine-learning-extension-manage-packages.md)
- [予測を行う](machine-learning-extension-predictions.md)
- [モデルのインポートまたは表示](machine-learning-extension-import-view-models.md)
- [Azure Data Studio のノートブック](../notebooks/notebooks-guidance.md)
- [SQL の機械学習のドキュメント](../../machine-learning/index.yml)
- [SQL Edge での ONNX を使用した機械学習と AI (プレビュー)](/azure/azure-sql-edge/onnx-overview)