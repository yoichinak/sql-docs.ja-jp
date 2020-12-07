---
title: azdata arc dc リファレンス
titleSuffix: SQL Server big data clusters
description: azdata arc dc コマンドのリファレンス記事です。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6f4f9c414221bc6eab400416d6ea09e692031aa5
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358780"
---
# <a name="azdata-arc-dc"></a>azdata arc dc

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] への適用

以下の記事では、**azdata** ツールの **sql** コマンドに関するリファレンスを提供します。 他の **azdata** コマンドの詳細については、[azdata リファレンス](reference-azdata.md)に関するページを参照してください。

## <a name="commands"></a>コマンド

|command|説明|
| --- | --- |
[azdata arc dc create](#azdata-arc-dc-create) | データ コントローラーを作成します。
[azdata arc dc delete](#azdata-arc-dc-delete) | データ コントローラーを削除します。
[azdata arc dc endpoint](reference-azdata-arc-dc-endpoint.md) | エンドポイント コマンド。
[azdata arc dc status](reference-azdata-arc-dc-status.md) | 状態コマンド。
[azdata arc dc config](reference-azdata-arc-dc-config.md) | 構成コマンド。
[azdata arc dc debug](reference-azdata-arc-dc-debug.md) | デバッグ コマンド。
[azdata arc dc export](#azdata-arc-dc-export) | メトリック、ログ、使用状況をエクスポートします。
[azdata arc dc upload](#azdata-arc-dc-upload) | エクスポートされたデータ ファイルをアップロードします。
## <a name="azdata-arc-dc-create"></a>azdata arc dc create
データ コントローラーを作成します。システムに Kube 構成と環境変数 ['AZDATA_USERNAME', 'AZDATA_PASSWORD'] が必要です。
```bash
azdata arc dc create --namespace -ns 
                     --name -n  
                     
--connectivity-mode  
                     
--resource-group -g  
                     
--location -l  
                     
--subscription -s  
                     
[--profile-name]  
                     
[--path -p]  
                     
[--storage-class -sc]
```
### <a name="examples"></a>使用例
データ コントローラーの配置。
```bash
azdata arc dc create
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--namespace -ns`
データ コントローラーを配置する Kubernetes 名前空間。 既に存在する場合は、それが使用されます。 存在しない場合は、最初に作成が試みられます。
#### `--name -n`
データ コントローラーの名前。
#### `--connectivity-mode`
データ コントローラーが動作する Azure への間接的または直接的な接続。
#### `--resource-group -g`
データ コントローラー リソースを追加する Azure リソース グループ。
#### `--location -l`
データ コントローラーのメタデータを格納する Azure の場所 (例: eastus)。
#### `--subscription -s`
データ コントローラー リソースを追加する Azure サブスクリプション ID。
### <a name="optional-parameters"></a>省略可能のパラメーター
#### `--profile-name`
既存の構成プロファイルの名前。 使用できるオプションを表示するには、`azdata arc dc config list` を実行します。 次のいずれかです: ["azure-arc-aks-premium-storage"、"azure-arc-ake"、"azure-arc-openshift"、"azure-arc-gke"、"azure-arc-aks-default-storage"、"azure-arc-kubeadm"、"azure-arc-eks"、"azure-arc-azure-openshift"、"azure-arc-aks-hci"]。
#### `--path -p`
使用するカスタム構成プロファイルが格納されているディレクトリへのパス。 カスタム構成プロファイルを作成するには、`azdata arc dc config init` を実行します。
#### `--storage-class -sc`
データとログの永続ボリュームを必要とするすべてのデータ コントローラー ポッドに対するすべてのそのボリュームに使用するストレージ クラス。
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
## <a name="azdata-arc-dc-delete"></a>azdata arc dc delete
データ コントローラーを削除します。Kube 構成がシステムに必要です。
```bash
azdata arc dc delete --name -n 
                     --namespace -ns  
                     
[--force -f]
```
### <a name="examples"></a>使用例
データ コントローラーの配置。
```bash
azdata arc dc delete
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--name -n`
データ コントローラー名。
#### `--namespace -ns`
データ コントローラーが存在している Kubernetes 名前空間。
### <a name="optional-parameters"></a>省略可能のパラメーター
#### `--force -f`
データ コントローラーを強制的に削除します。
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
## <a name="azdata-arc-dc-export"></a>azdata arc dc export
メトリック、ログ、または使用状況をファイルにエクスポートします。
```bash
azdata arc dc export --type -t 
                     --path -p  
                     
[--force -f]
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--type -t`
エクスポートするデータの種類。 オプション: logs、metrics、usage。
#### `--path -p`
エクスポート対象のファイルのファイル名を含む完全パスまたは相対パス。
### <a name="optional-parameters"></a>省略可能のパラメーター
#### `--force -f`
出力ファイルを強制的に作成します。 同じパスにある既存のファイルを上書きします。
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
## <a name="azdata-arc-dc-upload"></a>azdata arc dc upload
データ コントローラーからエクスポートされたデータ ファイルを Azure にアップロードします。
```bash
azdata arc dc upload --path -p 
                     
```
### <a name="required-parameters"></a>必須のパラメーター
#### `--path -p`
アップロード対象のファイルのファイル名を含む完全パスまたは相対パス。
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

