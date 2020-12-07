---
title: 可用性グループへのセカンダリ レプリカの追加
description: Transact-SQL (T-SQL)、PowerShell、または SQL Server Management Studio (SSMS) の可用性グループ ウィザードのいずれかを使用して、Always On 可用性グループにセカンダリ レプリカを追加する手順を説明します。
ms.custom: seodec18
ms.date: 05/18/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], configuring
ms.assetid: 6669dcce-85f9-495f-aadf-7f62cff4a9da
author: cawrites
ms.author: chadam
ms.openlocfilehash: 53d138f5273ef07174d1e926fe628f9e73146297
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584874"
---
# <a name="add-a-secondary-replica-to-an-always-on-availability-group"></a>Always On 可用性グループへのセカンダリ レプリカの追加
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  このトピックでは、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]で、 [!INCLUDE[tsql](../../../includes/tsql-md.md)]、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]、または PowerShell を使用して、既存の AlwaysOn 可用性グループにセカンダリ レプリカを追加する方法について説明します。  

  
##  <a name="prerequisites-and-restrictions"></a><a name="PrerequisitesRestrictions"></a> 前提条件と制限  
  
-   プライマリ レプリカをホストするサーバー インスタンスに接続されている必要があります。  
  
 詳細については、「 [Always On 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)の構成に関する一般的な問題のトラブルシューティングに役立つ情報を提供します。  

##  <a name="security"></a><a name="Security"></a> セキュリティ  
  
###  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 可用性グループの ALTER AVAILABILITY GROUP 権限、CONTROL AVAILABILITY GROUP 権限、ALTER ANY AVAILABILITY GROUP 権限、または CONTROL SERVER 権限が必要です。  

