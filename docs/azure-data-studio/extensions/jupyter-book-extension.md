---
title: Jupyter Book 拡張機能を作成する
description: 拡張機能ジェネレーターを使用して Jupyter Book を拡張機能にパッケージ化する方法について説明します。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: alayu, maghan
ms.custom: ''
ms.date: 08/28/2020
ms.openlocfilehash: 5d9138a5d02008cc173bc7f0b64d354d67112d3b
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364089"
---
# <a name="create-a-jupyter-book-extension"></a>Jupyter Book 拡張機能を作成する

このチュートリアルでは、新しい Jupyter Book Azure Data Studio 拡張機能を作成する方法について説明します。 この拡張機能では、Azure Data Studio で開いて実行できる Jupyter Book のサンプルが送信されます。

この記事では、次の方法について説明します。

> [!div class="checklist"]
> - 拡張機能プロジェクトを作成する。
> - 拡張機能ジェネレーターをインストールする。
> - Jupyter Book 拡張機能を作成する。
> - 拡張機能を実行する。
> - 拡張機能をパッケージ化する。
> - 拡張機能をマーケットプレースに公開する。

## <a name="apis-used"></a>使用される API

- `bookTreeView.openBook`

### <a name="extension-use-cases"></a>拡張機能のユース ケース

Jupyter Book 拡張機能を作成する理由はいくつかあります。

- 編成されセクションに分けられた対話型ドキュメントを共有する
- 完全なブック (電子書籍に似ているが、Azure Data Studio を通じて配布される) を共有する
- Jupyter Book の更新プログラムをバージョン管理して追跡する

Jupyter Book 拡張機能とノートブック拡張機能の主な違いは、Jupyter Book では編成が可能であることです。 Jupyter Book では、数十のノートブックを異なるチャプターに分割できますが、ノートブック拡張機能は、少数の個別ノートブックを送信することを目的としています。

## <a name="prerequisites"></a>前提条件

Azure Data Studio は Visual Studio Code と同じフレームワーク上に構築されるため、Azure Data Studio の拡張機能は、Visual Studio Code を使用して構築します。 開始するには、次のコンポーネントが必要です。

