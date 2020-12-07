---
title: azdata bdc spark statement のリファレンス
titleSuffix: SQL Server big data clusters
description: azdata bdc spark statement コマンドのリファレンス記事です。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5d39e9b28edf04848fd718459219691f9c020b67
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358422"
---
# <a name="azdata-bdc-spark-statement"></a>azdata bdc spark statement

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] への適用

以下の記事では、**azdata** ツールの **sql** コマンドに関するリファレンスを提供します。 他の **azdata** コマンドの詳細については、[azdata リファレンス](reference-azdata.md)に関するページを参照してください。

## <a name="commands"></a>コマンド

|command|説明|
| --- | --- |
[azdata bdc spark statement list](#azdata-bdc-spark-statement-list) | 指定した Spark セッションに含まれているすべてのステートメントを一覧表示します。
[azdata bdc spark statement create](#azdata-bdc-spark-statement-create) | 指定したセッションに新しい Spark ステートメントを作成します。
[azdata bdc spark statement info](#azdata-bdc-spark-statement-info) | 指定した Spark セッション内の要求したステートメントに関する情報を取得します。
[azdata bdc spark statement cancel](#azdata-bdc-spark-statement-cancel) | 指定した Spark セッション内のステートメントをキャンセルします。
## <a name="azdata-bdc-spark-statement-list"></a>azdata bdc spark statement list
指定した Spark セッションに含まれているすべてのステートメントを一覧表示します。
```bash
azdata bdc spark statement list --session-id -i 
                                
```
### <a name="examples"></a>例
セッションのすべてのステートメントを一覧表示します。
```bash
azdata bdc spark statement list --session-id 0
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--session-id -i`
Spark セッションの ID 番号。
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
## <a name="azdata-bdc-spark-statement-create"></a>azdata bdc spark statement create
これを使うと、指定したセッションで新しいステートメントの作成と実行を行うことができます。  簡単な実行の場合は、実行の出力が結果に含まれます。  それ以外の場合は、ステートメントの完了後に 'spark session info' を使って結果を取得できます。
```bash
azdata bdc spark statement create --session-id -i 
                                  --code -c
```
### <a name="examples"></a>例
ステートメントを実行します。
```bash
azdata bdc spark statement create --session-id 0 --code "2+2"
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--session-id -i`
Spark セッションの ID 番号。
#### `--code -c`
ステートメントの一部として実行するコードを含む文字列。
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
## <a name="azdata-bdc-spark-statement-info"></a>azdata bdc spark statement info
これを使うと、実行状態と、ステートメントが完了している場合は実行結果を取得できます。 ステートメント ID は 'spark statement create' から返されます。
```bash
azdata bdc spark statement info --session-id -i 
                                --statement-id -s
```
### <a name="examples"></a>例
セッション ID が 0、ステートメント ID が 0 のステートメント情報を取得します。
```bash
azdata bdc spark statement info --session-id 0 --statement-id 0
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--session-id -i`
Spark セッションの ID 番号。
#### `--statement-id -s`
指定したセッション ID 内の Spark ステートメントの ID 番号。
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
## <a name="azdata-bdc-spark-statement-cancel"></a>azdata bdc spark statement cancel
これを使うと、指定した Spark セッション内のステートメントをキャンセルできます。 ステートメント ID は 'spark statement create' から返されます。
```bash
azdata bdc spark statement cancel --session-id -i 
                                  --statement-id -s
```
### <a name="examples"></a>例
ステートメントをキャンセルします。
```bash
azdata bdc spark statement cancel --session-id 0 --statement-id 0
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--session-id -i`
Spark セッションの ID 番号。
#### `--statement-id -s`
指定したセッション ID 内の Spark ステートメントの ID 番号。
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

