---
title: azdata arc postgres server リファレンス
titleSuffix: SQL Server big data clusters
description: azdata arc postgres server コマンドに関するリファレンス記事です。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0a28ba44dfbeb2b0ef1b5191e6e3bfba5352d540
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358730"
---
# <a name="azdata-arc-postgres-server"></a>azdata arc postgres server

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] への適用

以下の記事では、**azdata** ツールの **sql** コマンドに関するリファレンスを提供します。 他の **azdata** コマンドの詳細については、[azdata リファレンス](reference-azdata.md)に関するページを参照してください。

## <a name="commands"></a>コマンド

|command|説明|
| --- | --- |
[azdata arc postgres server create](#azdata-arc-postgres-server-create) | PostgreSQL サーバー グループを作成します。
[azdata arc postgres server edit](#azdata-arc-postgres-server-edit) | PostgreSQL サーバー グループの構成を編集します。
[azdata arc postgres server delete](#azdata-arc-postgres-server-delete) | PostgreSQL サーバー グループを削除します。
[azdata arc postgres server show](#azdata-arc-postgres-server-show) | PostgreSQL サーバー グループの詳細を表示します。
[azdata arc postgres server list](#azdata-arc-postgres-server-list) | PostgreSQL サーバー グループの一覧を表示します。
[azdata arc postgres server config](reference-azdata-arc-postgres-server-config.md) | 構成コマンド。
[azdata arc postgres server backup](reference-azdata-arc-postgres-server-backup.md) | PostgreSQL サーバー グループのバックアップを管理します。
## <a name="azdata-arc-postgres-server-create"></a>azdata arc postgres server create
サーバー グループのパスワードを設定するには、環境変数 AZDATA_PASSWORD を設定してください
```bash
azdata arc postgres server create --name -n 
                                  [--path]  
                                  
[--cores-limit -cl]  
                                  
[--cores-request -cr]  
                                  
[--memory-limit -ml]  
                                  
[--memory-request -mr]  
                                  
[--storage-class-data -scd]  
                                  
[--storage-class-logs -scl]  
                                  
[--storage-class-backups -scb]  
                                  
[--extensions]  
                                  
[--volume-size-data -vsd]  
                                  
[--volume-size-logs -vsl]  
                                  
[--volume-size-backups -vsb]  
                                  
[--workers -w]  
                                  
[--engine-version -ev]  
                                  
[--no-external-endpoint]  
                                  
[--dev]  
                                  
[--port]  
                                  
[--no-wait]  
                                  
[--engine-settings -e]
```
### <a name="examples"></a>使用例
PostgreSQL サーバー グループを作成します。
```bash
azdata arc postgres server create -n pg1
```
エンジンの設定を使用して PostgreSQL サーバー グループを作成します。 次の例はいずれも有効です。
```bash
azdata arc postgres server create -n pg1 --engine-settings "key1=val1"
azdata arc postgres server create -n pg1 --engine-settings "key2=val2"
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--name -n`
インスタンスの名前。
### <a name="optional-parameters"></a>省略可能のパラメーター
#### `--path`
PostgreSQL サーバー グループのソース json ファイルへのパス。 これはオプションです。
#### `--cores-limit -cl`
ノードごとに使用できる Postgres インスタンスの CPU コアの最大数。 少数のコアがサポートされています。
#### `--cores-request -cr`
サービスをスケジュールするためにノードごとに使用できる必要がある CPU コアの最小数。 少数のコアがサポートされています。
#### `--memory-limit -ml`
Postgres インスタンスのメモリ制限。数値の後に Ki (キロバイト)、Mi (メガバイト)、または Gi (ギガバイト) を付けたもの。
#### `--memory-request -mr`
Postgres インスタンスのメモリ要求。数値の後に Ki (キロバイト)、Mi (メガバイト)、または Gi (ギガバイト) を付けたもの。
#### `--storage-class-data -scd`
データ永続ボリュームに使用するストレージ クラス。
#### `--storage-class-logs -scl`
ログ永続ボリュームに使用するストレージ クラス。
#### `--storage-class-backups -scb`
バックアップ永続ボリュームに使用するストレージ クラス。
#### `--extensions`
起動時に読み込む必要のある Postgres 拡張機能のコンマ区切りのリスト。 サポートされている値については、Postgres のドキュメントを参照してください。
#### `--volume-size-data -vsd`
データに使用するストレージ ボリュームのサイズを示す正の数値と、その後の Ki (キロバイト)、Mi (メガバイト)、または Gi (ギガバイト)。
#### `--volume-size-logs -vsl`
ログに使用するストレージ ボリュームのサイズを示す正の数値と、その後の Ki (キロバイト)、Mi (メガバイト)、または Gi (ギガバイト)。
#### `--volume-size-backups -vsb`
バックアップに使用するストレージ ボリュームのサイズを示す正の数値と、その後の Ki (キロバイト)、Mi (メガバイト)、または Gi (ギガバイト)。
#### `--workers -w`
シャード化クラスターにプロビジョニングするワーカー ノードの数。シングル ノードの Postgres の場合はゼロ (既定値)。
#### `--engine-version -ev`
11 または 12 にする必要があります。 既定値は 12 です。
#### `--no-external-endpoint`
指定した場合、外部サービスは作成されません。 それ以外の場合、データ コントローラーと同じサービスの種類を使用して外部サービスが作成されます。
#### `--dev`
これを指定した場合、それは dev インスタンスと見なされ、課金されません。
#### `--port`
省略可能。
#### `--no-wait`
指定した場合、コマンドは戻る前に、インスタンスが準備完了状態になるのを待機しません。
#### `--engine-settings -e`
"key1=val1, key2=val2" という形式の、Postgres エンジン設定のコンマ区切りリスト。
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
## <a name="azdata-arc-postgres-server-edit"></a>azdata arc postgres server edit
PostgreSQL サーバー グループの構成を編集します。
```bash
azdata arc postgres server edit --name -n 
                                [--path]  
                                
[--workers -w]  
                                
[--engine-version -ev]  
                                
[--cores-limit -cl]  
                                
[--cores-request -cr]  
                                
[--memory-limit -ml]  
                                
[--memory-request -mr]  
                                
[--extensions]  
                                
[--dev]  
                                
[--port]  
                                
[--no-wait]  
                                
[--engine-settings -e]  
                                
[--replace-engine-settings -re]  
                                
[--admin-password]
```
### <a name="examples"></a>使用例
PostgreSQL サーバー グループの構成を編集します。
```bash
azdata arc postgres server edit --src ./spec.json -n pg1
```
エンジンの設定を使用して PostgreSQL サーバー グループを編集します。
```bash
azdata arc postgres server edit -n pg1 --engine-settings "key2=val2"
```
PostgreSQL サーバー グループを編集し、既存のエンジン設定を新しい設定の key1=val1 に置き換えます。
```bash
azdata arc postgres server edit -n pg1 --engine-settings "key1=val1" --replace-engine-settings
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--name -n`
編集する PostgreSQL サーバー グループの名前。 インスタンスを配置するときに使用した名前を変更することはできません。
### <a name="optional-parameters"></a>省略可能のパラメーター
#### `--path`
PostgreSQL サーバー グループのソース json ファイルへのパス。 これはオプションです。
#### `--workers -w`
シャード化クラスターにプロビジョニングするワーカー ノードの数。シングル ノードの Postgres の場合はゼロ (既定値)。
#### `--engine-version -ev`
エンジンのバージョンは変更できません。 エンジン バージョンが異なる 2 つのサーバー グループの名前が同じである場合に、--engine-version を --name と組み合わせて使用すると、PostgreSQL Hyperscale サーバー グループを識別できます。 --engine-version は省略可能で、サーバー グループの識別に使用する場合、11 または 12 を使用する必要があります。
#### `--cores-limit -cl`
ノードごとに使用できる Postgres インスタンスの CPU コアの最大数。少数のコアがサポートされています。 cores_limit を削除するには、その値を空の文字列として指定します。
#### `--cores-request -cr`
サービスをスケジュールするためにノードごとに使用できる必要がある CPU コアの最小数。少数のコアがサポートされています。 cores_request を削除するには、その値を空の文字列として指定します。
#### `--memory-limit -ml`
Postgres インスタンスのメモリ制限。数値の後に Ki (キロバイト)、Mi (メガバイト)、または Gi (ギガバイト) を付けたもの。 memory_limit を削除するには、その値を空の文字列として指定します。
#### `--memory-request -mr`
Postgres インスタンスのメモリ要求。数値の後に Ki (キロバイト)、Mi (メガバイト)、または Gi (ギガバイト) を付けたもの。 memory_request を削除するには、その値を空の文字列として指定します。
#### `--extensions`
起動時に読み込む必要のある Postgres 拡張機能のコンマ区切りのリスト。 サポートされている値については、Postgres のドキュメントを参照してください。
#### `--dev`
これを指定した場合、それは dev インスタンスと見なされ、課金されません。
#### `--port`
省略可能。
#### `--no-wait`
指定した場合、コマンドは戻る前に、インスタンスが準備完了状態になるのを待機しません。
#### `--engine-settings -e`
"key1=val1, key2=val2" という形式の、Postgres エンジン設定のコンマ区切りリスト。 指定した設定は、既存の設定とマージされます。 設定を削除するには、"removedKey=" のように空の値を指定します。 再起動が必要なエンジン設定を変更すると、すぐに設定を適用するためにサービスが再起動されます。
#### `--replace-engine-settings -re`
--engine-settings と共に指定すると、既存のすべてのカスタム エンジンの設定が設定と値の新しいセットに置き換えられます。
#### `--admin-password`
指定すると、Postgres サーバーの管理者パスワードは、AZDATA_PASSWORD 環境変数が存在する場合はその値に設定され、それ以外の場合はプロンプトが表示されます。
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
## <a name="azdata-arc-postgres-server-delete"></a>azdata arc postgres server delete
PostgreSQL サーバー グループを削除します。
```bash
azdata arc postgres server delete --name -n 
                                  [--engine-version -ev]
```
### <a name="examples"></a>使用例
PostgreSQL サーバー グループを削除します。
```bash
azdata arc postgres server delete -n pg1
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--name -n`
PostgreSQL サーバー グループの名前。
### <a name="optional-parameters"></a>省略可能のパラメーター
#### `--engine-version -ev`
エンジン バージョンが異なる 2 つのサーバー グループの名前が同じである場合に、--engine-version を --name と組み合わせて使用すると、PostgreSQL Hyperscale サーバー グループを識別できます。 --engine-version は省略可能で、サーバー グループの識別に使用する場合、11 または 12 を使用する必要があります。
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
## <a name="azdata-arc-postgres-server-show"></a>azdata arc postgres server show
PostgreSQL サーバー グループの詳細を表示します。
```bash
azdata arc postgres server show --name -n 
                                [--engine-version -ev]  
                                
[--path -p]
```
### <a name="examples"></a>使用例
PostgreSQL サーバー グループの詳細を表示します。
```bash
azdata arc postgres server show -n pg1
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--name -n`
PostgreSQL サーバー グループの名前。
### <a name="optional-parameters"></a>省略可能のパラメーター
#### `--engine-version -ev`
エンジン バージョンが異なる 2 つのサーバー グループの名前が同じである場合に、--engine-version を --name と組み合わせて使用すると、PostgreSQL Hyperscale サーバー グループを識別できます。 --engine-version は省略可能で、サーバー グループの識別に使用する場合、11 または 12 を使用する必要があります。
#### `--path -p`
PostgreSQL サーバー グループの完全な仕様を書き込む先のパス。 省略した場合、仕様は標準出力に書き込まれます。
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
## <a name="azdata-arc-postgres-server-list"></a>azdata arc postgres server list
PostgreSQL サーバー グループの一覧を表示します。
```bash
azdata arc postgres server list 
```
### <a name="examples"></a>使用例
PostgreSQL サーバー グループの一覧を表示します。
```bash
azdata arc postgres server list
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

## <a name="next-steps"></a>次のステップ

他の **azdata** コマンドの詳細については、[azdata リファレンス](reference-azdata.md)に関するページを参照してください。 

**azdata** ツールをインストールする方法の詳細については、「[azdata のインストール](..\install\deploy-install-azdata.md)」を参照してください。

