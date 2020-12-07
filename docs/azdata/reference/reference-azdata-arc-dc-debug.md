---
title: azdata arc dc debug リファレンス
titleSuffix: SQL Server big data clusters
description: azdata arc dc debug コマンドのリファレンス記事です。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bfb4c13f262609328bf73dca282f9d3445a8bf8c
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358800"
---
# <a name="azdata-arc-dc-debug"></a>azdata arc dc debug

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] への適用

以下の記事では、**azdata** ツールの **sql** コマンドに関するリファレンスを提供します。 他の **azdata** コマンドの詳細については、[azdata リファレンス](reference-azdata.md)に関するページを参照してください。

## <a name="commands"></a>コマンド

|command|説明|
| --- | --- |
[azdata arc dc debug copy-logs](#azdata-arc-dc-debug-copy-logs) | ログをコピーします。
[azdata arc dc debug dump](#azdata-arc-dc-debug-dump) | メモリ ダンプをトリガーします。
## <a name="azdata-arc-dc-debug-copy-logs"></a>azdata arc dc debug copy-logs
データ コントローラーからデバッグ ログをコピーします。お使いのシステムには、Kubernetes を構成する必要があります。
```bash
azdata arc dc debug copy-logs --namespace -ns 
                              [--container -c]  
                              
[--target-folder -d]  
                              
[--pod]  
                              
[--resource-kind -rk]  
                              
[--resource-name -rn]  
                              
[--timeout -t]  
                              
[--skip-compress -sc]  
                              
[--exclude-dumps -ed]
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--namespace -ns`
データ コントローラーの Kubernetes 名前空間。
### <a name="optional-parameters"></a>省略可能なパラメーター
#### `--container -c`
類似した名前のコンテナーのログをコピーします (省略可能)。既定では、すべてのコンテナーのログがコピーされます。 複数回指定することはできません。 複数回指定した場合は、最後のものが使用されます
#### `--target-folder -d`
ログのコピー先となるターゲット フォルダーのパス。 省略可能。既定では、ローカル フォルダー内に結果が作成されます。  複数回指定することはできません。 複数回指定した場合は、最後のものが使用されます
#### `--pod`
類似した名前のポッドのログをコピーします。 省略可能。既定では、すべてのポッドのログがコピーされます。 複数回指定することはできません。 複数回指定した場合は、最後のものが使用されます
#### `--resource-kind -rk`
特定の種類のリソースのログをコピーします。 複数回指定することはできません。 複数回指定した場合は、最後のものが使用されます。 指定する場合は、リソースを識別する --resource-name も指定する必要があります。
#### `--resource-name -rn`
指定した名前のリソースのログをコピーします。 複数回指定することはできません。 複数回指定した場合は、最後のものが使用されます。 指定する場合は、リソースを識別する --resource-kind も指定する必要があります。
#### `--timeout -t`
コマンドが完了するまで待機する秒数。 既定値は 0 (無制限) です
#### `--skip-compress -sc`
結果フォルダーの圧縮をスキップするかどうかを指定します。 既定値は False で、結果フォルダーを圧縮します。
#### `--exclude-dumps -ed`
結果フォルダーからダンプを除外するかどうかを指定します。 既定値は False で、ダンプを含めます。
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
## <a name="azdata-arc-dc-debug-dump"></a>azdata arc dc debug dump
メモリ ダンプをトリガーし、それをコンテナーからコピーします。システム上に Kubernetes の構成が必要です。
```bash
azdata arc dc debug dump --namespace -ns 
                         [--container -c]  
                         
[--target-folder -d]
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--namespace -ns`
データ コントローラーの Kubernetes 名前空間。
### <a name="optional-parameters"></a>省略可能のパラメーター
#### `--container -c`
実行中のプロセスをダンプするためにトリガーされるターゲット コンテナー。
`controller`
#### `--target-folder -d`
ダンプをコピーするターゲット フォルダー。`./output/dump`
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

