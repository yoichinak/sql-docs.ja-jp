---
title: Azure Data Studio の Notebooks と Kusto Kernel
description: このチュートリアルでは、Kusto ノートブックを作成し、実行する方法について説明します。
ms.topic: how-to
ms.prod: azure-data-studio
ms.technology: azure-data-studio
author: markingmyname
ms.author: maghan
ms.reviewer: jukoesma
ms.custom: ''
ms.date: 09/22/2020
ms.openlocfilehash: a8379e10e8c3e3af64381e9a4536b253e203964e
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725126"
---
# <a name="create-and-run-a-kusto-kql-notebook-preview"></a>Kusto (KQL) ノートブックの作成と実行 (プレビュー)

この記事では、Azure Data Explorer クラスターに接続する [Kusto (KQL) 拡張機能](../extensions/kusto-extension.md)を使用して、[Azure Data Studio ノートブック](./notebooks-guidance.md)を作成して実行する方法について説明します。

Kusto (KQL) 拡張機能を使用すると、カーネル オプションを **Kusto** に変更できます。

現在、この機能はプレビュー段階にあります。

## <a name="prerequisites"></a>前提条件

Azure サブスクリプションをお持ちでない場合は、開始する前に[無料の Azure アカウント](https://azure.microsoft.com/free/)を作成してください。

- [接続可能なデータベースを備えた Azure Data Explorer クラスター](/azure/data-explorer/create-cluster-database-portal)。
- [Azure Data Studio](../download-azure-data-studio.md)
- [Azure Data Studio 用の Kusto (KQL) 拡張機能](../extensions/kusto-extension.md)。

## <a name="create-a-kusto-kql-notebook"></a>Kusto (KQL) ノートブックを作成する

次の手順では、Azure Data Studio でノートブック ファイルを作成する方法を示しています。

1. Azure Data Studio で、Azure Data Explorer クラスターに接続します。

2. **[接続]** ペインに移動し、 **[サーバー]** ウィンドウで [Kusto データベース] を右クリックして、 *[新しいノートブック]* を選択します。 または、 **[ファイル]**  >  **[新しいノートブック]** に移動します。

   :::image type="content" source="media/notebooks-kusto-kernel/kusto-new-notebook.png" alt-text="ノートブックを開く":::

3. **[カーネル]** として、 *[Kusto]* を選択します。 **[アタッチ先]** メニューがクラスター名とデータベースに設定されていることを確認します。 この記事では、サンプル データベース データを備えた help.kusto.windows.net クラスターを使用します。

   :::image type="content" source="media/notebooks-kusto-kernel/set-kusto-kernel.png" alt-text="ノートブックを開く":::

ノートブックを保存するには、 **[ファイル]** メニューで **[保存]** または **[名前を付けて保存...]** コマンドを使用します。

ノートブックを開くには、 **[ファイル]** メニューで **[ファイルを開く...]** コマンドを使用して、 **[ようこそ]** ページで **[ファイルを開く]** を選択するか、コマンド パレットで **File:Open** コマンドを使用します。

## <a name="change-the-connection"></a>接続の変更

ノートブックの Kusto 接続を変更するには、次のようにします。

1. ノートブック ツール バーから **[アタッチ先]** メニューを選択し、 **[接続の変更]** を選択します。

   :::image type="content" source="media/notebooks-kusto-kernel/kusto-select-attach-to-change-connections.png" alt-text="ノートブックを開く":::

   > [!Note]
   > データベースの値を確実に入力します。 Kusto ノートブックで、データベースを指定する必要があります。

2. これで最近使用した接続サーバーを選択するか、新しい接続の詳細を入力して接続できます。

   :::image type="content" source="media/notebooks-kusto-kernel/kusto-change-connection-cluster.png" alt-text="ノートブックを開く":::

   > [!Note]
   > クラスター名は、`https://` を含めずに指定してください。

## <a name="run-a-code-cell"></a>コード セルを実行する

セルの左側にある **[セルの実行]** ボタンを選択することで適切に実行できる KQL クエリを含むセルを作成できます。 セルが実行された後、結果がノートブックに表示されます。

次に例を示します。

1. ツールバーの **[+Code]** コマンドを選択して、新しいコード セルを追加します。

   :::image type="content" source="media/notebooks-kusto-kernel/kusto-kernel-code.png" alt-text="ノートブックを開く":::

2. 次の例をコピーしてセルに貼り付け、 **[セルの実行]** を選択します。 この例では、特定のイベントの種類について StormEvents データに対してクエリを実行します。

   ```kusto
    StormEvents
    | where EventType == "Waterspout"
   ```

   :::image type="content" source="media/notebooks-kusto-kernel/run-kusto-notebook-cell.png" alt-text="ノートブックを開く":::

## <a name="save-the-result-or-show-chart"></a>結果を保存する、またはグラフを表示する

結果を返すスクリプトを実行する場合、結果の上部に表示されるツールバーを使用して、その結果を別の形式で保存できます。

- CSV として保存
- Excel として保存
- JSON として保存
- XML として保存
- グラフの表示

```kusto
    StormEvents
    | limit 10
```

:::image type="content" source="media/notebooks-kusto-kernel/run-notebook-save-results.png" alt-text="ノートブックを開く":::

## <a name="known-issues"></a>既知の問題

| 詳細 | 回避策 |
|---------|------------|
| [クエリ結果には、列ヘッダーのみが表示されます](https://github.com/microsoft/azuredatastudio/issues/12565)。 | 該当なし |

製品チームにフィードバックを提供するために、[機能の要求](https://github.com/microsoft/azuredatastudio/issues/new?assignees=&labels=&template=feature_request.md&title=)を提出できます。  
製品チームにフィードバックを提供するために、[バグ](https://github.com/microsoft/azuredatastudio/issues/new?assignees=&labels=&template=bug_report.md&title=)を提出できます。

## <a name="next-steps"></a>次のステップ

ノートブックについてさらに学習します:

- [Azure Data Studio 用の Kusto (KQL) 拡張機能](../extensions/kusto-extension.md)
- [Azure Data Studio でノートブックを使用する方法](./notebooks-guidance.md)
- [Python ノートブックを作成して実行する](./notebooks-python-kernel.md)
- [SQL Server ノートブックを作成して実行する](./notebooks-sql-kernel.md)