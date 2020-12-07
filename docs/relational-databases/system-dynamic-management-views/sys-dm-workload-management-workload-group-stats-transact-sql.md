---
description: sys.dm_workload_management_workload_groups_stats (Transact-sql)
title: sys.dm_workload_management_workload_groups_stats (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/02/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
monikerRange: = azure-sqldw-latest||= sqlallproducts-allversions
ms.openlocfilehash: bc36846a62b8b71e0e21d7ea61d088a0f16c674d
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035183"
---
# <a name="sysdm_workload_management_workload_groups_stats-transact-sql"></a>sys.dm_workload_management_workload_groups_stats (Transact-sql)
[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

ワークロードグループの統計と、のワークロードグループの有効な値を返し [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ます。  
  
|列名|データ型|説明|Range|  
|-----------------|---------------|-----------------|-----------|  
|group_id|**int**|ワークロード グループの一意の ID。||
|name|**sysname**|ワークロードグループの名前。||
|statistics_start_time|**datetime**|ワークロードグループの統計コレクションが開始された時刻。  この値は、ワークロードグループが作成されたとき、またはインスタンスが一時停止またはスケーリングされたときのいずれかになります。||
|total_request_count|**bigint**|ワークロードグループ内の完了した要求の累積数。||
|total_shared_resource_reqeusts|**bigint**|共有プールからリソースを使用したワークロードグループ内の完了した要求の累積数。||
|total_queued_request_count|**bigint**|Max_concurrency の制限に達した後にキューに登録された要求の累積数。||
|total_request_execution_timeouts|**bigint**|Query_execution_timeout_sec の設定に基づいて、完了前にタイムアウトしたワークロードグループ内の要求の累積数。||
|effective_min_percentage_resource|**tinyint**|有効な min_percentage_resource 設定では、サービスレベルとワークロードグループの設定を考慮することができます。 有効な min_percentage_resource は、より低いサービスレベルで調整できます。  たとえば、DW100c では、許可されている最小 min_percentage_resource は25% です。  値がサービスレベルで許可されていない場合、min_percentage_resource は0% に調整されます。  たとえば、DW6000c で10% に設定されている min_percentage_resource、DW100c にスケールダウンすると、effective_min_percentage_resource は0% になります。||
|effective_cap_percentage_resource|**tinyint**|ワークロードグループの有効な cap_percentage_resource。  Min_percentage_resource > 0 のワークロードグループが他にある場合、effective_cap_percentage_resource は比例して低くなります。||
|effective_request_min_resource_grant_percent|**decimal (5, 2)**|ワークロードグループの request_min_resource_grant_percent の有効なランタイム値。 サービスレベルと、ワークロードグループの構成方法を検討している有効な値。  サービスレベルによって min_percentage_resource が調整された場合は、それに応じて effective_request_min_resource_grant_percent が調整されます。||
|effective_request_max_resource_grant_percent|**decimal (5, 2)**|ワークロードグループの request_max_resource_grant_percent の有効なランタイム値は、すべてのワークロードグループの構成を検討しています。||
|||||

## <a name="see-also"></a>関連項目

 [Azure Synapse Analytics と並列データウェアハウスの動的管理ビュー &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
