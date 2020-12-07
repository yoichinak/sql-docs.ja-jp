---
title: 分散型可用性グループの構成
description: Transact-SQL の例を使用して、分散型可用性グループを構成する方法について学習します。 また、分散型可用性グループに関する情報の入手先についても学習します。
ms.custom: seodec18
ms.date: 01/28/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
ms.assetid: f7c7acc5-a350-4a17-95e1-e689c78a0900
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 537dbc1d60fc707f3d00aacd85e1ec5e335519c0
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123840"
---
# <a name="configure-an-always-on-distributed-availability-group"></a>Always On 分散型可用性グループの構成  
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

分散型可用性グループを作成するには、それぞれに独自のリスナーを持つ可用性グループをそれぞれ 2 つ作成する必要があります。 次に、これらの可用性グループを分散型可用性グループに結合します。 次の手順は、Transact-SQL の基本的な例です。 この例では、可用性グループとリスナーを作成するすべての手順を取り上げていません。主な要件を強調することに重点を置いています。

分散型可用性グループの技術の概要については、「[Distributed availability groups](distributed-availability-groups.md)」 (分散可用性グループ) を参照してください。

## <a name="prerequisites"></a>前提条件

### <a name="set-the-endpoint-listeners-to-listen-to-all-ip-addresses"></a>エンドポイント リスナーがすべての IP アドレスをリッスンするよう設定する

分散型可用性グループで、エンドポイントが別の可用性グループとも通信できることを確認します。 エンドポイント上で 1 つの可用性グループが特定のネットワークに設定されている場合、分散型可用性グループは正しく機能しません。 分散型可用性グループ内のレプリカをホストする各サーバーで、リスナーがすべての IP アドレス (`LISTENER_IP = ALL`) をリッスンするように構成します。

#### <a name="create-a-listener-to-listen-to-all-ip-addresses"></a>リスナーがすべての IP アドレスをリッスンするようにする

たとえば、次のスクリプトで、TCP ポート 5022 上ですべての IP アドレスをリッスンするリスナー エンドポイントを作成します。  

```sql
CREATE ENDPOINT [aodns-hadr] 
    STATE=STARTED
    AS TCP (LISTENER_PORT = 5022, LISTENER_IP = ALL)
FOR DATA_MIRRORING (
   ROLE = ALL, 
   AUTHENTICATION = WINDOWS NEGOTIATE,
   ENCRYPTION = REQUIRED ALGORITHM AES
)
GO
```

#### <a name="alter-a-listener-to-listen-to-all-ip-addresses"></a>すべての IP アドレスをリッスンするようリスナーを変更する

たとえば、次のスクリプトで、すべての IP アドレスをリッスンするようリスナー エンドポイントを変更します。  

```sql
ALTER ENDPOINT [aodns-hadr] 
    AS TCP (LISTENER_IP = ALL)
GO
```

## <a name="create-first-availability-group"></a>最初の可用性グループを作成する

### <a name="create-the-primary-availability-group-on-the-first-cluster"></a>最初のクラスターにプライマリ可用性グループを作成する  
最初の Windows Server フェールオーバー クラスター (WSFC) に可用性グループを作成します。   この例では、データベース `ag1` の `db1`という可用性グループです。 プライマリ可用性グループのプライマリ レプリカは、分散型可用性グループでは **グローバル プライマリ** と呼ばれます。 この例の server1 はグローバル プライマリです。        
  
```sql  
CREATE AVAILABILITY GROUP [ag1]   
FOR DATABASE db1   
REPLICA ON N'server1' WITH (ENDPOINT_URL = N'TCP://server1.contoso.com:5022',  
    FAILOVER_MODE = AUTOMATIC,  
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC),   
N'server2' WITH (ENDPOINT_URL = N'TCP://server2.contoso.com:5022',   
    FAILOVER_MODE = AUTOMATIC,   
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC);   
GO  
  
```  
  
>[!NOTE]
>上記の例では、自動シード処理を使用しています。レプリカと分散型可用性グループの両方について、**SEEDING_MODE** は **AUTOMATIC** に設定されます。 この構成では、確立後に、セカンダリ レプリカとセカンダリ可用性グループは自動的に設定されます。プライマリ データベースの手動バックアップと復元を実行する必要はありません。  
  
