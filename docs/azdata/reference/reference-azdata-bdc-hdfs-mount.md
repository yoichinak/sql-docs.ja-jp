---
title: azdata bdc hdfs mount リファレンス
titleSuffix: SQL Server big data clusters
description: azdata bdc hdfs mount コマンドのリファレンス記事です。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b989a1cfcc1808c8a49da0e66e56897910a84286
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358550"
---
# <a name="azdata-bdc-hdfs-mount"></a>azdata bdc hdfs mount

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] への適用

以下の記事では、**azdata** ツールの **sql** コマンドに関するリファレンスを提供します。 他の **azdata** コマンドの詳細については、[azdata リファレンス](reference-azdata.md)に関するページを参照してください。

## <a name="commands"></a>コマンド

|command|説明|
| --- | --- |
[azdata bdc hdfs mount create](#azdata-bdc-hdfs-mount-create) | HDFS 内にリモート ストアのマウントを作成します。
[azdata bdc hdfs mount delete](#azdata-bdc-hdfs-mount-delete) | HDFS 内のリモート ストアのマウントを削除します。
[azdata bdc hdfs mount status](#azdata-bdc-hdfs-mount-status) | マウントの状態。
[azdata bdc hdfs mount refresh](#azdata-bdc-hdfs-mount-refresh) | HDFS 内のマウントの内容を更新します。
## <a name="azdata-bdc-hdfs-mount-create"></a>azdata bdc hdfs mount create
HDFS 内にリモート ストアのマウントを作成します。 リモート ストアにアクセスするための資格情報が存在する場合、それは環境変数 MOUNT_CREDENTIALS を使って、キーと値のペアのコンマ区切りリストとして指定する必要があります。 キーや値に含まれているコンマは、すべてエスケープする必要があります。
```bash
azdata bdc hdfs mount create --remote-uri -r 
                             --mount-path -m
```
### <a name="examples"></a>例
ADLS Gen 2 アカウント "adlsv2example" のコンテナー "data" を、HDFS パス /mounts/adlsv2/data に、共有キーを使ってマウントする場合
```bash
Set the MOUNT_CREDENTIALS environment variable as "fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>".
azdata bdc hdfs mount create --remote-uri abfs://data@adlsv2example.dfs.core.windows.net/
    --mount-path /mounts/adlsv2/data
```
リモートの HDFS BDC (hdfs://namenode1:8080/) を、ローカルの HDFS パス /mounts/hdfs/ にマウントする場合
```bash
azdata bdc hdfs mount create --remote-uri hdfs://namenode1:8080/ --mount-path /mounts/hdfs/
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--remote-uri -r`
マウントされるリモート ストアの URI (マウントのソース)。
#### `--mount-path -m`
マウントを作成する HDFS パス (マウント先)。
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
## <a name="azdata-bdc-hdfs-mount-delete"></a>azdata bdc hdfs mount delete
HDFS 内のリモート ストアのマウントを削除します。
```bash
azdata bdc hdfs mount delete --mount-path -m 
                             
```
### <a name="examples"></a>例
/mounts/adlsv2/data に作成された ADLS Gen 2 ストレージ アカウント用のマウントを削除します。
```bash
azdata bdc hdfs mount delete --mount-path /mounts/adlsv2/data
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--mount-path -m`
削除する必要があるマウントに対応する HDFS パス。
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
## <a name="azdata-bdc-hdfs-mount-status"></a>azdata bdc hdfs mount status
マウントの状態。
```bash
azdata bdc hdfs mount status [--mount-path -m] 
                             
```
### <a name="examples"></a>例
パスによってマウントの状態を取得します
```bash
azdata bdc hdfs mount status --mount-path /mounts/hdfs
```
すべてのマウントの状態を取得します。
```bash
azdata bdc hdfs mount status
```
### <a name="optional-parameters"></a>省略可能なパラメーター
#### `--mount-path -m`
マウントのパス。
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
## <a name="azdata-bdc-hdfs-mount-refresh"></a>azdata bdc hdfs mount refresh
HDFS 内のマウントの内容を更新します。
```bash
azdata bdc hdfs mount refresh --mount-path -m 
                              
```
### <a name="examples"></a>例
/mounts/adlsv2/data に作成されたマウントを更新します。
```bash
azdata bdc hdfs mount refresh --mount-path /mounts/adlsv2/data
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--mount-path -m`
更新する必要があるマウントに対応する HDFS パス。
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

