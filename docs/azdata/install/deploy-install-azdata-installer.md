---
title: Windows インストーラーを使用した Azure Data CLI (azdata) のインストール
titleSuffix: ''
description: インストーラーで Azure Data CLI (azdata) ツールをインストールする方法について説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9dd953a78a992a9a5fed7135ae0aee02f88e4de9
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257495"
---
# <a name="install-azure-data-cli-azdata-with-windows-installer"></a>Windows インストーラーを使用して [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] をインストールする

[!INCLUDE [azdata](../../includes/applies-to-version/azdata.md)]

この記事では、インストーラーを使用して Windows 上に `azdata` をインストールする方法について説明します。 `azdata` を使用して、SQL Server ビッグ データ クラスターまたは Azure Arc 対応データ サービスを管理します。

## <a name="steps-to-install-azdata-with-the-microsoft-windows-installer"></a>Microsoft Windows インストーラーを使用して `azdata` をインストールする手順

Microsoft Windows インストーラーで `azdata` をインストールするには、次のようにします。

1. `pip` を使用してインストールされた `azdata` がある場合は削除します。 Windows インストーラーを使用して `azdata` がインストールされている場合は、次のステップに進みます。
1. [Windows インストーラー](https://aka.ms/azdata-msi)を使用して `azdata` をインストールします。

### <a name="uninstall-azdata-with-windows-installer"></a>Windows インストーラーで `azdata` をアンインストールする

Windows インストーラーで `azdata` をアンインストールするには、該当するオペレーティング システムの指示に従います。

| プラットフォーム      | Instructions                                           |
| ------------- |--------------------------------------------------------|
| Windows 10| [スタート] > [設定] > [アプリ]                                |
| Windows 8     | [スタート] > [コントロール パネル] > [プログラム] > [プログラムのアンインストール] |

アンインストールするプログラムは `Azdata CLI` という名前です。 このアプリケーションを選択し、`Uninstall` ボタンをクリックします。

## <a name="next-steps"></a>次のステップ

ビッグ データ クラスターの詳細については、「[[!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]とは](../../big-data-cluster/big-data-cluster-overview.md)」を参照してください。

[Azure Arc 対応データ サービス](/azure/azure-arc/data/)で `azdata` を使用する
