---
description: MSSQLSERVER_17204
title: MSSQLSERVER_17204 | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17204 (Database Engine error)
ms.assetid: 40db66f9-dd5e-478c-891e-a06d363a2552
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d0dafe59102083ea1cd5c675819487eb88c9ecbc
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91869483"
---
# <a name="mssqlserver_17204"></a>MSSQLSERVER_17204
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |
| :-------- | :---- |
|製品名|SQL Server|  
|イベント ID|17204|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBLKIO_DEVOPENFAILED|  
|メッセージ テキスト|%ls:ファイル番号 %d のファイル %ls を開けませんでした。  OS エラー: %ls。|  
  
## <a name="explanation"></a>説明  
SQL Server で、指定された OS エラーが原因で指定されたファイルを開くことができませんでした。  

SQL Server でデータベースやトランザクション ログ ファイルを開くことができない場合、Windows アプリケーション イベントまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログにエラー 17204 が表示されることがあります。 このエラーの例を次に示します。

``` 
Error: 17204, Severity: 16, State: 1.
FCB::Open failed: Could not open file c:\Program Files\Microsoft SQL Server\MSSQL10.SQL2008\MSSQL\data\MyDB_Prm.mdf for file number 1.  OS error: 5(Access is denied.).
```

このようなエラーは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの起動プロセス中、またはデータベースを起動しようとするデータベース操作の実行中 (ALTER DATABASE など) に表示されることがあります。 シナリオによっては、17204 と 17207 の両方のエラーが表示される場合があり、別の状況ではそのうちの 1 つだけが表示される場合があります。

ユーザー データベースでこのようなエラーが発生した場合、そのデータベースは RECOVERY_PENDING 状態のままになり、アプリケーションはこのデータベースにアクセスできなくなります。 システム データベースでこのようなエラーが発生した場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスは起動せず、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のこのインスタンスに接続することはできません。 システム データベースで障害が発生すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスター リソースがオフラインになることもあります。

## <a name="cause"></a>原因
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースを使用する前には、そのデータベースを起動する必要があります。 データベースの起動プロセスは次のようになります。 
1. データベースおよびデータベース ファイルを表すさまざまなデータ構造を初期化する
1. データベースに属するすべてのファイルを開く
1. データベース上で復旧を実行する 

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、データベースに属するファイルを開くために、[CreateFile](/windows/win32/api/fileapi/nf-fileapi-createfilea) Windows API 関数が使用されます。
 
メッセージ 17204 (および 17207) は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の起動プロセス中にデータベース ファイルを開こうとしたときにエラーが発生したことを示します。
 
これらのエラー メッセージには、次の情報が含まれています。
1. ファイルを開こうとしている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 関数の名前。 通常、これらのエラー メッセージに表示される関数名は、次のいずれかになります。
   - FCB::Open - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でファイルを開こうとしたときにエラーが発生しました
   - FileMgr::StartPrimaryDataFiles - プライマリ データ ファイルまたはプライマリ ファイル グループに属するファイル
   - FileMgr::StartSecondaryDataFiles - セカンダリ ファイル グループに属するファイル
   - FileMgr::StartLogFiles - トランザクション ログ ファイル
   - STREAMFCB::Startup - SQL FileStream コンテナー
   - FCB::RemoveAlternateStreams
  
      
1. 状態情報によって、このエラー メッセージを生成する可能性がある関数内の複数の場所が識別されます
1. ファイルの完全な物理パス
1. ファイルに対応するファイル ID
1. オペレーティング システムのエラー コードとエラーの説明。 場合によっては、エラー コードのみが表示されます。
 
これらのエラー メッセージに表示されるオペレーティング システムのエラー情報は、エラー 17204 につながる根本原因です。 これらのエラー メッセージのよくある原因は、アクセス許可の問題か、ファイルへの正しくないパスです。


