---
title: azdata bdc hdfs key リファレンス
titleSuffix: SQL Server big data clusters
description: azdata bdc hdfs key コマンドに関するリファレンス記事です。
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c208d1c726bae41b349abdf475627afbc82ed2b8
ms.sourcegitcommit: 8dc7e0ececf15f3438c05ef2c9daccaac1bbff78
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/13/2021
ms.locfileid: "100342503"
---
# <a name="azdata-bdc-hdfs-key"></a>azdata bdc hdfs key

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] への適用

以下の記事では、**azdata** ツールの **sql** コマンドに関するリファレンスを提供します。 他の **azdata** コマンドの詳細については、[azdata リファレンス](reference-azdata.md)に関するページを参照してください。

## <a name="commands"></a>コマンド
|コマンド|説明|
| --- | --- |
[azdata bdc hdfs key create](#azdata-bdc-hdfs-key-create) | HDFS キーを作成します。
[azdata bdc hdfs key list](#azdata-bdc-hdfs-key-list) | すべての Hadoop 暗号化ゾーン キーを一覧表示します。
[azdata bdc hdfs key roll](#azdata-bdc-hdfs-key-roll) | HDFS キーをロールします。
## <a name="azdata-bdc-hdfs-key-create"></a>azdata bdc hdfs key create
指定された名前とサイズで HDFS キーを作成します。
```bash
azdata bdc hdfs key create --name -n 
                           [--size -size]
```
### <a name="examples"></a>例
key1 という名前の 256 ビット キーを作成するには、azdata hdfs key create --name key1 --size 256 を使用します
```bash
azdata hdfs key create --name key1 --size 256
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--name -n`
Hadoop 暗号化ゾーン キーの名前。 
### <a name="optional-parameters"></a>省略可能のパラメーター
#### `--size -size`
Hadoop 暗号化キーのビット長 (既定の長さは 256 です)。
`256`
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
## <a name="azdata-bdc-hdfs-key-list"></a>azdata bdc hdfs key list
すべての Hadoop 暗号化ゾーン キーを一覧表示します。
```bash
azdata bdc hdfs key list 
```
### <a name="examples"></a>例
すべての Hadoop 暗号化ゾーン キーを一覧表示するには、azdata bdc hdfs key list を使用します
```bash
azdata bdc hdfs key list
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
## <a name="azdata-bdc-hdfs-key-roll"></a>azdata bdc hdfs key roll
指定された名前で HDFS キーをロールします。
```bash
azdata bdc hdfs key roll --name -n 
                         
```
### <a name="examples"></a>例
key1 という名前でキーをロールするには、azdata hdfs key roll --name key1 を使用します。
```bash
azdata hdfs key roll --name key1
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--name -n`
新しいバージョンにロールする暗号化ゾーン キーの名前。 
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
