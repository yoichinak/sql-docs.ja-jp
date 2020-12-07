---
title: システム ビュー
description: 分析プラットフォームシステム (APS) SQL Server 並列データウェアハウス (PDW) のシステムビュー。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 87a6585d225617889c32167fdebcc79bd89c761c
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987208"
---
# <a name="system-views-for-analytics-platform-system-parallel-data-warehouse"></a>Analytics Platform System Parallel Data Warehouse のシステムビュー
分析プラットフォームシステム (APS) SQL Server 並列データウェアハウス (PDW) のシステムビュー。

## <a name="parallel-data-warehouse-catalog-views"></a>並列データウェアハウスのカタログビュー
* [sys.pdw_column_distribution_properties](../relational-databases/system-catalog-views/sys-pdw-column-distribution-properties-transact-sql.md?view=aps-pdw-2016-au7)
* [sys.pdw_database_mappings](../relational-databases/system-catalog-views/sys-pdw-database-mappings-transact-sql.md?view=aps-pdw-2016-au7)
* [sys.pdw_distributions](../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md?view=aps-pdw-2016-au7)
* [sys.pdw_index_mappings](../relational-databases/system-catalog-views/sys-pdw-index-mappings-transact-sql.md?view=aps-pdw-2016-au7)
* [sys.pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)
* [sys.pdw_loader_backup_runs](../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)
* [sys.pdw_nodes_column_store_dictionaries](../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-dictionaries-transact-sql.md?view=aps-pdw-2016-au7)
* [sys.pdw_nodes_column_store_row_groups](../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-row-groups-transact-sql.md?view=aps-pdw-2016-au7)
* [sys.pdw_nodes_column_store_segments](../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-segments-transact-sql.md?view=aps-pdw-2016-au7)
* [sys.pdw_nodes_columns](../relational-databases/system-catalog-views/sys-pdw-nodes-columns-transact-sql.md?view=aps-pdw-2016-au7)
* [sys.pdw_nodes_indexes](../relational-databases/system-catalog-views/sys-pdw-nodes-indexes-transact-sql.md?view=aps-pdw-2016-au7)
* [sys.pdw_nodes_partitions](../relational-databases/system-catalog-views/sys-pdw-nodes-partitions-transact-sql.md?view=aps-pdw-2016-au7)
* [sys.pdw_nodes_pdw_physical_databases](../relational-databases/system-catalog-views/sys-pdw-nodes-pdw-physical-databases-transact-sql.md?view=aps-pdw-2016-au7)
* [sys.pdw_nodes_tables](../relational-databases/system-catalog-views/sys-pdw-nodes-tables-transact-sql.md?view=aps-pdw-2016-au7)
* [sys.pdw_table_distribution_properties](../relational-databases/system-catalog-views/sys-pdw-table-distribution-properties-transact-sql.md?view=aps-pdw-2016-au7)
* [sys.pdw_table_mappings](../relational-databases/system-catalog-views/sys-pdw-table-mappings-transact-sql.md?view=aps-pdw-2016-au7)

## <a name="parallel-data-warehouse-dynamic-management-views-dmvs"></a>並列データウェアハウスの動的管理ビュー (Dmv)
* [sys.dm_pdw_dms_cores](../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-cores-transact-sql.md?view=aps-pdw-2016-au7)
* [sys.dm_pdw_dms_external_work](../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-external-work-transact-sql.md)
* [sys.dm_pdw_dms_workers](../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md?view=aps-pdw-2016-au7)
* [sys.dm_pdw_errors](../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md?view=aps-pdw-2016-au7)
* [sys.dm_pdw_exec_connections](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-connections-transact-sql.md?view=aps-pdw-2016-au7)
* [sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md?view=aps-pdw-2016-au7)
* [sys.dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md?view=aps-pdw-2016-au7)
* [sys.dm_pdw_hadoop_operations](../relational-databases/system-dynamic-management-views/sys-dm-pdw-hadoop-operations-transact-sql.md)
* [sys.dm_pdw_lock_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-lock-waits-transact-sql.md?view=aps-pdw-2016-au7)
* [sys.dm_pdw_nodes](../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md?view=aps-pdw-2016-au7)
* [sys.dm_pdw_nodes_database_encryption_keys](../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql.md?view=aps-pdw-2016-au7)
* [sys.dm_pdw_os_threads](../relational-databases/system-dynamic-management-views/sys-dm-pdw-os-threads-transact-sql.md?view=aps-pdw-2016-au7)
* [sys.dm_pdw_request_steps](../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md?view=aps-pdw-2016-au7)
* [sys.dm_pdw_resource_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md?view=aps-pdw-2016-au7)
* [sys.dm_pdw_sql_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-sql-requests-transact-sql.md?view=aps-pdw-2016-au7)
* [sys.dm_pdw_sys_info](../relational-databases/system-dynamic-management-views/sys-dm-pdw-sys-info-transact-sql.md?view=aps-pdw-2016-au7)
* [sys.dm_pdw_wait_stats](../relational-databases/system-dynamic-management-views/sys-dm-pdw-wait-stats-transact-sql.md?view=aps-pdw-2016-au7)
* [sys.dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-wait-stats-transact-sql.md?view=aps-pdw-2016-au7)

