---
description: MSSQLSERVER_3414
title: MSSQLSERVER_3414 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3414 (Database Engine error)
ms.assetid: f25852f9-b91c-4356-b817-78bec9ec8db4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a7a7d69c27ed422763c5c697f003ba9fb4c82286
ms.sourcegitcommit: a0245fdae1ff9045f587a3a67b72f34405d35a4f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/19/2020
ms.locfileid: "88618090"
---
# <a name="mssqlserver_3414"></a>MSSQLSERVER_3414
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|3414|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|REC_GIVEUP|  
|メッセージ テキスト|復元中にエラーが発生したので、データベース '%.*ls' (データベース ID %d) は再開されません。 復元エラーを診断して修正するか、既知の適切なバックアップから復元してください。 エラーが修正されない場合は、ご購入元に問い合わせてください。|  
  
## <a name="explanation"></a>説明  
示されているデータベースは復旧されましたが、復旧中にエラーが発生したために起動できませんでした。 このエラーによって、データベースは SUSPECT 状態になっています。 プライマリ ファイル グループ、また場合によってはその他のファイル グループには、問題があり、損傷している可能性があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の起動中はデータベースを復旧できないため、データベースを使用できません。 問題を解決するには、ユーザーによる操作が必要です。 SUSPECT 状態は、(データベースのアイコンの横にある) SQL Server Management Studio 内と、sys.databases.state_desc 列を確認したときの両方で、表示されます。 この状態のデータベースを使用しようとすると、次のエラーが発生します。

```
Msg 926, Level 14, State 1, Line 1 
Database 'mydb' cannot be opened. It has been marked SUSPECT by recovery. See the SQL Server errorlog for more information
```
  
このエラーが **tempdb** で発生した場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスはシャットダウンされます。  

## <a name="cause"></a>原因
このエラーは、サーバー インスタンスの起動またはデータベースの復旧を試行したときのシステム上の一時的な状態が原因である可能性があります。 また、データベースを起動しようとするたびに発生する永続的なエラーが原因である可能性もあります。 通常、復旧の失敗の原因は、ERRORLOG またはイベン トログ内のエラー 3414 より前にあるエラーにあります。 ログ ファイル内で前にあるエラーには、同じ spid<n> 値が含まれています。 たとえば、次の復旧の失敗は、ログ ブロックを読み取ろうとしたときのチェックサム エラーが原因です。 すべての行に *spid15s* が存在することに注意してください。

```
2020-03-31 17:33:13.00 spid15s     Error: 824, Severity: 24, State: 4.  
2020-03-31 17:33:13.00 spid15s     SQL Server detected a logical consistency-based I/O error: (bad checksum). It occurred during a read of page (0:-1) in database ID 13 at offset 0x0000000000b800 in file 'C:\Program Files\Microsoft SQL Server\MSSQL10.SQL2008\MSSQL\DATA\mydb_log.LDF'.  Additional messages in the SQL Server error log or system event log may provide more detail. This is a severe error condition that threatens database integrity and must be corrected immediately. Complete a full database consistency check (DBCC CHECKDB). This error can be caused by many factors; for more information, see SQL Server Books Online.   
2020-03-31 17:33:13.16 spid15s     Error: 3414, Severity: 21, State: 1.  
2020-03-31 17:33:13.16 spid15s     An error occurred during recovery, preventing the database 'mydb' (database ID 13) from restarting. Diagnose the recovery errors and fix them, or restore from a known good backup. If errors are not corrected or expected, contact Technical Support
```


データベースの復旧の失敗の原因となる可能性があるエラーには、さまざまなものがあります。 各エラーを個別に評価する必要はありますが、データベースの復旧の失敗の解決方法は通常、次の「ユーザーの操作」セクションで説明されているものと同じです。

## <a name="user-action"></a>ユーザー アクション  
 
