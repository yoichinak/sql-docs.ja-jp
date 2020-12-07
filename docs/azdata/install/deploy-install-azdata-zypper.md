---
title: zypper を使用して Azure Data CLI (azdata) をインストールする
titleSuffix: ''
description: zypper を使用して Azure Data CLI (azdata) ツールをインストールする方法について説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d43a1f9c65aa17fae3d262a51f45105b5f583cdd
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257515"
---
# <a name="install-azure-data-cli-azdata-with-zypper"></a>zypper での [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] のインストール

[!INCLUDE[azdata](../../includes/applies-to-version/azdata.md)]

`zypper` を使用した Linux ディストリビューションには、`azdata-cli` 用のパッケージが用意されています。 この CLI パッケージは、`zypper` を使用する Linux バージョンでテストされています。

- openSUSE 42.2 (leap) +
- SLES 12 SP 2 +

[!INCLUDE [azdata-package-installation-remove-pip-install](../../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="install-with-zypper"></a>zypper でのインストール

>[!IMPORTANT]
>`azdata-cli` の RPM パッケージは、python3 のパッケージによって異なります。 これは、お使いのシステムでは *Python 3.6.x* の要件より前から存在する Python バージョンである可能性があります。 これが問題となる場合、代わりの python3 パッケージを見つけるか、[`pip`](../install/deploy-install-azdata-pip.md) を使用する手動でのインストール手順に従ってください。

1. `azdata-cli` のインストールに必要な依存関係をインストールします。

   ```bash
   sudo zypper install -y curl
   ```

1. Microsoft リポジトリ キーをインポートします。

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```

1. ローカル リポジトリ情報を作成します。

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo
   ```

1. `azdata-cli`をインストールする。

   ```bash
   sudo zypper install --from packages-microsoft-com-mssql-server-2019 -y azdata-cli
   ```

## <a name="verify-install"></a>インストールの確認

```bash
azdata
azdata --version
```

## <a name="update"></a>更新

`zypper update` コマンドで `azdata-cli` を更新します。

```bash
sudo zypper refresh
sudo zypper update azdata-cli
```

## <a name="uninstall"></a>アンインストール

システムからパッケージを削除します。

```bash
sudo zypper removerepo azdata-cli
```

## <a name="next-steps"></a>次のステップ

ビッグ データ クラスターの詳細については、「[[!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]とは](../../big-data-cluster/big-data-cluster-overview.md)」を参照してください。

[Azure Arc 対応データ サービス](/azure/azure-arc/data/)で azdata を使用する