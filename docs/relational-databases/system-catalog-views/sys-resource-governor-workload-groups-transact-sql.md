---
description: sys.resource_governor_workload_groups (Transact-SQL)
title: resource_governor_workload_groups (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.resource_governor_workload_groups
- resource_governor_workload_groups_TSQL
- sys.resource_governor_workload_groups_TSQL
- resource_governor_workload_groups
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_governor_workload_groups catalog view
ms.assetid: 619ba4b7-868f-4784-b527-ec1dfd703c4f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f85ef2691091911e937bae9fbf21649ace7a943e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550430"
---
# <a name="sysresource_governor_workload_groups-transact-sql"></a>sys.resource_governor_workload_groups (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で格納されているワークロード グループの構成を返します。 各ワークロードグループは、1つのリソースプールにのみサブスクライブできます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|group_id|**int**|ワークロード グループの一意の ID。 NULL 値は許可されません。|  
|name|**sysname**|ワークロードグループの名前。 NULL 値は許可されません。|  
|importance|**sysname**|**注:** 重要度は、同じリソースプール内のワークロードグループにのみ適用されます。<br /><br /> は、このワークロードグループ内の要求の相対的な重要度です。 重要度は次のいずれかで、MEDIUM は既定値は LOW、MEDIUM、HIGH です。<br /><br /> NULL 値は許可されません。|  
|request_max_memory_grant_percent|**int**|1つの要求に対する最大メモリ許可 (パーセント)。 既定値は 25 です。 NULL 値は許可されません。<br /><br /> **注:** この設定が50% を超える場合、大規模なクエリは一度に1つずつ実行されます。 そのため、クエリの実行中にメモリ不足エラーが発生する危険性が高くなります。|  
|request_max_cpu_time_sec|**int**|1 つの要求に対する最大 CPU 使用制限 (秒単位)。 既定値は0で、無制限であることを示します。 NULL 値は許可されません。<br /><br /> **注:** 詳細については、「 [CPU しきい値を超えたイベントクラス](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md)」を参照してください。|  
|request_memory_grant_timeout_sec|**int**|1つの要求に対するメモリ許可のタイムアウト (秒単位)。 既定値は 0 で、クエリ コストに基づく内部の計算が使用されます。 NULL 値は許可されません。|  
|max_dop|**int**|ワークロード グループの並列処理の最大限度。 既定値は0で、グローバル設定が使用されます。 NULL 値は許可されません。<br /><br /> **ノード:** この設定は、クエリオプション **maxdop**を上書きします。|  
|group_max_requests|**int**|同時要求の最大数。 既定値は0で、無制限であることを示します。 NULL 値は許可されません。|  
|pool_id|**int**|このワークロード グループが使用するリソース プールの ID。|  
|external_pool_id|**int**|**適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降。<br /><br /> このワークロードグループが使用する外部リソースプールの ID。|  
  
## <a name="remarks"></a>解説  
 カタログビューには、格納されているメタデータが表示されます。 メモリ内の構成を表示するには、対応する動的管理ビューである [sys. dm_resource_governor_workload_groups &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md)を使用します。  
  
 リソース ガバナーの構成を変更したにもかかわらず、ALTER RESOURCE GOVERNOR RECONFIGURE ステートメントを適用していない場合、異なる構成がメモリ内に格納されている可能性があります。  
  
## <a name="permissions"></a>アクセス許可  
 コンテンツを表示するには VIEW ANY DEFINITION 権限が必要です。コンテンツを変更するには CONTROL SERVER 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [sys.dm_resource_governor_workload_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Resource Governor カタログビュー &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)  
  
  
