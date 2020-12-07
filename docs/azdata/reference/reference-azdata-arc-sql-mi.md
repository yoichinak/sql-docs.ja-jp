---
title: azdata arc sql mi リファレンス
titleSuffix: SQL Server big data clusters
description: azdata arc sql mi コマンドのリファレンス記事です。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 234a990cde52a6fd051410d30000413b9acfa3a0
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358680"
---
# <a name="azdata-arc-sql-mi"></a>azdata arc sql mi

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] への適用

以下の記事では、**azdata** ツールの **sql** コマンドに関するリファレンスを提供します。 他の **azdata** コマンドの詳細については、[azdata リファレンス](reference-azdata.md)に関するページを参照してください。

## <a name="commands"></a>コマンド

|command|説明|
| --- | --- |
[azdata arc sql mi create](#azdata-arc-sql-mi-create) | SQL マネージド インスタンスを作成します。
[azdata arc sql mi edit](#azdata-arc-sql-mi-edit) | SQL マネージド インスタンスの構成を編集します。
[azdata arc sql mi delete](#azdata-arc-sql-mi-delete) | SQL マネージド インスタンスを削除します。
[azdata arc sql mi show](#azdata-arc-sql-mi-show) | SQL マネージド インスタンスの詳細を表示します。
[azdata arc sql mi list](#azdata-arc-sql-mi-list) | SQL マネージド インスタンスの一覧を表示します。
[azdata arc sql mi config](reference-azdata-arc-sql-mi-config.md) | 構成コマンド。
## <a name="azdata-arc-sql-mi-create"></a>azdata arc sql mi create
SQL マネージド インスタンスのパスワードを設定するには、環境変数 AZDATA_PASSWORD を設定してください
```bash
azdata arc sql mi create --name -n 
                         [--path]  
                         
[--cores-limit -cl]  
                         
[--cores-request -cr]  
                         
[--memory-limit -ml]  
                         
[--memory-request -mr]  
                         
[--storage-class-data -scd]  
                         
[--storage-class-logs -scl]  
                         
[--storage-class-data-logs -scdl]  
                         
[--storage-class-backups -scb]  
                         
[--volume-size-data -vsd]  
                         
[--volume-size-logs -vsl]  
                         
[--volume-size-data-logs -vsdl]  
                         
[--volume-size-backups -vsb]  
                         
[--no-external-endpoint]  
                         
[--dev]  
                         
[--no-wait]
```
### <a name="examples"></a>使用例
SQL マネージド インスタンスを作成します。
```bash
azdata arc sql mi create -n sqlmi1
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--name -n`
SQL マネージド インスタンスの名前。
### <a name="optional-parameters"></a>省略可能のパラメーター
#### `--path`
SQL マネージド インスタンスの json ファイルに対する src ファイルへのパス。
#### `--cores-limit -cl`
マネージド インスタンスのコア数の制限 (整数)。
#### `--cores-request -cr`
マネージド インスタンスのコア数の要求 (整数)。
#### `--memory-limit -ml`
マネージド インスタンスの容量の制限 (整数)。
#### `--memory-request -mr`
メモリの GB 量を示す整数としての、マネージド インスタンスの容量に対する要求。
#### `--storage-class-data -scd`
データ (.mdf) に使用するストレージ クラス。 値を指定しないと、ストレージ クラスは指定されず、その結果、Kubernetes によって既定のストレージ クラスが使用されます。
#### `--storage-class-logs -scl`
ログ (/var/log) に使用するストレージ クラス。 値を指定しないと、ストレージ クラスは指定されず、その結果、Kubernetes によって既定のストレージ クラスが使用されます。
#### `--storage-class-data-logs -scdl`
データベース ログ (.ldf) に使用するストレージ クラス。 値を指定しないと、ストレージ クラスは指定されず、その結果、Kubernetes によって既定のストレージ クラスが使用されます。
#### `--storage-class-backups -scb`
バックアップ (/var/opt/mssql/backups) に使用するストレージ クラス。 値を指定しないと、ストレージ クラスは指定されず、その結果、Kubernetes によって既定のストレージ クラスが使用されます。
#### `--volume-size-data -vsd`
データに使用するストレージ ボリュームのサイズを示す正の数値と、その後の Ki (キロバイト)、Mi (メガバイト)、または Gi (ギガバイト)。
#### `--volume-size-logs -vsl`
ログに使用するストレージ ボリュームのサイズを示す正の数値と、その後の Ki (キロバイト)、Mi (メガバイト)、または Gi (ギガバイト)。
#### `--volume-size-data-logs -vsdl`
データ ログに使用するストレージ ボリュームのサイズを示す正の数値と、その後の Ki (キロバイト)、Mi (メガバイト)、または Gi (ギガバイト)。
#### `--volume-size-backups -vsb`
バックアップに使用するストレージ ボリュームのサイズを示す正の数値と、その後の Ki (キロバイト)、Mi (メガバイト)、または Gi (ギガバイト)。
#### `--no-external-endpoint`
指定した場合、外部サービスは作成されません。 それ以外の場合、データ コントローラーと同じサービスの種類を使用して外部サービスが作成されます。
#### `--dev`
これを指定した場合、それは dev インスタンスと見なされ、課金されません。
#### `--no-wait`
指定した場合、コマンドは戻る前に、インスタンスが準備完了状態になるのを待機しません。
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
## <a name="azdata-arc-sql-mi-edit"></a>azdata arc sql mi edit
SQL マネージド インスタンスの構成を編集します。
```bash
azdata arc sql mi edit --name -n 
                       [--path]  
                       
[--cores-limit -cl]  
                       
[--cores-request -cr]  
                       
[--memory-limit -ml]  
                       
[--memory-request -mr]  
                       
[--dev]  
                       
[--no-wait]
```
### <a name="examples"></a>使用例
SQL マネージド インスタンスの構成を編集します。
```bash
azdata arc sql mi edit --path ./spec.json -n sqlmi1
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--name -n`
編集されている SQL マネージド インスタンスの名前。 インスタンスを配置するときに使用した名前を変更することはできません。
### <a name="optional-parameters"></a>省略可能のパラメーター
#### `--path`
SQL マネージド インスタンスの json ファイルに対する src ファイルへのパス。
#### `--cores-limit -cl`
マネージド インスタンスのコア数の制限 (整数)。
#### `--cores-request -cr`
マネージド インスタンスのコア数の要求 (整数)。
#### `--memory-limit -ml`
マネージド インスタンスの容量の制限 (整数)。
#### `--memory-request -mr`
メモリの GB 量を示す整数としての、マネージド インスタンスの容量に対する要求。
#### `--dev`
これを指定した場合、それは dev インスタンスと見なされ、課金されません。
#### `--no-wait`
指定した場合、コマンドは戻る前に、インスタンスが準備完了状態になるのを待機しません。
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
## <a name="azdata-arc-sql-mi-delete"></a>azdata arc sql mi delete
SQL マネージド インスタンスを削除します。
```bash
azdata arc sql mi delete --name -n 
                         
```
### <a name="examples"></a>使用例
SQL マネージド インスタンスを削除します。
```bash
azdata arc sql mi delete -n sqlmi1
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--name -n`
削除する SQL マネージド インスタンスの名前。
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
## <a name="azdata-arc-sql-mi-show"></a>azdata arc sql mi show
SQL マネージド インスタンスの詳細を表示します。
```bash
azdata arc sql mi show --name -n 
                       [--path -p]
```
### <a name="examples"></a>使用例
SQL マネージド インスタンスの詳細を表示します。
```bash
azdata arc sql mi show -n sqlmi1
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--name -n`
表示する SQL マネージド インスタンスの名前。
### <a name="optional-parameters"></a>省略可能のパラメーター
#### `--path -p`
SQL マネージド インスタンスの完全な仕様が書き込まれるパス。 省略した場合、仕様は標準出力に書き込まれます。
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
## <a name="azdata-arc-sql-mi-list"></a>azdata arc sql mi list
SQL マネージド インスタンスの一覧を表示します。
```bash
azdata arc sql mi list 
```
### <a name="examples"></a>使用例
SQL マネージド インスタンスの一覧を表示します。
```bash
azdata arc sql mi list
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

