---
title: ダッシュボード拡張機能を作成する
description: このチュートリアルでは、カスタム機能を Azure Data Studio に追加するダッシュボード拡張機能を作成する方法について説明します。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: alayu, maghan
ms.custom: ''
ms.date: 08/28/2020
ms.openlocfilehash: 091bf94f01c66b3f991c0457adcfa4d119d49167
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364099"
---
# <a name="create-an-azure-data-studio-dashboard-extension"></a>Azure Data Studio ダッシュボード拡張機能を作成する

このチュートリアルでは、新しい Azure Data Studio ダッシュボード拡張機能を作成する方法について説明します。 この拡張機能は Azure Data Studio 接続ダッシュボードで役立つので、Azure Data Studio の機能をユーザーが見やすいように拡張することができます。

この記事では、次の方法について説明します。

> [!div class="checklist"]
> - 拡張機能ジェネレーターをインストールする。
> - 拡張機能を作成する。
> - 拡張機能のダッシュボードに役立つようにする。
> - 拡張機能をテストする。
> - 拡張機能をパッケージ化する。
> - 拡張機能をマーケットプレースに公開する。

## <a name="prerequisites"></a>前提条件

Azure Data Studio は Visual Studio Code と同じフレームワーク上に構築されるため、Azure Data Studio の拡張機能は、Visual Studio Code を使用して構築します。 開始するには、次のコンポーネントが必要です。