[!INCLUDE[Freshness](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **レプリカを追加するには**  
  
1.  オブジェクト エクスプローラーで、プライマリ レプリカをホストするサーバー インスタンスに接続し、サーバー ツリーを展開します。  
  
2.  **[AlwaysOn 高可用性]** ノードと **[可用性グループ]** ノードを展開します。  
  
3.  可用性グループを右クリックし、次のコマンドのどちらかを選択します。  
  
    -   可用性グループへのレプリカ追加ウィザードを起動するには、 **[レプリカの追加]** をクリックします。 詳細については、「[可用性グループへのレプリカ追加ウィザードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)」を参照してください。  
  
    -   または、 **[可用性グループのプロパティ]** ダイアログ ボックスで、 **[プロパティ]** をクリックします。 このダイアログ ボックスでレプリカを追加する手順は以下のとおりです。  
  
        1.  ダイアログ ボックスの **[可用性レプリカ]** ペインで、 **[追加]** をクリックします。 これにより、レプリカのエントリが作成され、空白の [サーバー インスタンス] フィールドが選択された状態になります。  
  
        2.  可用性レプリカをホストするための前提条件を満たしているサーバー インスタンスの名前を入力します。  
  
         さらにレプリカを追加するには、上記の手順を繰り返します。 レプリカの指定を完了したら、 **[OK]** をクリックして操作を完了します。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL の使用  
 **レプリカを追加するには**  
  
1.  プライマリ レプリカをホストする [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに接続します。  
  
2.  ALTER AVAILABILITY GROUP ステートメントの ADD REPLICA ON 句を使用して、可用性グループに新しいセカンダリ レプリカを追加します。 ADD REPLICA ON 句には、ENDPOINT_URL、AVAILABILITY_MODE、および FAILOVER_MODE オプションが必要です。 他のレプリカ オプション (BACKUP_PRIORITY、SECONDARY_ROLE、PRIMARY_ROLE、SESSION_TIMEOUT) は省略可能です。 詳細については、「 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)、または PowerShell を使用して、既存の AlwaysOn 可用性グループにセカンダリ レプリカを追加する方法について説明します。  
  
     たとえば、次の [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントは、 `MyAG` によってホストされるデフォルト サーバー インスタンス (エンドポイント URL が `COMPUTER04`) の `TCP://COMPUTER04.Adventure-Works.com:5022'`という名前の可用性グループに新しいレプリカを作成します。 このレプリカは、手動フェールオーバーと非同期コミット可用性モードをサポートします。  
  
    ```  
    ALTER AVAILABILITY GROUP MyAG ADD REPLICA ON 'COMPUTER04'   
       WITH (  
             ENDPOINT_URL = 'TCP://COMPUTER04.Adventure-Works.com:5022',  
             AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,  
             FAILOVER_MODE = MANUAL  
             );  
    ```  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> PowerShell の使用  
 **レプリカを追加するには**  
  
1.  プライマリ レプリカをホストするサーバー インスタンスにディレクトリを変更 (**cd**) します 。  
  
2.  **New-SqlAvailabilityReplica** コマンドレットを使用します。  
  
     たとえば、次のコマンドは、可用性レプリカを `MyAg`という名前の可用性グループに追加します。 このレプリカは、手動フェールオーバーと非同期コミット可用性モードをサポートします。 セカンダリ ロールでは、このレプリカは読み取りアクセス接続をサポートして、読み取り専用の処理をこのレプリカにオフロードできるようにします。  
  
    ```  
    $agPath = "SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg"  
    $endpointURL = "TCP://PrimaryServerName.domain.com:5022"  
    $failoverMode = "Manual"  
    $availabilityMode = "AsynchronousCommit"  
    $secondaryReadMode = "AllowAllConnections"  
  
    New-SqlAvailabilityReplica -Name SecondaryServer\Instance `   
    -EndpointUrl $endpointURL `   
    -FailoverMode $failoverMode `   
    -AvailabilityMode $availabilityMode `   
    -ConnectionModeInSecondaryRole $secondaryReadMode `   
    -Path $agPath  
    ```  
  
    > [!NOTE]  
    >  コマンドレットの構文を表示するには、 **PowerShell 環境で** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コマンドレットを使用します。 詳細については、「 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)」を参照してください。  
  
 **SQL Server PowerShell プロバイダーを設定して使用するには**  
  
-   [SQL Server PowerShell プロバイダー](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="follow-up-after-adding-a-secondary-replica"></a><a name="FollowUp"></a> 補足情報: セカンダリ レプリカを追加した後  
 既存の可用性グループのレプリカを追加するには、次の手順を実行する必要があります。  
  
1.  新しいセカンダリ レプリカをホストする予定のサーバー インスタンスに接続します。  
  
2.  新しいセカンダリ レプリカを可用性グループに参加させます。 詳細については、「 [可用性グループへのセカンダリ レプリカの参加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)、または PowerShell を使用して、既存の AlwaysOn 可用性グループにセカンダリ レプリカを追加する方法について説明します。  
  
3.  可用性グループ内の各データベースについて、セカンダリ レプリカをホストしているサーバー インスタンス上でセカンダリ データベースを作成します。 詳細については、「 [可用性グループに対するセカンダリ データベースの手動準備 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)、または PowerShell を使用して、AlwaysOn 可用性グループにセカンダリ データベースを参加させる方法について説明します。  
  
4.  新しいセカンダリ データベースのそれぞれを可用性グループに参加させます。 詳細については、「 [可用性グループへのセカンダリ データベースの参加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)のインスタンスに AlwaysOn 可用性グループを作成する方法について説明します。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 関連タスク  
 **可用性レプリカを管理するには**  
  
-   [可用性グループへのセカンダリ レプリカの参加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [可用性グループからのセカンダリ レプリカの削除 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
-   [可用性レプリカでの読み取り専用アクセスの構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [可用性レプリカの可用性モードの変更 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
-   [可用性レプリカのフェールオーバー モードの変更 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [可用性レプリカのセッション タイムアウト期間の変更 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
-   [可用性レプリカのセッション タイムアウト期間の変更 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
## <a name="see-also"></a>参照  
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [可用性グループの作成と構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)   
 [AlwaysOn ダッシュボードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)   
 [可用性グループの監視 &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
