---
title: azdata bdc settings のリファレンス
titleSuffix: SQL Server big data clusters
description: azdata bdc sql settings コマンドのリファレンス記事。
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 37688a962fc17679a1a642af1b83609d2b8f480a
ms.sourcegitcommit: 8dc7e0ececf15f3438c05ef2c9daccaac1bbff78
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/13/2021
ms.locfileid: "100342493"
---
# <a name="azdata-bdc-settings"></a>azdata bdc settings

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] への適用

以下の記事では、**azdata** ツールの **sql** コマンドに関するリファレンスを提供します。 他の **azdata** コマンドの詳細については、[azdata リファレンス](reference-azdata.md)に関するページを参照してください。

## <a name="commands"></a>コマンド
|コマンド|説明|
| --- | --- |
[azdata bdc settings set](#azdata-bdc-settings-set) | クラスタースコープの設定を行います。
[azdata bdc settings apply](#azdata-bdc-settings-apply) | 保留中の設定変更を BDC に適用します。
[azdata bdc settings cancel-apply](#azdata-bdc-settings-cancel-apply) | BDC 設定の適用をキャンセルします。
[azdata bdc settings show](#azdata-bdc-settings-show) | クラスタースコープの設定、または --recursive を使用してすべてのクラスターの設定を表示します。
[azdata bdc settings revert](#azdata-bdc-settings-revert) | すべてのスコープで BDC の保留中の設定変更を元に戻します。
## <a name="azdata-bdc-settings-set"></a>azdata bdc settings set
クラスタースコープの設定を行います。 設定の完全な名前と値を指定します。 適用を実行して設定を適用し、BDC の設定を更新します。
```bash
azdata bdc settings set --settings -s 
                        
```
### <a name="examples"></a>例
"bdc.telemetry.customerFeedback" のクラスターの既定値を設定します。
```bash
azdata bdc settings set --settings bdc.telemetry.customerFeedback=false
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--settings -s`
指定された設定の構成値を設定します。 コンマ区切り一覧を使用して複数の設定を設定できます。
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
## <a name="azdata-bdc-settings-apply"></a>azdata bdc settings apply
保留中の設定変更を BDC に適用します。
```bash
azdata bdc settings apply [--force -f] 
                          
```
### <a name="examples"></a>例
保留中の設定変更を BDC に適用します。
```bash
azdata bdc settings apply
```
強制的に適用すると、ユーザーは確認を求められず、すべての問題が stderr の一部として出力されます。
```bash
azdata bdc settings apply --force
```
### <a name="optional-parameters"></a>省略可能のパラメーター
#### `--force -f`
強制的に適用すると、ユーザーは確認を求められず、すべての問題が stderr の一部として出力されます。
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
## <a name="azdata-bdc-settings-cancel-apply"></a>azdata bdc settings cancel-apply
設定の適用中にエラーが発生した場合は、ビッグ データ クラスターをその最後の実行状態に戻します。 実行中のクラスターに適用された場合、このコマンドでは何も行われません。 以前の保留中の設定変更は、キャンセル後も保留中になります。
```bash
azdata bdc settings cancel-apply [--force -f] 
                                 
```
### <a name="examples"></a>例
BDC 設定の適用をキャンセルします。
```bash
azdata bdc settings cancel-apply
```
強制的に適用をキャンセルすると、ユーザーは確認を求められず、すべての問題が stderr の一部として出力されます。
```bash
azdata bdc settings cancel-apply --force
```
### <a name="optional-parameters"></a>省略可能のパラメーター
#### `--force -f`
強制的に適用をキャンセルすると、ユーザーは確認を求められず、すべての問題が stderr の一部として出力されます。
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
## <a name="azdata-bdc-settings-show"></a>azdata bdc settings show
BDC のクラスターレベルの設定を表示します。 既定では、このコマンドを実行すると、ユーザーが構成したクラスタースコープの設定が表示されます。 他のフィルターを使用して、すべての設定 (システム管理、ユーザー構成可能および継承済み)、すべての構成可能な設定、または保留中の設定を表示できます。 特定のクラスタースコープの設定を表示する場合は、設定名を指定できます。 すべてのスコープ (クラスター、サービス、およびリソース) の設定を表示する場合は、"recursive" を指定できます。
```bash
azdata bdc settings show [--settings -s] 
                         [--filter-option -f]  
                         
[--recursive -rec]  
                         
[--include-details -i]  
                         
[--description -d]
```
### <a name="examples"></a>例
BDC テレメトリ コレクションが有効になっているかどうかを表示します。
```bash
azdata bdc settings show --settings bdc.telemetry.customerFeedback
```
すべてのスコープで、ユーザーが構成した設定を BDC に表示します。
```bash
azdata bdc settings show --recursive
```
すべてのスコープで、すべての保留中の設定を BDC に表示します。
```bash
azdata bdc settings show –filter-option=pending --recursive
```
### <a name="optional-parameters"></a>省略可能のパラメーター
#### `--settings -s`
指定された設定名の情報を表示します。
#### `--filter-option -f`
'ユーザーが構成した' 設定だけでなく、表示されるクラスタースコープの設定をフィルター処理します。 フィルターを使用して、すべての設定 (システム管理およびユーザー構成可能)、すべての構成可能な設定、または保留中の設定を表示できます。
`userConfigured`
#### `--recursive -rec`
クラスター スコープおよびすべての下位スコープ コンポーネント (サービス、リソース) の設定情報を表示します。
#### `--include-details -i`
表示するように選択された設定に関する追加の詳細が含まれます。
#### `--description -d`
設定の説明が含まれます。
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
## <a name="azdata-bdc-settings-revert"></a>azdata bdc settings revert
すべてのスコープで BDC の保留中の設定変更を元に戻します。
```bash
azdata bdc settings revert [--force -f] 
                           
```
### <a name="examples"></a>例
すべてのスコープで BDC の保留中の設定変更を元に戻します。
```bash
azdata bdc settings revert
```
強制的に元に戻すと、ユーザーは確認を求められず、すべての問題が stderr の一部として出力されます。
```bash
azdata bdc settings revert --force
```
### <a name="optional-parameters"></a>省略可能のパラメーター
#### `--force -f`
強制的に元に戻すと、ユーザーは確認を求められず、すべての問題が stderr の一部として出力されます。
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

**azdata** ツールをインストールする方法の詳細については、「[azdata のインストール](..\install\deploy-install-azdata.md)」を参照してください。
