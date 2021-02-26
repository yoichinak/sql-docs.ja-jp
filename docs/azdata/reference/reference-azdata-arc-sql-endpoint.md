---
title: azdata arc sql endpoint リファレンス
titleSuffix: SQL Server big data clusters
description: azdata arc sql endpoint コマンドに関するリファレンス記事です。
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 190bc4360d8f8cd35f0ceda04887a1fc912243e3
ms.sourcegitcommit: 8dc7e0ececf15f3438c05ef2c9daccaac1bbff78
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/13/2021
ms.locfileid: "100342528"
---
# <a name="azdata-arc-sql-endpoint"></a>azdata arc sql endpoint

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] への適用

以下の記事では、**azdata** ツールの **sql** コマンドに関するリファレンスを提供します。 他の **azdata** コマンドの詳細については、[azdata リファレンス](reference-azdata.md)に関するページを参照してください。

## <a name="commands"></a>コマンド
|コマンド|説明|
| --- | --- |
[azdata arc sql endpoint list](#azdata-arc-sql-endpoint-list) | SQL エンドポイントを一覧表示します。
## <a name="azdata-arc-sql-endpoint-list"></a>azdata arc sql endpoint list
SQL エンドポイントを一覧表示します。
```bash
azdata arc sql endpoint list [--name -n] 
                             
```
### <a name="examples"></a>例
SQL マネージド インスタンスのエンドポイントを一覧表示します。
```bash
azdata arc sql endpoint list -n sqlmi1
```
### <a name="optional-parameters"></a>省略可能のパラメーター
#### `--name -n`
表示する SQL インスタンスの名前。 省略した場合、すべてのインスタンスのすべてのエンドポイントが表示されます。
### <a name="global-arguments"></a>グローバル引数
#### `--debug`
すべてのデバッグ ログを表示するようにログの詳細レベルを上げます。
#### `--help -h`
このヘルプ メッセージを表示して終了します。
#### `--output -o`
出力形式。  使用できる値: json、jsonc、table、tsv。  既定値: json。
#### `--query -q`
JMESPath クエリ文字列。 詳細と例については、[http://jmespath.org/](http://jmespath.org/) を参照してください。
#### `--verbose`
ログの詳細レベルを上げます。 詳細なデバッグ ログを表示するには --debug を使います。

## <a name="next-steps"></a>次のステップ

他の **azdata** コマンドの詳細については、[azdata リファレンス](reference-azdata.md)に関するページを参照してください。 

**azdata** ツールをインストールする方法の詳細については、「[azdata のインストール](..\install\deploy-install-azdata.md)」を参照してください。
