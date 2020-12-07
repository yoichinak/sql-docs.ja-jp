---
description: SQL および Parallel Data Warehouse の動的管理ビュー
title: SQL および Parallel Data Warehouse の動的管理ビュー
ms.custom: seo-dt-2019
ms.date: 11/05/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: julieMSFT
ms.author: jrasnick
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 877c1b09d443cafa30558d015cd604daaacc941b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482015"
---
# <a name="sql-and-parallel-data-warehouse-dynamic-management-views"></a>SQL および Parallel Data Warehouse の動的管理ビュー
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

このトピックでは、 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 動的管理ビュー (dmv) の一覧を示します。  
  
 すべての [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] および dmv は、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] **sys. dm_pdw**で始まります。  
  
## <a name="sssdw-and-sspdw-dynamic-management-views"></a>[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 動的管理ビュー  
 次の動的管理ビューは、との両方に適用され [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] ます。  
  
 [dm_pdw_dms_cores &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-cores-transact-sql.md)  
  
 [dm_pdw_dms_external_work &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-external-work-transact-sql.md)  
  
 [dm_pdw_dms_workers &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md)  
  
 [dm_pdw_errors &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md)  
  
 [dm_pdw_exec_connections &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-connections-transact-sql.md)  
  
 [dm_pdw_exec_requests &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)  
  
 [dm_pdw_exec_sessions &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)  
  
 [dm_pdw_hadoop_operations &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-hadoop-operations-transact-sql.md)  
  
 [dm_pdw_lock_waits &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-lock-waits-transact-sql.md)  
  
 [dm_pdw_nodes &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)  
  
 [dm_pdw_nodes_database_encryption_keys &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql.md)  
  
 [dm_pdw_os_threads &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-os-threads-transact-sql.md)  
  
 [dm_pdw_request_steps &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)  
  
 [dm_pdw_resource_waits &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md)  
  
 [dm_pdw_sql_requests &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-sql-requests-transact-sql.md)  
  
 [dm_pdw_sys_info &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-sys-info-transact-sql.md)  
  
 [dm_pdw_wait_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-wait-stats-transact-sql.md)  
  
 [dm_pdw_waits &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)

## <a name="sssdw-dynamic-management-views"></a>[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 動的管理ビュー 
 次の動的管理ビューはにのみ適用され [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ます。
 
[dm_pdw_nodes_exec_query_plan &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-exec-query-plan-transact-sql.md)  

[dm_pdw_nodes_exec_query_profiles &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-exec-query-profiles-transact-sql.md)  

[dm_pdw_nodes_exec_query_statistics_xml &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-exec-query-statistics-xml-transact-sql.md)  

[dm_pdw_nodes_exec_sql-text &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-exec-sql-text-transact-sql.md)  

[dm_pdw_nodes_exec_text_query_plan &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-exec-text-query-plan-transact-sql.md)

 [dm_workload_management_workload_groups_stats &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-workload-management-workload-group-stats-transact-sql.md) (プレビュー)

## <a name="sspdw-dynamic-management-views"></a>[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 動的管理ビュー  
 次の動的管理ビューはにのみ適用され [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] ます。  
  
 [dm_pdw_component_health_active_alerts &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md)  
  
 [dm_pdw_component_health_alerts &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-alerts-transact-sql.md)  
  
 [dm_pdw_component_health_status &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md)  
  
 [dm_pdw_diag_processing_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-diag-processing-stats-transact-sql.md)  
  
 [dm_pdw_network_credentials &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md)  
  
 [dm_pdw_node_status &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-node-status-transact-sql.md)  
  
 [dm_pdw_os_event_logs &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-os-event-logs-transact-sql.md)  
  
 [dm_pdw_os_performance_counters &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-os-performance-counters-transact-sql.md)  
  
 [dm_pdw_query_stats_xe &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-query-stats-xe-transact-sql.md)  
  
 [dm_pdw_query_stats_xe_file &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-query-stats-xe-file-transact-sql.md)  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
