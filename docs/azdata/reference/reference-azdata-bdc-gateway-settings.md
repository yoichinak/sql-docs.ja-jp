---
title: azdata bdc gateway settings のリファレンス
titleSuffix: SQL Server big data clusters
description: azdata bdc gateway settings コマンドのリファレンス記事です。
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8da7bc79600d1fdd052109c55039b33642079d0c
ms.sourcegitcommit: 129c084add904fd3f7e9ab35a800c3fd8b1a8927
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/17/2021
ms.locfileid: "100567325"
---
# <a name="azdata-bdc-gateway-settings"></a>azdata bdc gateway settings

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] への適用

次の記事では、**azdata** ツール内の **gateway settings** コマンドのリファレンスを提供します。 他の **azdata** コマンドの詳細については、[azdata リファレンス](reference-azdata.md)に関するページを参照してください。

## <a name="commands"></a>コマンド
|コマンド|説明|
| --- | --- |
[azdata bdc gateway settings set](#azdata-bdc-gateway-settings-set) | gateway service-scope 設定を設定します。
[azdata bdc gateway settings show](#azdata-bdc-gateway-settings-show) | 指定されたリソースの gateway service-scope 設定と、オプションで gateway 設定を表示します。

## <a name="azdata-bdc-gateway-settings-set"></a>azdata bdc gateway settings set
service-scoped または resource-scoped 設定を設定できます。 設定の完全な名前と値を指定します。 設定は、実行中の BDC には適用されません。 そのためには、アップグレードを実行します。
```bash
azdata bdc gateway settings set --settings -s 
                        
```
### <a name="examples"></a>例
ゲートウェイのタイムアウト制限を設定します。
```bash 
azdata bdc gateway settings set --settings gateway-site.gateway.httpclient.socketTimeout=100s –resources gateway 
```

### <a name="required-parameters"></a>必須のパラメーター
#### `--settings -s`
指定された設定の構成値を設定します。 コンマ区切り一覧を使用して複数の設定を設定できます。
### <a name="optional-parameters"></a>省略可能のパラメーター 
#### `--resources` 
指定されたリソースの指定された設定を設定します。 リソースをコンマ区切り一覧として一覧表示できます。 

### <a name="global-arguments"></a>グローバル引数
#### `--debug`
すべてのデバッグ ログを表示するようにログの詳細レベルを上げます。
#### `--help -h`
このヘルプ メッセージを表示して終了します。
#### `--output -o`
出力形式。  使用できる値: json、jsonc、table、tsv。  既定値: json。
#### `--query -q`
JMESPath クエリ文字列。 詳細と例については、[http://jmespath.org/](http://jmespath.org/) を参照してください。
#### `--verbose`
ログの詳細レベルを上げます。 詳細なデバッグ ログを表示するには --debug を使います。

## <a name="azdata-bdc-gateway-settings-show"></a>azdata bdc gateway settings show
BDC の `gateway` service-scope (オプションで resource-scope) の設定を表示します。 既定では、このコマンドは、ユーザーが構成した service-scope 設定を表示します。 フィルターを使用して、すべての設定 (システム管理および構成可能)、構成可能な設定、または保留中の設定を表示できます。 特定の service-scope または resource-scope 設定を表示するには、設定名を指定します。 サービスの一部としてすべてのリソースの設定を表示するには、"recursive" を使用します。 
```bash

azdata bdc gateway settings show 
[--settings -s]
[--filter-option -f]  
[--recursive -rec]
[--include-details -i]  
[--description -d]
```
### <a name="examples"></a>例
ユーザーが構成したゲートウェイの resource-scope 設定を表示します。 
```bash
azdata bdc gateway settings show --resource gateway 
```
ゲートウェイのタイムアウト制限を表示します。
```bash
azdata bdc gateway settings show --settings gateway-site.gateway.httpclient.socketTimeout --resources gateway 
```
ゲートウェイ リソースの保留中の設定変更を表示します。
```bash
azdata bdc gateway settings show --filter-options=pending –-resource gateway --include-details
```
### <a name="optional-parameters"></a>省略可能のパラメーター 
#### `--filter-options | -f` 
ユーザーが構成した設定だけでなく、表示する service-level または resource-scope 設定をフィルター処理するオプション。 フィルターを使用して、すべての設定 (システム管理およびユーザー構成可能)、すべての構成可能な設定、または保留中の設定を表示できます。 オプションは、`userConfigured`、`all`、`pending`、`configurable` です。
#### `--settings | -s` 
指定された設定名の情報を表示します 
#### `--include-details | -i` 
表示するように選択した設定に関する追加の詳細が含まれます 
#### `--description | -d` 
設定の説明が含まれます。 --include-details と組み合わせて使用する必要があります 
#### `--resources | -r` 
指定されたリソースの設定情報を表示します。 リソースをコンマ区切り一覧として一覧表示できます。 
#### `--recursive | -rec` 
指定されたスコープ (サービスまたはサービスリソース) の設定情報と、すべての下位スコープ コンポーネント (リソース) を表示します。 

### <a name="global-arguments"></a>グローバル引数
#### `--debug`
すべてのデバッグ ログを表示するようにログの詳細レベルを上げます。
#### `--help -h`
このヘルプ メッセージを表示して終了します。
#### `--output -o`
出力形式。  使用できる値: json、jsonc、table、tsv。  既定値: json。
#### `--query -q`
JMESPath クエリ文字列。 詳細と例については、[http://jmespath.org/](http://jmespath.org/) を参照してください。
#### `--verbose`
ログの詳細レベルを上げます。 詳細なデバッグ ログを表示するには --debug を使います。

## <a name="next-steps"></a>次のステップ

他の **azdata** コマンドの詳細については、[azdata リファレンス](reference-azdata.md)に関するページを参照してください。 

**azdata** ツールをインストールする方法の詳細については、[SQL Server 2019 ビッグ データ クラスターを管理する azdata のインストール](../install/deploy-install-azdata.md)に関するページを参照してください。
