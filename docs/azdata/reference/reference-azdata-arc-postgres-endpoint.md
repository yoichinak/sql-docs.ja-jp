---
title: azdata arc postgres endpoint リファレンス
titleSuffix: SQL Server big data clusters
description: azdata arc postgres endpoint コマンドのリファレンス記事です。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 097bfb40f8636f66f142fc785c4699dce2084440
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358760"
---
# <a name="azdata-arc-postgres-endpoint"></a>azdata arc postgres endpoint

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] への適用

以下の記事では、**azdata** ツールの **sql** コマンドに関するリファレンスを提供します。 他の **azdata** コマンドの詳細については、[azdata リファレンス](reference-azdata.md)に関するページを参照してください。

## <a name="commands"></a>コマンド

|command|説明|
| --- | --- |
[azdata arc postgres endpoint list](#azdata-arc-postgres-endpoint-list) | PostgreSQL サーバー グループのエンドポイントを一覧表示します。
## <a name="azdata-arc-postgres-endpoint-list"></a>azdata arc postgres endpoint list
PostgreSQL サーバー グループのエンドポイントを一覧表示します。
```bash
azdata arc postgres endpoint list --name -n 
                                  [--engine-version -ev]
```
### <a name="examples"></a>使用例
PostgreSQL サーバー グループのエンドポイントを一覧表示します。
```bash
azdata arc postgres endpoint list -n postgres01
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

## <a name="next-steps"></a>次のステップ

他の **azdata** コマンドの詳細については、[azdata リファレンス](reference-azdata.md)に関するページを参照してください。 

**azdata** ツールをインストールする方法の詳細については、「[azdata のインストール](..\install\deploy-install-azdata.md)」を参照してください。

