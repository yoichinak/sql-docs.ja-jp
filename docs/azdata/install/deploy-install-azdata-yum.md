---
title: yum を使用した azdata のインストール
titleSuffix: ''
description: yum で azdata ツールをインストールする方法について説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 35afcae7bb5cef31bd59b53688c2eec07ee74a7c
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257509"
---
# <a name="install-azure-data-cli-azdata-with-yum"></a>yum での [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] のインストール

[!INCLUDE[azdata](../../includes/applies-to-version/azdata.md)]

`yum` を使用した Linux ディストリビューションには、`azdata-cli` 用のパッケージが用意されています。 この CLI パッケージは、`yum` を使用する Linux バージョンでテストされています。

- RHEL 7、RHEL 8

[!INCLUDE [azdata-package-installation-remove-pip-install](../../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="install-with-yum"></a>yum でのインストール

>[!IMPORTANT]
> `azdata-cli` の RPM パッケージは、python3 のパッケージによって異なります。 これは、お使いのシステムでは *Python 3.6.x* の要件より前から存在する Python バージョンである可能性があります。 これが問題となる場合、代わりの python3 パッケージを見つけるか、[`pip`](../install/deploy-install-azdata-pip.md) を使用する手動でのインストール手順に従ってください。

1. `azdata-cli` のインストールに必要な依存関係をインストールします。

   ```bash
   sudo yum install -y curl
   ```

1. Microsoft リポジトリ キーをインポートします。

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```

1. ローカル リポジトリ情報を作成します。

   RHEL 7 クライアントには次を実行します。

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/prod.repo
   ```
  
   RHEL 8 クライアントには次を実行します。

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/8/prod.repo
   ```

1. `azdata-cli`をインストールする。

   ```bash
   sudo yum install azdata-cli
   ```

## <a name="verify-install"></a>インストールの確認

```bash
azdata
azdata --version
```

## <a name="update"></a>更新

`yum update` コマンドで `azdata-cli` を更新します。

```bash
sudo yum update azdata-cli
```

## <a name="uninstall"></a>アンインストール

1. システムからパッケージを削除します。

   ```bash
   sudo yum remove azdata-cli
   ```

1. `azdata-cli` を再インストールする予定がない場合は、リポジトリ情報を削除してください。

   ```bash
   sudo rm /etc/yum.repos.d/azdata-cli.repo
   ```

## <a name="next-steps"></a>次のステップ

ビッグ データ クラスターの詳細については、「[[!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]とは](../../big-data-cluster/big-data-cluster-overview.md)」を参照してください。

[Azure Arc 対応データ サービス](/azure/azure-arc/data/)で azdata を使用する
