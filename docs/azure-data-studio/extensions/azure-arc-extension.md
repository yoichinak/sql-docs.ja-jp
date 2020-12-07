---
title: Azure Arc 拡張機能 (プレビュー)
description: Azure Arc 拡張機能をインストールおよび使用して、Azure Arc data services を試す方法について説明します。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: maghan, sstein
ms.custom: ''
ms.date: 09/22/2020
ms.openlocfilehash: 3bcdd76cf143c94dc1e200a21972d00419f26b96
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725213"
---
# <a name="azure-arc-extension-for-azure-data-studio-preview"></a>Azure Data Studio 用の Azure Arc 拡張機能 (プレビュー)

[Azure Arc 拡張機能 (プレビュー)](/azure/azure-arc/data/) は、Azure Arc data services リソースを作成および管理するための拡張機能です。

**主要なアクションには、次のようなものがあります。**
- リソースの作成
    - データ コントローラー
    - Azure Arc 用 SQL Managed Instance
    - Azure Arc 用 PostgreSQL
- リソースを管理する
    - データ コントローラー ダッシュボードを表示する
    - Azure Arc 用 SQL Managed Instance ダッシュボードを表示する
    - Azure Arc 用 PostgreSQL ダッシュボードを表示する
- Azure Arc Jupyter ブックを実行する

## <a name="install-the-extension"></a>拡張機能をインストールする
- **Azure Data CLI** 拡張機能をギャラリーからインストールします。
- **Azure Arc** 拡張機能をギャラリーからインストールします。
- Azure Data Studio を再起動します

## <a name="sign-in-with-azure-account"></a>Azure アカウントでサインインする
1. 左下の [アカウント] を選択します
1. [アカウントの追加] を選択します
1. この操作により、ブラウザーが起動します。 Azure アカウントにサインインします。

## <a name="create-a-resource"></a>リソースの作成
この拡張機能によって、Azure Arc データ コントローラー、Azure Arc 用 Postgres、Azure Arc 用 SQL Managed Instance のデプロイがサポートされています。組み込みのデプロイ ウィザードを使用してデプロイを行うことができます。

1. 左側のアクティビティ バーの [接続] ビューレットを選択します
1. 3 つのドットを選択し、 **[新しいデプロイ]** を選択します
1. 画面の指示に従って、新しい Azure Arc リソースを作成します。

## <a name="manage-a-resource"></a>リソースを管理する
azdata、Azure portal、または Azure Data Studio から Azure Arc データ コントローラーをデプロイしたら、Azure Data Studio からそれに接続できるようになります。

1. 左側のアクティビティ バーの [接続] ビューレットを開きます。
1. **[Azure Arc コントローラー]** を展開します
1. **[コントローラーの接続]** を選択します
1. パラメーターを入力して接続します。

接続すると、データ コントローラーにデプロイされているリソースを表示できます。 次に、右クリックして **[管理]** を選択すると、リソース ダッシュボードにアクセスできます。  

これらのダッシュボードには、Azure portal で開くオプションなど、リソースに関する追加情報が表示されます。

## <a name="next-steps"></a>次のステップ
Azure Arc data services の詳細については、[Microsoft のドキュメントをご確認ください](/azure/azure-arc/data/)。