---
title: Azure Data Studio でのノートブックのパラメーター化
description: このチュートリアルでは、ADS でパラメーター化されたノートブックを作成する方法を示します。
ms.topic: how-to
ms.prod: azure-data-studio
ms.technology: azure-data-studio
author: vasubhog
ms.author: vasubhog
ms.reviewer: mikeray, alayu, maghan
ms.custom: ''
ms.date: 01/25/2021
ms.openlocfilehash: dc0558d660143de35340010735c74e9abc0cdd56
ms.sourcegitcommit: 8dc7e0ececf15f3438c05ef2c9daccaac1bbff78
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/13/2021
ms.locfileid: "100343446"
---
# <a name="create-a-parameterized-notebook"></a>パラメーター化されたノートブックを作成する

**パラメーター化** は、異なるパラメーターを使用して同じノートブックを実行する機能です。

この記事では、Python カーネルを使用して Azure Data Studio でパラメーター化されたノートブックを作成して実行する方法を示します。

## <a name="prerequisites"></a>前提条件

- [Azure Data Studio](../download-azure-data-studio.md)
- [Python](https://www.python.org/downloads/)

## <a name="install-and-set-up-papermill-in-azure-data-studio"></a>Azure Data Studio に Papermill をインストールして設定する

このセクションのステップはすべて Azure Data Studio ノートブック内で実行されます。

1. 新しいノートブックを作成し、 **[カーネル]** を *[Python 3]* に変更します。

   ![新しい Notebook](media/notebooks-kqlmagic/install-new-notebook.png)

2. パッケージを更新する必要がある場合は、Python パッケージをアップグレードするように求められることがあります。

   ![はい](media/notebooks-kqlmagic/install-python-yes.png)

3. Papermill をインストールします。

   ```python
   import sys
   !{sys.executable} -m pip install papermill --no-cache-dir --upgrade
   ```

   インストールされていることを確認します。

   ```python
   import sys
   !{sys.executable} -m pip list
   ```

   :::image type="content" source="media/notebooks-parameterization/install-list-papermill.png" alt-text="リスト":::

5. Papermill のバージョンをチェックすることで、Papermill が正しく読み込まれているかどうかをテストできます。

   ```python
   import papermill
   papermill
   ```

   :::image type="content" source="media/notebooks-parameterization/install-validation-papermill.png" alt-text="検証":::

## <a name="set-up-a-parameterized-notebook"></a>パラメーター化されたノートブックを設定する

1. **[カーネル]** が *[Python 3]* に設定されていることを確認します。

   ![Kernel 変更](media/notebooks-kqlmagic/change-kernel.png)

2. 新しいコード セルを作成し、**パラメーター セル** としてタグを付けます。

   ```python
   x = 2.0
   y = 5.0
   ```

   :::image type="content" source="media/notebooks-parameterization/make-parameter-cell.png" alt-text="パラメーター セル ノートブック":::

3. 他のセルを追加して、異なるパラメーターをテストします。

   ```python
   addition = x + y
   multiply = x * y
   ```

   ```python
   print("Addition: " + str(addition))
   print("Multiplication: " + str(multiply))
   ```

   入力例ノートブックのセル: :::image type="content" source="media/notebooks-parameterization/test-cells.png" alt-text="追加の入力ノートブック セル":::

4. ノートブックを **Input.ipynb** として保存します。
   :::image type="content" source="media/notebooks-parameterization/save-notebook.png" alt-text="ノートブックを保存する":::

## <a name="how-to-execute-papermill-notebook"></a>Papermill ノートブックを実行する方法

Papermill は、2 つの方法で実行できます。

- コマンド ライン インターフェイス (CLI)
- Python API

### <a name="parameterized-cli-execution"></a>パラメーター化された CLI の実行

CLI を使用してノートブックを実行するには、入力ノートブック、出力ノートブックの場所、オプションを指定して、ターミナルで papermill コマンドを入力します。

> [!Note]
   > Papermill のコマンド ライン インターフェイスのドキュメントについては、[こちら](https://papermill.readthedocs.io/en/latest/usage-execute.html#execute-via-cli)を参照してください。

1. 新しいパラメーターを使用して入力ノートブックを実行します。

   ```shell
   papermill Input.ipynb Output.ipynb -p x 10 -p y 20
   ```

   これにより、パラメーター **x** と **y** に新しい値を使用して、入力ノートブックが実行されます。

2. 実行後、新しい出力パラメーター化ノートブックを表示します。
   CLI を使用して渡された新しいパラメーター値を含む **# Injected-Parameters** というラベルが付いた新しいセルがあることがわかります。

   :::image type="content" source="media/notebooks-parameterization/output-notebook.png" alt-text="出力ノートブック":::

### <a name="parameterized-python-api-execution"></a>パラメーター化された Python API の実行

> [!Note]
   > Papermill Python API のドキュメントについては、[こちら](https://papermill.readthedocs.io/en/latest/usage-execute.html#execute-via-the-python-api)を参照してください。

1. 新しいノートブックを作成し、 **[カーネル]** を *[Python 3]* に変更します。
   ![新しい Notebook](media/notebooks-kqlmagic/install-new-notebook.png)

2. 新しいコード セルを追加し、papermill を使用して execute メソッドを使用します。

   ```python
   import papermill as pm

   pm.execute_notebook(
   '/Users/vasubhog/GitProjects/AzureDataStudio-Notebooks/Demo_Parameterization/Input.ipynb',
   '/Users/vasubhog/GitProjects/AzureDataStudio-Notebooks/Demo_Parameterization/Output.ipynb',
   parameters = dict(x = 10, y = 20)
   )
   ```

   ![Papermill Python API の実行](media/notebooks-parameterization/python-api-execute.png)

3. 実行後、新しい出力パラメーター化ノートブックを表示します。

   CLI を使用して渡された新しいパラメーター値を含む **# Injected-Parameters** というラベルが付いた新しいセルがあることがわかります。

   :::image type="content" source="media/notebooks-parameterization/output-notebook.png" alt-text="出力ノートブック":::

## <a name="next-steps"></a>次の手順

ノートブックとパラメーター化についてさらに学習します。

- [Azure Data Studio でノートブックを使用する方法](./notebooks-guidance.md)
- [Papermill のパラメーター化に関するドキュメント](https://papermill.readthedocs.io/en/latest/index.html)