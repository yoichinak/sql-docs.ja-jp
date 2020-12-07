---
description: sys.resource_governor_resource_pools (Transact-SQL)
title: resource_governor_resource_pools (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.resource_governor_resource_pools
- resource_governor_resource_pools
- sys.resource_governor_resource_pools_TSQL
- resource_governor_resource_pools_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_governor_resource_pools catalog view
ms.assetid: 56793e9c-aa90-452e-88c6-d9b799239888
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 24c19d78cdd0d4b38398b4212568134aaee74e15
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550450"
---
# <a name="sysresource_governor_resource_pools-transact-sql"></a>sys.resource_governor_resource_pools (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で格納されているリソース プール構成を返します。 ビューの各行によって、プールの構成が決まります。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|pool_id|**int**|リソース プールの一意の ID。 NULL 値は許可されません。|  
|name|**sysname**|リソース プールの名前。 NULL 値は許可されません。|  
|min_cpu_percent|**int**|CPU の競合がある場合にリソース プールのすべての要求に保証される平均 CPU 帯域幅。 NULL 値は許可されません。|  
|max_cpu_percent|**int**|CPU の競合がある場合に、リソースプール内のすべての要求で許容される最大平均 CPU 帯域幅。 NULL 値は許可されません。|  
|min_memory_percent|**int**|リソースプール内のすべての要求に対して保証されるメモリの量。 これは、他のリソース プールとは共有されません。 NULL 値は許可されません。|  
|max_memory_percent|**int**|このリソースプールの要求で使用できる合計サーバーメモリの割合。 NULL 値は許可されません。 有効な最大値はプールの最小値によって異なります。 たとえば、max_memory_percent は100に設定できますが、有効な最大値は低くなります。|  
|cap_cpu_percent|**int**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> リソースプール内のすべての要求が受信する CPU 帯域幅のハードキャップ。 CPU の最大帯域幅を、指定したレベルに制限します。 value の許容範囲は 1 ～ 100 です。|  
|min_iops_per_volume|**int**|**適用対象**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降。<br /><br /> このプールのボリューム設定ごとの1秒あたりの最小 i/o 操作 (IOPS)。 0 = 予約なし。 null にすることはできません。|  
|max_iops_per_volume|**int**|**適用対象**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降。<br /><br /> このプールのボリューム設定ごとの、1 秒あたりの最大 I/O 操作 (IOPS)。 0 = 無制限。 null にすることはできません。|  
  
## <a name="remarks"></a>解説  
 カタログビューには、格納されているメタデータが表示されます。 メモリ内の構成を表示するには、対応する動的管理ビューである [sys. dm_resource_governor_resource_pools &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)を使用します。  
  
## <a name="permissions"></a>アクセス許可  
 コンテンツを表示するには VIEW ANY DEFINITION 権限が必要です。コンテンツを変更するには CONTROL SERVER 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [Resource Governor カタログビュー &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)   
 [dm_resource_governor_resource_pools &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)   
 [リソース ガバナー](../../relational-databases/resource-governor/resource-governor.md)   
 [sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)  
  
  
