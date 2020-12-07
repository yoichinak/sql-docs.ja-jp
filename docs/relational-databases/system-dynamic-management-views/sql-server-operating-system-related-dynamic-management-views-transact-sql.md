---
description: SQL Server オペレーティングシステム関連の動的管理ビュー (Transact-sql)
title: SQL Server オペレーティングシステム関連の動的管理ビュー (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 04/17/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operating systems [SQL Server], dynamic management objects
- SQL Operating System dynamic management objects [SQL Server]
- SQL OS dynamic management objects [SQL Server]
- dynamic management objects [SQL Server], SQL OS
ms.assetid: 3030c86a-0a74-4fed-ac0f-392e244cb965
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6ca14e58a777603fc0bbfed73834597641fddf08
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548922"
---
# <a name="sql-server-operating-system-related-dynamic-management-views-transact-sql"></a>SQL Server オペレーティングシステム関連の動的管理ビュー (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

このセクションでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オペレーティングシステム (SQLOS) に関連付けられている動的管理ビュー (DMV) について説明します。 SQLOS は、に固有のオペレーティングシステムリソースの管理を担当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。


|  |  |
|---------|---------|
|**sys.dm_os_buffer_descriptors** | **sys.dm_os_buffer_pool_extension_configuration**|
|**sys.dm_os_child_instances** | **sys.dm_os_cluster_nodes** |
|**sys.dm_os_cluster_properties** | **sys.dm_os_dispatcher_pools** |
|**sys.dm_os_enumerate_fixed_drives** | **sys.dm_os_host_info** |
|**sys.dm_os_hosts** | **sys.dm_os_latch_stats** |
|**sys.dm_os_loaded_modules** |**sys.dm_os_memory_brokers**|
|**sys.dm_os_memory_cache_clock_hands**|**sys.dm_os_memory_cache_counters** |
|**sys.dm_os_memory_cache_entries**|**sys.dm_os_memory_cache_hash_tables**|
|**sys.dm_os_memory_clerks**|**sys.dm_os_memory_nodes**|
|**sys.dm_os_nodes**|**sys.dm_os_performance_counters**|
|**sys.dm_os_process_memory**|**sys.dm_os_schedulers**|
|**sys.dm_os_server_diagnostics_log_configurations**|**sys.dm_os_spinlock_stats** |
|**sys.dm_os_stacks**|**sys.dm_os_sys_info**|
|**sys.dm_os_sys_memory**|**sys.dm_os_tasks**|
|**sys.dm_os_threads** |**sys.dm_os_virtual_address_dump**|
|**sys.dm_os_volume_stats**|**sys.dm_os_waiting_tasks**|
|**sys.dm_os_wait_stats**|**sys.dm_os_windows_info**|
|**sys.dm_os_workers** ||








 次の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オペレーティングシステム関連の動的管理ビューは [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] です。  
  
|||  
|-|-|  
|**sys.dm_os_function_symbolic_name**|**sys.dm_os_ring_buffers**|  
|**dm_os_memory_allocations**|**dm_os_sublatches**|  
|**dm_os_worker_local_storage**||  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

