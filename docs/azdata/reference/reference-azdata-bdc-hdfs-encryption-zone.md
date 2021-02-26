---
title: azdata bdc hdfs encryption-zone リファレンス
titleSuffix: SQL Server big data clusters
description: azdata bdc hdfs encryption-zone コマンドに関するリファレンス記事です。
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7c094d489cb925e280f5a44a8234d70fc817554b
ms.sourcegitcommit: 8dc7e0ececf15f3438c05ef2c9daccaac1bbff78
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/13/2021
ms.locfileid: "100342525"
---
# <a name="azdata-bdc-hdfs-encryption-zone"></a>azdata bdc hdfs encryption-zone

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] への適用

以下の記事では、**azdata** ツールの **sql** コマンドに関するリファレンスを提供します。 他の **azdata** コマンドの詳細については、[azdata リファレンス](reference-azdata.md)に関するページを参照してください。

## <a name="commands"></a>コマンド
|コマンド|説明|
| --- | --- |
[azdata bdc hdfs encryption-zone create](#azdata-bdc-hdfs-encryption-zone-create) | HDFS フォルダーを暗号化ゾーンに変換します。
[azdata bdc hdfs encryption-zone list](#azdata-bdc-hdfs-encryption-zone-list) | すべての暗号化ゾーンと、暗号化ゾーンに関連付けられているキーの一覧を表示します。
[azdata bdc hdfs encryption-zone get-file-encryption-info](#azdata-bdc-hdfs-encryption-zone-get-file-encryption-info) | 指定された HDFS ファイル パスの暗号化情報を取得します。
[azdata bdc hdfs encryption-zone status](#azdata-bdc-hdfs-encryption-zone-status) | HDFS クラスターの再暗号化の状態を取得します。
[azdata bdc hdfs encryption-zone reencrypt](#azdata-bdc-hdfs-encryption-zone-reencrypt) | --path 引数で指定された暗号化ゾーンの再暗号化を制御します。
## <a name="azdata-bdc-hdfs-encryption-zone-create"></a>azdata bdc hdfs encryption-zone create
指定されたキーを使用して暗号化ゾーン内のファイルを暗号化することにより、HDFS フォルダーを暗号化ゾーンに変換します。
```bash
azdata bdc hdfs encryption-zone create --path -p 
                                       --keyname -k
```
### <a name="examples"></a>例
securelake というキーを使用して、既存のフォルダー /user/securefolder を暗号化ゾーンに変換するには
```bash
azdata bdc hdfs encryption-zone create --path /home/securefolder --keyname securelake
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--path -p`
暗号化ゾーンに変換する HDFS フォルダーのパス。
#### `--keyname -k`
暗号化ゾーンを保護するために使用する Hadoop KMS キー。
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
## <a name="azdata-bdc-hdfs-encryption-zone-list"></a>azdata bdc hdfs encryption-zone list
すべての暗号化ゾーンと、暗号化ゾーンに関連付けられているキーの一覧を表示します。
```bash
azdata bdc hdfs encryption-zone list 
```
### <a name="examples"></a>例
すべての暗号化ゾーンの一覧を表示します。
```bash
azdata bdc hdfs encryption-zone list
```
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
## <a name="azdata-bdc-hdfs-encryption-zone-get-file-encryption-info"></a>azdata bdc hdfs encryption-zone get-file-encryption-info
指定された HDFS ファイル パスの暗号化情報を取得します。
```bash
azdata bdc hdfs encryption-zone get-file-encryption-info --path -p 
                                                         
```
### <a name="examples"></a>例
/user/securefolder/data.csv にあるファイルの暗号化情報を取得します。
```bash
azdata bdc hdfs encryption-zone get-file-encryption-info --path /user/securefolder/data.csv
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--path -p`
暗号化情報を取得する必要がある HDFS ファイルのパス。
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
## <a name="azdata-bdc-hdfs-encryption-zone-status"></a>azdata bdc hdfs encryption-zone status
HDFS クラスターの再暗号化の状態を取得します。
```bash
azdata bdc hdfs encryption-zone status 
```
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
## <a name="azdata-bdc-hdfs-encryption-zone-reencrypt"></a>azdata bdc hdfs encryption-zone reencrypt
--path 引数で指定された暗号化ゾーンの再暗号化を制御します。
```bash
azdata bdc hdfs encryption-zone reencrypt --path -p 
                                          --action -a
```
### <a name="examples"></a>例
暗号化ゾーン securelake の再暗号化を開始します。
```bash
azdata bdc hdfs encryption-zone reencrypt --path /securelake --action start
```
暗号化ゾーン securelake の再暗号化をキャンセルします。
```bash
azdata bdc hdfs encryption-zone reencrypt --path /securelake --action cancel
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--path -p`
再暗号化する必要がある HDFS 暗号化ゾーン フォルダーのパス
#### `--action -a`
実行する再暗号化アクション。 有効な値は start と cancel です
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
