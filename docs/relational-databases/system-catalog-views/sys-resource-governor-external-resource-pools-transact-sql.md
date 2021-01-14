---
description: sys.resource_governor_external_resource_pools (Transact-sql)
title: sys.resource_governor_external_resource_pools (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/13/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.resource_governor_external_resource_pools
- sys.resource_governor_external_resource_pools_TSQL
- resource_governor_external_resource_pools
- resource_governor_external_resource_pools_TSQL
helpviewer_keywords:
- sys.resource_governor_external_resource_pools
- resource_governor_external_resource_pools
ms.assetid: 75063e36-a91b-496f-9936-88f3d57bd447
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 49ea05c98551b8faa06b981d5a5b5b4c37e743fc
ms.sourcegitcommit: f29f74e04ba9c4d72b9bcc292490f3c076227f7c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2021
ms.locfileid: "98169302"
---
# <a name="sysresource_governor_external_resource_pools-transact-sql"></a>sys.resource_governor_external_resource_pools (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]
**適用対象:** [!INCLUDE[sssql15-md](../../includes/sssql16-md.md)][!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]および [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)][!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

に格納されている外部リソースプール構成を返し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 ビューの各行によって、プールの構成が決まります。
  
|列名|データ型|説明|
|-----------------|---------------|-----------------|
|external_pool_id|**int**|リソース プールの一意の ID。 NULL 値は許可されません。|
|name|**sysname**|リソース プールの名前。 NULL 値は許可されません。|
|max_cpu_percent|**int**|CPU の競合がある場合に、リソースプール内のすべての要求で許容される最大平均 CPU 帯域幅。 NULL 値は許可されません。|
|max_memory_percent|**int**|このリソースプールの要求で使用できる合計サーバーメモリの割合。 NULL 値は許可されません。 有効な最大値はプールの最小値によって異なります。 たとえば、max_memory_percent は100に設定できますが、有効な最大値は低くなります。|
|max_processes|**int**|同時外部プロセスの最大数。 既定値は0で、無制限であることを示します。 NULL 値は許可されません。|
|version|**bigint**|内部バージョン番号。|
  
## <a name="permissions"></a>アクセス許可

VIEW SERVER STATE 権限が必要です。

## <a name="see-also"></a>関連項目

[SQL Server での Machine Learning のリソース管理](../../machine-learning/administration/resource-governor.md)

[Resource Governor カタログビュー &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)

[sys.dm_resource_governor_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)

[リソース ガバナー](../../relational-databases/resource-governor/resource-governor.md)

[sys.dm_resource_governor_resource_pool_affinity &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)

[external scripts enabled サーバー構成オプション](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)

[ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)
