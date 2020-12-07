---
title: キーマップ拡張機能の作成
description: このチュートリアルでは、カスタム機能を Azure Data Studio に追加するキーマップ拡張機能を作成する方法について説明します。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu
ms.custom: ''
ms.date: 08/28/2020
ms.openlocfilehash: 76fd809993b47f3ae3dad363887eb9ac735e6b0b
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364079"
---
# <a name="create-an-azure-data-studio-keymap-extension"></a>Azure Data Studio キーマップ拡張機能を作成する

このチュートリアルでは、新しい Azure Data Studio 拡張機能を作成する方法について説明します。 この拡張機能では、使い慣れた SSMS キーバインドが Azure Data Studio で作成されます。

この記事では、次の方法について説明します。
> [!div class="checklist"]
> - 拡張機能プロジェクトを作成する
> - 拡張機能ジェネレーターをインストールする
> - 拡張機能を作成する
> - カスタム キーバインディングを拡張機能に追加する
> - 拡張機能をテストする
> - 拡張機能をパッケージ化する
> - 拡張機能をマーケットプレースに公開する

## <a name="prerequisites"></a>前提条件

Azure Data Studio は Visual Studio Code と同じフレームワーク上に構築されるため、Azure Data Studio の拡張機能は Visual Studio Code を使用して構築されます。 開始するには、次のコンポーネントが必要です。

