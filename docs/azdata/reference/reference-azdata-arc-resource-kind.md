---
title: azdata arc resource-kind リファレンス
titleSuffix: SQL Server big data clusters
description: azdata arc resource-kind コマンドのリファレンス記事です。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 68d6d4c30e43804c8c18a7dc36d0a9d53bcb5677
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358710"
---
# <a name="azdata-arc-resource-kind"></a>azdata arc resource-kind

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] への適用

以下の記事では、**azdata** ツールの **sql** コマンドに関するリファレンスを提供します。 他の **azdata** コマンドの詳細については、[azdata リファレンス](reference-azdata.md)に関するページを参照してください。

## <a name="commands"></a>コマンド

|command|説明|
| --- | --- |
[azdata arc resource-kind list](#azdata-arc-resource-kind-list) | 定義および作成できる Arc で使用できるカスタム リソースの種類を一覧表示します。
[azdata arc resource-kind get](#azdata-arc-resource-kind-get) | Arc resource-kind のテンプレート ファイルを取得します。
## <a name="azdata-arc-resource-kind-list"></a>azdata arc resource-kind list
定義および作成できる Arc で使用できるカスタム リソースの種類を一覧表示します。 一覧表示したら、そのカスタム リソースの定義または作成に必要なテンプレート ファイルの取得に進みます。
```bash
azdata arc resource-kind list 
```
### <a name="examples"></a>使用例
Arc で使用できるカスタム リソースの種類を一覧表示するコマンド例です。
```bash
azdata arc resource-kind list
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
## <a name="azdata-arc-resource-kind-get"></a>azdata arc resource-kind get
Arc resource-kind のテンプレート ファイルを取得します。
```bash
azdata arc resource-kind get --kind -k 
                             [--dest -d]
```
### <a name="examples"></a>使用例
Arc resource-kind の CRD テンプレート ファイルを取得するコマンド例です。
```bash
azdata arc resource-kind get --kind sqldb
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--kind -k`
テンプレート ファイルを使用する arc のリソースの種類。
### <a name="optional-parameters"></a>省略可能のパラメーター
#### `--dest -d`
テンプレート ファイルを配置するディレクトリ。
`template`
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

