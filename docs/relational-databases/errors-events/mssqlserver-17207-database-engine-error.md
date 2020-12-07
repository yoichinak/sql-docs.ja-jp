---
description: MSSQLSERVER_17207
title: MSSQLSERVER_17207
ms.custom: ''
ms.date: 07/25/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17204 (Database Engine error)
ms.assetid: ''
author: PijoCoder
ms.author: mathoma
ms.openlocfilehash: d1c0face9315a38d4748cffef71e135401102dd0
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91869465"
---
# <a name="mssqlserver_17207"></a>MSSQLSERVER_17207
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |
| :-------- | :---- |
|製品名|SQL Server|  
|イベント ID|17207|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBLKIO_OS2DISKERROR|  
|メッセージ テキスト|%ls:ファイル '%ls' を作成中または開いているときに、オペレーティング システム エラー %ls が発生しました。 オペレーティング システム エラーを診断して修正し、操作を再試行してください。|  


## <a name="explanation"></a>説明  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で、指定された OS エラーが原因で指定されたファイルを開くことができませんでした。  

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でデータベースやトランザクション ログ ファイルを開くことができない場合、Windows アプリケーション イベントまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログにエラー 17207 が表示されることがあります。 このエラーの例を次に示します。

``` 
Error: 17207, Severity: 16, State: 1.
FileMgr::StartSecondaryDataFiles: Operating system error 2(The system cannot find the file specified.) occurred while creating or opening file 'F:\MSSQL\DATA\MyDB_FG1_1.ndf'. Diagnose and correct the operating system error, and retry the operation.
```

このようなエラーは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの起動プロセス中、またはデータベースを起動しようとするデータベース操作の実行中 (ALTER DATABASE など) に表示されることがあります。 シナリオによっては、17207 と 17204 の両方のエラーが表示される場合があり、別の状況ではそのうちの 1 つだけが表示される場合があります。

ユーザー データベースでこのようなエラーが発生した場合、そのデータベースは RECOVERY_PENDING 状態のままになり、アプリケーションはこのデータベースにアクセスできなくなります。 システム データベースでこのようなエラーが発生した場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスは起動せず、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のこのインスタンスに接続することはできません。 これにより、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスター リソースがオフラインになることもあります。

問題が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] FileStream ファイル グループに関連している場合は、ファイル名の代わりに完全なディレクトリ パスのみが表示されていることがわかります。 次に例を示します。 
```
Error: 17207, Severity: 16, State: 1.
STREAMFCB::Startup: Operating system error 2(The system cannot find the file specified.) occurred while creating or opening file 'C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\DATA\bpa_files_test_fs_1\bpa_files_test_fs_1'. Diagnose and correct the operating system error, and retry the operation.
```

## <a name="cause"></a>原因
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースを使用する前には、そのデータベースを起動する必要があります。 データベースの起動プロセスでは、データベースおよびデータベース ファイルを表すさまざまなデータ構造が初期化され、データベースに属するすべてのファイルが開かれ、最後にデータベースの復旧が実行されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、データベースに属するファイルを開くために、[CreateFile](/windows/win32/api/fileapi/nf-fileapi-createfilea) Windows API 関数が使用されます。
 
メッセージ 17207 (および 17204) は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の起動プロセス中にデータベース ファイルを開こうとしたときにエラーが発生したことを示します。
 
これらのエラー メッセージには、次の情報が含まれています。
1. ファイルを開こうとしている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 関数の名前。 通常、これらのエラー メッセージに表示される関数名は、次のいずれかになります。
   - FCB::Open                              - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でファイルを開こうとしたときにエラーが発生しました
   - FileMgr::StartPrimaryDataFiles         - プライマリ データ ファイルまたはプライマリ ファイル グループに属するファイル
   - FileMgr::StartSecondaryDataFiles       - セカンダリ ファイル グループに属するファイル
   - FileMgr::StartLogFiles                 - トランザクション ログ ファイル
   - STREAMFCB::Startup                     - SQL FileStream コンテナー
   - FCB::RemoveAlternateStreams
  
      
