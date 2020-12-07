---
title: 可用性グループ レプリカのセッション タイムアウトの変更
description: Always On 可用性グループ内のレプリカのセッション タイムアウト期間を構成する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
helpviewer_keywords:
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], session timeout
- session timeout [SQL Server]
ms.assetid: e23c6e06-1cd1-4d4a-9bc2-e3e06ab2933d
author: cawrites
ms.author: chadam
ms.openlocfilehash: 2ed683fc46e41ace933d478cd7872f0b2e47af31
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584597"
---
# <a name="modify-the-session-timeout-period-for-an-availability-group-replica"></a>可用性グループ レプリカのセッション タイムアウト期間の変更
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  このトピックでは、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]で [!INCLUDE[tsql](../../../includes/tsql-md.md)]、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]、または PowerShell を使用して、Always On 可用性レプリカのセッション タイムアウト期間を構成する方法について説明します。 セッション タイムアウト期間は、接続されたレプリカからの ping 応答を可用性レプリカが何秒待機するかを制御するレプリカ プロパティです。この期間を過ぎると、接続に失敗したと見なされます。 既定では、レプリカは ping 応答を 10 秒間待機します。 このレプリカ プロパティは、可用性グループ内の指定したセカンダリ レプリカとプライマリ レプリカ間の接続のみに適用されます。 セッション タイムアウト期間の詳細については、「[Always On 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)」を参照してください。  
   
##  <a name="prerequisites"></a><a name="Prerequisites"></a> 前提条件  
  
-   プライマリ レプリカをホストするサーバー インスタンスに接続されている必要があります。  
  
##  <a name="recommendations"></a><a name="Recommendations"></a> 推奨事項  
 タイムアウト期間を 10 秒以上にしておくことをお勧めします。 値を 10 秒未満に設定すると、負荷の高いシステムでは PING を受信できず、誤認エラーが示される可能性があります。  
  
  
## <a name="permissions"></a><a name="Permissions"></a> Permissions  
 可用性グループの ALTER AVAILABILITY GROUP 権限、CONTROL AVAILABILITY GROUP 権限、ALTER ANY AVAILABILITY GROUP 権限、または CONTROL SERVER 権限が必要です。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **可用性レプリカのセッション タイムアウト期間を変更するには**  
  
1.  オブジェクト エクスプローラーで、プライマリ レプリカをホストするサーバー インスタンスに接続し、サーバー ツリーを展開します。  
  
2.  **[AlwaysOn 高可用性]** ノードと **[可用性グループ]** ノードを展開します。  
  
3.  構成する可用性レプリカが含まれる可用性グループをクリックします。  
  
4.  構成するレプリカを右クリックし、 **[プロパティ]** をクリックします。  
  
5.  **[可用性レプリカ プロパティ]** ダイアログ ボックスで **[セッションのタイムアウト (秒)]** フィールドを使用して、このレプリカでのセッション タイムアウト期間の秒数を変更します。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL の使用  
 **可用性レプリカのセッション タイムアウト期間を変更するには**  
  
1.  プライマリ レプリカをホストするサーバー インスタンスに接続します。  
  
2.  [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) ステートメントを使用します。次にその例を示します。  
  
     ALTER AVAILABILITY GROUP *group_name*  
  
     MODIFY REPLICA ON '*instance_name*' WITH ( SESSION_TIMEOUT =*seconds* )  
  
     *group_name* の部分には、可用性グループの名前を指定します。 *instance_name* の部分には、変更する可用性レプリカをホストするサーバー インスタンスの名前を指定します。 *seconds* には、レプリカがセカンダリ レプリカとして機能している場合に、データベースにログを適用する前に待機する必要がある最小秒数を指定します。 既定値は 0 秒です。つまり、適用の遅延はありません。  
  
     次の例は、 `AccountsAG` 可用性グループのプライマリ レプリカに入力すると、 `15` サーバー インスタンスにあるレプリカのセッション タイムアウト値を `INSTANCE09` 秒に変更します。  
  
    ```  
    ALTER AVAILABILITY GROUP AccountsAG   
       MODIFY REPLICA ON 'INSTANCE09' WITH (SESSION_TIMEOUT = 15);  
    ```  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> PowerShell の使用  
 **可用性レプリカのセッション タイムアウト期間を変更するには**  
  
1.  プライマリ レプリカをホストするサーバー インスタンスにディレクトリを変更 (**cd**) します 。  
  
2.  **Set-SqlAvailabilityReplica** コマンドレットを **SessionTimeout** パラメーターを指定して使用し、指定された可用性レプリカのセッション タイムアウト期間の秒数を変更します。  
  
     たとえば、次のコマンドは、セッションのタイムアウト期間を 15 秒に設定します。  
  
    ```  
    Set-SqlAvailabilityReplica -SessionTimeout 15 `   
    -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
    > [!NOTE]  
    >  コマンドレットの構文を表示するには、 **PowerShell 環境で** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コマンドレットを使用します。 詳細については、「 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)」を参照してください。  
  
 **SQL Server PowerShell プロバイダーを設定して使用するには**  
  
-   [SQL Server PowerShell プロバイダー](../../../powershell/sql-server-powershell-provider.md)  
  
## <a name="see-also"></a>参照  
 [Always On 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
