---
title: macOS 用 Azure Data CLI (azdata) のインストール
titleSuffix: ''
description: macOS に Azure Data CLI (azdata) ツールをインストールする方法について説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3c172eea166f93d3e612145a2675e195c9dfdf76
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100052763"
---
# <a name="install-azure-data-cli-azdata-on-macos"></a>[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] の macOS へのインストール

macOS プラットフォームの場合、Homebrew パッケージ マネージャーを使用して `azdata-cli` をインストールできます。 この CLI パッケージは、macOS の次のバージョンでテストされています。

- 10.13 High Sierra
- 10.14 Mojave
- 10.15 Catalina

## <a name="install-with-homebrew"></a>Homebrew でインストールする

```bash
brew tap microsoft/azdata-cli-release
brew update
brew install azdata-cli
```

>[!IMPORTANT]
>`azdata-cli` は Homebrew の `python3`、`freetds`、`unixodbc`、`zeromq` パッケージに依存しており、それらをインストールします。 `azdata-cli` は、Homebrew で公開されるこれらの依存関係の最新バージョンとの互換性が保証されています。

## <a name="verify-install"></a>インストールの確認

```bash
azdata
azdata --version
```

## <a name="update"></a>更新

ローカル リポジトリ情報を更新してから、`azdata-cli` パッケージをアップグレードします。

```bash
brew tap microsoft/azdata-cli-release
brew update
brew upgrade azdata-cli
```

## <a name="uninstall"></a>アンインストール

Homebrew を使用して、`azdata-cli` パッケージをアンインストールします。

```bash
brew uninstall azdata-cli
```

## <a name="next-steps"></a>次のステップ

ビッグ データ クラスターの詳細については、「[[!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]とは](../../big-data-cluster/big-data-cluster-overview.md)」を参照してください。

[Azure Arc 対応データ サービス](/azure/azure-arc/data/)で azdata を使用する
