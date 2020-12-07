---
description: dm_resource_governor_external_resource_pool_affinity (Transact-sql)
title: dm_resource_governor_external_resource_pool_affinity (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_external_resource_pool_affinity
- sys.dm_resource_governor_external_resource_pool_affinity_TSQL
- dm_resource_governor_external_resource_pool_affinity
- dm_resource_governor_external_resource_pool_affinity_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_resource_governor_external_resource_pool_affinity
- dm_resource_governor_external_resource_pool_affinity
ms.assetid: e32fac49-5161-47c0-8540-af3fe730c00c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9ad8fa57e43d1b456434f007e224464af11aa53e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546499"
---
# <a name="sysdm_resource_governor_external_resource_pool_affinity-transact-sql"></a>dm_resource_governor_external_resource_pool_affinity (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]
**適用対象:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)][!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]および [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)][!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

現在の外部リソースプールの構成に関する CPU アフィニティ情報を返します。
  
|列名|データ型|説明|
|----------------|---------------|-----------------|
|pool_id|**int**|外部リソースプールの ID。 NULL 値は許可されません。|
|processor_group|**smallint**|Windows 論理プロセッサグループの ID。 NULL 値は許可されません。|
|cpu_mask|**bigint**|このプールに関連付けられている Cpu を表すバイナリマスク。 NULL 値は許可されません。|
  
## <a name="remarks"></a>解説

アフィニティを使用して作成されたプールは、アフィニティがない `AUTO` ため、このビューに表示されません。 詳細については、「 [CREATE EXTERNAL RESOURCE pool &#40;transact-sql&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md) 」および「 [ALTER external Resource pool &#40;transact-sql&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md) ステートメント」を参照してください。

## <a name="permissions"></a>アクセス許可

`VIEW SERVER STATE` 権限が必要です。

## <a name="see-also"></a>関連項目

[SQL Server での Machine Learning のリソース管理](../../machine-learning/administration/resource-governor.md)

[dm_resource_governor_resource_pool_affinity &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)

[external scripts enabled サーバー構成オプション](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)

[ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)