- `$PATH` にインストールされ、利用できる [Node.js](https://nodejs.org)。 Node.js には、拡張機能ジェネレーターのインストールに使用される [npm](https://www.npmjs.com/) (Node.js パッケージ マネージャー) が含まれています。
- 拡張機能をデバッグするための [Visual Studio Code](https://code.visualstudio.com)。
- The Azure Data Studio [Debug 拡張機能](https://marketplace.visualstudio.com/items?itemName=ms-mssql.sqlops-debug) (任意)。 これにより、パッケージ化して Azure Data Studio にインストールしなくても拡張機能をテストできます。
- 確実に `azuredatastudio` をパスに含めます。 Windows の場合、setup.exe で `Add to Path` オプションを選択します。 Mac または Linux の場合、*[PATH 内に 'azuredatastudio' コマンドをインストールします]* オプションを実行します。

## <a name="install-the-extension-generator"></a>拡張機能ジェネレーターをインストールする

拡張機能作成のプロセスを簡単にするため、Yeoman を利用して[拡張機能ジェネレーター](https://code.visualstudio.com/docs/extensions/yocode)を構築しました。 これをインストールするには、コマンド プロンプトで次のコードを実行します。

```console
`npm install -g yo generator-azuredatastudio`
```

## <a name="create-your-keymap-extension"></a>キーマップ拡張機能を作成する

拡張機能を作成するには: 

1. 次のコマンドを使用して拡張機能ジェネレーターを起動します。

   `yo azuredatastudio`

2. 拡張機能の種類の一覧から **[新しいキーマップ]** を選択します。

   :::image type="content" source="media/keymap-extension/extension-generator.png" alt-text="拡張機能ジェネレーター":::

3. 次の手順に従って拡張機能名を入力し (このチュートリアルでは **ssmskeymap2** を使用)、説明を追加します。

前の手順を完了すると、新しいフォルダーが作成されます。 Visual Studio Code でフォルダーを開きます。これで独自のキー バインド拡張機能を作成する準備ができました。

### <a name="add-a-keyboard-shortcut"></a>キーボード ショートカットを追加する

**ステップ 1:置換するショートカットを見つける**

拡張機能を準備できたので、いくつかの SSMS キーボード ショートカット (またはキーバインド) を Azure Data Studio に追加します。 今回、[Andy Mallon のチートシート](https://am2.co/2018/02/updated-cheat-sheet/)と RedGate のキーボード ショートカットの一覧を参考にしています。

不足していた重要なショートカット:

- 実際の実行プランを有効にしてクエリを実行します。 これは SSMS では **Ctrl + M** ですが、Azure Data Studio にはバインドがありません。
- **Ctrl + SHIFT + E** をクエリ実行の 2 つ目の方法にします。 ユーザーからのフィードバックにより、これが不足していたことが示されました。
- **ALT + F1** で `sp_help` を実行します。 Azure Data Studio でこれを追加しましたが、そのバインドは既に使用されていたため、代わりに **ALT+F2** にマッピングしました。
- 全画面表示の切り替え (**SHIFT + ALT + ENTER**)。
- **F8** で **[オブジェクト エクスプローラー** / **サーバー ビュー]** を表示します。

これらのキー バインドは簡単に見つけて置換できます。 *[キーボード ショートカットを開く]* を実行して Azure Data Studio で **[キーボード ショートカット]** タブを表示し、「*query*」で検索し、**[Change Key binding]\(キー バインドの変更\)** を選択します。 キー バインドを変更すると、更新後のマッピングを keybindings.json ファイルで確認できます (*[キーボード ショートカットを開く]* を実行すると表示されます)。

:::image type="content" source="media/keymap-extension/keyboard-shortcuts.png" alt-text="キーボード ショートカット":::

:::image type="content" source="media/keymap-extension/key-bindings-json.png" alt-text="Keybindings.json 拡張機能":::

**手順 2:拡張機能にショートカットを追加する**

拡張機能にショートカットを追加するには、(拡張機能の) *package.json* ファイルを開き、`contributes` セクションを次のコードに置換します。

```json
"contributes": {
  "keybindings": [
    {
      "key": "shift+cmd+e",
      "command": "runQueryKeyboardAction"
    },
    {
      "key": "ctrl+cmd+e",
      "command": "workbench.view.explorer"
    },
    {
      "key": "alt+f1",
      "command": "workbench.action.query.shortcut1"
    },
    {
      "key": "shift+alt+enter",
      "command": "workbench.action.toggleFullScreen"
    },
    {
      "key": "f8",
      "command": "workbench.view.connections"
    },
    {
      "key": "ctrl+m",
      "command": "runCurrentQueryWithActualPlanKeyboardAction"
    }
  ]
}
```

## <a name="test-your-extension"></a>拡張機能をテストする

Azure Data Studio で [PATH 内に 'azuredatastudio' コマンドをインストールします] コマンドを実行し、確実に PATH に `azuredatastudio` が含まれているようにします。

Azure Data Studio Debug 拡張機能を、確実に Visual Studio Code にインストールします。

**F5** を選択すると、Azure Data Studio がデバッグ モードで起動し、拡張機能が実行されます。

:::image type="content" source="media/keymap-extension/install-extension.png" alt-text="拡張機能のインストール":::

:::image type="content" source="media/keymap-extension/test-extension.png" alt-text="拡張機能のテスト":::

キー マップは、最も簡単に作成できる拡張機能の 1 つです。新しい拡張機能は正常に動作し、共有できるはずです。

## <a name="package-your-extension"></a>拡張機能をパッケージ化する

他者と共有するには、拡張機能を 1 つのファイルにパッケージ化する必要があります。 ファイルは Azure Data Studio 拡張機能マーケットプレースに公開するか、チームやコミュニティで共有できます。 それを行うには、別の npm パッケージをコマンド ラインからインストールする必要があります。

```console
`npm install -g vsce`
```

拡張機能のベース ディレクトリに移動し、`vsce package` を実行します。 *vsce* ツールからの不満を解消する目的で余計な行をいくつか追加する必要がありました。

```json
"repository": {
    "type": "git",
    "url": "https://github.com/kevcunnane/ssmskeymap.git"
},
"bugs": {
    "url": "https://github.com/kevcunnane/ssmskeymap/issues"
},
```

それが完了したとき、ssmskeymap-0.1.0.vsix ファイルが作成され、インストールし、世界中の人と共有する準備ができました。

:::image type="content" source="media/keymap-extension/extensions.png" alt-text="インストール":::

## <a name="publish-your-extension-to-the-marketplace"></a>拡張機能をマーケットプレースに公開する

Azure Data Studio 拡張機能マーケットプレースはまだ完成していません。現行のプロセスでは、拡張機能 VSIX をどこか (GitHub リリース ページなど) でホストしてから、[こちらの JSON ファイル](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json)をご自分の拡張機能情報で更新する PR を送信します。

## <a name="next-steps"></a>次のステップ

このチュートリアルでは、以下の内容を学習しました。
> [!div class="checklist"]
> - 拡張機能プロジェクトを作成する
> - 拡張機能ジェネレーターをインストールする
> - 拡張機能を作成する
> - カスタム キーバインディングを拡張機能に追加する
> - 拡張機能をテストする
> - 拡張機能をパッケージ化する
> - 拡張機能をマーケットプレースに公開する

読了後、Azure Data Studio の拡張機能を自分でも作るべく奮起していただけたら幸いです。 Dashboard Insights (SQL Server に対して実行される美麗なグラフ)、さまざまな SQL 固有 API、Visual Studio Code から継承された大量の既存の拡張ポイント セットをサポートしています。

アイデアはあるが、どのように始めたらいいのかわからない場合は、お問い合わせいただくか、チーム宛てにツイートしてください ([azuredatastudio](https://twitter.com/azuredatastudio))。

[Visual Studio Code 拡張ガイド](https://code.visualstudio.com/docs/extensions/overview)では、既存の API やパターンがすべて取り上げられているので、いつでも参考にできます。

Azure Data Studio で T-SQL を使用する方法については、T-SQL エディターのチュートリアルを完了してください。

> [!div class="nextstepaction"]
> [Transact-SQL エディターを使用し、データベース オブジェクトを作成する](../tutorial-sql-editor.md)