## <a name="sql-server-dmvs-applicable-to-parallel-data-warehouse"></a>並列データウェアハウスに適用可能な SQL Server Dmv
次の Dmv は並列データウェアハウスに適用できますが、 **master** データベースに接続することによって実行する必要があります。

* [sys.database_service_objectives](../relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database.md)
* [sys.dm_operation_status](../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)
* [sys.fn_helpcollations()](../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)

## <a name="sql-server-catalog-views"></a>SQL Server カタログ ビュー
* [sys.all_columns](../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md?view=sql-server-ver15)
* [sys.all_objects](../relational-databases/system-catalog-views/sys-all-objects-transact-sql.md?view=sql-server-ver15)
* [sys.all_parameters](../relational-databases/system-catalog-views/sys-all-parameters-transact-sql.md?view=sql-server-ver15)
* [sys.all_sql_modules](../relational-databases/system-catalog-views/sys-all-sql-modules-transact-sql.md?view=sql-server-ver15)
* [sys.all_views](../relational-databases/system-catalog-views/sys-all-views-transact-sql.md?view=sql-server-ver15)
* [sys.assemblies](../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md?view=sql-server-ver15)
* [sys.assembly_modules](../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md?view=sql-server-ver15)
* [sys.assembly_types](../relational-databases/system-catalog-views/sys-assembly-types-transact-sql.md?view=sql-server-ver15)
* [sys.certificates](../relational-databases/system-catalog-views/sys-certificates-transact-sql.md?view=sql-server-ver15)
* [sys.check_constraints](../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md?view=sql-server-ver15)
* [sys.columns](../relational-databases/system-catalog-views/sys-columns-transact-sql.md?view=sql-server-ver15)
* [sys.computed_columns](../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md?view=sql-server-ver15)
* [sys.credentials](../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)
* [sys.data_spaces](../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md?view=sql-server-ver15)
* [sys.database_credentials](../relational-databases/system-catalog-views/sys-database-credentials-transact-sql.md)
* [sys.database_files](../relational-databases/system-catalog-views/sys-database-files-transact-sql.md?view=sql-server-ver15)
* [sys.database_permissions](../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md?view=sql-server-ver15)
* [sys.database_principals](../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md?view=sql-server-ver15)
* [sys.database_role_members](../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md?view=sql-server-ver15)
* [sys.databases](../relational-databases/system-catalog-views/sys-databases-transact-sql.md?view=sql-server-ver15)
* [sys.default_constraints](../relational-databases/system-catalog-views/sys-default-constraints-transact-sql.md?view=sql-server-ver15)
* [sys.external_data_sources](../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md?view=sql-server-ver15)
* [sys.external_file_formats](../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md?view=sql-server-ver15)
* [sys.external_tables](../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md?view=sql-server-ver15)
* [sys.filegroups](../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md?view=sql-server-ver15)
* [sys.foreign_key_columns](../relational-databases/system-catalog-views/sys-foreign-key-columns-transact-sql.md?view=sql-server-ver15)
* [sys.foreign_keys](../relational-databases/system-catalog-views/sys-foreign-keys-transact-sql.md?view=sql-server-ver15)
* [sys.identity_columns](../relational-databases/system-catalog-views/sys-identity-columns-transact-sql.md?view=sql-server-ver15)
* [sys.index_columns](../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md?view=sql-server-ver15)
* [sys.indexes](../relational-databases/system-catalog-views/sys-indexes-transact-sql.md?view=sql-server-ver15)
* [sys.key_constraints](../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md?view=sql-server-ver15)
* [sys.numbered_procedures](../relational-databases/system-catalog-views/sys-numbered-procedures-transact-sql.md?view=sql-server-ver15)
* [sys.objects](../relational-databases/system-catalog-views/sys-objects-transact-sql.md?view=sql-server-ver15)
* [sys.parameters](../relational-databases/system-catalog-views/sys-parameters-transact-sql.md?view=sql-server-ver15)
* [sys.partition_functions](../relational-databases/system-catalog-views/sys-partition-functions-transact-sql.md?view=sql-server-ver15)
* [sys.partition_parameters](../relational-databases/system-catalog-views/sys-partition-parameters-transact-sql.md?view=sql-server-ver15)
* [sys.partition_range_values](../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md?view=sql-server-ver15)
* [sys.partition_schemes](../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md?view=sql-server-ver15)
* [sys.partitions](../relational-databases/system-catalog-views/sys-partitions-transact-sql.md?view=sql-server-ver15)
* [sys.procedures](../relational-databases/system-catalog-views/sys-procedures-transact-sql.md?view=sql-server-ver15)
* [sys.schemas](../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md?view=sql-server-ver15)
* [sys.securable_classes](../relational-databases/system-catalog-views/sys-securable-classes-transact-sql.md?view=sql-server-ver15)
* [sys.sql_expression_dependencies](../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md?view=sql-server-ver15)
* [sys.sql_modules](../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md?view=sql-server-ver15)
* [sys.stats](../relational-databases/system-catalog-views/sys-stats-transact-sql.md?view=sql-server-ver15)
* [sys.stats_columns](../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md?view=sql-server-ver15)
* [sys.symmetric_keys](../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)
* [sys.synonyms](../relational-databases/system-catalog-views/sys-synonyms-transact-sql.md)
* [sys.syscharsets](../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)
* [sys.syscolumns](../relational-databases/system-compatibility-views/sys-syscolumns-transact-sql.md)
* [sys.sysdatabases](../relational-databases/system-compatibility-views/sys-sysdatabases-transact-sql.md)
* [sys.syslanguages](../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)
* [sys.sysobjects](../relational-databases/system-compatibility-views/sys-sysobjects-transact-sql.md)
* [sys.sysreferences](../relational-databases/system-compatibility-views/sys-sysreferences-transact-sql.md)
* [sys.system_columns](../relational-databases/system-catalog-views/sys-system-columns-transact-sql.md?view=sql-server-ver15)
* [sys.system_objects](../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md?view=sql-server-ver15)
* [sys.system_parameters](../relational-databases/system-catalog-views/sys-system-parameters-transact-sql.md)
* [sys.system_sql_modules](../relational-databases/system-catalog-views/sys-system-sql-modules-transact-sql.md?view=sql-server-ver15)
* [sys.system_views](../relational-databases/system-catalog-views/sys-system-views-transact-sql.md?view=sql-server-ver15)
* [sys.systypes](../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md)
* [sys.sysusers](../relational-databases/system-compatibility-views/sys-sysusers-transact-sql.md)
* [sys.tables](../relational-databases/system-catalog-views/sys-tables-transact-sql.md?view=sql-server-ver15)
* [sys.types](../relational-databases/system-catalog-views/sys-types-transact-sql.md?view=sql-server-ver15)
* [sys.views](../relational-databases/system-catalog-views/sys-views-transact-sql.md?view=sql-server-ver15)

