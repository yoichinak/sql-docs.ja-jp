---
description: sys.dm_exec_query_memory_grants (Transact-SQL)
title: dm_exec_query_memory_grants (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 05/19/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_query_memory_grants_TSQL
- sys.dm_exec_query_memory_grants
- sys.dm_exec_query_memory_grants_TSQL
- dm_exec_query_memory_grants
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_memory_grants dynamic management view
ms.assetid: 2c417747-2edd-4e0d-8a9c-e5f445985c1a
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: da496a91a9ed3fa6a391d0862de7eb7fde391480
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546607"
---
# <a name="sysdm_exec_query_memory_grants-transact-sql"></a>sys.dm_exec_query_memory_grants (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  メモリ許可を待機しているか、メモリ許可が与えられている、要求されたすべてのクエリに関する情報を返します。 メモリ許可を必要としないクエリは、このビューに表示されません。 たとえば、並べ替えとハッシュ結合の操作には、クエリの実行にメモリ許可がありますが、 **ORDER by** 句を使用しないクエリにはメモリ許可がありません。  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] では、動的管理ビューは、データベースの包含に影響する情報を公開することも、ユーザーがアクセスできる他のデータベースに関する情報を公開することもできません。 この情報を公開しないように、接続されたテナントに属していないデータを含むすべての行がフィルターで除外されます。また、列 **scheduler_id**、 **wait_order**、 **pool_id**、 **group_id** の値がフィルター処理されます。列の値が NULL に設定されています。  
  
> [!NOTE]  
> またはからこれを呼び出すに [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] は [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 、 **dm_pdw_nodes_exec_query_memory_grants**という名前を使用します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**session_id**|**smallint**|このクエリを実行中のセッションの ID (SPID)。|  
|**request_id**|**int**|要求の ID。 セッションのコンテキスト内で一意です。|  
|**scheduler_id**|**int**|このクエリのスケジュールを設定しているスケジューラの ID。|  
|**dop**|**smallint**|このクエリの並行処理の程度。|  
|**request_time**|**datetime**|このクエリがメモリ許可を要求した日付と時刻。|  
|**grant_time**|**datetime**|このクエリにメモリが許可された日付と時刻。 メモリがまだ許可されていない場合は NULL です。|  
|**requested_memory_kb**|**bigint**|メモリの要求量の合計 (KB 単位)。|  
|**granted_memory_kb**|**bigint**|実際に許可されたメモリの総量 (KB 単位)。 メモリがまだ許可されていない場合、NULL になることがあります。 一般的な状況では、この値は **requested_memory_kb** と同じになります。 インデックス作成では、最初に許可されたメモリ量を超えて、追加のオンデマンド メモリが許可される場合があります。|  
|**required_memory_kb**|**bigint**|このクエリを実行するために必要な最小メモリ (kb 単位)。 **requested_memory_kb** がこの値と同じか、それより大きいです。|  
|**used_memory_kb**|**bigint**|この時点で使用されている物理メモリ (KB 単位)。|  
|**max_used_memory_kb**|**bigint**|この時点までに使用された最大物理メモリ (KB 単位)。|  
|**query_cost**|**float**|推定クエリ コスト。|  
|**timeout_sec**|**int**|このクエリがメモリ許可要求をやめるまでのタイムアウト (秒単位)。|  
|**resource_semaphore_id**|**smallint**|このクエリが待機しているリソース セマフォの非一意の ID。<br /><br /> **注:** この ID は、よりも前のバージョンので一意です [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 。 この変更は、クエリの実行のトラブルシューティングに影響する可能性があります。 詳細については、後の「解説」を参照してください。|  
|**queue_id**|**smallint**|このクエリがメモリ許可を待機している待機キューの ID。 メモリが既に許可されている場合は NULL です。|  
|**wait_order**|**int**|指定した **queue_id** 内の待機キューの順番。 この値は、他のクエリがメモリ許可を取得したり、タイムアウトしたりした場合に、特定のクエリで変更される可能性があります。メモリが既に許可されている場合は NULL です。|  
|**is_next_candidate**|**bit**|次のメモリ許可の候補。<br /><br /> 1 = はい<br /><br /> 0 = いいえ<br /><br /> NULL = メモリが既に許可されている|  
|**wait_time_ms**|**bigint**|待機時間 (ミリ秒単位)。 メモリが既に許可されている場合は NULL です。|  
|**plan_handle**|**varbinary(64)**|このクエリ プランの識別子。 実際の XML プランを抽出するには、**sys.dm_exec_query_plan** を使用します。|  
|**sql_handle**|**varbinary(64)**|このクエリの [!INCLUDE[tsql](../../includes/tsql-md.md)] テキストの識別子。 実際の [!INCLUDE[tsql](../../includes/tsql-md.md)] テキストを取得するには、**sys.dm_exec_sql_text** を使用します。|  
|**group_id**|**int**|このクエリが実行されているワークロード グループの ID。|  
|**pool_id**|**int**|このワークロード グループが属するリソース プールの ID。|  
|**is_small**|**tinyint**|1 に設定すると、この許可で小さなリソース セマフォが使用されます。 0 に設定すると、通常のセマフォが使用されます。|  
|**ideal_memory_kb**|**bigint**|物理メモリ内にすべてを収めるために必要なメモリ許可のサイズ (KB 単位)。 これはカーディナリティの推定値に基づいています。|  
|**pdw_node_id**|**int**|このディストリビューションが配置されているノードの識別子。<br /><br /> **適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] |  
|**reserved_worker_count**|**bigint**|予約済み [ワーカースレッド](../../relational-databases/thread-and-task-architecture-guide.md#sql-server-task-scheduling)の数。<br /><br />**適用対象**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (開始値 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) および [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] |  
|**used_worker_count**|**bigint**|現時点で使用されている [ワーカースレッド](../../relational-databases/thread-and-task-architecture-guide.md#sql-server-task-scheduling) の数。<br /><br />**適用対象**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (開始値 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) および [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**max_used_worker_count**|**bigint**|この時点までに使用された [ワーカースレッド](../../relational-databases/thread-and-task-architecture-guide.md#sql-server-task-scheduling) の最大数。<br /><br />**適用対象**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (開始値 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) および [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**reserved_node_bitmap**|**bigint**|[ワーカースレッド](../../relational-databases/thread-and-task-architecture-guide.md#sql-server-task-scheduling)が予約されている NUMA ノードのビットマップ。<br /><br />**適用対象**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (開始値 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) および [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
  
## <a name="permissions"></a>アクセス許可  

で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   
[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 上では、データベース内の `VIEW DATABASE STATE` アクセス許可が必要です。   
   
## <a name="remarks"></a>解説  
 クエリ タイムアウトの一般的なデバッグ方法は、次のようになります。  
  
-   [sys.dm_os_memory_clerks](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)、[sys.dm_os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)、およびさまざまなパフォーマンス カウンターを使用して、全体的なシステム メモリ状態を調べます。  
  
-   **sys.dm_os_memory_clerks** で、`type = 'MEMORYCLERK_SQLQERESERVATIONS'` であるクエリ実行メモリ予約を調べます。  
  
-   **Sys. dm_exec_query_memory_grants**を使用した許可について<sup>1</sup>を待機しているクエリを確認します。  
  
    ```sql  
    --Find all queries waiting in the memory queue  
    SELECT * FROM sys.dm_exec_query_memory_grants where grant_time is null  
    ```  
    
    <sup>1</sup> このシナリオの場合、待機の種類は一般的に RESOURCE_SEMAPHORE になります。 詳細については、「[sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)」を参照してください。 
  
-   Dm_exec_cached_plans を使用してメモリ許可を持つクエリのキャッシュを検索し [ます。 transact-sql dm_exec_query_plan&#41;&#40;transact-sql ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md) [&#40;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)  
  
    ```sql  
    -- retrieve every query plan from the plan cache  
    USE master;  
    GO  
    SELECT * FROM sys.dm_exec_cached_plans cp CROSS APPLY sys.dm_exec_query_plan(cp.plan_handle);  
    GO  
    ```  
  
-   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md) を使用して、メモリを集中的に使用するクエリをさらに調べます。  
  
    ```sql  
    --Find top 5 queries by average CPU time  
    SELECT TOP 5 total_worker_time/execution_count AS [Avg CPU Time],  
      plan_handle, query_plan   
    FROM sys.dm_exec_query_stats AS qs  
    CROSS APPLY sys.dm_exec_query_plan(qs.plan_handle)  
    ORDER BY total_worker_time/execution_count DESC;  
    GO  
    ```  
  
-   ランナウェイ クエリの疑いがある場合は、[sys.dm_exec_query_plan](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md) のプラン表示と、[sys.dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md) のバッチ テキストを調べます。  
  
 または集計を含む動的管理ビューを使用するクエリで `ORDER BY` は、メモリ使用量が増加し、トラブルシューティングの問題に寄与する場合があります。  
  
 データベース管理者は、リソース ガバナー機能を使用することで、サーバー リソースを最大 64 個までのリソース プールに分散できます。 以降 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] では、各プールは小規模の独立したサーバーインスタンスのように動作し、2つのセマフォが必要です。 **Dm_exec_query_resource_semaphores**から返される行の数は、で返された行より最大で20倍になることがあります [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 。  
  
## <a name="see-also"></a>参照  
 [dm_exec_query_resource_semaphores &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql.md)     
 [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)     
 [実行関連の動的管理ビューおよび関数 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)    
 [スレッドおよびタスクのアーキテクチャ ガイド](../../relational-databases/thread-and-task-architecture-guide.md)   
  