- `$PATH` にインストールされ、利用できる [Node.js](https://nodejs.org)。 Node.js には、拡張機能ジェネレーターのインストールに使用される [npm](https://www.npmjs.com/) (Node.js パッケージ マネージャー) が含まれています。
- 拡張機能をデバッグするための [Visual Studio Code](https://code.visualstudio.com)。
- The Azure Data Studio [Debug 拡張機能](https://marketplace.visualstudio.com/items?itemName=ms-mssql.sqlops-debug) (任意)。 このデバッグ拡張機能を使用すると、拡張機能は、パッケージ化して Azure Data Studio にインストールしなくてもテストできます。
- 確実に `azuredatastudio` をパスに含めます。 Windows の場合、setup.exe で **[Add to Path]\(パスに追加\)** オプションを選択します。 Mac または Linux の場合、**[PATH 内に 'azuredatastudio' コマンドをインストールします]** オプションを実行します。

## <a name="install-the-extension-generator"></a>拡張機能ジェネレーターをインストールする

拡張機能作成のプロセスを簡単にするため、Yeoman を利用して[拡張機能ジェネレーター](https://code.visualstudio.com/docs/extensions/yocode)を構築しました。 これをインストールするには、コマンド プロンプトから次のコマンドを実行します。

```console
`npm install -g yo generator-azuredatastudio`
```

## <a name="create-your-dashboard-extension"></a>ダッシュボード拡張機能を作成する

### <a name="introduction-to-the-dashboard"></a>ダッシュボードの概要

Azure Data Studio 接続ダッシュボードとは、ユーザーの接続を要約すると共に分析情報を提供する強力なツールです。

ダッシュボードには 2 つのバリエーションがあります。 サーバー全体を要約する "*サーバー ダッシュボード*" と、個々のデータベースを要約する "*データベース ダッシュボード*" です。 Azure Data Studio の **[接続]** ビューレットでサーバーまたはデータベースを右クリックし、 **[管理]** を選択すると、いずれかのダッシュボードにアクセスできます。

:::image type="content" source="media/dashboard-extension/dashboard-summary.gif" alt-text="ダッシュボードの概要を示すスクリーンショット。":::

ダッシュボードに機能を追加するための拡張機能には、次の 3 つの主要なコントリビューション ポイントがあります。

1. **完全なダッシュボード タブ**:拡張機能のダッシュボードにある独立したタブ。 サーバーまたはデータベースのダッシュボードに追加できます。 ウィジェット、ツールバー、およびナビゲーション セクションでカスタマイズできます。
2. **ホームページの操作**: 接続ツールバーの上部にあるアクション ボタン。
3. **ウィジェット**: ご利用の SQL Server に対して実行されるグラフ。

   :::image type="content" source="media/dashboard-extension/dashboard-contrib-points.png" alt-text="コントリビューション ポイントを示すスクリーンショット。":::

### <a name="run-the-extension-generator"></a>拡張機能ジェネレーターを実行する

拡張機能を作成するには: 

1. 次のコマンドを使用して拡張機能ジェネレーターを起動します。

   `yo azuredatastudio`

1. 拡張機能の種類の一覧から **[新しいダッシュボード]** を選択します。

1. プロンプトに以下のように入力して、サーバー ダッシュボードにタブを提供する拡張機能を作成します。

   :::image type="content" source="media/dashboard-extension/dashboard-generator.png" alt-text="拡張機能ジェネレーターを示すスクリーンショット。":::

   プロンプトの数が多いため、各質問の意味についてもう少し詳しく説明します。

   :::image type="content" source="media/dashboard-extension/dashboard-flowchart.png" alt-text="ダッシュボードのフローチャートを示すスクリーンショット。":::

前の手順を完了すると、新しいフォルダーが作成されます。 Visual Studio Code でフォルダーを開きます。これで独自のダッシュボード拡張機能を作成する準備ができました。

### <a name="run-the-extension"></a>拡張機能を実行する

拡張機能を実行して、ダッシュボード テンプレートが提供する内容を見てみましょう。 実行する前に、**Azure Data Studio Debug 拡張機能**が確実に Visual Studio Code にインストールされているようにします。

Visual Studio Code で **F5** を選択すると、Azure Data Studio がデバッグ モードで起動され、拡張機能が実行されます。 この既定のテンプレートがダッシュボードにどのように役立つのかを確認できます。

次に、この既定のダッシュボードを変更する方法について説明します。

### <a name="develop-the-dashboard"></a>ダッシュボードを開発する

拡張機能の開発を始めるうえで最も重要なファイルは、`package.json` です。 このファイルは、ダッシュボードのコントリビューションが登録されているマニフェスト ファイルです。 `dashboard.tabs`、`dashboard.insights`、`dashboard.containers` の各セクションに注目してください。

ここで、いくつかの変更を試してみます。

- bar、horizontalBar、timeSeries などの分析情報の種類を試してみます。
- ご利用の SQL Server 接続に対して実行する独自のクエリを記述します。
- 具体的な分析情報チュートリアルについては、[サンプル分析情報チュートリアル](../tutorial-qds-sql-server.md)または[こちらのチュートリアル](../tutorial-table-space-sql-server.md)を参照してください。

## <a name="package-your-extension"></a>拡張機能をパッケージ化する

他者と共有するには、拡張機能を 1 つのファイルにパッケージ化する必要があります。 拡張機能は、Azure Data Studio 拡張機能マーケットプレースに公開することも、チームまたはコミュニティと共有することもできます。 この手順を行うには、別の npm パッケージをコマンド ラインからインストールする必要があります。

```console
`npm install -g vsce`
```

`README.md` ファイルを好みに合わせて編集します。 次に、拡張機能のベース ディレクトリに移動し、`vsce package` を実行します。 必要に応じてリポジトリを拡張機能とリンクすることも、それなしで続行することもできます。 1 つ追加するには、`package.json` ファイルに同様の行を追加します。

```json
"repository": {
    "type": "git",
    "url": "https://github.com/anjalia/my-test-extension.git"
}
```

これらの行が追加されると、`my-test-extension-0.0.1.vsix` ファイルが作成され、Azure Data Studio にインストールできるようになります。

:::image type="content" source="media/dashboard-extension/install-vsix.png" alt-text="VSIX のインストールを示すスクリーンショット。":::

## <a name="publish-your-extension-to-the-marketplace"></a>拡張機能をマーケットプレースに公開する

Azure Data Studio 拡張機能マーケットプレースはまだ完成していません。 現在のプロセスでは、拡張機能 VSIX をどこか (GitHub リリース ページなど) でホストします。 次に、[こちらの JSON ファイル](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json)をご自分の拡張機能情報で更新するプル要求を送信します。

## <a name="next-steps"></a>次のステップ

このチュートリアルでは、以下の内容を学習しました。
> [!div class="checklist"]
> - 拡張機能ジェネレーターをインストールする。
> - 拡張機能を作成する。
> - 拡張機能のダッシュボードに役立つようにする。
> - 拡張機能をテストする。
> - 拡張機能をパッケージ化する。
> - 拡張機能をマーケットプレースに公開する。

この記事を読むことで、Azure Data Studio の独自の拡張機能を構築するヒントが得られることを願っています。 Microsoft は Dashboard Insights (SQL Server に対して実行される魅力的なグラフ)、さまざまな SQL 固有 API、Visual Studio Code から継承された大量の既存の拡張ポイント セットをサポートしています。

アイデアをお持ちで、始める方法に迷われている場合は、チーム宛てに問題をお送りいただくかツイート ([azuredatastudio](https://twitter.com/azuredatastudio)) してください。

詳細については、[Visual Studio Code 拡張機能ガイド](https://code.visualstudio.com/docs/extensions/overview)に関するページをご覧ください。既存の API とパターンがすべて網羅されています。

Azure Data Studio で T-SQL を使用する方法については、T-SQL エディターのチュートリアルを完了してください。

> [!div class="nextstepaction"]
> [Transact-SQL エディターを使用し、データベース オブジェクトを作成する](../tutorial-sql-editor.md)
