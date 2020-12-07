---
title: azdata arc dc endpoint リファレンス
titleSuffix: SQL Server big data clusters
description: azdata arc dc endpoint コマンドのリファレンス記事です。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ea53bb8faef2534034a41422a83af1f16b81a5bf
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358810"
---
# <a name="azdata-arc-dc-endpoint"></a>azdata arc dc endpoint

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] への適用

以下の記事では、**azdata** ツールの **sql** コマンドに関するリファレンスを提供します。 他の **azdata** コマンドの詳細については、[azdata リファレンス](reference-azdata.md)に関するページを参照してください。

## <a name="commands"></a>コマンド

|command|説明|
| --- | --- |
[azdata arc dc endpoint list](#azdata-arc-dc-endpoint-list) | データ コントローラーのエンドポイントを一覧表示します。
## <a name="azdata-arc-dc-endpoint-list"></a>azdata arc dc endpoint list
データ コントローラーのエンドポイントを一覧表示します。
```bash
azdata arc dc endpoint list [--endpoint-name -e] 
                            
```
### <a name="examples"></a>使用例
特定の名前空間のデータ コントローラーのエンドポイントを一覧表示します。
```bash
azdata arc dc endpoint list --namespace <ns>
```
### <a name="optional-parameters"></a>省略可能のパラメーター
#### `--endpoint-name -e`
Arc データ コントローラーのエンドポイント名。
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

