---
description: MSSQLSERVER_3023
title: MSSQLSERVER_3023
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3023 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 0197c7e5b75164615572e4041a5b348a4d5abcc4
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418797"
---
# <a name="mssqlserver_3023"></a>MSSQLSERVER_3023
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>詳細

|属性|値|
|---|---|
|製品名|SQL Server|
|イベント ID|3023|
|イベント ソース|MSSQLSERVER|
|コンポーネント|SQLEngine|
|シンボル名|DB_IN_USE_DUMP|
|メッセージ テキスト|データベースに対するバックアップ操作およびファイル操作 (ALTER DATABASE ADD FILE など) は、シリアル化する必要があります。 現在のバックアップ、またはファイル操作が完了してからステートメントを再実行してください|
||

## <a name="explanation"></a>説明

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でデータベースのバックアップ、圧縮、または変更のコマンドを実行しようとすると、次のメッセージが表示されます。

> メッセージ 3023、レベル 16、状態 2、行 1  
データベースに対するバックアップ操作およびファイル操作 (ALTER DATABASE ADD FILE など) は、シリアル化する必要があります。 現在のバックアップ、またはファイル操作が完了してからステートメントを再実行してください。

> メッセージ 3013、レベル 16、状態 1、行 1  
バックアップ データベースが異常終了しています。

さらに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエラー ログには、次のようなメッセージが含まれています。

> \<Datetime> バックアップ エラー:3041、重大度:16、状態: 1.  
\<Datetime> バックアップ BACKUP で、コマンド BACKUP DATABASE MyDatabase WITH DIFFERENTIAL を完了できませんでした。 詳細メッセージについては、バックアップ アプリケーション ログを確認してください。

これらのコマンドの状態が、`sys.dm_exec_requests` や `sys.dm_os_waiting_tasks` などのさまざまな動的管理ビュー (DMV) から表示されると、これらのコマンドで `wait_type = LCK_M_U` と `wait_resource = DATABASE: <id> [BULKOP_BACKUP_DB]` が発生することにもご注意ください。

## <a name="possible-causes"></a>考えられる原因

データベースに対してデータベースの完全バックアップが現在実行されている場合に、許可するまたは許可しない操作について、いくつかの規則があります。 いくつかの例を次に示します。

- データ バックアップは、一度に 1 つしか実行できません (データベースの完全バックアップが実行されているときに、差分または増分のバックアップを同時に行うことはできません)。
- ログ バックアップは、一度に 1 つしか実行できません (データベースの完全バックアップが実行されている場合にログ バックアップを実行することはできます)。
- バックアップの実行中に、データベースに対してファイルの追加や削除を行うことはできません。
- データベースのバックアップ中にファイルを圧縮することはできません。
- バックアップの実行中に許可される復旧モデルの変更は限られています。

これらの競合する操作のいずれかが実行されると、「説明」セクションに記載されているロック待機がコマンドで発生し、その後、3023 および 3041 メッセージを受信します。

## <a name="user-action"></a>ユーザー アクション

さまざまなデータベース メンテナンス作業のスケジュールを確認し、これらの操作またはコマンドが互いに競合しないようにスケジュールを調整します。

## <a name="more-information"></a>詳細情報

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって、バックアップの開始時刻と終了時刻が `msdb` データベースに記録されます。 バックアップ履歴を調べると、増分バックアップの実行中にデータベースの完全バックアップが発生したためにエラーが発生したかどうかを判断できます。 このプロセスを実行するには、次のクエリを使用します。

```sql
select database_name, type, backup_start_date, backup_finish_date
from msdb.dbo.backupset
order by database_name, type, backup_start_date, backup_finish_date
go
```

また、SQL Profiler トレースの **User Error Message** イベントや、拡張イベントの **error_reported** イベントを使用して、バックアップまたはその他のメンテナンス コマンドを開始したアプリケーションに戻り、3023 メッセージのレポートを追跡することもできます。