1. 状態情報によって、このエラー メッセージを生成する可能性がある関数内の複数の場所が識別されます。
1. ファイルの完全な物理パス。
1. ファイルに対応するファイル ID。
1. オペレーティング システムのエラー コードとエラーの説明。 場合によっては、エラー コードのみが表示されます。
 
これらのエラー メッセージに表示されるオペレーティング システムのエラー情報は、エラー 17204 につながる根本原因です。 これらのエラー メッセージのよくある原因は、アクセス許可の問題か、ファイルへの正しくないパスです。


## <a name="user-action"></a>ユーザー アクション  
1. エラー 17207 を解決するには、関連付けられているオペレーティング システムのエラー コードを理解し、そのエラーを診断する必要があります。 オペレーティング システムのエラー状態が解決されたら、(ALTER DATABASE SET ONLINE などを使用して) データベースを再起動するか、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを再起動して、影響を受けたデータベースをオンラインにすることができます。 場合によっては、このオペレーティング システム エラーを解決できないことがあります。その場合は、特定の是正措置を講じる必要があります。 このセクションでは、それらの操作について説明します。
1. 17207 エラー メッセージにエラー コードのみが含まれていて、エラーの説明が含まれていない場合は、オペレーティング システムのシェルから次のコマンドを使用して、エラー コードの解決を試みることができます: net helpmsg <error code> 。 エラー コードとして 8 桁の状態コードを取得している場合は、「[HRESULT を Win32 エラー コードに変換する方法](https://devblogs.microsoft.com/oldnewthing/20061103-07/?p=29133)」などの情報源を参照して、これらの状態コードを OS エラーにデコードできます。
1. ```Access is Denied``` オペレーティング システム エラー = 5 を取得している場合は、次の方法を検討してください。
   -  エクスプローラーでファイルのプロパティを参照して、ファイルに設定されているアクセス許可を確認します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、Windows グループを使用して、さまざまなファイル リソースに Access Control をプロビジョニングします。 適切なグループ (SQLServerMSSQLUser$ComputerName$MSSQLSERVER や SQLServerMSSQLUser$ComputerName$InstanceName などの名前) に、エラー メッセージで言及されているデータベース ファイルに対して必要なアクセス許可が付与されていることを確認します。 詳細については、「[データベース エンジン アクセスのファイル システム権限の構成](/previous-versions/sql/2014/database-engine/configure-windows/configure-file-system-permissions-for-database-engine-access?view=sql-server-2014)」を参照してください。 Windows グループに、実際に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス開始アカウントまたはサービス SID が含まれていることを確認します。
   -  現在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスの実行に使用されているユーザー アカウントを確認します。 Windows タスク マネージャーを使用して、この情報を取得できます。 実行可能ファイル "sqlservr.exe" の "ユーザー名" の値を探します。 また、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントを最近変更した場合は、SQL Server 構成マネージャー ユーティリティを使用してこの操作を実行する方法がサポートされています。 これについて詳しくは、「[SQL Server 構成マネージャー](../sql-server-configuration-manager.md)」をご覧ください。 
   -  操作の種類 (サーバー起動中にデータベースを開く、データベースのアタッチ、データベースの復元など) によっては、偽装とデータベース ファイルへのアクセスに使用されるアカウントが異なる場合があります。 トピック「[データ ファイルとログ ファイルのセキュリティ保護](/previous-versions/sql/sql-server-2008-r2/ms189128(v=sql.105))」を確認して、どの操作によってどのアクセス許可が、どのアカウントに設定されるかを理解してください。 Windows SysInternals [Process Monitor](/sysinternals/downloads/procmon) などのツールを使用して、SQL Server インスタンスのサービス開始アカウント (またはサービス SID)、または偽装されたアカウントのセキュリティ コンテキストにおいて、ファイルへのアクセスが行われているかどうかを把握します。

      SQL Server によって、ALTER DATABASE または CREATE DATABASE 操作を実行するログインのユーザー資格情報が偽装されている場合は、Process Monitor ツールに次の情報が表示されます (一例)。

        ```
        Date & Time:      3/27/2010 8:26:08 PM
        Event Class:        File System
        Operation:          CreateFile
        Result:                ACCESS DENIED
        Path:                  C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\DATA\attach_test.mdf
        TID:                   4288
        Duration:             0.0000366
        Desired Access:Generic Read/Write
        Disposition:        Open
        Options:            Synchronous IO Non-Alert, Non-Directory File, Open No Recall
        Attributes:          N
        ShareMode:       Read
        AllocationSize:   n/a
        Impersonating: DomainName\UserName
        ```
  
1. `The system cannot find the file specified` オペレーティング システム エラー = 3 が表示された場合:
   - エラー メッセージで完全なパスを確認します。
   - エクスプローラーでディスク ドライブとフォルダー パスが表示され、アクセス可能であることを確認します。
   - Windows イベントログを確認して、このディスク ドライブに問題があるかどうかを調べます。
   - パスが正しくない場合、またこのデータベースがシステムに既に存在する場合は、「[データベース ファイルの移動](../databases/move-database-files.md)」の記事で説明されている方法を使用してデータベース ファイルのパスを変更できます。 特に 17204 または 17207 が発生しているシステム データベース ファイルで、指定されたディスク ドライブが使用できないディザスター リカバリー シナリオに取り組んでいる場合に、この手順を使用する必要があります。 このトピックでは、さまざまなシステム データベース (master、model、tempdb、msdb、および mssqlsystemresource.mdf) の現在の場所を特定する方法についても説明します。
   - データベース ファイルが見つからないためにこのエラーが表示される場合は、有効なバックアップからデータベースを復元する必要があります。
     - エラーに関連付けられているデータベース ファイルがセカンダリ ファイル グループに属している場合は、必要に応じて、ファイル グループをオフラインにし、データベースをオンラインにしてから、そのファイル グループの復元を単独で実行します。 詳細については、「[ALTER DATABASE (Transact-SQL) の File および Filegroup オプション](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)」のオフラインに関するセクションを参照してください。
     - エラーを生成したファイルがトランザクション ログ ファイルである場合は、[CREATE DATABASE (Transact-SQL)](../../t-sql/statements/create-database-transact-sql.md) に関するトピックの "FOR ATTACH" と "FOR ATTACH_REBUILD_LOG" に関するセクションの情報を参照して、欠落しているトランザクション ログ ファイルを再作成する方法を確認してください。
   - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がこれらの場所にあるデータベース ファイルへのアクセスを試行する前に、ディスクまたはネットワークの場所 (iSCSI ドライブなど) が使用可能であることを確認してください。 必要に応じて、クラスター アドミニストレーターまたはサービス コントロール マネージャーで必要な依存関係を作成します。

1. `The process cannot access the file because it is being used by another process` オペレーティング システム エラー = 32 が表示された場合:
   - Windows Sysinternals の[プロセス エクスプローラー](/sysinternals/downloads/process-explorer)や[ハンドル](/sysinternals/downloads/handle)を使用して、別のプロセスまたはサービスがこのデータベース ファイルに対して排他的ロックを取得しているかどうかを確認します。
   - プロセスが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース ファイルにアクセスしていれば、それを停止します。 一般的な例としては、ウイルス対策プログラムがあります (次の[サポート技術情報の記事](https://support.microsoft.com/help/309422/choosing-antivirus-software-for-computers-that-run-sql-server)を参照してください)。
   - クラスター環境で、以前に所有していたノードの sqlservr.exe プロセスによって、データベース ファイルへのハンドルが実際に解放されていることを確認します。 通常、このような状況は起こりませんが、クラスターまたは I/O パスが正しく構成されていない場合に、このような問題が発生する可能性があります。
