---
description: sys.dm_fts_memory_pools (Transact-sql)
title: sys.dm_fts_memory_pools (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- dm_fts_memory_pools_TSQL
- sys.dm_fts_memory_pools_TSQL
- sys.dm_fts_memory_pools
- dm_fts_memory_pools
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_memory_pools dynamic management view
ms.assetid: 24747239-cd78-4d55-a00a-19233a457f42
author: pmasl
ms.author: pelopes
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4864095f66786ce08227b6853b31c4f190f0d22a
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99161932"
---
# <a name="sysdm_fts_memory_pools-transact-sql"></a>sys.dm_fts_memory_pools (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  フルテキストクロールまたはフルテキストクロール範囲の Full-Text Gatherer コンポーネントで使用できる共有メモリプールに関する情報を返します。  
   
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**pool_id**|**int**|割り当てられたメモリプールの ID。<br /><br /> 0 = 小さいバッファー<br /><br /> 1 = 大きいバッファー|  
|**buffer_size**|**int**|メモリ プール内に割り当てられた各バッファーのサイズ。|  
|**min_buffer_limit**|**int**|メモリプールで許可されるバッファーの最小数。|  
|**max_buffer_limit**|**int**|メモリプールで許可されるバッファーの最大数。|  
|**buffer_count**|**int**|メモリプール内の現在の共有メモリバッファーの数。|  
  
## <a name="permissions"></a>アクセス許可  

で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   
SQL Database Basic、S0、S1 のサービス目標、およびエラスティックプール内のデータベースについて `Server admin` は、または `Azure Active Directory admin` アカウントが必要です。 その他のすべての SQL Database サービスの目的で `VIEW DATABASE STATE` は、データベースで権限が必要になります。   
 
## <a name="physical-joins"></a>物理結合  
 ![この動的管理ビューの重要な結合](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-memory-pools-1.gif "この動的管理ビューの重要な結合")  
  
## <a name="relationship-cardinalities"></a>リレーションシップ基数  
  
|差出人|終了|リレーションシップ|  
|----------|--------|------------------|  
|dm_fts_memory_buffers dm_fts_memory_buffers.pool_id|dm_fts_memory_pools.pool_id|多対一|  
  
## <a name="examples"></a>例  
 次の例では、[!INCLUDE[msCoName](../../includes/msconame-md.md)] プロセスの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フルテキスト Gatherer コンポーネントが所有する共有メモリの合計を返します。  
  
```  
SELECT SUM(buffer_size * buffer_count) AS "total memory"   
    FROM sys.dm_fts_memory_pools;  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のフルテキスト検索とセマンティック検索の動的管理ビューおよび関数 ](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  
