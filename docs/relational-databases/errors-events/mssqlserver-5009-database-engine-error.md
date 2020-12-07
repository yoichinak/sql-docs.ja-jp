---
description: MSSQLSERVER_5009
title: MSSQLSERVER_5009
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5009 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 1ca7fb52969d9ec08d8c80c48ec1325277a13fa7
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418832"
---
# <a name="mssqlserver_5009"></a>MSSQLSERVER_5009
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>詳細

|属性|値|
|---|---|
|製品名|SQL Server|
|イベント ID|5009|
|イベント ソース|MSSQLSERVER|
|コンポーネント|SQLEngine|
|シンボル名|ALT_BADDISKS|
|メッセージ テキスト|ステートメントに一覧されている 1 つ以上のファイルが見つからなかったか、初期化できませんでした|
||

## <a name="explanation"></a>説明

このエラーは、解決できなかった ALTER DATABASE または DBCC SHRINK* コマンドでファイル名または fileID を指定したことを示します。

次のシナリオを想定してください。

- 完全または一括ログ復旧モデルを使用する Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースがある。
- *db_file1* という名前の新しいデータ ファイルをデータベースに追加する。
- `db_file1` ファイルのファイルの種類をデータとして設定する。
- ファイルの種類を正しく指定しなかったことに気付く。
- `db_file1` ファイルを削除してから、このデータベースのトランザクション ログをバックアップする。
- 同じデータベースに *db_file1* という名前の新しいログ ファイルを追加する。
- ALTER DATABASE ステートメントまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio を使用して、 *db_file1* という名前のログ ファイルを削除しようとする。

このシナリオの場合、次のようなエラー メッセージが表示されます。

> メッセージ 5009、レベル 16、状態 9、行 1 ステートメントに一覧されている 1 つ以上のファイルが見つからなかったか、初期化できませんでした。

## <a name="possible-causes"></a>考えられる原因

この問題は、削除しようとしたファイルの論理名がシステム カタログ テーブル内で一意でない場合に発生します。 たとえば、この問題は、以前にデータベースにファイルが存在していて、その後、そのファイルが削除された場合に発生します。

同じ論理名を持つファイルを削除しようとすると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって、ドロップされた論理ファイルの削除が試みられます。 この結果、エラー メッセージが表示されます。

## <a name="user-action"></a>ユーザー アクション

この問題を回避するには、次の手順を実行します。

> [!NOTE]
> これらの手順を行うと、ファイル ID の値が再利用されます。

1. ALTER DATABASE ステートメントを使用して、名前が異なり、データ型が同じである新しい論理ファイルを作成します。 たとえば、次の例のように、論理ファイルに `db_file1` ではなく、`different_remove_file_name` という名前を付けます。

    ```sql
    ALTER DATABASE [DBNAME] ADD FILE ( NAME = N'different_remove_file_name',
    FILENAME = N'D:\MSSQL.1\MSSQL\DATA\db_file1.ndf', SIZE = 1MB, MAXSIZE = 1MB)
    ```

    > [!NOTE]
    > 任意のファイル名または任意のファイル パスを使用できます。

1. 次の例のように、ALTER DATABASE ステートメントを使用して、手順 1 で作成した論理ファイルを削除します。

    ```sql
    ALTER DATABASE [DBNAME] REMOVE FILE [different_remove_file_name]
    ```

1. データベースのトランザクション ログ バックアップを作成します。
1. もう一度 *db_file1* という名前の論理ファイルを削除してみてください。
