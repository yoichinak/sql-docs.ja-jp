---
title: azdata bdc spark settings のリファレンス
titleSuffix: SQL Server big data clusters
description: azdata bdc spark settings コマンドのリファレンス記事です。
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 66c80bc7d77ebc1f1f5c18e5fe972e4c6d61419d
ms.sourcegitcommit: 129c084add904fd3f7e9ab35a800c3fd8b1a8927
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/17/2021
ms.locfileid: "100567318"
---
# <a name="azdata-bdc-spark-settings"></a>azdata bdc spark settings

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] への適用

次の記事では、**azdata** ツール内の **spark settings** コマンドのリファレンスを提供します。 他の **azdata** コマンドの詳細については、[azdata リファレンス](reference-azdata.md)に関するページを参照してください。

## <a name="commands"></a>コマンド
|コマンド|説明|
| --- | --- |
[azdata bdc spark settings set](#azdata-bdc-spark-settings-set) | spark service-scope 設定を設定します。
[azdata bdc spark settings show](#azdata-bdc-spark-settings-show) | 指定されたリソースの spark service-scope 設定と、オプションで spark 設定を表示します。

## <a name="azdata-bdc-spark-settings-set"></a>azdata bdc spark settings set
service-scoped または resource-scoped 設定を設定できます。 設定の完全な名前と値を指定します。 設定は、実行中の BDC には適用されません。 そのためには、アップグレードを実行します。
```bash
azdata bdc spark settings set --settings -s 
                        
```
### <a name="examples"></a>例
Spark サービスのドライバー コアの既定数を 1 に、ドライバー メモリを 1664m に設定します。 
```bash 
azdata bdc spark settings set --settings spark-defaults-conf.spark.driver.cores=1,spark-defaults-conf.spark.driver.memory=1664m 
``` 
記憶域プールの Executor コアの既定数を 1 に設定します 
```bash 
azdata bdc spark  settings set --settings spark-defaults-conf.spark.executor.cores=1 –resources storage-0 
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

## <a name="azdata-bdc-spark-settings-show"></a>azdata bdc spark settings show
BDC の `spark` service-scope (オプションで resource-scope) の設定を表示します。 既定では、このコマンドは、ユーザーが構成した service-scope 設定を表示します。 フィルターを使用して、すべての設定 (システム管理および構成可能)、構成可能な設定、または保留中の設定を表示できます。 特定の service-scope または resource-scope 設定を表示するには、設定名を指定します。 サービスの一部としてすべてのリソースの設定を表示するには、"recursive" を使用します。 
```bash

azdata bdc spark settings show 
[--settings -s]
[--filter-option -f]  
[--recursive -rec]
[--include-details -i]  
[--description -d]
```
### <a name="examples"></a>例
ユーザーが構成した Spark service-scope 設定を表示します。
```bash
azdata bdc spark settings show
```
記憶域プール内の Spark ドライバー コアの実行中および構成済みの値を表示します。 
```bash
azdata bdc spark settings show --settings spark-defaults-conf.spark.driver.cores --resources storage-0 --include-details
```
Spark サービスの構成可能なメモリ関連の設定を表示します。
```bash
azdata bdc spark settings show --settings *memory* --resources storage-0 
```
Spark service-scope および resource-scope の保留中の設定変更を表示します。
```bash
azdata bdc spark settings show --filter-options=pending --recursive --include-details
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