- `$PATH` にインストールされ、利用できる [Node.js](https://nodejs.org)。 Node.js には、拡張機能ジェネレーターのインストールに使用される [npm](https://www.npmjs.com/) (Node.js パッケージ マネージャー) が含まれています。
- 拡張機能に変更を加えたり、拡張機能をデバッグしたりするための [Visual Studio Code](https://code.visualstudio.com)。
- 確実に `azuredatastudio` をパスに含めます。 Windows の場合、setup.exe で **[Add to Path]\(パスに追加\)** オプションを選択します。 Mac または Linux の場合、**[PATH 内に 'azuredatastudio' コマンドをインストールします]** オプションを実行します。

## <a name="install-the-extension-generator"></a>拡張機能ジェネレーターをインストールする

拡張機能作成のプロセスを簡単にするため、Yeoman を利用して[拡張機能ジェネレーター](https://www.npmjs.com/package/generator-azuredatastudio)を構築しました。 これをインストールするには、コマンド プロンプトから次のコマンドを実行します。

```console
`npm install -g yo generator-azuredatastudio`
```

## <a name="create-your-extension"></a>拡張機能を作成する

拡張機能を作成するには: 

1. 次のコマンドを使用して拡張機能ジェネレーターを起動します。

   `yo azuredatastudio`

1. 拡張機能の種類の一覧から **[New Jupyter Book]\(新しい Jupyter Book\)** を選択します。

   :::image type="content" source="media/jupyter-book-extension/jupyter-book-extension-generator.png" alt-text="拡張機能ジェネレーターを示すスクリーンショット。":::

1. 手順に従って、拡張機能の名前を入力します。 このチュートリアルでは、「**Test Book**」を使用します。 次に、公開元の名前を入力します。 このチュートリアルでは、「**Microsoft**」を使用します。 最後に、説明を追加します。

既存の Jupyter Book を提供するか、提供されているサンプルを使用するか、または新しい Jupyter Book を作成するかを選択します。 3 つのオプションがすべて表示されます。

### <a name="provide-an-existing-book"></a>既存のブックを提供する

既に作成したブックを送信する場合は、ブックのコンテンツが含まれているフォルダーへの絶対ファイル パスを指定します。 その後、拡張機能について学習し、送信する準備が整います。

:::image type="content" source="media/jupyter-book-extension/jupyter-book-existing-book.png" alt-text="既存のブックを示すスクリーンショット。":::

### <a name="use-the-sample-book"></a>サンプル ブックを使用する

既存のブックまたはノートブックがない場合は、提供されているサンプルをジェネレーターで使用できます。

:::image type="content" source="media/jupyter-book-extension/jupyter-book-sample-path.png" alt-text="サンプル Jupyter ブックを示すスクリーンショット。":::

このサンプル ブックは、単純な Jupyter Book の外観を示しています。 Jupyter Book のカスタマイズの詳細については、既存のノートブックを使用して新しいブックを作成する方法に関する次のセクションを参照してください。

### <a name="create-a-new-book"></a>新しいブックを作成する

Jupyter Book にパッケージ化するノートブックがある場合は、パッケージ化を行うことができます。 ジェネレーターによって、ブック内にチャプターを設定するかどうかが確認され、設定する場合はその数とタイトルが求められます。 選択プロセスがどのようなものかをここで確認できます。 スペースバーを使用して、各チャプターに配置するノートブックを選択します。

:::image type="content" source="media/jupyter-book-extension/jupyter-book-create-book.png" alt-text="Jupyter ブックの作成を示すスクリーンショット。":::

前の手順を完了すると、新しい Jupyter Book を含む新しいフォルダーが作成されます。 Visual Studio Code でフォルダーを開くと、Jupyter Book 拡張機能を送信する準備が整います。

## <a name="understand-your-extension"></a>拡張機能を理解する

この時点で、プロジェクトは次のように表示されます。

   :::image type="content" source="media/jupyter-book-extension/jupyter-book-file-structure-generator.png" alt-text="拡張ファイルの構造を示すスクリーンショット。":::

`vsc-extension-quickstart.md` ファイルには、重要なファイルのリファレンスが用意されています。 `README.md` は、新しい拡張機能のドキュメントを提供できるファイルです。 `package.json`、`jupyter-book.ts`、`content`、`toc.yml` のファイルに注目してください。 `content` フォルダーには、すべてのノートブック ファイルまたはマークダウン ファイルが格納されています。 `toc.yml` は、これによって Jupyter Book が構造化され、拡張機能ジェネレーターを使用してカスタム Jupyter Book を作成することを選択した場合に自動生成されます。

ジェネレーターを使用してブックを作成し、ブック内にチャプターを設定することを選択した場合、フォルダー構造は少し異なります。 `content` フォルダーには、マークダウン ファイルと Jupyter Notebook ファイルの代わりに、チャプターに対して選択するタイトルに対応するサブフォルダーが含まれます。

公開したくないファイルまたはフォルダーがある場合は、その名前を `.vscodeignore` ファイルに含めることができます。

`jupyter-book.ts` を確認して、新しく作成した拡張機能の動作を見てみましょう。

```javascript
// This function is called when you run the command `Launch Book: Test Book` from the
// command palette in Azure Data Studio. If you want any additional functionality
// to occur when you launch the book, add it to the activate function.
export function activate(context: vscode.ExtensionContext) {
    context.subscriptions.push(vscode.commands.registerCommand('launchBook.test-book', () => {
        processNotebooks();
    }));

    // Add other code here if you want to register another command.
}
```

`activate` 関数は、拡張機能の主要なアクションです。 登録するコマンドは、`launchBook.test-book` コマンドと同様に `activate` 関数内に表示される必要があります。 `processNotebooks` 関数の内部で、Jupyter Book が格納されている拡張機能フォルダーを見つけ、拡張機能フォルダーをパラメーターとして使用して `bookTreeView.openBook` を呼び出します。

また、`package.json` ファイルは、拡張機能のコマンドを登録するときに重要な役割を果たします。

```json
"activationEvents": [
        "onCommand:launchBook.test-book"
    ],
    "main": "./out/notebook.js",
    "contributes": {
        "commands": [
            {
                "command": "launchBook.test-book",
                "title": "Launch Book: Test Book"
            }
        ]
    }
```

アクティブ化イベント `onCommand` によって、コマンドを呼び出すときに登録した関数がトリガーされます。 他にも追加のカスタマイズが可能なアクティブ化イベントがいくつかあります。 詳細については、[アクティブ化イベント](https://code.visualstudio.com/api/references/activation-events)に関するページをご覧ください。

## <a name="package-your-extension"></a>拡張機能をパッケージ化する

他者と共有するには、拡張機能を 1 つのファイルにパッケージ化する必要があります。 拡張機能は、Azure Data Studio 拡張機能マーケットプレースに公開することも、チームまたはコミュニティと共有することもできます。 この手順を行うには、別の npm パッケージをコマンド ラインからインストールする必要があります。

```console
`npm install -g vsce`
```

`README.md` ファイルを好みに合わせて編集します。 次に、拡張機能のベース ディレクトリに移動し、`vsce package` を実行します。 必要に応じてリポジトリを拡張機能とリンクすることも、それなしで続行することもできます。 1 つ追加するには、`package.json` ファイルに同様の行を追加します。

```json
"repository": {
    "type": "git",
    "url": "https://github.com/laurajjiang/testbook.git"
}
```

これらの行が追加されると、`my test-book-0.0.1.vsix` ファイルが作成され、Azure Data Studio にインストールできるようになります。

## <a name="run-your-extension"></a>拡張機能を実行する

拡張機能を実行してテストするには、Azure Data Studio を開き、**Ctrl + Shift + P** を選択してコマンド パレットを開きます。 コマンド **Extensions: Install from VSIX** を見つけて、新しい拡張機能が格納されているフォルダーに移動します。 この時点で、Azure Data Studio の拡張機能パネルに表示されます。

   :::image type="content" source="media/jupyter-book-extension/install-vsix.png" alt-text="VSIX のインストールを示すスクリーンショット。":::

コマンド パレットをもう一度開き、登録したコマンドを見つけます: **Launch Book:Test Notebook\(ノートブックの起動: Test Notebook\)** を登録する場合にも重要な役割を果たします。 実行すると、拡張機能とともにパッケージ化した Jupyter Book が開きます。

   :::image type="content" source="media/jupyter-book-extension/jupyter-book-launch-ads.png" alt-text="ノートブック コマンドを示すスクリーンショット。":::

おめでとうございます! これで、最初の Jupyter Book 拡張機能がビルドされ、送信できるようになりました。 Jupyter Book の詳細については、「[Books with Jupyter](https://jupyterbook.org/intro.html)」(Jupyter で作る本) を参照してください。

## <a name="publish-your-extension-to-the-marketplace"></a>拡張機能をマーケットプレースに公開する

Azure Data Studio 拡張機能マーケットプレースはまだ完成していません。 公開するには、たとえば、GitHub リリース ページで拡張機能の VSIX をホストします。 [こちらの JSON ファイル](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json)をご自分の拡張機能情報で更新するプル要求を送信します。

## <a name="next-steps"></a>次のステップ

このチュートリアルでは、以下の内容を学習しました。
> [!div class="checklist"]
> - 拡張機能プロジェクトを作成する。
> - 拡張機能ジェネレーターをインストールする。
> - Jupyter Book 拡張機能を作成する。
> - 拡張機能をパッケージ化する。
> - 拡張機能をマーケットプレースに公開する。

この記事を読むことで、Jupyter Book に関して Azure Data Studio コミュニティと共有したくなるアイデアが得られることを願っています。

アイデアをお持ちで、始める方法に迷われている場合は、チーム宛てに問題をお送りいただくかツイート ([azuredatastudio](https://twitter.com/azuredatastudio)) してください。

詳細については、[Visual Studio Code 拡張機能ガイド](https://code.visualstudio.com/docs/extensions/overview)に関するページをご覧ください。既存の API とパターンがすべて網羅されています。
