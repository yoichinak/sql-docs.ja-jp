---
title: ウィザード拡張機能を作成する
description: このチュートリアルでは、カスタム機能を Azure Data Studio に追加するウィザード拡張機能を作成する方法について説明します。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: maghan
ms.custom: ''
ms.date: 08/28/2020
ms.openlocfilehash: 50440aca120dad6cfd165262bd4bfd2e139393cf
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364059"
---
# <a name="create-an-azure-data-studio-wizard-extension"></a>Azure Data Studio のウィザード拡張機能を作成する

このチュートリアルでは、新しい **Azure Data Studio のウィザード拡張機能**を作成する方法について説明します。 この拡張機能は、Azure Data Studio でのウィザードとユーザーのやりとりに役立ちます。

この記事では、次の方法について説明します。
> [!div class="checklist"]
> - 拡張機能ジェネレーターをインストールする
> - 拡張機能を作成する
> - 拡張機能にカスタム ウィザードを追加する
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

拡張機能作成のプロセスを簡単にするため、Yeoman を利用して[拡張機能ジェネレーター](https://code.visualstudio.com/docs/extensions/yocode)を構築しました。 これをインストールするには、コマンド プロンプトから次を実行します。

```console
`npm install -g yo generator-azuredatastudio`
```

## <a name="create-your-wizard-extension"></a>ウィザード拡張機能を作成する

### <a name="introduction-to-wizards"></a>ウィザードの概要

ウィザードはユーザー インターフェイスの一種であり、タスクを完了するために、ユーザーが入力するページを手順ごとに表示するものです。 一般的な例として、ソフトウェアのセットアップ ウィザードやトラブルシューティング ウィザードなどがあります。 次に例を示します。

:::image type="content" source="media/wizard-extension/dacpac-wizard.gif" alt-text="Dacpac ウィザード":::

ウィザードは、データを操作して Azure Data Studio の機能を拡張するときに役立つことが多いため、Azure Data Studio には、ユーザー独自のカスタム ウィザードを作成する API が用意されています。 ここでは、ウィザード テンプレートを生成し、それを変更して独自のカスタム ウィザードを作成する方法について説明します。

### <a name="run-the-extension-generator"></a>拡張機能ジェネレーターを実行する

拡張機能を作成するには: 

1. 次のコマンドを使用して拡張機能ジェネレーターを起動します。

   `yo azuredatastudio`

2. 拡張機能の種類一覧から **[New Wizard or Dialog]\(新しいウィザードまたはダイアログ\)** を選択します。 次に、 **[ウィザード]** 、 **[Getting Started Template]\(テンプレートの開始\)** の順に選択します。

3. 次の手順に従って拡張機能名を入力し (このチュートリアルでは **My Test Extension** を使用)、説明を追加します。

    :::image type="content" source="media/wizard-extension/extension-generator.png" alt-text="拡張機能ジェネレーター":::

前の手順を完了すると、新しいフォルダーが作成されます。 Visual Studio Code でフォルダーを開きます。これで独自のウィザード拡張機能を作成する準備ができました。

### <a name="run-the-extension"></a>拡張機能を実行する

拡張機能を実行して、ウィザード テンプレートが提供する内容を見てみましょう。 実行する前に、**Azure Data Studio Debug 拡張機能**を、確実に Visual Studio Code にインストールします。

VS Code で **F5** を選択します。すると、Azure Data Studio がデバッグ モードで起動し、拡張機能が実行されます。 次に、Azure Data Studio で、新しいウィンドウのコマンド パレット (Ctr + Shift + P キー) から **[Launch Wizard]\(ウィザードの起動\)** コマンドを実行します。 その結果、この拡張機能によって提供される既定のウィザードが起動します。

:::image type="content" source="media/wizard-extension/wizard-template.gif" alt-text="ウィザード テンプレート":::

次に、この既定のウィザードを変更する方法を見ていきます。

### <a name="develop-the-wizard"></a>ウィザードを開発する

拡張機能の開発を始める上で最も重要なファイルは、`package.json`、`src/main.ts`、および `vsc-extension-quickstart.md` です。

- `package.json`:これはマニフェスト ファイルです。ここに **[Launch Wizard]\(ウィザードの起動\)** コマンドが登録されます。 これは、`main.ts` がメイン プログラムのエントリ ポイントとして宣言されている場所でもあります。
- `main.ts`:ページ、テキスト、ボタンなどの UI 要素をウィザードに追加するコードが含まれています
- `vsc-extension-quickstart.md`:開発時に参考になる可能性のある技術ドキュメントが含まれています

ウィザードを変更してみましょう。4 ページ目として空白のページを追加します。 以下に示すように `src/main.ts` を変更すると、ウィザードを起動したときに追加のページが表示されます。

:::image type="content" source="media/wizard-extension/wizard-main.png" alt-text="ウィザードのメイン":::
テンプレートについて理解したら、その他のアイデアを試してみてください。

- 新しいページに 300 の幅のボタンを追加します
- 可変コンポーネントを追加してボタンを配置します
- ボタンにアクションを追加します。 たとえば、ボタンがクリックされたとき、ファイルを開くダイアログを起動したり、クエリ エディターを開いたりします。

## <a name="package-your-extension"></a>拡張機能をパッケージ化する

他者と共有するには、拡張機能を 1 つのファイルにパッケージ化する必要があります。 ファイルは Azure Data Studio 拡張機能マーケットプレースに公開するか、チームやコミュニティで共有できます。 それを行うには、別の npm パッケージをコマンド ラインからインストールする必要があります。

```console
npm install -g vsce`
```

`README.md` を好みに応じて編集し、次に拡張機能のベース ディレクトリに移動して、`vsce package` を実行します。 必要に応じてリポジトリを拡張機能とリンクすることも、それなしで続行することもできます。 1 つ追加するには、`package.json` ファイルに同様の行を追加します。

```json
"repository": {
    "type": "git",
    "url": "https://github.com/anjalia/my-test-extension.git"
}
```

これらの行が追加されると、my-test-extension-0.0.1.vsix ファイルが作成され、Azure Data Studio にインストールできるようになります。

:::image type="content" source="media/wizard-extension/install-vsix.png" alt-text="VSIX のインストール":::

## <a name="publish-your-extension-to-the-marketplace"></a>拡張機能をマーケットプレースに公開する

Azure Data Studio 拡張機能マーケットプレースはまだ完全には実装されておらず、現行のプロセスは、拡張機能 VSIX をどこか (GitHub リリース ページなど) でホストし、その後、PR を送信し、[この JSON ファイル](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json)を自分の拡張機能情報で更新するというものです。

## <a name="next-steps"></a>次のステップ

このチュートリアルでは、以下の内容を学習しました。
> [!div class="checklist"]
> - 拡張機能ジェネレーターをインストールする
> - 拡張機能を作成する
> - 拡張機能にカスタム ウィザードを追加する
> - 拡張機能をテストする
> - 拡張機能をパッケージ化する
> - 拡張機能をマーケットプレースに公開する

読了後、Azure Data Studio の拡張機能を自分でも作るべく奮起していただけたら幸いです。 Dashboard Insights (SQL Server に対して実行される美麗なグラフ)、さまざまな SQL 固有 API、Visual Studio Code から継承された大量の既存の拡張ポイント セットをサポートしています。

アイデアはあるが、どこから始めたらいいのかわからない場合、チーム宛に問題提起またはツイートしてください ([azuredatastudio](https://twitter.com/azuredatastudio))。

[Visual Studio Code 拡張ガイド](https://code.visualstudio.com/docs/extensions/overview)では、既存の API やパターンがすべて取り上げられているので、いつでも参考にできます。

Azure Data Studio で T-SQL を使用する方法については、T-SQL エディターのチュートリアルを完了してください。

> [!div class="nextstepaction"]
> [Transact-SQL エディターを使用し、データベース オブジェクトを作成する](../tutorial-sql-editor.md)
