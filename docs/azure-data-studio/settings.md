---
title: ユーザーとワークスペースの設定
description: 設定を使用し、Azure Data Studio のエディター、ユーザー インターフェイス、機能動作を自分の好みに合わせてカスタマイズする方法について説明します。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: how-to
author: yualan
ms.author: alayu
ms.reviewer: maghan, sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 06e9efa72ef82d8335db4b7ec6b8941c95501790
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364183"
---
# <a name="modify-user-and-workspace-settings"></a>ユーザーとワークスペースの設定を変更する

設定を使用すると、Azure Data Studio を好みに合わせて簡単に構成できます。 Azure Data Studio のエディター、ユーザー インターフェイス、機能的な動作のほとんどすべての部分に、変更可能なオプションがあります。

Azure Data Studio には、次の 2 つの異なる設定のスコープがあります。

* **ユーザー** - これらの設定は、開いた Azure Data Studio のインスタンスにグローバルに適用されます。
* **ワークスペース** - ワークスペースの設定は、コンピューター上のフォルダーに固有の設定であり、Explorer のサイドバーでフォルダーが開かれている場合のみ使用できます。 このスコープで定義された設定は、ユーザー スコープよりも優先されます。

## <a name="creating-user-and-workspace-settings"></a>ユーザーとワークスペースの設定を作成する

メニュー コマンド **[ファイル]** 、 **[基本設定]** 、 **[設定]** (Mac の場合は、 **[コード]** 、 **[基本設定]** 、 **[設定]** ) の順にクリックすると、ユーザーおよびワークスペースの設定の構成を開始できます。 既定の設定の一覧が表示されます。 変更する任意の設定を適切な `settings.json` ファイルにコピーします。 右側のタブでは、ユーザーとワークスペースの設定ファイル間をすばやく切り替えることができます。

また、**コマンド パレット** (**Ctrl + Shift + P**) からユーザーとワークスペースの設定を開くこともできます。ここで、 **[基本設定]: [ユーザー設定を開く]** および **[基本設定]: [ワークスペース設定を開く]** を使用します。またはキーボード ショートカット (**Ctrl +** ) を使用することもできます。

次の例は、エディターで行番号を無効にし、コード行が自動的にインデントされるように構成します。

![設定例](media/settings/sample-settings.png)

変更した `settings.json` ファイルを保存した後、設定の変更が Azure Data Studio によって再度読み込まれます。

> [!NOTE]
> ワークスペースの設定は、チーム全体でプロジェクト固有の設定を共有する場合に便利です。

## <a name="settings-file-locations"></a>設定ファイルの場所

ユーザー設定ファイルは、プラットフォームに応じて次の場所に格納されます。

* **Windows** `%APPDATA%\azuredatastudio\User\settings.json`
* **Mac** `$HOME/Library/Application Support/azuredatastudio/User/settings.json`
* **Linux** `$HOME/.config/azuredatastudio/User/settings.json`

ワークスペース設定ファイルは、プロジェクトの `.Azure Data Studio` フォルダーの下に格納されます。

## <a name="hot-exit"></a>Hot Exit

既定で、終了時に保存されていないファイルの変更は Azure Data Studio によって記憶されます。 Visual Studio Code では、これは Hot Exit 機能と同じです。

既定では、Hot Exit は無効になっています。 Hot Exit を有効にするには、`files.hotExit` 設定を編集します。 詳細については、「[Hot Exit (Visual Studio Code のドキュメント)](https://code.visualstudio.com/docs/editor/codebasics#_hot-exit)」を参照してください。

## <a name="tab-color"></a>タブの色

操作している接続を簡単に識別できるように、エディターで開くタブの色を、その接続が属しているサーバー グループの色と一致するように設定できます。 既定では、タブの色は無効になっています。 タブの色を有効にするには、`sql.tabColorMode` 設定を編集します。

## <a name="additional-resources"></a>その他のリソース

Azure Data Studio では、ユーザーとワークスペースの設定機能が Visual Studio Code から継承されているため、設定の詳細については、[Visual Studio Code の設定](https://code.visualstudio.com/docs/getstarted/settings)に関する記事を参照してください。
