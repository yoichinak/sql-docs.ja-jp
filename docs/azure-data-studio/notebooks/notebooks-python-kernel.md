---
title: Azure Data Studio のノートブックと Python カーネル
description: このチュートリアルでは、Python ノートブックを作成し、実行する方法について説明します。
ms.topic: how-to
ms.prod: azure-data-studio
ms.technology: azure-data-studio
author: garyericson
ms.author: garye
ms.reviewer: mikeray, alayu, maghan
ms.custom: ''
ms.date: 07/01/2020
ms.openlocfilehash: e019777c629084c5265cac1cd531ee01bdede01f
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364219"
---
# <a name="create-and-run-a-python-notebook"></a>Python ノートブックを作成して実行する

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

このチュートリアルでは、Python カーネルを使用して、Azure Data Studio でノートブックを作成し、実行する方法について説明します。

## <a name="prerequisites"></a>前提条件

- [Azure Data Studio をインストールしていること](../download-azure-data-studio.md)

## <a name="create-a-notebook"></a>ノートブックを作成する

次の手順では、Azure Data Studio でノートブック ファイルを作成する方法を示しています。

1. Azure Data Studio を開きます。 SQL Server に接続するかどうかを確認するメッセージが表示されたら、接続するか、 **[キャンセル]** をクリックします。

1. **[ファイル]** メニューで **[新しいノートブック]** を選択します。

1. **[カーネル]** で **[Python 3]** を選択します。 **[アタッチ先]** は "localhost" に設定されています。

   :::image type="content" source="media/notebooks-python-kernel/set-kernel-and-attach-to-python.png" alt-text="カーネルを設定する":::

ノートブックを保存するには、 **[ファイル]** メニューで **[保存]** または **[名前を付けて保存...]** コマンドを使用します。

ノートブックを開くには、 **[ファイル]** メニューで **[ファイルを開く...]** コマンドを使用して、 **[ようこそ]** ページで **[ファイルを開く]** を選択するか、コマンド パレットで **File:Open** コマンドを使用します。

## <a name="change-the-python-kernel"></a>Python カーネルを変更する

ノートブックの Python カーネルに初めて接続するときには、 **[ノートブック用 Python の構成]** ページが表示されます。 次のいずれかを選択できます。

- **[新しい Python インストール]** を選択して、Azure Data Studio 用の Python の新しいコピーをインストールする
- **[既存の Python インストールを使用する]** を選択して、Azure Data Studio で使用する既存の Python インストールのパスを指定する

アクティブな Python カーネルの場所とバージョンを表示するには、コード セルを作成し、次の Python コマンドを実行します。

```python
import os
import sys
print(sys.version_info)
print(os.path.dirname(sys.executable))
```

別の Python インストールに接続するには、次の操作を実行します。

1. **[ファイル]** メニューから、 **[基本設定]** を選択し、次に **[設定]** を選択します。
1. **[拡張機能]** の下にある **[Notebook 構成]** までスクロールします。
1. **[Use Existing Python]\(既存の Python の使用\)** で、[Local path to a preexisting python installation used by Notebooks]\(Notebooks で使用する既存の Python インストールのローカル パス\) オプションをオフにします。
1. Azure Data Studio を再起動します。

Azure Data Studio が起動したら、Python カーネルに接続します。 **[ノートブック用 Python の構成]** ページが表示されたら、新しい Python インストールを作成するか、既存のインストールへのパスを指定するかを選択できます。

## <a name="run-a-code-cell"></a>コード セルを実行する

その場で実行できる SQL コードを含むセルを作成するには、セルの左側にある **[セルの実行]** ボタン (黒の円矢印) をクリックします。 セルの実行が完了した後、結果がノートブックに表示されます。

次に例を示します。

1. ツールバーの **[+Code]** コマンドを選択して、新しい Python コード セルを追加します。

   :::image type="content" source="media/notebooks-python-kernel/notebook-toolbar-python.png" alt-text="ノートブック ツール バー":::

1. 次の例をコピーしてセルに貼り付け、 **[セルの実行]** をクリックします。 この例では、単純な数値演算を実行し、結果が下に表示されます。

   ```python
   a = 1
   b = 2
   c = a/b
   print(c)
   ```

   :::image type="content" source="media/notebooks-python-kernel/run-notebook-cell-python.png" alt-text="ノートブック セルを実行する":::

## <a name="next-steps"></a>次のステップ

ノートブックについてさらに学習します:

- [Kqlmagic を使用して Python を拡張する](./notebooks-kqlmagic.md)
- [Azure Data Studio でノートブックを使用する方法](./notebooks-guidance.md)
- [SQL Server ノートブックを作成して実行する](./notebooks-sql-kernel.md)
