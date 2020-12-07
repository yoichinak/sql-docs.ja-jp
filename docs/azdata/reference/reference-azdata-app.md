---
title: azdata app リファレンス
titleSuffix: SQL Server big data clusters
description: azdata app コマンドのリファレンス記事です。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a9a30029248a82f913fc45834e108712f48d1a36
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358830"
---
# <a name="azdata-app"></a>azdata app

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] への適用

以下の記事では、**azdata** ツールの **sql** コマンドに関するリファレンスを提供します。 他の **azdata** コマンドの詳細については、[azdata リファレンス](reference-azdata.md)に関するページを参照してください。

## <a name="commands"></a>コマンド

|command|説明|
| --- | --- |
[azdata app template](reference-azdata-app-template.md) | テンプレート。
[azdata app init](#azdata-app-init) | 新しいアプリケーションのスケルトンを開始します。
[azdata app create](#azdata-app-create) | アプリケーションを作成します。
[azdata app update](#azdata-app-update) | アプリケーションを更新します。
[azdata app list](#azdata-app-list) | アプリケーションを一覧表示します。
[azdata app delete](#azdata-app-delete) | アプリケーションを削除します。
[azdata app run](#azdata-app-run) | アプリケーションを実行します。
[azdata app describe](#azdata-app-describe) | アプリケーションについて記述します。
## <a name="azdata-app-init"></a>azdata app init
ランタイム環境に基づいて、新しいアプリケーションのスケルトンや仕様ファイルを開始するのに役立ちます。
```bash
azdata app init [--spec -s] 
                [--name -n]  
                
[--version -v]  
                
[--template -t]  
                
[--destination -d]  
                
[--url -u]
```
### <a name="examples"></a>例
新しいアプリケーション `spec.yaml` のみをスキャフォールディングします。
```bash
azdata app init --spec
```
`r` テンプレートに基づいて、新しい R アプリケーションのスケルトンをスキャフォールディングします。
```bash
azdata app init --name reduce --template r
```
`python` テンプレートに基づいて、新しい Python アプリケーションのスケルトンをスキャフォールディングします。
```bash
azdata app init --name reduce --template python
```
`ssis` テンプレートに基づいて、新しい SSIS アプリケーションのスケルトンをスキャフォールディングします。
```bash
azdata app init --name reduce --template ssis            
```
### <a name="optional-parameters"></a>省略可能なパラメーター
#### `--spec -s`
アプリケーションの spec.yaml だけを生成します。
#### `--name -n`
アプリケーション名。
#### `--version -v`
アプリケーションのバージョン。
#### `--template -t`
テンプレート名。 サポートされているテンプレート名の完全な一覧を表示するには、`azdata app template list` を実行します
#### `--destination -d`
アプリケーションのスケルトンを配置する場所。 既定値: 現在の作業ディレクトリ。
#### `--url -u`
別のテンプレート リポジトリの場所を指定します。 既定値: https://github.com/Microsoft/SQLBDC-AppDeploy.git
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
## <a name="azdata-app-create"></a>azdata app create
アプリケーションを作成します。
```bash
azdata app create --spec -s 
                  
```
### <a name="examples"></a>例
有効な spec.yaml デプロイ仕様を含むディレクトリから新しいアプリケーションを作成します。
```bash
azdata app create --spec /path/to/dir/with/spec/yaml
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--spec -s`
アプリケーションについて記述した YAML 仕様ファイルが含まれているディレクトリのパス。
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
## <a name="azdata-app-update"></a>azdata app update
アプリケーションを更新します。
```bash
azdata app update [--spec -s] 
                  [--yes -y]
```
### <a name="examples"></a>例
有効な spec.yaml デプロイ仕様を含むディレクトリから既存のアプリケーションを更新します。
```bash
azdata app update --spec /path/to/dir/with/spec/yaml    
```
### <a name="optional-parameters"></a>省略可能なパラメーター
#### `--spec -s`
アプリケーションについて記述した YAML 仕様ファイルが含まれているディレクトリのパス。
#### `--yes -y`
CWD の spec.yaml ファイルからアプリケーションを更新するときに、確認を求めるメッセージを表示しません。
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
## <a name="azdata-app-list"></a>azdata app list
アプリケーションを一覧表示します。
```bash
azdata app list [--name -n] 
                [--version -v]
```
### <a name="examples"></a>例
名前とバージョンでアプリケーションを一覧表示します。
```bash
azdata app list --name reduce  --version v1
```
名前ですべてのアプリケーションのバージョンを一覧表示します。
```bash
azdata app list --name reduce
```
名前ですべてのアプリケーションのバージョンを一覧表示します。
```bash
azdata app list
```
### <a name="optional-parameters"></a>省略可能なパラメーター
#### `--name -n`
アプリケーション名。
#### `--version -v`
アプリケーションのバージョン。
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
## <a name="azdata-app-delete"></a>azdata app delete
アプリケーションを削除します。
```bash
azdata app delete --name -n 
                  --version -v
```
### <a name="examples"></a>例
名前とバージョンでアプリケーションを削除します。
```bash
azdata app delete --name reduce --version v1    
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--name -n`
アプリケーション名。
#### `--version -v`
アプリケーションのバージョン。
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
## <a name="azdata-app-run"></a>azdata app run
アプリケーションを実行します。
```bash
azdata app run --name -n 
               --version -v  
               
[--inputs]
```
### <a name="examples"></a>例
入力パラメーターなしでアプリケーションを実行します。
```bash
azdata app run --name reduce --version v1
```
1 つの入力パラメーターを使ってアプリケーションを実行します。
```bash
azdata app run --name reduce --version v1 --inputs x=10
```
複数の入力パラメーターを使ってアプリケーションを実行します。
```bash
azdata app run --name reduce --version v1 --inputs x=10,y5.6    
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--name -n`
アプリケーション名。
#### `--version -v`
アプリケーションのバージョン。
### <a name="optional-parameters"></a>省略可能なパラメーター
#### `--inputs`
アプリケーションの入力パラメーター (CSV の `name=value` 形式)。
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
## <a name="azdata-app-describe"></a>azdata app describe
アプリケーションについて記述します。
```bash
azdata app describe [--spec -s] 
                    [--name -n]  
                    
[--version -v]
```
### <a name="examples"></a>例
アプリケーションについて記述します。
```bash
azdata app describe --name reduce --version v1    
```
### <a name="optional-parameters"></a>省略可能なパラメーター
#### `--spec -s`
アプリケーションについて記述した YAML 仕様ファイルが含まれているディレクトリのパス。
#### `--name -n`
アプリケーション名。
#### `--version -v`
アプリケーションのバージョン。
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

