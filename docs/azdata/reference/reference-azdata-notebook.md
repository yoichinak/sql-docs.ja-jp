---
title: azdata notebook リファレンス
titleSuffix: SQL Server big data clusters
description: azdata notebook コマンドのリファレンス記事です。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4a0e171861d01d7a3afe7904905d373aa5e57639
ms.sourcegitcommit: 22e97435c8b692f7612c4a6d3fe9e9baeaecbb94
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/27/2020
ms.locfileid: "92678732"
---
# <a name="azdata-notebook"></a>azdata notebook

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] への適用

以下の記事では、 **azdata** ツールの **sql** コマンドに関するリファレンスを提供します。 他の **azdata** コマンドの詳細については、 [azdata リファレンス](reference-azdata.md)に関するページを参照してください。

## <a name="commands"></a>コマンド

|command|説明|
| --- | --- |
[azdata notebook view](#azdata-notebook-view) | ノートブックを表示します。  最初のセル実行エラー時に停止するオプションです。
[azdata notebook run](#azdata-notebook-run) | ノートブックを実行します。  最初のエラーで実行が停止します。
## <a name="azdata-notebook-view"></a>azdata notebook view
このコマンドでノートブック ファイルを取得し、マークダウン、コード、および出力をカラー ターミナル形式に変換できます。
```bash
azdata notebook view --path -p 
                     [--continue-on-error -c]
```
### <a name="examples"></a>例
ノートブックを表示します。  これにより、すべてのセルが表示されます。
```bash
azdata notebook view --path "/home/me/notebooks/demo_notebook.ipynb"
```
ノートブックを表示します。  これにより、出力にエラーのあるセルが検出された場合を除き、すべてのセルが表示されます。  その場合、出力は停止します。
```bash
azdata notebook view --path "/home/me/notebooks/demo_notebook.ipynb" --stop-on-error
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--path -p`
表示するノートブックのパス。
### <a name="optional-parameters"></a>省略可能なパラメーター
#### `--continue-on-error -c`
ノートブックの出力で見つかったセル エラーを無視して、その他のセルの表示を継続します。  既定の動作では、エラーの発生時に停止します。  停止すると、エラーが発生した最初のセルがわかりやすくなります。
### <a name="global-arguments"></a>グローバル引数
#### `--debug`
すべてのデバッグ ログを表示するようにログの詳細レベルを上げます。
#### `--help -h`
このヘルプ メッセージを表示して終了します。
#### `--output -o`
出力形式。  使用できる値: json、jsonc、table、tsv。  既定値: json。
#### `--query -q`
JMESPath クエリ文字列。 詳細と例については、[http://jmespath.org/](http://jmespath.org) を参照してください。
#### `--verbose`
ログの詳細レベルを上げます。 詳細なデバッグ ログを表示するには --debug を使います。
## <a name="azdata-notebook-run"></a>azdata notebook run
このコマンドで、一時ディレクトリが作成され、作業ディレクトリとして指定されたノートブックが実行されます。
```bash
azdata notebook run --path -p 
                    [--output-path]  
                    
[--output-html]  
                    
[--arguments -a]  
                    
[--interactive -i]  
                    
[--clear -c]  
                    
[--timeout -t]
```
### <a name="examples"></a>例
ノートブックを実行します。
```bash
azdata notebook run --path "/home/me/notebooks/demo_notebook.ipynb"
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--path -p`
実行するノートブックのファイル パス。
### <a name="optional-parameters"></a>省略可能なパラメーター
#### `--output-path`
ノートブックの出力に使用するディレクトリ パス。  出力データを含むノートブックと、ノートブックによって生成されるファイルは、このディレクトリに対して相対的に生成されます。
#### `--output-html`
さらに出力ノートブックを HTML 形式に変換するかどうかを示す省略可能なフラグ。  2 つ目の出力ファイルを作成します。
#### `--arguments -a`
ノートブックの実行に挿入するノートブック引数のオプションの省略可能なリスト。  JSON ディクショナリとしてエンコードされます。  例: '{"name":"value", "name2":"value2"}'
#### `--interactive -i`
ノートブックを対話モードで実行します。
#### `--clear -c`
対話モードでは、セルをレンダリングする前にコンソールをクリアします。
#### `--timeout -t`
実行が完了するまで待機する秒数。 値 -1 は、無期限に待機することを示します。
`600`
### <a name="global-arguments"></a>グローバル引数
#### `--debug`
すべてのデバッグ ログを表示するようにログの詳細レベルを上げます。
#### `--help -h`
このヘルプ メッセージを表示して終了します。
#### `--output -o`
出力形式。  使用できる値: json、jsonc、table、tsv。  既定値: json。
#### `--query -q`
JMESPath クエリ文字列。 詳細と例については、[http://jmespath.org/](http://jmespath.org) を参照してください。
#### `--verbose`
ログの詳細レベルを上げます。 詳細なデバッグ ログを表示するには --debug を使います。

## <a name="next-steps"></a>次のステップ

他の **azdata** コマンドの詳細については、 [azdata リファレンス](reference-azdata.md)に関するページを参照してください。 

**azdata** ツールをインストールする方法の詳細については、「 [azdata のインストール](..\install\deploy-install-azdata.md)」を参照してください。

