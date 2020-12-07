---
title: azdata bdc spark batch リファレンス
titleSuffix: SQL Server big data clusters
description: azdata bdc spark batch コマンドのリファレンス記事です。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 74968c1efd64ecc382b7a0ab9669a983bb442ef7
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358509"
---
# <a name="azdata-bdc-spark-batch"></a>azdata bdc spark batch

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] への適用

以下の記事では、**azdata** ツールの **sql** コマンドに関するリファレンスを提供します。 他の **azdata** コマンドの詳細については、[azdata リファレンス](reference-azdata.md)に関するページを参照してください。

## <a name="commands"></a>コマンド

|command|説明|
| --- | --- |
[azdata bdc spark batch create](#azdata-bdc-spark-batch-create) | 新しい Spark バッチを作成します。
[azdata bdc spark batch list](#azdata-bdc-spark-batch-list) | Spark 内のすべてのバッチを一覧表示します。
[azdata bdc spark batch info](#azdata-bdc-spark-batch-info) | アクティブな Spark バッチに関する情報を取得します。
[azdata bdc spark batch log](#azdata-bdc-spark-batch-log) | Spark バッチの実行ログを取得します。
[azdata bdc spark batch state](#azdata-bdc-spark-batch-state) | Spark バッチの実行状態を取得します。
[azdata bdc spark batch delete](#azdata-bdc-spark-batch-delete) | Spark バッチを削除します。
## <a name="azdata-bdc-spark-batch-create"></a>azdata bdc spark batch create
これを使うと、指定したコードを実行する新しいバッチ Spark ジョブを作成できます。
```bash
azdata bdc spark batch create --file -f 
                              [--class-name -c]  
                              
[--arguments -a]  
                              
[--jar-files -j]  
                              
[--py-files -p]  
                              
[--files]  
                              
[--driver-memory]  
                              
[--driver-cores]  
                              
[--executor-memory]  
                              
[--executor-cores]  
                              
[--executor-count]  
                              
[--archives]  
                              
[--queue -q]  
                              
[--name -n]  
                              
[--config]
```
### <a name="examples"></a>例
新しい Spark バッチを作成します。
```bash
azdata bdc spark batch create --code "2+2"
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--file -f`
実行するファイルのパス。
### <a name="optional-parameters"></a>省略可能なパラメーター
#### `--class-name -c`
1 つ以上の jar ファイルを渡すときに実行するクラスの名前。
#### `--arguments -a`
引数のリスト。  リストを渡すには、値を JSON エンコードします。  例: '["entry1", "entry2"]'。
#### `--jar-files -j`
jar ファイル パスのリスト。  リストを渡すには、値を JSON エンコードします。  例: '["entry1", "entry2"]'。
#### `--py-files -p`
python ファイル パスのリスト。  リストを渡すには、値を JSON エンコードします。  例: '["entry1", "entry2"]'。
#### `--files`
ファイル パスのリスト。  リストを渡すには、値を JSON エンコードします。  例: '["entry1", "entry2"]'。
#### `--driver-memory`
ドライバーに割り当てるメモリの量。  値の一部として単位を指定します。  例: 512M または 2G。
#### `--driver-cores`
ドライバーに割り当てる CPU コアの量。
#### `--executor-memory`
実行プログラムに割り当てるメモリの量。  値の一部として単位を指定します。  例: 512M または 2G。
#### `--executor-cores`
実行プログラムに割り当てる CPU コアの量。
#### `--executor-count`
実行する実行プログラムのインスタンスの数。
#### `--archives`
アーカイブ パスのリスト。  リストを渡すには、値を JSON エンコードします。  例: '["entry1", "entry2"]'。
#### `--queue -q`
セッションを実行する Spark キューの名前。
#### `--name -n`
Spark セッションの名前。
#### `--config`
Spark 構成値を含む名前と値のペアのリスト。  JSON ディクショナリとしてエンコードされます。  例: '{"name":"value", "name2":"value2"}'。
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
## <a name="azdata-bdc-spark-batch-list"></a>azdata bdc spark batch list
Spark 内のすべてのバッチを一覧表示します。
```bash
azdata bdc spark batch list 
```
### <a name="examples"></a>例
すべてのアクティブなバッチを一覧表示します。
```bash
azdata bdc spark batch list
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
## <a name="azdata-bdc-spark-batch-info"></a>azdata bdc spark batch info
これを使うと、指定した ID を持つ Spark バッチに関する情報を取得できます。  バッチ ID は 'spark batch create' から返されます。
```bash
azdata bdc spark batch info --batch-id -i 
                            
```
### <a name="examples"></a>例
ID が 0 のバッチのバッチ情報を取得します。
```bash
azdata bdc spark batch info --batch-id 0
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--batch-id -i`
Spark バッチの ID 番号。
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
## <a name="azdata-bdc-spark-batch-log"></a>azdata bdc spark batch log
これを使うと、指定した ID を持つ Spark バッチのバッチ ログ エントリを取得できます。  バッチ ID は 'spark batch create' から返されます。
```bash
azdata bdc spark batch log --batch-id -i 
                           
```
### <a name="examples"></a>例
ID が 0 のバッチのバッチ ログを取得します。
```bash
azdata bdc spark batch log --batch-id 0
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--batch-id -i`
Spark バッチの ID 番号。
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
## <a name="azdata-bdc-spark-batch-state"></a>azdata bdc spark batch state
これを使うと、指定した ID を持つ Spark バッチのバッチ状態を取得できます。  バッチ ID は 'spark batch create' から返されます。
```bash
azdata bdc spark batch state --batch-id -i 
                             
```
### <a name="examples"></a>例
ID が 0 のバッチのバッチ状態を取得します。
```bash
azdata bdc spark batch state --batch-id 0
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--batch-id -i`
Spark バッチの ID 番号。
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
## <a name="azdata-bdc-spark-batch-delete"></a>azdata bdc spark batch delete
これを使うと、Spark バッチを削除できます。 バッチ ID は 'spark batch create' から返されます。
```bash
azdata bdc spark batch delete --batch-id -i 
                              
```
### <a name="examples"></a>例
バッチを削除します。
```bash
azdata bdc spark batch delete --batch-id 0
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--batch-id -i`
Spark バッチの ID 番号。
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

