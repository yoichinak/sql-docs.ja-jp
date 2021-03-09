---
description: sys.dm_os_spinlock_stats (Transact-sql)
title: sys.dm_os_spinlock_stats (Transact-sql)
ms.custom: ''
ms.date: 02/10/2021
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- sys.dm_os_spinlock_stats_TSQL
- dm_os_spinlock_stats_TSQL
- dm_os_spinlock_stats
- sys.dm_os_spinlock_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_spinlock_stats dynamic management view
author: bluefooted
ms.author: pamela
ms.reviewer: wiassaf
manager: amitban
ms.openlocfilehash: 2e48f40003412a2db5340a32e5408f649bf5bb18
ms.sourcegitcommit: 15c7cd187dcff9fc91f2daf0056b12ed3f0403f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2021
ms.locfileid: "102464996"
---
# <a name="sysdm_os_spinlock_stats-transact-sql"></a>sys.dm_os_spinlock_stats (Transact-sql)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

型別に分類されたすべてのスピンロック待機に関する情報を返します。  
  

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|name|**nvarchar (256)**|スピンロックの種類の名前。|  
|発生|**bigint**|現在、別のスレッドがスピンロックを保持しているために、スレッドがスピンロックを取得しようとしてブロックされた回数。|  
|スピン|**bigint**|スピンロックを取得しようとしているときに、スレッドがループを実行する回数。|  
|spins_per_collision|**real**|競合あたりのスピン数の比率。|  
|sleep_time|**bigint**|バックオフが発生した場合にスレッドがスリープに費やした時間 (ミリ秒単位)。|  
|バックオフだけ|**int**|"スピンしている" スレッドがスピンロックの取得に失敗し、スケジューラが生成される回数。|  