## <a name="user-action"></a>ユーザーの操作  
1. エラー 17204 を解決するには、関連付けられているオペレーティング システムのエラー コードを理解し、そのエラーを診断する必要があります。 オペレーティング システムのエラー状態が解決されたら、(ALTER DATABASE SET ONLINE などを使用して) データベースを再起動するか、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを再起動して、影響を受けたデータベースをオンラインにすることができます。 場合によっては、オペレーティング システムのエラーを解決できないことがあります。 その場合、特定の是正措置を講じる必要があります。 このセクションでは、それらの操作について説明します。
1. 17204 エラー メッセージにエラー コードのみが含まれていて、エラーの説明が含まれていない場合は、オペレーティング システムのシェルから次のコマンドを使用して、エラー コードの解決を試みることができます: net helpmsg <error code> 。 エラー コードとして 8 桁の状態コードを取得している場合は、「[HRESULT を Win32 エラー コードに変換する方法](https://devblogs.microsoft.com/oldnewthing/20061103-07/?p=29133)」などの情報源を参照して、これらの状態コードを OS エラーにデコードできます。
1. `Access is Denied` オペレーティング システム エラー = 5 を取得している場合は、次の方法を検討してください。
   -  エクスプローラーでファイルのプロパティを参照して、ファイルに設定されているアクセス許可を確認します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、Windows グループを使用して、さまざまなファイル リソースに Access Control をプロビジョニングします。 適切なグループ [SQLServerMSSQLUser$ComputerName$MSSQLSERVER や SQLServerMSSQLUser$ComputerName$InstanceName などの名前] に、エラー メッセージで言及されているデータベース ファイルに対して必要なアクセス許可が付与されていることを確認します。 詳細については、「[データベース エンジン アクセスのファイル システム権限の構成](/previous-versions/sql/2014/database-engine/configure-windows/configure-file-system-permissions-for-database-engine-access?view=sql-server-2014)」を参照してください。 Windows グループに、実際に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス開始アカウントまたはサービス SID が含まれていることを確認します。
   -  現在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスの実行に使用されているユーザー アカウントを確認します。 Windows タスク マネージャーを使用して、この情報を取得できます。 実行可能ファイル "sqlservr.exe" の "ユーザー名" の値を探します。 また、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントを最近変更した場合は、SQL Server 構成マネージャー ユーティリティを使用してこの操作を実行する方法がサポートされています。 これについて詳しくは、「[SQL Server 構成マネージャー](../sql-server-configuration-manager.md)」をご覧ください。 
   -  操作の種類 (サーバー起動中にデータベースを開く、データベースのアタッチ、データベースの復元など) によっては、偽装とデータベース ファイルへのアクセスに使用されるアカウントが異なる場合があります。 トピック「[データ ファイルとログ ファイルのセキュリティ保護](/previous-versions/sql/sql-server-2008-r2/ms189128(v=sql.105))」を確認して、どの操作によってどのアクセス許可が、どのアカウントに設定されるかを理解してください。 Windows SysInternals [Process Monitor](/sysinternals/downloads/procmon) などのツールを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスのサービス開始アカウント [またはサービス SID]、または偽装されたアカウントのセキュリティ コンテキストにおいて、ファイルへのアクセスが行われているかどうかを把握します。

      [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって、ALTER DATABASE または CREATE DATABASE 操作を実行するユーザーの資格情報が偽装されている場合は、Process Monitor ツールに次の情報が表示されます (一例)。
        ```Date & Time:      3/27/2010 8:26:08 PM
        Event Class:        File System
        Operation:          CreateFile
        Result:                ACCESS DENIED
        Path:                  C:\Program Files\Microsoft SQL Server\MSSQL10.SQL2008\MSSQL\DATA\attach_test.mdf
        TID:                   4288
        Duration:             0.0000366
        Desired Access:Generic Read/Write
        Disposition:        Open
        Options:            Synchronous IO Non-Alert, Non-Directory File, Open No Recall
        Attributes:          N
        ShareMode:       Read
        AllocationSize:   n/a
        Impersonating: DomainName\UserName```
  
1. If you are getting `The system cannot find the file specified` OS error = 3:
   - Review the complete path from the error message
   - Ensure the disk drive and the folder path is visible and accessible from Windows Explorer
   - Review the Windows Event log to find out if any problems exist with this disk drive
   - If the path is incorrect and if this database already exists in the system, you can change the database file paths using the methods explained in the topic [Move Database Files](../databases/move-database-files.md). You may have to use this procedure, especially for system database files that encounter 17204 or 17207 and you are working through a disaster recovery scenario where the specified disk drives are unavailable. This topic also explains how you can identify the current location of the various system databases [master, model, tempdb, msdb and mssqlsystemresource].
   - If you see this error because the database files are missing, you have to restore the database from a valid backup.
     - If the database file associated with the error belongs to a secondary filegroup, then you can optionally mark that filegroup offline, bring the database online and then perform a restore of that filegroup alone. For more information, refer to the OFFLINE section of the topic [ALTER DATABASE File and Filegroup Options (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).
     - If the file that produced the error is a transaction log file, review the information under the sections "FOR ATTACH" and "FOR ATTACH_REBUILD_LOG" of the topic [CREATE DATABASE (Transact-SQL)](../../t-sql/statements/create-database-transact-sql.md) to understand how you can recreate the missing transaction log files.
   - Ensure that any disk or network location [like iSCSI drive] is available before [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] attempts to access the database files on these locations. If needed create the required dependencies in Cluster Administrator or Service Control Manager.
1. If you're getting the `The process cannot access the file because it is being used by another process` operating system error = 32:
   - Use a tool like [Process Explorer](/sysinternals/downloads/process-explorer) or [Handle](/sysinternals/downloads/handle) from Windows Sysinternals to find out if another process or service has acquired exclusive lock on this database file
   - Stop that process from accessing [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Database files. Common examples include anti-virus programs (see guidance for file exclusions in the following [KB article](https://support.microsoft.com/help/309422/choosing-antivirus-software-for-computers-that-run-sql-server) )
   - In a cluster environment, make sure that the sqlservr.exe process from the previous owning node has actually released the handles to the database files. Normally, this doesn't occur, but misconfigurations of the cluster or I/O paths can lead to such issues.
