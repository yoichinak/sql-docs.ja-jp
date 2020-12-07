---
title: Machine Learning 拡張機能を使用してパッケージを管理する
description: Azure Data Studio の Machine Learning 拡張機能を使用して、データベース内の Python または R パッケージを管理する方法について説明します。
ms.prod: azure-data-studio
ms.technology: machine-learning
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.reviewer: sstein
ms.custom: ''
ms.date: 05/19/2020
ms.openlocfilehash: 2977f25e09d3d634d479abd8371d010206edea90
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725169"
---
# <a name="manage-packages-in-database-with-machine-learning-extension-for-azure-data-studio-preview"></a>Azure Data Studio の Machine Learning 拡張機能を使用してデータベース内のパッケージを管理する (プレビュー)

[Azure Data Studio の Machine Learning 拡張機能](machine-learning-extension.md)を使用して、データベース内の Python または R パッケージを管理する方法について説明します。

> [!IMPORTANT]
> Machine Learning 拡張機能を使用したデータベース内のパッケージの管理では、現在、SQL Server 2019 の [Machine Learning Services](../../machine-learning/sql-server-machine-learning-services.md) のみがサポートされています。

## <a name="prerequisites"></a>前提条件

- [Azure Data Studio の Machine Learning 拡張機能](machine-learning-extension.md)のインストールと構成。 パッケージ管理を機能させるには、[[拡張機能の設定] で Python または R のインストール パス](machine-learning-extension.md#settings)を指定する必要があります。

- **sqlmlutils** パッケージ。 パッケージがまだインストールされていない場合は、Machine Learning 拡張機能によってインストールするように求められます。

- SQL Server on Linux の場合、Windows 認証はサポートされていません。 そのため、SQL Server on Linux に接続するには、SQL 認証を使用する必要があります。

## <a name="manage-python-packages"></a>Python パッケージの管理

Machine Learning 拡張機能を使用して、Python パッケージをインストールおよびアンインストールできます。

### <a name="install-new-python-package"></a>新しい Python パッケージのインストール

次の手順に従って、データベースに Python パッケージをインストールします。

1. **[Manage packages in database]\(データベース内のパッケージの管理\)** を選択します。

1. **sqlmlutils** をインストールするように求められたら、 **[はい]** を選択します。

1. **[インストール済み]** タブで、 **[パッケージの種類]** で **[Python]** を選択し、 **[場所]** でデータベースを選択します。

1. **[新規追加]** タブを選択します。

1. **[Python パッケージの検索]** にインストールする Python パッケージを入力し、 **[検索]** を選択します。

1. **[パッケージ名]** の下にパッケージが一覧表示されていること、および必要なバージョンが **[パッケージ バージョン]** の下に表示されていることを確認します。

1. **[インストール]** を選択します。

1. **[閉じる]** を選択し、 **[タスク]** でパッケージが正常にインストールされたことを確認します。

### <a name="uninstall-a-python-package"></a>Python パッケージのアンインストール

次の手順に従って、データベース内の Python パッケージをアンインストールします。

> [!NOTE]
> アンインストールできるのは、データベースにインストールされているパッケージのみです。 SQL Server Machine Learning Services でプレインストールされているパッケージをアンインストールすることはできません。

1. **[Manage packages in database]\(データベース内のパッケージの管理\)** を選択します。

1. **sqlmlutils** をインストールするように求められたら、 **[はい]** を選択します。

1. **[インストール済み]** タブで、 **[パッケージの種類]** で **[Python]** を選択し、 **[場所]** でデータベースを選択します。

1. アンインストールするパッケージを選択します。

1. **[選択したパッケージをアンインストールする]** を選択します。

1. **[閉じる]** を選択し、 **[タスク]** でパッケージが正常にインストールされたことを確認します。

## <a name="manage-r-packages"></a>R パッケージの管理

Machine Learning 拡張機能を使用して、R パッケージをインストールおよびアンインストールできます。

### <a name="install-new-r-package"></a>新しい R パッケージのインストール

次の手順に従って、データベースに Python パッケージをインストールします。

1. **[Manage packages in database]\(データベース内のパッケージの管理\)** を選択します。

1. **sqlmlutils** をインストールするように求められたら、 **[はい]** を選択します。

1. **[インストール済み]** タブで、 **[パッケージの種類]** で **[R]** を選択し、 **[場所]** でデータベースを選択します。

1. **[新規追加]** タブを選択します。

1. **[R パッケージの検索]** にインストールする R パッケージを入力し、 **[検索]** を選択します。

1. **[パッケージ名]** の下にパッケージが一覧表示されていること、および必要なバージョンが **[パッケージ バージョン]** の下に表示されていることを確認します。

1. **[インストール]** を選択します。

1. **[閉じる]** を選択し、 **[タスク]** でパッケージが正常にインストールされたことを確認します。

### <a name="uninstall-an-r-package"></a>R パッケージのアンインストール

次の手順に従って、データベース内の R パッケージをアンインストールします。

> [!NOTE]
> アンインストールできるのは、データベースにインストールされているパッケージのみです。 SQL Server Machine Learning Services でプレインストールされているパッケージをアンインストールすることはできません。

1. **[Manage packages in database]\(データベース内のパッケージの管理\)** を選択します。

1. **sqlmlutils** をインストールするように求められたら、 **[はい]** を選択します。

1. **[インストール済み]** タブで、 **[パッケージの種類]** で **[R]** を選択し、 **[場所]** でデータベースを選択します。

1. アンインストールするパッケージを選択します。

1. **[選択したパッケージをアンインストールする]** を選択します。

1. **[閉じる]** を選択し、 **[タスク]** でパッケージが正常にインストールされたことを確認します。

## <a name="next-steps"></a>次のステップ

- [Azure Data Studio の Machine Learning 拡張機能](machine-learning-extension.md)
- [予測を行う](machine-learning-extension-predictions.md)
- [モデルのインポートまたは表示](machine-learning-extension-import-view-models.md)
- [Azure Data Studio のノートブック](../notebooks/notebooks-guidance.md)
- [SQL の機械学習のドキュメント](../../machine-learning/index.yml)