## <a name="permissions"></a>アクセス許可  
で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   
SQL Database Basic、S0、S1 のサービス目標、およびエラスティックプール内のデータベースについては、 [サーバー管理者](/azure/azure-sql/database/logins-create-manage#existing-logins-and-user-accounts-after-creating-a-new-database) アカウントまたは [Azure Active Directory 管理者](/azure/azure-sql/database/authentication-aad-overview#administrator-structure) アカウントが必要です。 その他のすべての SQL Database サービスの目的で `VIEW DATABASE STATE` は、データベースで権限が必要になります。    
  
## <a name="remarks"></a>解説  
 
 sys.dm_os_spinlock_stats は、スピンロックの競合の原因を特定するために使用できます。 場合によっては、スピンロックの競合を解決または減少させることができます。 ただし、場合によっては、カスタマーサポートサービスに問い合わせる必要があり [!INCLUDE[msCoName](../../includes/msconame-md.md)] ます。  
  
 次のようにを使用して sys.dm_os_spinlock_stats の内容をリセットでき `DBCC SQLPERF` ます。  
  
```  
DBCC SQLPERF ('sys.dm_os_spinlock_stats', CLEAR);  
GO  
```  
  
 これにより、すべてのカウンターが0にリセットされます。  
  
> [!NOTE]  
>  これらの統計は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が再起動されると保存されません。 すべてのデータは、統計が最後にリセットされた後、またはが開始されてから累積され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
## <a name="spinlocks"></a>スピンロック  
 スピンロックは、通常は短時間保持されるデータ構造へのアクセスをシリアル化するために使用される軽量の同期オブジェクトです。 あるスレッドが、別のスレッドによって保持されているスピンロックによって保護されているリソースにアクセスしようとすると、そのスレッドは、ラッチやその他のリソース待機と同様にスケジューラを直ちに開始するのではなく、ループを実行し、"スピン" してリソースへのアクセスを再試行します。 スレッドは、リソースが使用可能になるかループが完了するまでスピンし続け、その時点でスレッドがスケジューラを生成して実行可能キューに戻ります。 これにより、スレッドコンテキストの過度の切り替えを減らすことができますが、スピンロックの競合が高くなると、CPU 使用率が著しく低下する可能性があります。

> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Intel Skylake プロセッサにがインストールされている場合は、[この記事](https://support.microsoft.com/topic/kb4538688-fix-severe-spinlock-contention-occurs-in-sql-server-2019-43faea65-fdcb-6835-f7fe-93abdb235837)を参照して必要な更新プログラムを適用し、トレースフラグ8101を有効にしてください。

 次の表に、最も一般的なスピンロックの種類の簡単な説明を示します。  
  
|スピンロックの種類|説明|  
|-----------------|-----------------|  
|ABR|内部使用のみ。|
|ADB_CACHE|内部使用のみ。|
|ALLOC_CACHES_HASH|内部使用のみ。|
|APPENDONLY_STORAGE|内部使用のみ。|
|APRC_BACK_OFF_STATS|内部使用のみ。|
|APRC_EVENT_LIST|内部使用のみ。|
|APRC_QUEUE_LIST|内部使用のみ。|
|APRC_VALIDATION_QUEUE_LIST|内部使用のみ。|
|ASYNC_OP_ADMIN_CLIENT_REGISTRATION_LIST|内部使用のみ。|
|ASYNC_OP_ADMIN_WORK_REGISTRATION_HASH_TABLE|内部使用のみ。|
|ASYNCSTATSLIST 場合|内部使用のみ。|
|BACKUP|内部使用のみ。|
|BACKUP_COPY_CONTEXT|内部使用のみ。|
|BACKUP_CTX|内部使用のみ。|
|BASE_XACT_HASH|内部使用のみ。|
|BLOCKER_ENUM|内部使用のみ。|
|BPREPARTITION|内部使用のみ。|
|BPWORKFILE|内部使用のみ。|
|BUF_HASH|内部使用のみ。|
|BUF_LINK|内部使用のみ。|
|BUF_WRITE_LOG|内部使用のみ。|
|CACHEOBJ_DBG|内部使用のみ。|
|CHANNELFORCECLOSEMANAGER|内部使用のみ。|
|CHECK_AGGREGATE_STATE|内部使用のみ。|
|CLR_HOSTTASK|内部使用のみ。|
|CLR_SPIN_LOCK|内部使用のみ。|
|CMED_DATABASE|内部使用のみ。|
|CMED_HASH_SET|内部使用のみ。<br><br>**適用対象:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[sssql16-md](../../includes/sssql16-md.md)] CU1 経由)<br><br> **注:** このスピンロックの名前は [SQL Server 2016 CU2](https://support.microsoft.com/topic/kb3195888-fix-high-cpu-usage-causes-performance-issues-in-sql-server-2016-and-2017-9514b80d-938f-e179-3131-74e6c757c4d5)を適用した後に LOCK_RW_CMED_HASH_SET に変わります。|
|COLUMNDATASETSESSIONLIST|内部使用のみ。|
|COLUMNSTORE_HASHTABLE|内部使用のみ。|
|COLUMNSTOREBUILDSTATE_LIST|内部使用のみ。|
|COM_INIT|内部使用のみ。|
|コミットでき|内部使用のみ。|
|COMPPLAN_SKELETON|内部使用のみ。|
|CONNECTION_MANAGER|内部使用のみ。|
|接続|内部使用のみ。|
|CSIBUILDMEM|内部使用のみ。|
|CURSOR|内部使用のみ。|
|CURSQL|内部使用のみ。|
|DATAPORTCONSUMER|内部使用のみ。|
|DATAPORTSOURCEINFOCREDIT|内部使用のみ。|
|DATAPORTSOURCEINFOQUEUE|内部使用のみ。|
|DATASET_FREELIST|内部使用のみ。|
|DBCC_CHECK|内部使用のみ。|
|DBSEEDING_OPERATION|内部使用のみ。|
|DBT_HASH|内部使用のみ。|
|DBT_IO_LIST|内部使用のみ。|
|DBTABLE|データベースのプロパティを格納している内のすべてのデータベースに対するメモリ内データ構造へのアクセスを制御し [!INCLUDE[ssde_md](../../includes/ssde_md.md)] ます。 詳細については、[この記事](https://techcommunity.microsoft.com/t5/SQL-Server/Improving-Concurrency-Scalability-of-SQL-Server-workload-by/ba-p/384789)を参照してください。 |
|DEFERRED_WF_EXT_DROP|内部使用のみ。|
|DEK_INSTANCE|内部使用のみ。|
|DELAYED_PARTITIONED_STACK|内部使用のみ。|
|DELETEBITMAP|内部使用のみ。|
|DIAG_MANAGER|内部使用のみ。|
|DIAG_OBJECT|内部使用のみ。|
|DIGEST_CACHE|内部使用のみ。|
|DINPBUF|内部使用のみ。|
|DIRECTLOGCONSUMER|内部使用のみ。|
|DP_LIST|間接チェックポイントが有効になっているデータベースのダーティページの一覧へのアクセスを制御します。 [記事 4497928](https://support.microsoft.com/kb/4497928)、[記事 4040276](https://support.microsoft.com/kb/4040276)の修正プログラムを適用するか、[トレースフラグ 3468](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)を使用します。 詳細については、[この記事](https://techcommunity.microsoft.com/t5/SQL-Server/Indirect-Checkpoint-and-tempdb-8211-the-good-the-bad-and-the-non/ba-p/385510)を参照してください。|
|DROP|内部使用のみ。|
|DROP_TEMPO|内部使用のみ。|
|DROPPED_ALLOC_UNIT|内部使用のみ。|
|DTC_HASHTABLE|内部使用のみ。|
|DTT_LIST|内部使用のみ。|
|ENDD_LIST|内部使用のみ。|
|EXT_CACHE|内部使用のみ。|
|EXTENT_ACTIVATION|内部使用のみ。|
|FABRIC_DB_MGR_PTR|内部使用のみ。|
|FABRIC_LOG_MANAGEMENT_INPUT_VALUE|内部使用のみ。|
|FABRIC_REPLICA_TRANSPORT|内部使用のみ。|
|FABRIC_TVF_DATA_CONSUMER_LIST|内部使用のみ。|
|FABRIC_TVF_LOAD_LIB|内部使用のみ。|
|FCB_REPLICA_SYNC|内部使用のみ。|
|FGCB_PRP_FILL|内部使用のみ。|
|FILE_HANDLE_CACHE|内部使用のみ。|
|FILE_TABLE|内部使用のみ。|
|FILESTREAM_CHUNKER|内部使用のみ。|
|FREE_SPACE_CACHE_ENTRY|内部使用のみ。|
|FS_CONTAINER_LIST_WITH_DELETE|内部使用のみ。|
|FS_DELETED_FOLDER_CLEANUP|内部使用のみ。|
|FSAGENT|内部使用のみ。|
|FSGHOST_STATUS|内部使用のみ。|
|FT_INIT|内部使用のみ。|
|GHOST_FREE|内部使用のみ。|
|GHOST_HASH|内部使用のみ。|
|GLOBAL_SCHEDULER_LIST|内部使用のみ。|
|GLOBAL_TRACE_FLAGS|内部使用のみ。|
|GLOBALTRANS|内部使用のみ。|
|GROUP_COMMIT_FEEDBACK_LOOP|内部使用のみ。|
|GUARDIAN|内部使用のみ。|
|HADR_AGH_X_ACCESS|内部使用のみ。|
|HADR_AR_CONTROLLER_COLLECTION|内部使用のみ。|
|HADR_AR_DB_MGR|内部使用のみ。|
|HADR_AR_TRANSPORT|内部使用のみ。|
|HADR_COMPRESSION_MGR_POOL|内部使用のみ。|
|HADR_FABRIC_FACTORY|内部使用のみ。|
|HADR_PRIORITY_QUEUE|内部使用のみ。|
|HADR_TRANSPORT_CONTROL|内部使用のみ。|
|HADR_TRANSPORT_LIST|内部使用のみ。|
|HADRSEEDINGLIST|内部使用のみ。|
|HOBT_DROPPED|内部使用のみ。|
|HOBT_HASH|内部使用のみ。|
|HTTP|内部使用のみ。|
|HTTP_CONNCACHE|内部使用のみ。|
|HTTP_ENDPOINT|内部使用のみ。|
|IDENTITY|内部使用のみ。|
|INDEX_CREATE|内部使用のみ。|
|IO_DISPENSER_PAUSE|内部使用のみ。|
|IO_RG_VOLUME_HASHTABLE|内部使用のみ。|
|IOREQ|内部使用のみ。|
|ISSRESOURCE|内部使用のみ。|
|KTM_ENLISTMENT|内部使用のみ。|
|LANG_RES_LOAD|内部使用のみ。|
|LIVE_TARGET_TVF|内部使用のみ。|
|LOCK_FREE_LIST|内部使用のみ。|
|LOCK_HASH|データベースに保持されているロックに関する情報を格納するロックマネージャーハッシュテーブルへのアクセスを保護します。 詳細については、 [この記事](https://support.microsoft.com/kb/2926217) と、 [トランザクションのロックおよび行のバージョン管理](../../relational-databases/sql-server-transaction-locking-and-row-versioning-guide.md#Lock_Engine)に関するガイドを参照してください。|
|LOCK_NOTIFICATION|内部使用のみ。|
|LOCK_RESOURCE_ID|内部使用のみ。|
|LOCK_RW_ABTX_HASH_SET|内部使用のみ。|
|LOCK_RW_AGDB_HEALTH_DIAG|内部使用のみ。|
|LOCK_RW_CMED_HASH_SET|内部使用のみ。<br><br>**適用対象:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (以降 [!INCLUDE[sssql16-md](../../includes/sssql16-md.md)] CU2)、 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 、および [!INCLUDE[ssSDSMIfull](../../includes/sssdsmifull-md.md)]|
|LOCK_RW_DPT_TABLE|内部使用のみ。|
|LOCK_RW_IN_ROW_TRACKER|内部使用のみ。|
|LOCK_RW_LOGIN_RATE_STATS|内部使用のみ。|
|LOCK_RW_PVS_PAGE_TRACKER|内部使用のみ。|
|LOCK_RW_RBIO_REQ|内部使用のみ。|
|LOCK_RW_SECURITY_CACHE|セキュリティトークンとアクセスチェックに関連するキャッシュエントリを保護します。 <br><br>**適用対象:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (以降 [!INCLUDE[sssql16-md](../../includes/sssql16-md.md)] CU2)、 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 、および [!INCLUDE[ssSDSMIfull](../../includes/sssdsmifull-md.md)]<br><br> TokenAndPermUserStore cache ストア内のエントリが継続的に増加している場合は、このスピンロックの大きなスピンに気付くことがあります。 [トレースフラグ](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)4610 と4618を使用して、エントリを制限するように評価します。 詳細については、「 [access check Cache サーバー構成オプション](../../database-engine/configure-windows/access-check-cache-server-configuration-options.md)」、この [記事](https://support.microsoft.com/topic/queries-take-a-longer-time-to-finish-running-when-the-size-of-the-tokenandpermuserstore-cache-grows-in-sql-server-2005-ad1622e7-3bb5-7902-19a0-5d0e6271033d)、およびこの [ブログ](https://techcommunity.microsoft.com/t5/sql-server-support/query-performance-issues-associated-with-a-large-sized-security/ba-p/315494)を参照してください。|
|LOCK_RW_TEST|内部使用のみ。|
|LOCK_RW_WPR_BUCKET|内部使用のみ。|
|LOCK_SORT_STREAM|内部使用のみ。|
|LOCK_SQLSATELLITE_MESSAGE|内部使用のみ。|
|LOG_CONSOLIDATION|内部使用のみ。|
|LOG_RG_GOVERNOR|内部使用のみ。|
|LOGCACHE_ACCESS|内部使用のみ。|
|LOGFLUSHQ|内部使用のみ。|
|LOGIOSEQ|内部使用のみ。|
|LOGIOSEQMAPPENDINGMESSAGEQUEUE|内部使用のみ。|
|LOGLC|内部使用のみ。|
|LOGLFM|内部使用のみ。|
|LOGON_TRIGGER_CACHE|内部使用のみ。|
|LOGPOOL_HASHBUCKET|内部使用のみ。|
|LOGPOOL_REFCOUNTEDOBJECT|内部使用のみ。|
|LOGPOOL_SHAREDCACHEBUFFER|内部使用のみ。|
|LOGPOOL_SIZEPERRESOURCEPOOL|内部使用のみ。|
|LPE_BATCH|内部使用のみ。|
|LPE_SESSION|内部使用のみ。|
|LPE_SXTP|内部使用のみ。|
|LSID|内部使用のみ。|
|LSLIST|内部使用のみ。|
|LSNREFLIST|内部使用のみ。|
|LSS_SYNC_DTC|内部使用のみ。|
|MD_CHANGE_NOTIFICATION|内部使用のみ。|
|MDB_REMOTE_BATCH_STATS_HASH_TABLE|内部使用のみ。|
|MDB_REMOTE_SESSION_HASH_TABLE|内部使用のみ。|
|MEM_MGR|内部使用のみ。|
|MGR_CACHE|内部使用のみ。|
|MIGRATION_BUF_LIST|内部使用のみ。|
|ロック|セキュリティトークンとアクセスチェックに関連するキャッシュエントリを保護します。 <br><br>**適用対象:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (最大 [!INCLUDE[sssql11-md](../../includes/sssql11-md.md)] )<br><br>TokenAndPermUserStore cache ストア内のエントリが継続的に増加している場合は、このスピンロックの大きなスピンに気付くことがあります。 [トレースフラグ](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)4610 と4618を使用して、エントリを制限するように評価します。 詳細については、「 [access check Cache サーバー構成オプション](../../database-engine/configure-windows/access-check-cache-server-configuration-options.md)」、この [記事](https://support.microsoft.com/topic/queries-take-a-longer-time-to-finish-running-when-the-size-of-the-tokenandpermuserstore-cache-grows-in-sql-server-2005-ad1622e7-3bb5-7902-19a0-5d0e6271033d)、およびこの [ブログ](https://techcommunity.microsoft.com/t5/sql-server-support/query-performance-issues-associated-with-a-large-sized-security/ba-p/315494)を参照してください。|
|NETCONN_ADDRESS|内部使用のみ。|
|ONDEMAND_TASK|内部使用のみ。|
|ONE_PROC_SIM_NODE_CONTEXT|内部使用のみ。|
|ONE_PROC_SIM_NODE_CONTEXT_LIST|内部使用のみ。|
|ONE_PROC_SIM_REPLICA_CONTEXT|内部使用のみ。|
|ONE_PROC_SIM_SERVICE_PARTITION|内部使用のみ。|
|OPT_IDX_MISS_ID|内部使用のみ。|
|OPT_IDX_MISS_KEY|内部使用のみ。|
|OPT_IDX_STATS|内部使用のみ。|
|OPT_INFO_MGR|内部使用のみ。|
|PAGE_WORKITEMLIST|内部使用のみ。|
|PAGECOPIER|内部使用のみ。|
|PARALLELREDOCACHE|内部使用のみ。|
|PARTITIONED_HEAP_FREE_LIST|内部使用のみ。|
|PROGRESS_REPORT|内部使用のみ。|
|QE_SHUTDOWN|内部使用のみ。|
|QSCAN_CACHE|内部使用のみ。|
|QUERY_EXEC_STATS|内部使用のみ。|
|QUERY_STORE_ASYNC_PERSIST|内部使用のみ。|
|QUERY_STORE_ASYNC_QUEUE_TLIST|内部使用のみ。|
|QUERY_STORE_CAPTURE_POLICY_INTERVAL|内部使用のみ。|
|QUERY_STORE_CAPTURE_POLICY_STATS|内部使用のみ。|
|QUERY_STORE_CAPTURE_POLICY_THRESHOLD|内部使用のみ。|
|QUERY_STORE_CURRENT_INTERVAL|内部使用のみ。|
|QUERY_STORE_HT_CACHE|内部使用のみ。|
|QUERY_STORE_LIST|内部使用のみ。|
|QUERY_STORE_PLAN_COMP_AGG|内部使用のみ。|
|QUERY_STORE_PLAN_LIST|内部使用のみ。|
|QUERY_STORE_READ_ONLY_FLAGS|内部使用のみ。|
|QUERY_STORE_SELF_AGG|内部使用のみ。|
|QUERY_STORE_STMT_COMP_AGG|内部使用のみ。|
|QUERYEXEC|内部使用のみ。|
|QUERYSCAN|内部使用のみ。|
|RANGE_GENERATION|内部使用のみ。|
|READ_AHEAD|内部使用のみ。|
|REDOMGRSTATE|内部使用のみ。|
|REMOTE_SESSION_CACHE|内部使用のみ。|
|REMOTEBLOCKIO|内部使用のみ。|
|REMOTEOP|内部使用のみ。|
|REPL_LOGREADER_HISTORY_CACHE|内部使用のみ。|
|REPL_LOGREADER_PERDB_HISTORY_CACHE|内部使用のみ。|
|RESMANAGER|内部使用のみ。|
|リソース|内部使用のみ。|
|RESQUEUE|内部使用のみ。|
|RFS_THREAD_QUEUE|内部使用のみ。|
|RG_TIMER|内部使用のみ。|
|ROWGROUP_VERSIONS|内部使用のみ。|
|RPCCHANNELPOOL|内部使用のみ。|
|RPCPACKAGE|内部使用のみ。|
|RPCREQUESTORCONTEXT|内部使用のみ。|
|RWLOCK_LAST|内部使用のみ。|
|SATELLITE_CONNECTION|内部使用のみ。|
|SBS_CLIENT_ENDPOINTS|内部使用のみ。|
|SBS_CLIENT_REQUESTS|内部使用のみ。|
|SBS_DISPATCH|内部使用のみ。|
|SBS_PENDING|内部使用のみ。|
|SBS_SERVER_XACT_TASK_PROXY|内部使用のみ。|
|SBS_TRANSPORT|内部使用のみ。|
|SBS_UCS_DISPATCH|内部使用のみ。|
|セキュリティ|内部使用のみ。|
|SECURITY_CACHE|セキュリティトークンとアクセスチェックに関連するキャッシュエントリを保護します。 <br><br>**適用対象:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[sssql16-md](../../includes/sssql16-md.md)] CU1 経由)<br><br> TokenAndPermUserStore cache ストア内のエントリが継続的に増加している場合は、このスピンロックの大きなスピンに気付くことがあります。 [トレースフラグ](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)4610 と4618を使用して、エントリを制限するように評価します。 詳細については、「 [access check Cache サーバー構成オプション](../../database-engine/configure-windows/access-check-cache-server-configuration-options.md)」、この [記事](https://support.microsoft.com/topic/queries-take-a-longer-time-to-finish-running-when-the-size-of-the-tokenandpermuserstore-cache-grows-in-sql-server-2005-ad1622e7-3bb5-7902-19a0-5d0e6271033d)、およびこの [ブログ](https://techcommunity.microsoft.com/t5/sql-server-support/query-performance-issues-associated-with-a-large-sized-security/ba-p/315494)を参照してください。<br><br>**注:** このスピンロックの名前は [SQL Server 2016 CU2](https://support.microsoft.com/topic/kb3195888-fix-high-cpu-usage-causes-performance-issues-in-sql-server-2016-and-2017-9514b80d-938f-e179-3131-74e6c757c4d5)を適用した後に LOCK_RW_SECURITY_CACHE に変わります。|
|SECURITY_FEDAUTH_AAD_BECWSCONNS|内部使用のみ。|
|SEMANTIC_TICACHE|内部使用のみ。|
|SEQUENCED_OBJECT|内部使用のみ。|
|SEQUEUE_SIZED_THREADSAFE|内部使用のみ。|
|SESSION_KILLER|内部使用のみ。|
|SESSION_MANAGER|内部使用のみ。|
|SESSION_SEC_CONTEXT|内部使用のみ。|
|SETRANGE_SYNC|内部使用のみ。|
|SHARABLE_SESSION_OBJECTS|内部使用のみ。|
|SLO_INFO_LIST|内部使用のみ。|
|SNI|内部使用のみ。|
|SNI_NODE_PENDING_IO_QUEUE|内部使用のみ。|
|SOAPSESSIONS|内部使用のみ。|
|SOS_ABORT_TASK|内部使用のみ。|
|SOS_ACTIVEDESCRIPTOR|内部使用のみ。|
|SOS_BLOCKALLOCPARTIALLIST|内部使用のみ。|
|SOS_BLOCKDESCRIPTORBUCKET|内部使用のみ。|
|SOS_CACHESTORE|プランキャッシュや一時テーブルキャッシュなど、内のさまざまなメモリ内キャッシュへのアクセスを同期し [!INCLUDE[ssde_md](../../includes/ssde_md.md)] ます。 このスピンロックの種類の競合が多い場合は、競合している特定のキャッシュに応じて、さまざまなことを意味します。 [!INCLUDE[msCoName](../../includes/msconame-md.md)]このスピンロックの種類のトラブルシューティングについては、カスタマーサポートサービスにお問い合わせください。 |
|SOS_CACHESTORE_CLOCK|内部使用のみ。|
|SOS_CLOCKALG_INTERNODE_SYNC|内部使用のみ。|
|SOS_DEBUG_HOOK|内部使用のみ。|
|SOS_DESCDATABUFFERLIST|内部使用のみ。|
|SOS_LARGEPAGE_ALLOCATOR|内部使用のみ。|
|SOS_MINITHREAD|内部使用のみ。|
|SOS_NODE|内部使用のみ。|
|SOS_OBJECT_POOL|内部使用のみ。|
|SOS_OBJECT_STORE|内部使用のみ。|
|SOS_OOM_CHECK|内部使用のみ。|
|SOS_PHYS_PAGE_CACHE|内部使用のみ。|
|SOS_RESOURCE_CLERK_LIST|内部使用のみ。|
|SOS_RINGBUFFER_RECORD|内部使用のみ。|
|SOS_RW|内部使用のみ。|
|SOS_SATELLITE_USER_POOL|内部使用のみ。|
|SOS_SCHEDULER|内部使用のみ。|
|SOS_SELIST_SIZED_SLOCK|内部使用のみ。|
|SOS_SUSPEND_QUEUE|内部使用のみ。|
|SOS_SYSTHREAD|内部使用のみ。|
|SOS_SYSTHREAD_DISPATCHER|内部使用のみ。|
|SOS_TASK|内部使用のみ。|
|SOS_TLIST|内部使用のみ。|
|SOS_VM_LOW|内部使用のみ。|
|SOS_WAIT_STATS|内部使用のみ。|
|SOS_WAITABLE_ADDRESS_HASHBUCKET|内部使用のみ。|
|SPIN_EVENT_MUTEX|内部使用のみ。|
|SPL_DISPATCHER_LIST|内部使用のみ。|
|SPL_DISPATCHER_QUEUE|内部使用のみ。|
|SPL_NONYIELD_ANALYSIS|内部使用のみ。|
|SPL_QUERY_STORE_CTX_INITIALIZED|内部使用のみ。|
|SPL_QUERY_STORE_EXEC_STATS_AGG|内部使用のみ。|
|SPL_QUERY_STORE_EXEC_STATS_READ|内部使用のみ。|
|SPL_QUERY_STORE_STATS_COOKIE_CACHE|内部使用のみ。|
|SPL_SOS_DISPATCHER|内部使用のみ。|
|SPL_TDS_PKT_QUEUE|内部使用のみ。|
|SPL_XE_BUFFER_MGR|内部使用のみ。|
|SPL_XE_DISPATCHER_QUEUE|内部使用のみ。|
|SPL_XE_NOTIFICATION_CALLBACK_LIST|内部使用のみ。|
|SPL_XE_SESSION_EVENT_MGR|内部使用のみ。|
|SPL_XE_SESSION_MGR|内部使用のみ。|
|SPL_XE_SESSION_TARGET_MGR|内部使用のみ。|
|SPT_PROFILE|内部使用のみ。|
|SQL_MGR|内部使用のみ。|
|SQL_NORM|内部使用のみ。|
|SQLTRACE_FILE_BUFFER|内部使用のみ。|
|SRVPROC|内部使用のみ。|
|STACK_HASHER|内部使用のみ。|
|SUBLATCH|内部使用のみ。|
|SUBPDESC|内部使用のみ。|
|SUBPDESC_LIST|内部使用のみ。|
|SVC_BROKER_CTRL|内部使用のみ。|
|SVC_BROKER_DEBUG_LIST|内部使用のみ。|
|SVC_BROKER_LIST|内部使用のみ。|
|SVC_BROKER_OBJECT|内部使用のみ。|
|SYNCPOINT_RESOURCE|内部使用のみ。|
|TaskElapsedExecutionMonitor|内部使用のみ。|
|TDS_TVP|内部使用のみ。|
|TESTTEAM|内部使用のみ。|
|TESTTEAMEXPONENTIAL|内部使用のみ。|
|TESTTEAMEXPONENTIALTASTAS|内部使用のみ。|
|TESTTEAMTASTAS|内部使用のみ。|
|TMP_SESS_KEY|内部使用のみ。|
|TSQL_DEBUG|内部使用のみ。|
|TXFRM_REPL|内部使用のみ。|
|VDI_OPERATION|内部使用のみ。|
|WINFAB_REPORT_FAULT|内部使用のみ。|
|WRITE_PAGE_RECORDER|内部使用のみ。|
|X_PACKET_LIST|内部使用のみ。|
|X_PIPE|内部使用のみ。|
|X_PIPE_DEMAND|内部使用のみ。|
|X_PORT|内部使用のみ。|
|XACT_LOCK_INFO|内部使用のみ。|
|XACT_LOCKINFO_TASK|内部使用のみ。|
|XACT_WORKSPACE|内部使用のみ。|
|XCB|内部使用のみ。|
|XCB_FREE_LIST|内部使用のみ。|
|XCB_HASH|内部使用のみ。|
|XCHNG_TRACE|内部使用のみ。|
|XDES|内部使用のみ。|
|XDES_HASH|内部使用のみ。|
|XDESMGR|内部使用のみ。|
|XDESTABLELIST|内部使用のみ。|
|XE_RATE_LIMITER_STRETCHDB|内部使用のみ。|
|XE_SESSION_STORAGE|内部使用のみ。|
|XID_ARRAY|内部使用のみ。|
|XIO_BLOCKLIST|内部使用のみ。|
|XIO_REQSTR|内部使用のみ。|
|XIO_SEQNUMBUMP|内部使用のみ。|
|XIOSTATS|内部使用のみ。|
|XTP_RT_DATA_LIST|内部使用のみ。|
|XTS_MGR|内部使用のみ。|
|XVB_CSN|内部使用のみ。|
|XVB_LIST|内部使用のみ。|
 
## <a name="see-also"></a>参照  
 
 [DBCC SQLPERF &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)   
 
 [SQL Server オペレーティングシステム関連の動的管理ビュー &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  

 [スピンロックが SQL Server の CPU 使用率の重要なドライバーです。](https://techcommunity.microsoft.com/t5/SQL-Server-Support/When-is-Spinlock-a-Significant-Driver-of-CPU-utilization-in-SQL/ba-p/530142)

 [SQL Server でのスピンロックの競合の診断と解決](../diagnose-resolve-spinlock-contention.md)
  
