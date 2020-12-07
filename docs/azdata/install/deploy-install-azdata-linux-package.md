---
title: apt を使用して Azure Data CLI (azdata) をインストールする
description: apt を使用して Azure Data CLI (azdata) ツールをインストールする方法について説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4508db56c0246f181f9244fe0a3b853a3e91eb24
ms.sourcegitcommit: 4b7ecc080795c5f90322d60df5c0550884f48140
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2020
ms.locfileid: "94334451"
---
# <a name="install-azure-data-cli-azdata-with-apt"></a>apt での [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] のインストール

[!INCLUDE[azdata](../../includes/applies-to-version/azdata.md)]

`apt` を使用した Linux ディストリビューションには、`azdata-cli` 用のパッケージが用意されています。 この CLI パッケージは、`apt` を使用する Linux バージョンでテストされています。

- Ubuntu 16.04、Ubuntu 18.04

[!INCLUDE [azdata-package-installation-remove-pip-install](../../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="install-with-apt"></a>apt でのインストール

>[!IMPORTANT]
> `azdata-cli` の RPM パッケージは、python3 のパッケージによって異なります。 これは、お使いのシステムでは *Python 3.6.x* の要件より前から存在する Python バージョンである可能性があります。 これが問題となる場合、代わりの python3 パッケージを見つけるか、[`pip`](../install/deploy-install-azdata-pip.md) を使用する手動でのインストール手順に従ってください。

1. `azdata-cli` のインストールに必要な依存関係をインストールします。

   ```bash
   sudo apt-get update
   sudo apt-get install gnupg ca-certificates curl wget software-properties-common apt-transport-https lsb-release -y
   ```

2. Microsoft リポジトリ キーをインポートします。

   ```bash
   curl -sL https://packages.microsoft.com/keys/microsoft.asc |
   gpg --dearmor |
   sudo tee /etc/apt/trusted.gpg.d/microsoft.asc.gpg > /dev/null
   ```

3. ローカル リポジトリ情報を作成します。

   Ubuntu 16.04 クライアントには次を実行します。

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/prod.list)"
    ```

   Ubuntu 18.04 クライアントには次を実行します。

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/18.04/prod.list)"
    ```

   Ubuntu 20.04 クライアントには次を実行します。

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/20.04/prod.list)"
    ```

4. `azdata-cli`をインストールする。

   ```bash
   sudo apt-get update
   sudo apt-get install -y azdata-cli
   ```

## <a name="verify-install"></a>インストールの確認

```bash
azdata
azdata --version
```

## <a name="update"></a>更新

`apt-get update` および `apt-get install` コマンドを使用して、`azdata-cli` を更新します。

```bash
sudo apt-get update && sudo apt-get install --only-upgrade -y azdata-cli
```

## <a name="uninstall"></a>アンインストール

1. システムからパッケージを削除します。

   ```bash
   sudo apt-get remove -y azdata-cli
   ```

2. `azdata-cli` を再インストールする予定がない場合は、リポジトリ情報を削除してください。

   ```bash
   sudo rm /etc/apt/sources.list.d/azdata-cli.list
   ```

3. リポジトリ キーを削除します。

   ```bash
   sudo rm /etc/apt/trusted.gpg.d/dpgswdist.v1.asc.gpg
   ```

4. 不要になった依存関係を削除します。

   ```bash
   sudo apt autoremove
   ```

## <a name="next-steps"></a>次のステップ

ビッグ データ クラスターの詳細については、「[[!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]とは](../../big-data-cluster/big-data-cluster-overview.md)」を参照してください。

[Azure Arc 対応データ サービス](/azure/azure-arc/data/)で azdata を使用する
