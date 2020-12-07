---
title: azdata arc postgres server backup リファレンス
titleSuffix: SQL Server big data clusters
description: azdata arc postgres server backup コマンドのリファレンス記事です。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 44a3811ab3412a7631a0a0bf95aecc85150206b0
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358750"
---
# <a name="azdata-arc-postgres-server-backup"></a>azdata arc postgres server backup

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] への適用

以下の記事では、**azdata** ツールの **sql** コマンドに関するリファレンスを提供します。 他の **azdata** コマンドの詳細については、[azdata リファレンス](reference-azdata.md)に関するページを参照してください。

## <a name="commands"></a>コマンド

|command|説明|
| --- | --- |
[azdata arc postgres server backup create](#azdata-arc-postgres-server-backup-create) | PostgreSQL サーバー グループのバックアップを作成します。
[azdata arc postgres server backup delete](#azdata-arc-postgres-server-backup-delete) | PostgreSQL サーバー グループのバックアップを削除します。
[azdata arc postgres server backup restore](#azdata-arc-postgres-server-backup-restore) | PostgreSQL サーバー グループのバックアップを復元します。
[azdata arc postgres server backup restorestatus](#azdata-arc-postgres-server-backup-restorestatus) | 存在する場合、最新の復元操作の状態を取得します。
[azdata arc postgres server backup show](#azdata-arc-postgres-server-backup-show) | PostgreSQL サーバー グループのバックアップの詳細を表示します。
## <a name="azdata-arc-postgres-server-backup-create"></a>azdata arc postgres server backup create
PostgreSQL サーバー グループのバックアップを作成します。
```bash
azdata arc postgres server backup create 
```
### <a name="examples"></a>使用例
サービス 'pg' のバックアップを作成します。
```bash
azdata arc postgres server backup create -sn pg
```
サービス 'pg' の名前付きバックアップを作成します。
```bash
azdata arc postgres server backup create -sn pg -n backup1
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
## <a name="azdata-arc-postgres-server-backup-delete"></a>azdata arc postgres server backup delete
PostgreSQL サーバー グループのバックアップを削除します。
```bash
azdata arc postgres server backup delete 
```
### <a name="examples"></a>使用例
PostgreSQL サーバー グループのバックアップを削除します。
```bash
azdata arc postgres backup delete -sn pg -id e07dd3940e374bd9acbc86869cbc123d
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
## <a name="azdata-arc-postgres-server-backup-restore"></a>azdata arc postgres server backup restore
PostgreSQL サーバー グループのバックアップを復元します。
```bash
azdata arc postgres server backup restore 
```
### <a name="examples"></a>使用例
最新のバックアップを復元します。
```bash
azdata arc postgres server restore -sn pg```
Restore a backup by ID
```bash
azdata arc postgres server restore -sn pg -id 123e4567e89b12d3a456426655440000
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
## <a name="azdata-arc-postgres-server-backup-restorestatus"></a>azdata arc postgres server backup restorestatus
存在する場合、最新の復元操作の状態を取得します。
```bash
azdata arc postgres server backup restorestatus 
```
### <a name="examples"></a>使用例
ID でサービス 'pg' の最新の復元状態を取得します。
```bash
azdata arc postgres server backup restorestatus -sn pg -id 123e4567e89b12d3a456426655440000
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
## <a name="azdata-arc-postgres-server-backup-show"></a>azdata arc postgres server backup show
PostgreSQL サーバー グループのバックアップの詳細を表示します。
```bash
azdata arc postgres server backup show 
```
### <a name="examples"></a>使用例
ID でサービス 'pg' のバックアップを取得します。
```bash
azdata arc postgres server backup show -sn pg -id 123e4567e89b12d3a456426655440000
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