## <a name="sql-server-dmvs-available-in-parallel-data-warehouse"></a>並列データウェアハウスで使用できる Dmv の SQL Server
並列データウェアハウスは、SQL Server の動的管理ビュー (Dmv) の多くを公開します。 これらのビューは、並列データウェアハウスでクエリを実行すると、ディストリビューションで実行されている SQL Server データベースの状態を報告します。

これらの DMV には、pdw_node_id と呼ばれる特定の列があります。 これは、コンピューティングノードの識別子です。 

> [!NOTE]
> これらのビューを使用するには、次の表に示すように、名前に ' pdw_nodes_ ' を挿入します。
> 
> 

| Parallel Data Warehouse の DMV 名 | SQL Server T-sql トピックへのリンク |
|:--- |:--- |
| sys.dm_pdw_nodes_db_file_space_usage |[sys.dm_db_file_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_db_index_usage_stats |[sys.dm_db_index_usage_stats](../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_db_partition_stats |[sys.dm_db_partition_stats](../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_db_session_space_usage |[sys.dm_db_session_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_db_task_space_usage |[sys.dm_db_task_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_exec_background_job_queue |[sys.dm_exec_background_job_queue](../relational-databases/system-dynamic-management-views/sys-dm-exec-background-job-queue-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_exec_background_job_queue_stats |[sys.dm_exec_background_job_queue_stats](../relational-databases/system-dynamic-management-views/sys-dm-exec-background-job-queue-stats-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_exec_cached_plans |[sys.dm_exec_cached_plans](../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_exec_connections |[sys.dm_exec_connections](../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_exec_procedure_stats |[sys.dm_exec_procedure_stats](../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_exec_query_memory_grants |[sys.dm_exec_query_memory_grants](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_exec_query_optimizer_info |[sys.dm_exec_query_optimizer_info](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-optimizer-info-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_exec_query_resource_semaphores |[sys.dm_exec_query_resource_semaphores](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_exec_query_stats |[sys.dm_exec_query_stats](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_exec_requests |[sys.dm_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_exec_sessions |[sys.dm_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md) |
| sys.dm_pdw_nodes_io_pending_io_requests |[sys.dm_io_pending_io_requests](../relational-databases/system-dynamic-management-views/sys-dm-io-pending-io-requests-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_os_buffer_descriptors |[sys.dm_os_buffer_descriptors](../relational-databases/system-dynamic-management-views/sys-dm-os-buffer-descriptors-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_os_child_instances |[sys.dm_os_child_instances](../relational-databases/system-dynamic-management-views/sys-dm-os-child-instances-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_os_cluster_nodes |[sys.dm_os_cluster_nodes](../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_os_dispatcher_pools |[sys.dm_os_dispatcher_pools](../relational-databases/system-dynamic-management-views/sys-dm-os-dispatcher-pools-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_os_dispatchers |Transact-SQL のドキュメントはありません。 |
| sys.dm_pdw_nodes_os_hosts |[sys.dm_os_hosts](../relational-databases/system-dynamic-management-views/sys-dm-os-hosts-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_os_latch_stats |[sys.dm_os_latch_stats](../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_os_memory_brokers |[sys.dm_os_memory_brokers](../relational-databases/system-dynamic-management-views/sys-dm-os-memory-brokers-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_os_memory_cache_clock_hands |[sys.dm_os_memory_cache_clock_hands](../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-clock-hands-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_os_memory_cache_counters |[sys.dm_os_memory_cache_counters](../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-counters-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_os_memory_cache_entries |[sys.dm_os_memory_cache_entries](../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-entries-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_os_memory_cache_hash_tables |[sys.dm_os_memory_cache_hash_tables](../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-hash-tables-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_os_memory_clerks |[sys.dm_os_memory_clerks](../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_os_memory_node_access_stats |Transact-SQL のドキュメントはありません。 |
| sys.dm_pdw_nodes_os_memory_nodes |[sys.dm_os_memory_nodes](../relational-databases/system-dynamic-management-views/sys-dm-os-memory-nodes-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_os_memory_objects |[sys.dm_os_memory_objects](../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md) |
| sys.dm_pdw_nodes_os_memory_pools |[sys.dm_os_memory_pools](../relational-databases/system-dynamic-management-views/sys-dm-os-memory-pools-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_os_nodes |[sys.dm_os_nodes](../relational-databases/system-dynamic-management-views/sys-dm-os-nodes-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_os_performance_counters |[sys.dm_os_performance_counters](../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_os_process_memory |[sys.dm_os_process_memory](../relational-databases/system-dynamic-management-views/sys-dm-os-process-memory-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_os_schedulers |[sys.dm_os_schedulers](../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_os_spinlock_stats |Transact-SQL のドキュメントはありません。 |
| sys.dm_pdw_nodes_os_sys_info |[sys.dm_os_sys_info](../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_os_sys_memory |[sys.dm_os_memory_nodes](../relational-databases/system-dynamic-management-views/sys-dm-os-memory-nodes-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_os_tasks |[sys.dm_os_tasks](../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_os_threads |[sys.dm_os_threads](../relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_os_virtual_address_dump |[sys.dm_os_virtual_address_dump](../relational-databases/system-dynamic-management-views/sys-dm-os-virtual-address-dump-transact-sql.md) |
| sys.dm_pdw_nodes_os_wait_stats |[sys.dm_os_wait_stats](../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md) |
| sys.dm_pdw_nodes_os_waiting_tasks |[sys.dm_os_waiting_tasks](../relational-databases/system-dynamic-management-views/sys-dm-os-waiting-tasks-transact-sql.md) |
| sys.dm_pdw_nodes_os_workers |[sys.dm_os_workers](../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md) |
| sys.dm_pdw_nodes_resource_governor_resource_pools |[sys.dm_resource_governor_resource_pools](../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_resource_governor_workload_groups |[sys.dm_resource_governor_workload_groups](../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_tran_active_snapshot_database_transactions |[sys.dm_tran_active_snapshot_database_transactions](../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_tran_active_transactions |[sys.dm_tran_active_transactions](../relational-databases/system-dynamic-management-views/sys-dm-tran-active-transactions-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_tran_commit_table |[sys.dm_tran_commit_table](../relational-databases/system-dynamic-management-views/change-tracking-sys-dm-tran-commit-table.md) |
| sys.dm_pdw_nodes_tran_current_snapshot |[sys.dm_tran_current_snapshot](../relational-databases/system-dynamic-management-views/sys-dm-tran-current-snapshot-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_tran_current_transaction |[sys.dm_tran_current_transaction](../relational-databases/system-dynamic-management-views/sys-dm-tran-current-transaction-transact-sql.md) |
| sys.dm_pdw_nodes_tran_database_transactions |[sys.dm_tran_database_transactions](../relational-databases/system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md) |
| sys.dm_pdw_nodes_tran_locks |[sys.dm_tran_locks](../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_tran_session_transactions |[sys.dm_tran_session_transactions](../relational-databases/system-dynamic-management-views/sys-dm-tran-session-transactions-transact-sql.md?view=sql-server-ver15) |
| sys.dm_pdw_nodes_tran_top_version_generators |[sys.dm_tran_top_version_generators](../relational-databases/system-dynamic-management-views/sys-dm-tran-top-version-generators-transact-sql.md?view=sql-server-ver15) |

## <a name="sql-server-2016-polybase-dmvs-available-in-parallel-data-warehouse"></a>並列データウェアハウスで使用可能な SQL Server 2016 PolyBase Dmv
* [sys.dm_exec_compute_node_errors](../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md?view=sql-server-ver15)
* [sys.dm_exec_compute_node_status](../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-status-transact-sql.md?view=sql-server-ver15)
* [sys.dm_exec_compute_nodes](../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)
* [sys.dm_exec_distributed_request_steps](../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md)
* [sys.dm_exec_distributed_requests](../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-requests-transact-sql.md?view=sql-server-ver15)
* [sys.dm_exec_distributed_sql_requests](../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-sql-requests-transact-sql.md?view=sql-server-ver15)
* [sys.dm_exec_dms_services](../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-services-transact-sql.md)
* [sys.dm_exec_dms_workers](../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)
* [sys.dm_exec_external_operations](../relational-databases/system-dynamic-management-views/sys-dm-exec-external-operations-transact-sql.md)
* [sys.dm_exec_external_work](../relational-databases/system-dynamic-management-views/sys-dm-exec-external-work-transact-sql.md)

## <a name="sql-server-information_schema-views"></a>SQL Server INFORMATION_SCHEMA ビュー
* [CHECK_CONSTRAINTS](../relational-databases/system-information-schema-views/check-constraints-transact-sql.md)
* [COLUMNS](../relational-databases/system-information-schema-views/columns-transact-sql.md)
* [PARAMETERS](../relational-databases/system-information-schema-views/parameters-transact-sql.md)
* [ROUTINES](../relational-databases/system-information-schema-views/routines-transact-sql.md)
* [SCHEMATA](../relational-databases/system-information-schema-views/schemata-transact-sql.md)
* [TABLES](../relational-databases/system-information-schema-views/tables-transact-sql.md)
* [VIEW_COLUMN_USAGE](../relational-databases/system-information-schema-views/view-column-usage-transact-sql.md)
* [VIEW_TABLE_USAGE](../relational-databases/system-information-schema-views/view-table-usage-transact-sql.md)
* [VIEWS](../relational-databases/system-information-schema-views/views-transact-sql.md)

## <a name="next-steps"></a>次のステップ
詳細については、「 [t-sql 言語要素](tsql-language-elements.md) 」および「 [t-sql ステートメント](tsql-statements.md)」を参照してください。

<!--Image references-->

<!--Article references-->
[Azure Synapse Analytics reference overview]: sql-data-warehouse-overview-reference.md

<!--MSDN references-->


<!--Other Web references-->