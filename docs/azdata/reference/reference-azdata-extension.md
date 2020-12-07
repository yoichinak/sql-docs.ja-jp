---
title: azdata 拡張機能リファレンス
titleSuffix: SQL Server big data clusters
description: azdata 拡張機能コマンドのリファレンス記事です。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 07862632feeb4fc33f82597cf7d2b1319f320776
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358152"
---
# <a name="azdata-extension"></a>azdata 拡張機能

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] への適用

以下の記事では、**azdata** ツールの **sql** コマンドに関するリファレンスを提供します。 他の **azdata** コマンドの詳細については、[azdata リファレンス](reference-azdata.md)に関するページを参照してください。

## <a name="commands"></a>コマンド

|command|説明|
| --- | --- |
[azdata extension add](#azdata-extension-add) | 拡張機能を追加します。
[azdata extension remove](#azdata-extension-remove) | 拡張機能を削除します。
[azdata extension list](#azdata-extension-list) | インストールされているすべての拡張機能を一覧表示します。
## <a name="azdata-extension-add"></a>azdata extension add
拡張機能を追加します。
```bash
azdata extension add --source -s 
                     [--index]  
                     
[--pip-proxy]  
                     
[--pip-extra-index-urls]  
                     
[--yes -y]
```
### <a name="examples"></a>例
URL から拡張機能を追加します。
```bash
azdata extension add --source https://contoso.com/some_ext-0.0.1-py2.py3-none-any.whl```
Add extension from local disk.
```bash
azdata extension add --source ~/some_ext-0.0.1-py2.py3-none-any.whl```
Add extension from local disk and use pip proxy for dependencies.
```bash
azdata extension add --source ~/some_ext-0.0.1-py2.py3-none-any.whl --pip-proxy https://user:pass@proxy.server:8080
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--source -s`
ディスク上の拡張機能ホイールへのパスまたは拡張機能の URL
### <a name="optional-parameters"></a>省略可能なパラメーター
#### `--index`
Python パッケージ インデックスのベース URL (既定: https://pypi.org/simple) 。 これは、PEP 503 (simple repository API) に準拠しているリポジトリ、または同じ形式でレイアウトされたローカル ディレクトリを指している必要があります。
#### `--pip-proxy`
[user:passwd@]proxy.server:port の形式で拡張機能の依存関係に使用する pip のプロキシ
#### `--pip-extra-index-urls`
使用するパッケージ インデックスの追加 URL のスペース区切りの一覧です。 これは、PEP 503 (simple repository API) に準拠しているリポジトリ、または同じ形式でレイアウトされたローカル ディレクトリを指している必要があります。
#### `--yes -y`
確認のダイアログを表示しません。
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
## <a name="azdata-extension-remove"></a>azdata extension remove
拡張機能を削除します。
```bash
azdata extension remove --name -n 
                        [--yes -y]
```
### <a name="examples"></a>例
拡張機能を削除します。
```bash
azdata extension remove --name some-ext
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--name -n`
拡張機能の名前
### <a name="optional-parameters"></a>省略可能なパラメーター
#### `--yes -y`
確認のダイアログを表示しません。
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
## <a name="azdata-extension-list"></a>azdata extension list
インストールされているすべての拡張機能を一覧表示します。
```bash
azdata extension list 
```
### <a name="examples"></a>例
拡張機能を一覧表示します。
```bash
azdata extension list
```
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

他の **azdata** コマンドの詳細については、[azdata リファレンス](reference-azdata.md)に関するページを参照してください。 

**azdata** ツールをインストールする方法の詳細については、「[azdata のインストール](..\install\deploy-install-azdata.md)」を参照してください。

