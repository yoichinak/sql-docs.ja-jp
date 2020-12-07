---
title: azdata postgres のリファレンス
titleSuffix: SQL Server big data clusters
description: azdata postgres コマンドのリファレンス記事です。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ab6518677ffdbba92ec51da9f3c0fb7dbb0af0d7
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358131"
---
# <a name="azdata-postgres"></a>azdata postgres

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] への適用

以下の記事では、**azdata** ツールの **sql** コマンドに関するリファレンスを提供します。 他の **azdata** コマンドの詳細については、[azdata リファレンス](reference-azdata.md)に関するページを参照してください。

## <a name="commands"></a>コマンド

|command|説明|
| --- | --- |
[azdata postgres shell](#azdata-postgres-shell) | Postgres 用のコマンド ライン シェル インターフェイス。 「https://www.pgcli.com/」を参照してください。
[azdata postgres query](#azdata-postgres-query) | query コマンドを使用すると、データベース セッションで PostgreSQL コマンドを実行できます。
## <a name="azdata-postgres-shell"></a>azdata postgres shell
Postgres 用のコマンド ライン シェル インターフェイス。 「https://www.pgcli.com/」を参照してください。
```bash
azdata postgres shell [--dbname -d] 
                      [--host]  
                      
[--port -p]  
                      
[--password -w]  
                      
[--no-password]  
                      
[--single-connection]  
                      
[--username -u]  
                      
[--pgclirc]  
                      
[--dsn]  
                      
[--list-dsn]  
                      
[--row-limit]  
                      
[--less-chatty]  
                      
[--prompt]  
                      
[--prompt-dsn]  
                      
[--list -l]  
                      
[--auto-vertical-output]  
                      
[--warn]  
                      
[--no-warn]
```
### <a name="examples"></a>例
対話型エクスペリエンスを開始するコマンド ラインの例。
```bash
azdata postgres shell
```
指定されたデータベースとユーザーを使用したコマンド ラインの例
```bash
azdata postgres shell --dbname <database> --username <username> --host <host>
```
完全な接続文字列を使用して開始するコマンド ラインの例。
```bash
azdata postgres shell --dbname postgres://user:passw0rd@example.com:5432/master 
```
### <a name="optional-parameters"></a>省略可能のパラメーター
#### `--dbname -d`
接続先のデータベース名。
#### `--host`
postgres データベースのホスト アドレス。
#### `--port -p`
postgres インスタンスがリッスンしているポート番号。
#### `--password -w`
パスワード プロンプトを強制します。
#### `--no-password`
パスワードの入力を求めません。
#### `--single-connection`
入力候補として別の接続を使用しないでください。
#### `--username -u`
postgres データベースに接続するためのユーザー名。
#### `--pgclirc`
pgclirc ファイルの場所。
#### `--dsn`
pgclirc ファイルの [alias_dsn] セクションに構成されている DSN を使用します。
#### `--list-dsn`
pgclirc ファイルの [alias_dsn] セクションに構成されている DSN の一覧。
#### `--row-limit`
行制限プロンプトのしきい値を設定します。 プロンプトを無効にするには 0 を使用します。
#### `--less-chatty`
起動時にイントロを、終了時にさようならをスキップします。
#### `--prompt`
プロンプト形式 (既定値: "\u@\h:\d> ")。
#### `--prompt-dsn`
DSN エイリアスを使用した接続用のプロンプト形式 (既定値: "\u@\h:\d> ")。
#### `--list -l`
使用可能なデータベースを一覧表示してから終了します。
#### `--auto-vertical-output`
結果がターミナルの横方向に収まりきれない場合は、自動的に縦方向出力モードに切り替わります。
#### `--warn`
破壊的なクエリを実行する前に警告を出します。
#### `--no-warn`
破壊的なクエリを実行する前に警告を出します。
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
## <a name="azdata-postgres-query"></a>azdata postgres query
query コマンドを使用すると、データベース セッションで PostgreSQL コマンドを実行できます。
```bash
azdata postgres query --q -q 
                      [--host]  
                      
[--dbname -d]  
                      
[--port -p]  
                      
[--username -u]
```
### <a name="examples"></a>使用例
Information_schema 内のすべてのテーブルを一覧表示します。
```bash
azdata postgres query --host <host> --username <username> -q "SELECT * FROM information_schema.tables"
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--q -q`
実行する PostgreSQL クエリ。
### <a name="optional-parameters"></a>省略可能のパラメーター
#### `--host`
postgres データベースのホスト アドレス。
`localhost`
#### `--dbname -d`
クエリを実行するデータベース。
#### `--port -p`
postgres インスタンスがリッスンしているポート番号。
`5432`
#### `--username -u`
postgres データベースに接続するためのユーザー名。
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

