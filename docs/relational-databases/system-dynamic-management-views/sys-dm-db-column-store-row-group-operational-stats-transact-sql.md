---
description: dm_db_column_store_row_group_operational_stats (Transact-sql)
title: dm_db_column_store_row_group_operational_stats (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 31b71c68-50a0-4fd8-a7fe-2d2292be1163
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d384029cb8a226dfed01d14360247d00cb998cd8
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537617"
---
# <a name="sysdm_db_column_store_row_group_operational_stats-transact-sql"></a>dm_db_column_store_row_group_operational_stats (Transact-sql)

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

  列ストアインデックスの圧縮された行グループについて、現在の行レベル i/o、ロック、およびアクセスメソッドのアクティビティを返します。 Dm_db_column_store_row_group_operational_stats を使用して、ユーザークエリが列ストアインデックスの圧縮された行グループまたはパーティションに対する読み取りまたは書き込みを待機する時間の長さを追跡し、重要な i/o アクティビティまたはホットスポットが発生している行グループを特定し **ます** 。  
  
 インメモリ列ストアインデックスは、この DMV には表示されません。  
 
 
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|列ストアインデックスを持つテーブルの ID。|  
|**index_id**|**int**|列ストアインデックスの ID。|  
|**partition_number**|**int**|インデックスまたはヒープ内の、1 から始まるパーティション番号。|  
|**row_group_id**|**int**|列ストアインデックスの行グループの ID。 これは、パーティション内で一意です。|  
|**scan_count**|**int**|前回の SQL の再起動以降に行グループを通過するスキャンの回数。|  
|**delete_buffer_scan_count**|**int**|削除バッファーがこの行グループ内の削除された行を確認するために使用された回数。 これには、メモリ内のハッシュテーブルおよび基になる btree へのアクセスが含まれます。|  
|**index_scan_count**|**int**|列ストアインデックスパーティションがスキャンされた回数。 これは、パーティション内のすべての行グループで同じです。|  
|**rowgroup_lock_count**|**bigint**|前回の SQL 再起動以降にこの行グループに対して行われたロック要求の累積数。|  
|**rowgroup_lock_wait_count**|**bigint**|前回の SQL の再起動以降に、データベースエンジンがこの行グループのロックを待機した累積回数。|  
|**rowgroup_lock_wait_in_ms**|**bigint**|前回の SQL の再起動以降に、データベースエンジンがこの行グループのロックを待機した累積ミリ秒数。|  
  
## <a name="permissions"></a>アクセス許可  
 次の権限が必要です。  
  
-   Object_id によって指定されたテーブルに対する CONTROL 権限。  
  
-   オブジェクトのワイルドカード @*object_id* = NULL を使用して、データベース内のすべてのオブジェクトに関する情報を返す VIEW database STATE 権限  
  
 VIEW DATABASE STATE 権限を許可すると、特定のオブジェクトに対して CONTROL 権限が拒否されていたとしても、データベース内のすべてのオブジェクトを取得することができます。  
  
 VIEW DATABASE STATE 権限を拒否すると、特定のオブジェクトに対する CONTROL 権限が許可されていたとしても、そのデータベース内のどのオブジェクトも取得できません。 また、データベースのワイルドカード @*database_id*= NULL が指定されている場合、データベースは省略されます。  
  
 詳細については、「 [transact-sql&#41;&#40;動的管理ビューと関数 ](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [インデックス関連の動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [パフォーマンスの監視とチューニング](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [dm_db_index_usage_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)   
 [sys.dm_os_latch_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)   
 [dm_db_partition_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)   
 [sys.allocation_units &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  

