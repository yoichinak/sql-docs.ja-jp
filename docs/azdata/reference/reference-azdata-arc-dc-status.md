---
title: azdata arc dc status リファレンス
titleSuffix: SQL Server big data clusters
description: azdata arc dc status コマンドのリファレンス記事です。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 817571e809ab9ea4133a2f1933c3b23d99d9b1bc
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358790"
---
# <a name="azdata-arc-dc-status"></a>azdata arc dc status

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] への適用

以下の記事では、**azdata** ツールの **sql** コマンドに関するリファレンスを提供します。 他の **azdata** コマンドの詳細については、[azdata リファレンス](reference-azdata.md)に関するページを参照してください。

## <a name="commands"></a>コマンド

|command|説明|
| --- | --- |
[azdata arc dc status show](#azdata-arc-dc-status-show) | データ コントローラーの状態を表示します。
## <a name="azdata-arc-dc-status-show"></a>azdata arc dc status show
データ コントローラーの状態を表示します。
```bash
azdata arc dc status show [--namespace -ns] 
                          
```
### <a name="examples"></a>使用例
特定の名前空間のデータ コントローラーの状態を表示します。
```bash
azdata arc dc status show --namespace <ns>
```
### <a name="optional-parameters"></a>省略可能のパラメーター
#### `--namespace -ns`
データ コントローラーが存在している Kubernetes 名前空間。
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

