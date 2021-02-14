---
description: sys.dm_hadr_db_threads (Transact-sql)
title: sys.dm_hadr_db_threads (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 02/08/2021
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_db_threads_TSQL
- sys.dm_hadr_db_threads
- dm_hadr_db_threads_TSQL
- dm_hadr_db_threads
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.dm_hadr_db_threads catalog view
ms.assetid: ''
author: kfarlee
ms.author: kfarlee
monikerRange: ''
ms.openlocfilehash: 7637c5b2acb302c4af8960161fb5a687ff7a02d0
ms.sourcegitcommit: 8dc7e0ececf15f3438c05ef2c9daccaac1bbff78
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/13/2021
ms.locfileid: "100338844"
---
# <a name="sysdm_hadr_db_threads-transact-sql"></a>sys.dm_hadr_db_threads (Transact-sql)

HADR スレッドテレメトリ Dmv (**sys.dm_hadr_db_threads** と [sys.dm_hadr_ag_threads](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-ag-threads-transact-sql.md)) を使用すると、ユーザーは可用性グループと高可用性データベースによるスレッドの使用状況をすばやく把握できます。 このスレッド使用状況を理解することは、可用性グループを調整するための重要なベンチマークです。

この DMV は、可用性グループデータベースレベルでのスレッドの使用状況を報告します。

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|データベースが属する可用性グループの識別子。|
|**ag_db_id**|**uniqueidentifier**|可用性グループ内のデータベースの識別子。 この識別子は、このデータベースが参加しているすべてのレプリカで同じです。|
|**name**|**nvarchar(128)**|データベース名。|
|**num_capture_threads**|**int**|このデータベースのログキャプチャスレッド数。|
|**num_redo_threads**|**int**|このデータベースの再実行スレッドの数。|
|**num_parallel_redo_threads**|**int**|このデータベースの並列再実行スレッドの数。|

## <a name="permissions"></a>アクセス許可  

 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="see-also"></a>参照

 [Always On 可用性グループの動的管理ビューおよび関数 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [AlwaysOn 可用性グループのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Transact-sql&#41;&#40;可用性グループの監視 ](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性グループ &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  