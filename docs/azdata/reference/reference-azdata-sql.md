---
title: azdata sql リファレンス
titleSuffix: SQL Server big data clusters
description: azdata sql コマンドのリファレンス記事です。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 794c7be56eaa0591d120b4fea40a725fdeecaac1
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358110"
---
# <a name="azdata-sql"></a>azdata sql

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] への適用

以下の記事では、**azdata** ツールの **sql** コマンドに関するリファレンスを提供します。 他の **azdata** コマンドの詳細については、[azdata リファレンス](reference-azdata.md)に関するページを参照してください。

## <a name="commands"></a>コマンド

|command|説明|
| --- | --- |
[azdata sql shell](#azdata-sql-shell) | SQL CLI を使用すると、ユーザーは T-SQL を使用して SQL Server や Azure SQL とやりとりすることができます。
[azdata sql query](#azdata-sql-query) | SQL CLI を使用すると、ユーザーは T-SQL を使用して SQL Server や Azure SQL とやりとりすることができます。
## <a name="azdata-sql-shell"></a>azdata sql shell
SQL CLI を使用すると、ユーザーは T-SQL を使用して SQL Server や Azure SQL とやりとりすることができます。
```bash
azdata sql shell [--username -u] 
                 [--database -d]  
                 
[--server -s]  
                 
[--integrated -e]  
                 
[--mssqlclirc]  
                 
[--row-limit]  
                 
[--less-chatty]  
                 
[--auto-vertical-output]  
                 
[--encrypt -n]  
                 
[--trust-server-certificate -c]  
                 
[--connect-timeout -l]  
                 
[--application-intent -k]  
                 
[--multi-subnet-failover -m]  
                 
[--packet-size]  
                 
[--dac-connection -a]  
                 
[--input-file -i]  
                 
[--output-file]  
                 
[--enable-sqltoolsservice-logging]  
                 
[--prompt]
```
### <a name="examples"></a>例
対話型エクスペリエンスを開始するコマンド ラインの例。
```bash
azdata sql shell
```
指定されたサーバー、ユーザー、データベースを使用したコマンド ラインの例
```bash
azdata sql shell --server localhost --username sa --database master         
```
### <a name="optional-parameters"></a>省略可能のパラメーター
#### `--username -u`
データベースに接続するためのユーザー名。
#### `--database -d`
接続先のデータベース名。
#### `--server -s`
SQL Server インスタンスの名前またはアドレス。
#### `--integrated -e`
Windows で統合認証を使用します。
#### `--mssqlclirc`
mssqlclirc 構成ファイルの場所。
#### `--row-limit`
行制限プロンプトのしきい値を設定します。 プロンプトを無効にするには 0 を使用します。
#### `--less-chatty`
起動時にイントロを、終了時にさようならをスキップします。
#### `--auto-vertical-output`
結果がターミナルの横方向に収まりきれない場合は、自動的に縦方向出力モードに切り替わります。
#### `--encrypt -n`
サーバーに証明書がインストールされている場合、SQL Server によってすべてのデータに SSL 暗号化が使用されます。
#### `--trust-server-certificate -c`
信頼を検証するための証明書チェーンの走査をバイパスする間、チャネルは暗号化されます。
#### `--connect-timeout -l`
要求を終了する前にサーバーへの接続を待機する時間 (秒)。
#### `--application-intent -k`
SQL Server 可用性グループのデータベースに接続するときに、アプリケーションのワークロードの種類を宣言します。
#### `--multi-subnet-failover -m`
アプリケーションで異なるサブネット上の AlwaysOn AG に接続している場合、これを設定すると、現在アクティブなサーバーに対する検出と接続が高速化されます。
#### `--packet-size`
SQL Server との通信に使用されるネットワーク パケットのサイズ (バイト)。
#### `--dac-connection -a`
専用管理者接続を使用して SQL Server に接続します。
#### `--input-file -i`
処理対象の SQL ステートメントのバッチが含まれるファイルを指定します。
#### `--output-file`
クエリからの出力を受け取るファイルを指定します。
#### `--enable-sqltoolsservice-logging`
SqlToolsService 用の診断ログを有効にします。
#### `--prompt`
プロンプトの形式 (既定値: \d>)
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
## <a name="azdata-sql-query"></a>azdata sql query
SQL CLI を使用すると、ユーザーは T-SQL を使用して SQL Server や Azure SQL とやりとりすることができます。
```bash
azdata sql query -q 
                 [--database -d]  
                 
[--username -u]  
                 
[--server -s]  
                 
[--integrated -e]
```
### <a name="examples"></a>使用例
テーブル名の一覧を選択するためのコマンド ラインの例。
```bash
azdata sql query --server localhost --username sa --database master -q "SELECT name FROM SYS.TABLES"
```
### <a name="required-parameters"></a>必須のパラメーター
#### `-q`
実行する SQL クエリ。
### <a name="optional-parameters"></a>省略可能のパラメーター
#### `--database -d`
接続先のデータベース名。
`master`
#### `--username -u`
データベースに接続するためのユーザー名。
#### `--server -s`
SQL Server インスタンスの名前またはアドレス。
#### `--integrated -e`
Windows で統合認証を使用します。
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

