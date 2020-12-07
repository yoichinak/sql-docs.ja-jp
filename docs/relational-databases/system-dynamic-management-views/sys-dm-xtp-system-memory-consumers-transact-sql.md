---
description: dm_xtp_system_memory_consumers (Transact-sql)
title: dm_xtp_system_memory_consumers (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_xtp_system_memory_consumers
- sys.dm_xtp_system_memory_consumers_TSQL
- sys.dm_xtp_system_memory_consumers
- dm_xtp_system_memory_consumers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xtp_system_memory_consumers dynamic management view
ms.assetid: 9eb0dd82-7920-42e0-9e50-7ce6e7ecee8b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e998b531c867d78bbf27bff516aaecda6f7f9f88
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543791"
---
# <a name="sysdm_xtp_system_memory_consumers-transact-sql"></a>dm_xtp_system_memory_consumers (Transact-sql)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  のシステムレベルのメモリコンシューマーを報告 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] します。 これらのコンシューマーのメモリは、既定のプール (割り当てがユーザースレッドのコンテキスト内にある場合)、または内部プール (割り当てがシステムスレッドのコンテキスト内にある場合) から取得されます。  
  
```  
-- system memory consumers @ instance  
select * from sys.dm_xtp_system_memory_consumers  
```  
  
 詳細については、「[インメモリ OLTP &#40;インメモリ最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)」を参照してください。  
  
|列名|種類|説明|  
|-----------------|----------|-----------------|  
|memory_consumer_id|**bigint**|メモリコンシューマーの内部 ID。|  
|memory_consumer_type|**int**|次のいずれかの値を持つメモリコンシューマーの種類を表す整数。<br /><br /> 0: 表示されません。 複数のコンシューマーのメモリ使用量を集計します。<br /><br /> 1-ルックアサイド: システムルックアサイドのメモリ使用量を追跡します。<br /><br /> 2-VARHEAP: 可変長ヒープのメモリ使用量を追跡します。<br /><br /> 4-IO ページプール: IO 操作に使用されるシステムページプールのメモリ使用量を追跡します。|  
|memory_consumer_type_desc|**nvarchar (16)**|メモリコンシューマーの種類の説明。<br /><br /> 0: 表示されません。<br /><br /> 1-ルックアサイド<br /><br /> 2-VARHEAP<br /><br /> 4-PGPOOL|  
|memory_consumer_desc|**nvarchar (64)**|メモリ コンシューマー インスタンスの説明。<br /><br /> VARHEAP <br />システム ヒープ。 汎用的な用途。 現在、ガベージコレクション作業項目の割り当てにのみ使用されます。<br />\- または -<br />ルックアサイドヒープ。 ルック アサイド リストに含まれる項目の数が事前に定義された上限 (通常は約 5,000 個の項目) に達した場合にルック アサイドで使用されます。<br /><br /> PGPOOL: IO システムプールには、システム4K ページプール、システム 64 K ページプール、およびシステム 256 K ページプールの3種類のサイズがあります。|  
|lookaside_id|**bigint**|スレッドローカルのルックアサイドメモリプロバイダーの ID。|  
|pagepool_id|**bigint**|スレッドローカルのページプールメモリプロバイダーの ID。|  
|allocated_bytes|**bigint**|このコンシューマーのために予約されたバイト数。|  
|used_bytes|**bigint**|このコンシューマーによって使用されているバイト数。 varheap メモリ コンシューマーのみに適用されます。|  
|allocation_count|**int**|割り当ての数。|  
|partition_count|**int**|内部使用のみです。|  
|sizeclass_count|**int**|内部使用のみです。|  
|min_sizeclass|**int**|内部使用のみです。|  
|max_sizeclass|**int**|内部使用のみです。|  
|memory_consumer_address|**varbinary**|コンシューマーの内部アドレス。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="user-scenario"></a>ユーザーシナリオ  
  
```  
-- system memory consumers @ instance  
selectmemory_consumer_type_desc,   
allocated_bytes/1024 as allocated_bytes_kb,   
used_bytes/1024 as used_bytes_kb, allocation_count  
from sys.dm_xtp_system_memory_consumers  
```  
  
 出力はシステム レベルのすべてのメモリ コンシューマーを示します。 たとえば、トランザクションのルックアサイドのコンシューマーがあります。  
  
```  
memory_consumer_type_name           memory_consumer_desc                           allocated_bytes_kb   used_bytes_kb        allocation_count  
-------------------------------          ---------------------                          -------------------  --------------        ----------------  
VARHEAP                                  Lookaside heap                                 0                    0                    0  
VARHEAP                                  System heap                                    768                  0                    2  
LOOKASIDE                                GC transaction map entry                       64                   64                   910  
LOOKASIDE                                Redo transaction map entry                     128                  128                  1260  
LOOKASIDE                                Recovery table cache entry                     448                  448                  8192  
LOOKASIDE                                Transaction recent rows                        3264                 3264                 4444  
LOOKASIDE                                Range cursor                                   0                    0                    0  
LOOKASIDE                                Hash cursor                                    3200                 3200                 11070  
LOOKASIDE                                Transaction save-point set entry               0                    0                    0  
LOOKASIDE                                Transaction partially-inserted rows set        704                  704                  1287  
LOOKASIDE                                Transaction constraint set                     576                  576                  1940  
LOOKASIDE                                Transaction save-point set                     0                    0                    0  
LOOKASIDE                                Transaction write set                          704                  704                  672  
LOOKASIDE                                Transaction scan set                           320                  320                  156  
LOOKASIDE                                Transaction read set                           704                  704                  343  
LOOKASIDE                                Transaction                                    4288                 4288                 1459  
PGPOOL                                   System 256K page pool                          5120                 5120                 20  
PGPOOL                                   System 64K page pool                           0                    0                    0  
PGPOOL                                   System 4K page pool                            24                   24                   6  
```  
  
 システム アロケーターが使用するメモリの合計を表示するには、以下を実行します。  
  
```  
select sum(allocated_bytes)/(1024*1024) as total_allocated_MB, sum(used_bytes)/(1024*1024) as total_used_MB   
from sys.dm_xtp_system_memory_consumers  
  
total_allocated_MB   total_used_MB  
-------------------- --------------------  
2                    2  
```  
  
## <a name="see-also"></a>参照  
 [メモリ最適化テーブルの動的管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
