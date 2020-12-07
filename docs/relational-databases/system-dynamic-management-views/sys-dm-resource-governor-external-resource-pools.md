---
description: dm_resource_governor_external_resource_pools (Transact-sql)
title: dm_resource_governor_external_resource_pools (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/06/2020
ms.prod: sql
ms.technology: machine-learning-services
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_external_resource_pools_TSQL
- sys.dm_resource_governor_external_resource_pools
- dm_resource_governor_external_resource_pools
- dm_resource_governor_external_resource_pools_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_resource_governor_external_resource_pools
- sys.dm_resource_governor_external_resource_pools
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 99a85cb9c329752e35f720ec97dabbb417498d3d
ms.sourcegitcommit: 5da46e16b2c9710414fe36af9670461fb07555dc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/01/2020
ms.locfileid: "89283633"
---
# <a name="sysdm_resource_governor_external_resource_pools-transact-sql"></a>dm_resource_governor_external_resource_pools (Transact-sql)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

現在の外部リソースプールの状態、リソースプールの現在の構成、およびリソースプールの統計に関する情報を返します。 
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
|列名      |データ型      |説明|  
|----------------|---------------|-----------------| 
| external_pool_id|**int**|リソースプールの ID。 NULL 値は許可されません。 |
| name|**sysname**|共有リソースの名前。 NULL 値は許可されません。 
| pool_version|**int**|内部バージョン番号。|
| max_cpu_percent|**int**|CPU の競合がある場合に、リソースプールのすべての要求で許容される最大平均 CPU 帯域幅の現在の構成。 NULL 値は許可されません。 |
| max_processes|**int**|同時外部プロセスの最大数。 既定値は0で、無制限であることを示します。 NULL 値は許可されません。|
| max_memory_percent|**int**|このリソースプール内の要求で使用できる合計サーバーメモリの割合の現在の構成。 NULL 値は許可されません。 |
| statistics_start_time|**datetime**|このプールの統計がリセットされた時刻。 NULL 値は許可されません。 
| peak_memory_kb|**bigint**|リソースプールに使用されるメモリの最大量 (kb 単位)。 NULL 値は許可されません。 |
| write_io_count|**int**|Resource Governor の統計がリセットされてから発行された書き込み IO の合計。 NULL 値は許可されません。 |
| read_io_count|**int**|Resource Governor の統計がリセットされてから発行された読み取り IO の合計。 NULL 値は許可されません。 |
| total_cpu_kernel_ms|**bigint**|Resource Governor の統計がリセットされてからの累積 CPU ユーザー カーネル時間 (ミリ秒単位)。 NULL 値は許可されません。 |
| total_cpu_user_ms|**bigint**|Resource Governor の統計がリセットされてからの累積 CPU ユーザー時間 (ミリ秒単位)。 NULL 値は許可されません。 |
| active_processes_count|**int**|要求の時点で実行されている外部プロセスの数。 NULL 値は許可されません。 |

 
## <a name="permissions"></a>アクセス許可

`VIEW SERVER STATE` 権限が必要です。

## <a name="see-also"></a>参照  
 [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)  
  
  
