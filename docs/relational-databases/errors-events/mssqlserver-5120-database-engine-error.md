---
description: MSSQLSERVER_5120
title: MSSQLSERVER_5120
ms.custom: ''
ms.date: 07/25/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5120 (Database Engine error)
ms.assetid: ''
author: PijoCoder
ms.author: mathoma
ms.openlocfilehash: 368fba2b9f56af0b86741db0d15ceebcc238ab52
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91869434"
---
# <a name="mssqlserver_5120"></a>MSSQLSERVER_5120
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|5120|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DSK_FCB_FAILURE|  
|メッセージ テキスト|テーブル エラー:物理ファイル "%.*ls" を開けません。 オペレーティング システム エラー %d: "%ls"。|  
  
## <a name="explanation"></a>説明  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でデータベース ファイルを開けませんでした。  メッセージに示されたオペレーティング システム エラーにより、エラーのより具体的な根本原因が示されます。 このエラーは、[17204](mssqlserver-17204-database-engine-error.md) や [17207](mssqlserver-17207-database-engine-error.md) などの他のエラーと共に表示されることがよくあります。
  
## <a name="user-action"></a>ユーザー アクション  
  
  オペレーティング システム エラーを診断して修正してから、操作を再試行してください。 Microsoft で領域の発生している製品の領域を絞り込むのに役立つ、複数の状態があります。 
  
### <a name="access-is-denied"></a>アクセスが拒否されました 
`Access is Denied` オペレーティング システム エラー = 5 を取得している場合は、次の方法を検討してください。
   -  エクスプローラーでファイルのプロパティを参照して、ファイルに設定されているアクセス許可を確認します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、Windows グループを使用して、さまざまなファイル リソースに Access Control をプロビジョニングします。 適切なグループ [SQLServerMSSQLUser$ComputerName$MSSQLSERVER や SQLServerMSSQLUser$ComputerName$InstanceName などの名前] に、エラー メッセージで言及されているデータベース ファイルに対して必要なアクセス許可が付与されていることを確認します。 詳細については、「[データベース エンジン アクセスのファイル システム権限の構成](/previous-versions/sql/2014/database-engine/configure-windows/configure-file-system-permissions-for-database-engine-access?view=sql-server-2014)」を参照してください。 Windows グループに、実際に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス開始アカウントまたはサービス SID が含まれていることを確認します。
   -  現在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスの実行に使用されているユーザー アカウントを確認します。 Windows タスク マネージャーを使用して、この情報を取得できます。 実行可能ファイル "sqlservr.exe" の "ユーザー名" の値を探します。 また、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントを最近変更した場合は、[SQL Server 構成マネージャー](../sql-server-configuration-manager.md) ユーティリティを使用してこの操作を実行する方法がサポートされています。 
   -  操作の種類 (サーバー起動中にデータベースを開く、データベースのアタッチ、データベースの復元など) によっては、偽装とデータベース ファイルへのアクセスに使用されるアカウントが異なる場合があります。 トピック「[データ ファイルとログ ファイルのセキュリティ保護](/previous-versions/sql/sql-server-2008-r2/ms189128(v=sql.105))」を確認して、どの操作によってどのアクセス許可が、どのアカウントに設定されるかを理解してください。 Windows SysInternals [Process Monitor](/sysinternals/downloads/procmon) などのツールを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスのサービス開始アカウント [またはサービス SID]、または偽装されたアカウントのセキュリティ コンテキストにおいて、ファイルへのアクセスが行われているかどうかを把握します。

      [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって、ALTER DATABASE または CREATE DATABASE 操作を実行するログインのユーザー資格情報が偽装されている場合は、Process Monitor ツールに次の情報が表示されます (一例)。
      
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
  
  
### <a name="attaching-files-that-reside-on-a-network-attached-storage"></a>ネットワークに接続された記憶域に存在するファイルをアタッチする  
ネットワークに接続された記憶域に存在するデータベースを再アタッチできない場合は、このようなメッセージがアプリケーション ログに記録される可能性があります。

`Msg 5120, Level 16, State 101, Line 1 Unable to open the physical file "\\servername\sharename\filename.mdf". Operating system error 5: (Access is denied.).`

この問題が発生するのは、データベースがデタッチされたときに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってファイルのアクセス許可がリセットされるためです。 データベースを再アタッチしようとすると、共有のアクセス許可が制限されているためにエラーが発生します。

解決するには、次の手順に従ってください。
1. -T スタートアップ オプションを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を開始します。 このスタートアップ オプションを使用して、[SQL Server 構成マネージャー](../sql-server-configuration-manager.md) でトレース フラグ 1802 を有効にします (1802 の詳細については、[トレース フラグ](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)を参照してください)。 スタートアップ パラメーターの変更方法の詳細については、「[データベース エンジン サービスのスタートアップ オプション](../../database-engine/configure-windows/database-engine-service-startup-options.md)」を参照してください。

2. 次のコマンドを使用して、データベースをデタッチします。
   ```sql
    exec sp_detach_db DatabaseName
    go 
   ```

3. 次のコマンドを使用して、データベースを再アタッチします。
   ```sql
   exec sp_attach_db DatabaseName, '\\Network-attached storage_Path\DatabaseMDFFile.mdf', '\\Network-attached storage_Path\DatabaseLDFFile.ldf'
   go
   ```
