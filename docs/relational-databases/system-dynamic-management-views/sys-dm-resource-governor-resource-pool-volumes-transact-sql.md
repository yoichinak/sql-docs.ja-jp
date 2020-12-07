---
description: dm_resource_governor_resource_pool_volumes (Transact-sql)
title: dm_resource_governor_resource_pool_volumes (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_resource_pool_volumes_TSQL
- dm_resource_governor_resource_pool_volumes_TSQL
- dm_resource_governor_resource_pool_volumes
- sys.dm_resource_governor_resource_pool_volumes
dev_langs:
- TSQL
helpviewer_keywords:
- dm_resource_governor_resource_pool_volumes
- sys.dm_resource_governor_resource_pool_volumes
ms.assetid: fa692e56-c561-4533-97c5-bc12c600553f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7fd7feb957b93590d76ff92aab14fd745b7c43dd
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543851"
---
# <a name="sysdm_resource_governor_resource_pool_volumes-transact-sql"></a>dm_resource_governor_resource_pool_volumes (Transact-sql)
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

  各ディスクボリュームの現在のリソースプール IO 統計に関する情報を返します。 この情報は、 [sys. dm_resource_governor_resource_pools &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)のリソースプールレベルでも使用できます。 transact-sql&#41;を参照してください。  
  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|pool_id|**int**|リソースプールの ID。 NULL 値は許可されません。|  
|volume_name|**sysname**|ディスクの名前。 NULL 値は許可されません。|  
|read_io_queued_total|**int**|リソースガバナーがリセットされた後にエンキューされた読み取り Io の合計。 NULL 値は許可されません。|  
|read_io_issued_total|**int**|リソースガバナー統計がリセットされた後に発行された読み取り Io の合計。 NULL 値は許可されません。|  
|read_ios_completed_total|**int**|リソース ガバナー統計がリセットされた後に完了した読み取り IO の合計。 NULL 値は許可されません。|  
|read_ios_throttled_total|**int**|リソースガバナー統計がリセットされた後に調整された読み取り Io の合計。 NULL 値は許可されません。|  
|read_bytes_total|**bigint**|リソース ガバナー統計がリセットされた後に読み取られたバイト数の合計。 NULL 値は許可されません。|  
|read_io_stall_total_ms|**bigint**|読み取り IO の到着から完了までの合計時間 (ミリ秒単位)。 NULL 値は許可されません。|  
|read_io_stall_queued_ms|**bigint**|読み取り IO の到着から問題までの合計時間 (ミリ秒)。 これは、IO リソースガバナンスで導入された遅延です。 NULL 値は許可されません。|  
|write_io_queued_total|**int**|リソースガバナー統計がリセットされた後にエンキューされた書き込み Io の合計。 NULL 値は許可されません。|  
|write_io_issued_total|**int**|リソースガバナー統計がリセットされた後に発行された書き込み Io の合計。 NULL 値は許可されません。|  
|write_io_completed_total|**int**|リソース ガバナー統計がリセットされた後に完了した書き込み IO の合計。 Null 値はありません|  
|write_io_throttled_total|**int**|リソースガバナー統計がリセットされた後に調整された書き込み Io の合計。 Null 値はありません|  
|write_bytes_total|**bigint**|リソース ガバナー統計がリセットされた後に書き込まれたバイト数の合計。 NULL 値は許可されません。|  
|write_io_stall_total_ms|**bigint**|書き込み IO の問題と完了の合計時間 (ミリ秒単位)。 NULL 値は許可されません。|  
|write_io_stall_queued_ms|**bigint**|書き込み IO の到着から発行までの合計時間 (ミリ秒単位)。 これは、IO リソースガバナンスで導入された遅延です。 NULL 値は許可されません。|  
|io_issue_violations_total|**int**|IO 発行違反の合計。 つまり、IO の問題の発生率が予約されたレートを下回った回数です。 NULL 値は許可されません。|  
|io_issue_delay_total_ms|**bigint**|スケジュールされた問題と IO の実際の問題との間の合計時間 (ミリ秒単位)。 NULL 値は許可されません。|  
  
## <a name="permissions"></a>アクセス許可  
 VIEW SERVER STATE 権限が必要です。  
  
## <a name="see-also"></a>関連項目  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [sys.dm_resource_governor_workload_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md)   
 [resource_governor_resource_pools &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-resource-pools-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  

