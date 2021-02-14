---
description: sys.dm_hadr_ag_threads (Transact-sql)
title: sys.dm_hadr_ag_threads (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 02/08/2021
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_ag_threads_TSQL
- sys.dm_hadr_ag_threads
- dm_hadr_ag_threads_TSQL
- dm_hadr_ag_threads
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.dm_hadr_ag_threads catalog view
ms.assetid: ''
author: kfarlee
ms.author: kfarlee
monikerRange: ''
ms.openlocfilehash: c8487dd07e424b7edccc17b8a9587cfc91f74268
ms.sourcegitcommit: 8dc7e0ececf15f3438c05ef2c9daccaac1bbff78
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/13/2021
ms.locfileid: "100354132"
---
# <a name="sysdm_hadr_ag_threads-transact-sql"></a>sys.dm_hadr_ag_threads (Transact-sql)

HADR スレッドテレメトリ Dmv (**sys.dm_hadr_ag_threads** と [sys.dm_hadr_db_threads](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-db-threads-transact-sql.md)) を使用すると、ユーザーは可用性グループと高可用性データベースによるスレッドの使用状況をすばやく把握できます。 このスレッド使用状況を理解することは、可用性グループを調整するための重要なベンチマークです。

この DMV は、可用性グループレベルでのスレッドの使用状況を報告します。

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|可用性グループの識別子。|
|**name**|**nvarchar(128)**|可用性グループの名前。|
|**num_databases**|**int**|可用性グループ内のデータベースの数。|
|**num_capture_threads**|**int**|この可用性グループ内のすべてのデータベースで使用されているログキャプチャスレッドの数。|
|**num_redo_threads**|**int**|この可用性グループ内のすべてのデータベースで使用されている再実行スレッドの数。|
|**num_parallel_redo_threads**|**int**|この可用性グループ内のすべてのデータベースで使用されている並列再実行スレッドの数。|
|**num_hadr_threads**|**int**|この可用性グループ内のすべてのデータベースで使用されているすべての always on スレッドの数。|

## <a name="permissions"></a>アクセス許可  

 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="see-also"></a>参照  

 [Always On 可用性グループの動的管理ビューおよび関数 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [AlwaysOn 可用性グループのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Transact-sql&#41;&#40;可用性グループの監視 ](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性グループ &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  