---
title: ソース管理
description: Azure Data Studio を使用すると、ソース コントロール管理 (SCM) 用に Git をサポートできます。 既存の Git リポジトリを開く方法と、新しい Git リポジトリを初期化する方法について説明します。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, sstein
ms.custom: seodec18
ms.date: 09/24/2019
ms.openlocfilehash: 7f032d870952cdadbde79dbf56f4c63ae351d6e9
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081571"
---
# <a name="source-control-in-azure-data-studio"></a>Azure Data Studio のソース管理

Azure Data Studio は、バージョン管理/ソース管理用の Git をサポートします。

## <a name="git-support-in-azure-data-studio"></a>Azure Data Studio の Git サポート

Azure Data Studio には、Git ソース管理マネージャー (SCM) が付属していますが、これらの機能を使用できるようにする前に [Git (バージョン 2.0.0 以降) をインストールする](https://git-scm.com/download)必要があります。

## <a name="open-an-existing-git-repository"></a>既存の Git リポジトリを開く

1. **[ファイル]** メニューで、 **[フォルダーを開く]** を選択します。
2. Git によって追跡されるファイルが含まれているフォルダーを参照して、 **[フォルダーの選択]** を選択します。 ここで、ローカル リポジトリ内のサブフォルダーを選択できます。

## <a name="initialize-a-new-git-repository"></a>新しい Git リポジトリを初期化する

1. **[ソース管理]** を選択して、Git アイコンを選択します。

   ![ソース管理 Git アイコン](media/source-control/source-control.png)

1. Git リポジトリとして初期化するフォルダーへのパスを入力して、**Enter** キーを押します。

   ![Git リポジトリを初期化する](media/source-control/initialize-git-repository.png)

## <a name="working-with-git-repositories"></a>Git リポジトリの操作

Azure Data Studio は、VS Code から Git 実装を継承していますが、追加の SCM プロバイダーについては、現在サポートしていません。 リポジトリを開くか、初期化した後に Git を操作する方法の詳細については、[VS コードでの Git のサポート](https://code.visualstudio.com/docs/editor/versioncontrol#_git-support)に関する記事を参照してください。

## <a name="additional-resources"></a>その他のリソース

- [Git のドキュメント](https://git-scm.com/documentation)