このエラー 3414 の発生の原因については、Windows イベント ログまたは ERRORLOG をさかのぼって、具体的な問題点を示すエラーを調べてください。 ユーザーに求められる適切な対処は、Windows イベント ログが示している情報、つまり、その [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラーが一時的な状態によって引き起こされたのか、永続的なエラーが原因で引き起こされたのかによって異なります。 エラー メッセージには、"復元エラーを診断して修正するか、既知の適切なバックアップから復元してください。" と示されています。 したがって、復旧の完了を可能にするため、発生したエラーの修正を試みることができます (「[修正可能なエラーと遅延トランザクション](#correctable-errors-and-deferred-transactions)」を参照してください)。

エラーを修正できない場合、この問題を解決するための最初の最適なオプションは、適切なバックアップから復元することです。 ただし、バックアップから復旧できない場合は、2 つの追加オプションがあります。これは、完全なデータ復旧を保証するものではありません。[DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) を使用した緊急修復を行うか、またはできるだけ多くのデータを別のデータベースにコピーします。 

 1. 正常に機能することが確認されている最新のバックアップから復元する
 1. [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) で実行可能な緊急修復方法を使用する
 1. できるだけ多くのデータを別のデータベースにコピーする。

適切なデータベース バックアップから復元する最初の方法は、データベースを既知の一貫性のある状態にするための最も適した選択です。  

2 番目に適した選択は、使用可能なバックアップがない場合に、データベースをオンラインにしてアクセスできるようにすることです。 ただし、復旧が失敗しているため、トランザクションの整合性は保証されないことを理解する必要があります。 ロールバックまたはロールフォワードする必要があったにもかかわらず、復旧が失敗したためにできなかったトランザクションはどれであるのか、知る方法はありません。 緊急修復を行う手順については、DBCC CHECKDB ドキュメントの[緊急モードでのデータベース エラーの解決](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md#resolving-errors-in-database-emergency-mode)に関するセクションを参照してください。 

緊急修復が機能せず、いくつかのデータを別のデータベースに復旧したい場合、データベースへのアクセスを取得する方法は、ALTER DATABASE <dbname> SET EMERGENCY コマンドを使用してデータベースを緊急モードに設定することです。 その後、テーブルからデータをコピーすることができます。

### <a name="correctable-errors-and-deferred-transactions"></a>修正可能なエラーと遅延トランザクション
データベースの復旧中に発生したエラーのすべてが、復旧の失敗と問題のあるデータベースを引き起こすわけではありません。

データベースまたはトランザクション ログ ファイルを初めて開いたときのエラーは、復旧前に発生します。 そのようなエラーの例には、[17204](mssqlserver-17204-database-engine-error.md) と [17207](mssqlserver-17207-database-engine-error.md) があります。 これらのエラーが修正されると、復旧が続行される可能性はあります (ただし、他の復旧エラーが発生した場合は、完了することは保証されません)。 17204 や 17207 などのエラーは、SUSPECT データベースの原因にはなりません。 実際、これらの問題が発生したときのデータベースの状態は、RECOVERY_PENDING です。 

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、ページレベルのエラーが発生しても復旧を完了することができ、トランザクションの一貫性も維持されます。 このプロセスによって、SUSPECT データベースの原因となるシナリオ数が減少しました。 この概念は[遅延トランザクション](../backup-restore/deferred-transactions-sql-server.md)と呼ばれます。

復旧中に発生したエラーによってデータベース ページに問題があることが示された場合 (チェックサム エラーやメッセージ 824 など)、エラーが保留状態のまま復旧を完了できることがあります。 トランザクションがコミットされていない場合、ページのエラーによって[遅延トランザクション](../backup-restore/deferred-transactions-sql-server.md)が発生し、復旧は完了できます。  

次の ERRORLOG エントリは、復旧中にメッセージ [824](mssqlserver-824-database-engine-error.md) エラーが発生したけれども、遅延トランザクションによって復旧が完了できた、という例を示しています。 この状況ではエラー 3414 が発生していないことと、データベースの復旧が完了したことを示すメッセージに注目してください。

```2010-03-31 19:17:18.45 spid7s      Error: 824, Severity: 24, State: 2.   
2010-03-31 19:17:18.45 spid7s      SQL Server detected a logical consistency-based I/O error: incorrect checksum (expected: 0xb2c87a0a; actual: 0xb6c0a5e2). It occurred during a read of page (1:153) in database ID 13 at offset 0x00000000132000 in file 'C:\Program Files\Microsoft SQL Server\MSSQL10.SQL2008\MSSQL\DATA\mydb.mdf'.  Additional messages in the SQL Server error log or system event log may provide more detail. This is a severe error condition that threatens database integrity and must be corrected immediately. Complete a full database consistency check (DBCC CHECKDB). This error can be caused by many factors; for more information, see SQL Server Books Online.   
2010-03-31 19:17:18.45 spid7s      Error: 3314, Severity: 21, State: 1.   
2010-03-31 19:17:18.45 spid7s      During undoing of a logged operation in database 'mydb', an error occurred at log record ID (25:100:19). Typically, the specific failure is logged previously as an error in the Windows Event Log service. Restore the database or file from a backup, or repair the database.
2010-03-31 19:17:18.45 spid7s      Errors occurred during recovery while rolling back a transaction. The transaction was deferred. Restore the bad page or file, and re-run recovery.   
2010-03-31 19:17:18.45 spid7s      Recovery completed for database mydb (database ID 13) in 2 second(s) (analysis 204 ms, redo 25 ms, undo 1832 ms.) This is an informational message only. No user action is required.   
```

コミットされたトランザクションをロールフォワードする必要がある場合、ページにアクセス不可とマークを付け (このページにこれ以降アクセスしようとするとメッセージ 829 が発生します)、復旧を完了することができます。 この状況では、バックアップからページを復元するか、または DBCC CHECKDB を repair とともに使用してページの割り当てを解除することによって、エラーを修正する必要があります。


  
## <a name="see-also"></a>関連項目  
[ALTER DATABASE &#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql-set-options.md)  
[DBCC CHECKDB &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
[データベースの全体復元 &#40;単純復旧モデル&#41;](~/relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)  
[遅延トランザクション](../backup-restore/deferred-transactions-sql-server.md)  
[MSSQLSERVER_824](~/relational-databases/errors-events/mssqlserver-824-database-engine-error.md)  
[sys.databases &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-databases-transact-sql.md)

  