### <a name="join-the-secondary-replicas-to-the-primary-availability-group"></a>セカンダリ レプリカをプライマリ可用性グループに追加する  
**ALTER AVAILABILITY GROUP** に **JOIN** オプションを指定して、すべてのセカンダリ レプリカを可用性グループに追加する必要があります。 この例では自動シード処理を使用しているため、**ALTER AVAILABILITY GROUP** に **GRANT CREATE ANY DATABASE** オプションを指定して呼び出す必要もあります。 この設定では、可用性グループでデータベースを作成し、プライマリ レプリカから自動的にシード処理を開始できるようになります。  
  
この例では、セカンダリ レプリカ `server2`で次のコマンドが実行され、 `ag1` 可用性グループに追加されます。 この可用性グループは、セカンダリ上にデータベースを作成できるようになります。  
  
```sql  
ALTER AVAILABILITY GROUP [ag1] JOIN   
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE  
GO  
```  

>[!NOTE]
>可用性グループがセカンダリ レプリカにデータベースを作成すると、`ALTER AVAILABILITY GROUP` ステートメントを実行したアカウントとしてデータベース所有者が設定され、任意のデータベースを作成するアクセス許可が付与されます。 詳細については、「[セカンダリ レプリカの CREATE DATABASE アクセス許可を可用性グループに付与する](automatic-seeding-secondary-replicas.md#grantCreate)」を参照してください。
  
### <a name="create-a-listener-for-the-primary-availability-group"></a>プライマリ可用性グループのリスナーを作成する  

次に、プライマリ可用性グループのリスナーを最初の WSFC に追加します。 この例では、 `ag1-listener`というリスナーです。 リスナーの詳細な作成手順については、「[可用性グループ リスナーの作成または構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)」を参照してください。  
  
```sql
ALTER AVAILABILITY GROUP [ag1]    
    ADD LISTENER 'ag1-listener' ( 
        WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , 
        PORT = 60173);    
GO  
```  
  

## <a name="create-second-availability-group"></a>2 つ目の可用性グループを作成する  
 2 つ目の WSFC に 2 つ目の可用性グループ `ag2`を作成します。 この場合、データベースはプライマリ可用性グループから自動的にシード処理されるため、データベースを指定しません。  セカンダリ可用性グループのプライマリ レプリカは、分散型可用性グループでは **フォワーダー** と呼ばれます。 この例の server3 はフォワーダーです。 
  
```sql  
CREATE AVAILABILITY GROUP [ag2]   
FOR   
REPLICA ON N'server3' WITH (ENDPOINT_URL = N'TCP://server3.contoso.com:5022',   
    FAILOVER_MODE = MANUAL,   
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC),   
N'server4' WITH (ENDPOINT_URL = N'TCP://server4.contoso.com:5022',   
    FAILOVER_MODE = MANUAL,   
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC);   
GO  
```  
  
> [!NOTE]  
> セカンダリ可用性グループは、同じデータベース ミラーリング エンドポイント (この例ではポート 5022) を使用する必要があります。 そうしないと、ローカルのフェールオーバー後にレプリケーションは停止します。  
  
### <a name="join-the-secondary-replicas-to-the-secondary-availability-group"></a>セカンダリ レプリカをセカンダリ可用性グループに追加する  
 この例では、セカンダリ レプリカ `server4`で次のコマンドが実行され、 `ag2` 可用性グループに追加されます。 この可用性グループは、自動シード処理をサポートするデータベースをセカンダリ上に作成できるようになります。  
  
```sql  
ALTER AVAILABILITY GROUP [ag2] JOIN   
ALTER AVAILABILITY GROUP [ag2] GRANT CREATE ANY DATABASE  
GO  
```  
  
### <a name="create-a-listener-for--the-secondary-availability-group"></a>セカンダリ可用性グループのリスナーを作成する  
 次に、セカンダリ可用性グループのリスナーを 2 つ目の WSFC に追加します。 この例では、 `ag2-listener`というリスナーです。 リスナーの詳細な作成手順については、「[可用性グループ リスナーの作成または構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)」を参照してください。  
  
```sql  
ALTER AVAILABILITY GROUP [ag2]    
    ADD LISTENER 'ag2-listener' ( WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , PORT = 60173);    
GO  
```  
  
## <a name="create-distributed-availability-group-on-first-cluster"></a>最初のクラスターに分散型可用性グループを作成する  
 最初の WSFC に分散型可用性グループ (この例では `distributedag` ) を作成します。 **CREATE AVAILABILITY GROUP** コマンドに **DISTRIBUTED** オプションを指定して実行します。 **AVAILABILITY GROUP ON** パラメーターに、メンバー可用性グループの `ag1` と `ag2` を指定します。  
  
```sql  
CREATE AVAILABILITY GROUP [distributedag]  
   WITH (DISTRIBUTED)   
   AVAILABILITY GROUP ON  
      'ag1' WITH    
      (   
         LISTENER_URL = 'tcp://ag1-listener.contoso.com:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      ),   
      'ag2' WITH    
      (   
         LISTENER_URL = 'tcp://ag2-listener.contoso.com:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      );    
GO   
```  
  
> [!NOTE]  
>  **LISTENER_URL** で、各可用性グループのリスナーと、可用性グループのデータベース ミラーリング エンドポイントを指定します。 この例では、ポート `5022` です (リスナーの作成に使用したポート `60173` ではありません)。 Azure でインスタンスにロード バランサーを使用している場合、[分散型可用性グループのポートの負荷分散の規則を追加します](/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener#add-load-balancing-rule-for-distributed-availability-group)。 SQL Server インスタンスのポートだけでなく、リスナー ポートの規則を追加します。 

### <a name="cancel-automatic-seeding-to-forwarder"></a>フォワーダーへの自動シード処理を取り消す

何らかの理由で、2 つの可用性グループを同期する _前に_ フォワーダーの初期化を取り消すことが必要になる場合、フォワーダーの SEEDING_MODE パラメーターを MANUAL に設定することで分散型可用性グループを変更し、すぐにシード処理を取り消します。 グローバル プライマリでコマンドを実行します。 

```sql
-- Cancel automatic seeding.  Connect to global primary but specify DAG AG2
ALTER AVAILABILITY GROUP [distributedag]   
   MODIFY  
   AVAILABILITY GROUP ON  
   'ag2' WITH  
   (  SEEDING_MODE = MANUAL  );   
```

  
## <a name="join-distributed-availability-group-on-second-cluster"></a>2 つ目のクラスターの分散型可用性グループに参加する  
 次に、2 つ目の WSFC の分散型可用性グループに参加します。  
  
```sql  
ALTER AVAILABILITY GROUP [distributedag]   
   JOIN   
   AVAILABILITY GROUP ON  
      'ag1' WITH    
      (   
         LISTENER_URL = 'tcp://ag1-listener.contoso.com:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      ),   
      'ag2' WITH    
      (   
         LISTENER_URL = 'tcp://ag2-listener.contoso.com:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      );    
GO  
```  

## <a name="join-the-database-on-the-secondary-of-the-second-availability-group"></a><a name="failover"></a> 2 つ目の可用性グループのセカンダリ上のデータベースを結合する
2 つ目の可用性グループのセカンダリ レプリカ上のデータベースが復元状態になったら、それを可用性グループに手動で結合する必要があります。

```sql  
ALTER DATABASE [db1] SET HADR AVAILABILITY GROUP = [ag2];   
```
  
## <a name="fail-over-to-a-secondary-availability-group"></a><a name="failover"></a> セカンダリ可用性グループにフェールオーバーする  

現在のところ、手動フェールオーバーのみがサポートされています。 分散型可用性グループを手動でフェールオーバーするには:

1. データが決して失われないようにするには、グローバル プライマリ データベース (つまり、プライマリ可用性グループのデータベース) でのすべてのトランザクションを停止してから、分散型可用性グループを同期コミットに設定します。
1. 分散型可用性グループが同期され、データベースごとの last_hardened_lsn が同じになるまで待機します。 
1. グローバル プライマリ レプリカで、分散型可用性グループのロールを `SECONDARY` に設定します。
1. フェールオーバーの準備ができたかテストします。
1. プライマリ可用性グループにフェールオーバーします。

次の Transact-SQL の例では、`distributedag` という名前の分散可用性グループをフェールオーバーする詳細な手順を示しています。

1. データが決して失われないようにするには、グローバル プライマリ データベース (つまり、プライマリ可用性グループのデータベース) でのすべてのトランザクションを停止します。 次に、グローバル プライマリとフォワーダーの "*両方*" で次のコードを実行して、分散型可用性グループを同期コミットに設定します。   
    
      ```sql  
      -- sets the distributed availability group to synchronous commit 
       ALTER AVAILABILITY GROUP [distributedag] 
       MODIFY 
       AVAILABILITY GROUP ON
       'ag1' WITH 
        ( 
        AVAILABILITY_MODE = SYNCHRONOUS_COMMIT 
        ), 
        'ag2' WITH  
        ( 
        AVAILABILITY_MODE = SYNCHRONOUS_COMMIT 
        );
       
       -- verifies the commit state of the distributed availability group
       select ag.name, ag.is_distributed, ar.replica_server_name, ar.availability_mode_desc, ars.connected_state_desc, ars.role_desc, 
       ars.operational_state_desc, ars.synchronization_health_desc from sys.availability_groups ag  
       join sys.availability_replicas ar on ag.group_id=ar.group_id
       left join sys.dm_hadr_availability_replica_states ars
       on ars.replica_id=ar.replica_id
       where ag.is_distributed=1
       GO

      ```  
   > [!NOTE]
   > 分散型可用性グループでは、2 つの可用性グループが同期された状態であるかどうかは、両方のレプリカの可用性モードに依存します。 同期コミット モードでは、現在のプライマリ可用性グループと現在のセカンダリ可用性グループの両方が、`SYNCHRONOUS_COMMIT` 可用性モードである必要があります。 このため、グローバルのプライマリ レプリカと、フォワーダーの両方で上記のスクリプトを実行する必要があります。


1. 分散型可用性グループの状態が `SYNCHRONIZED` に変化し、すべてのレプリカの (データベースごとの) last_hardened_lsn が同じになるまで待機します。 プライマリ可用性グループのプライマリ レプリカであるグローバル プライマリと、フォワーダーの両方に対して次のクエリを実行することで、synchronization_state_desc と last_hardened_lsn を確認します。 
    
      ```sql  
      -- Run this query on the Global Primary and the forwarder
      -- Check the results to see if synchronization_state_desc is SYNCHRONIZED, and the last_hardened_lsn is the same per database on both the global primary and       forwarder 
      -- If not rerun the query on both side every 5 seconds until it is the case
      --
      SELECT ag.name
             , drs.database_id
             , db_name(drs.database_id) as database_name
             , drs.group_id
             , drs.replica_id
             , drs.synchronization_state_desc
             , drs.last_hardened_lsn  
      FROM sys.dm_hadr_database_replica_states drs 
      INNER JOIN sys.availability_groups ag on drs.group_id = ag.group_id;
      ```  

    可用性グループ **synchronization_state_desc** が `SYNCHRONIZED` になり、さらにグローバル プライマリとフォワーダーの両方でデータベースごとの last_hardened_lsn が同じになったら、先に進みます。  **synchronization_state_desc** が `SYNCHRONIZED` ではない場合、または last_hardened_lsn が同じではない場合は、その状態に変化するまで 5 秒間隔でコマンドを実行します。 **synchronization_state_desc** = `SYNCHRONIZED` となり、かつデータベースごとの last_hardened_lsn が同じになるまで、先に進まないでください。 

1. グローバル プライマリで、分散型可用性グループのロールを `SECONDARY` に設定します。 

    ```sql
    ALTER AVAILABILITY GROUP distributedag SET (ROLE = SECONDARY); 
    ```  

    この時点で、分散型可用性グループは使用できません。

1. フェールオーバーの準備をテストします。 グローバル プライマリとフォワーダーの両方に対して次のクエリを実行します。

    ```sql
     -- Run this query on the Global Primary and the forwarder
     -- Check the results to see if the last_hardened_lsn is the same per database on both the global primary and forwarder 
     -- The availability group is ready to fail over when the last_hardened_lsn is the same for both availability groups per database
     --
     SELECT ag.name, 
         drs.database_id, 
         db_name(drs.database_id) as database_name,
         drs.group_id, 
         drs.replica_id,
         drs.last_hardened_lsn
     FROM sys.dm_hadr_database_replica_states drs
     INNER JOIN sys.availability_groups ag ON drs.group_id = ag.group_id;
    ```  

    可用性グループは、両方の可用性グループにおいてデータベースごとの **last_hardened_lsn** が同じである場合に、フェールオーバーできる状態となります。 一定の時間が経過しても last_hardened_lsn が同じにならない場合は、データの損失を避けるために、グローバル プライマリ上で次のコマンドを実行することでグローバル プライマリにフェールバックして、2 番目の手順からやり直します。 

    ```sql
    -- If the last_hardened_lsn is not the same after a period of time, to avoid data loss, 
    -- we need to fail back to the global primary by running this command on the global primary 
    -- and then start over from the second step:

    ALTER AVAILABILITY GROUP distributedag FORCE_FAILOVER_ALLOW_DATA_LOSS; 
    ```


1. プライマリ可用性グループからセカンダリ可用性グループにフェールオーバーします。 セカンダリ可用性グループのプライマリ レプリカをホストする SQL Server であるフォワーダーに対して、次のコマンドを実行します。 

    ```sql
    -- Once the last_hardened_lsn is the same per database on both sides
    -- We can Fail over from the primary availability group to the secondary availability group. 
    -- Run the following command on the forwarder, the SQL Server instance that hosts the primary replica of the secondary availability group.

    ALTER AVAILABILITY GROUP distributedag FORCE_FAILOVER_ALLOW_DATA_LOSS; 
    ```  

    この手順の後で、分散型可用性グループが使用できるようになります。
      
上記の手順が完了すると、データ損失なしで、分散型可用性グループのフェールオーバーが行われます。 可用性グループ間の地理的な距離が遅延を引き起こす距離にある場合、可用性モードを ASYNCHRONOUS_COMMIT に変更してください。 
  
## <a name="remove-a-distributed-availability-group"></a>分散型可用性グループを削除する  
 次の Transact-SQL ステートメントは、 `distributedag`という分散型可用性グループを削除します。  
  
```sql  
DROP AVAILABILITY GROUP [distributedag]  
```  

## <a name="create-distributed-availability-group-on-failover-cluster-instances"></a>フェールオーバー クラスター インスタンスに分散可用性グループを作成する

フェールオーバー クラスター インスタンス (FCI) で可用性グループを使用して、分散可用性グループを作成することができます。 この場合、可用性グループ リスナーは必要ありません。 FCI インスタンスのプライマリ レプリカに対して仮想ネットワーク名 (VNN) を使用します。 次の例は、SQLFCIDAG と呼ばれる分散型可用性グループを示しています。 1 つの可用性グループは SQLFCIAG です。 SQLFCIAG には、2 つの FCI レプリカがあります。 プライマリ FCI レプリカの VNN は SQLFCIAG-1 であり、セカンダリ FCI レプリカの VNN は SQLFCIAG 2 です。 分散型可用性グループには、ディザスター リカバリーのための SQLAG DR も含まれています。

![分散型の AlwaysOn 可用性グループ](../../../database-engine/availability-groups/windows/media/always-on-availability-group-distributed.png)

 
 
 次の DDL では、この分散可用性グループが作成されます。 

```sql  
CREATE AVAILABILITY GROUP [SQLFCIDAG]  
   WITH (DISTRIBUTED)   
   AVAILABILITY GROUP ON  
  'SQLFCIAG' WITH    
    (   
        LISTENER_URL = 'tcp://SQLFCIAG-1.contoso.com:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC
      ),   
  'SQLAG-DR' WITH    
       (   
         LISTENER_URL = 'tcp://SQLAG-DR.contoso.com:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC
      );   
```  

リスナーの URL は、プライマリ FCI インスタンスの VNN です。

## <a name="manually-fail-over-fci-in-distributed-availability-group"></a>分散型可用性グループで FCI を手動でフェールオーバーする

FCI 可用性グループを手動でフェールオーバーするには、分散型可用性グループを更新してリスナー URL の変更を反映します。 たとえば、SQLFCIAG のプライマリ AG とセカンダリ AG の両方で次の DDL を実行します。

```sql  
ALTER AVAILABILITY GROUP [SQLFCIDAG]  
   MODIFY AVAILABILITY GROUP ON  
 'SQLFCIAG' WITH    
    (   
        LISTENER_URL = 'tcp://SQLFCIAG-2.contoso.com:5022'
    )
```  
  
## <a name="next-steps"></a>次のステップ

 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
