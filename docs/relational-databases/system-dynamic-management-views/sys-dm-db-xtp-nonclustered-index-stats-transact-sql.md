---
description: dm_db_xtp_nonclustered_index_stats (Transact-sql)
title: dm_db_xtp_nonclustered_index_stats (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_nonclustered_index_stats_TSQL
- dm_db_xtp_nonclustered_index_stats
- sys.dm_db_xtp_nonclustered_index_stats_TSQL
- sys.dm_db_xtp_nonclustered_index_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_nonclustered_index_stats
ms.assetid: d55ba31c-296c-419b-9c4b-c126e0a3d156
author: markingmyname
ms.author: maghan
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8c48807db007bd5d622283fd07c3aed8aec0198a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542211"
---
# <a name="sysdm_db_xtp_nonclustered_index_stats-transact-sql"></a>dm_db_xtp_nonclustered_index_stats (Transact-sql)
[!INCLUDE[sql-asdb-asdbmi](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  sys.dm_db_xtp_nonclustered_index_stats には、メモリ最適化テーブルの非クラスター化インデックスの操作に関する統計が含まれます。 dm_db_xtp_nonclustered_index_stats 現在のデータベース内のメモリ最適化テーブルの非クラスター化インデックスごとに1行のデータを格納します。  
  
 sys.dm_db_xtp_nonclustered_index_stats に反映されている統計は、インメモリ インデックス構造の作成時に収集されます。 インメモリインデックス構造は、データベースの再起動時に再作成されます。  
  
 DML 操作中やデータベースがオンラインになったときに、インデックスの利用状況を把握して監視するには、dm_db_xtp_nonclustered_index_stats を使用します。 メモリ最適化テーブルを含むデータベースを再起動すると、一度に1行ずつメモリに挿入することによってインデックスが作成されます。 ページ分割、マージ、および統合の数は、データベースがオンラインになったときにインデックスを構築するために実行された作業を理解するのに役立ちます。 また、一連の DML 操作の前後にこれらのカウントを確認することもできます。  
  
 再試行回数が多い場合は、同時実行の問題を示しています。サポートにお問い合わせ [!INCLUDE[msCoName](../../includes/msconame-md.md)] ください。  
  
 メモリ最適化された非クラスター化インデックスの詳細については、 [SQL Server インメモリ OLTP の概要](https://t.co/T6zToWc6y6)、ページ17を参照してください。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|object_id|**int**|オブジェクトの ID。|  
|xtp_object_id|**bigint**|メモリ最適化テーブルの ID。|  
|index_id|**int**|インデックスの ID。|  
|delta_pages|**bigint**|ツリー内のこのインデックスに対するデルタページの合計数。|  
|internal_pages|**bigint**|内部使用です。 ツリー内のこのインデックスに対する内部ページの合計数。|  
|leaf_pages|**bigint**|ツリー内のこのインデックスに対するリーフページの合計数。|  
|outstanding_retired_nodes|**bigint**|内部使用です。 内部構造のこのインデックスに対するノードの合計数。|  
|page_update_count|**bigint**|インデックス内のページを更新する操作の累積数。|  
|page_update_retry_count|**bigint**|インデックス内のページを更新する操作の再試行の累積数。|  
|page_consolidation_count|**bigint**|インデックス内のページ統合の累積数。|  
|page_consolidation_retry_count|**bigint**|ページ統合操作の再試行の累積数。|  
|page_split_count|**bigint**|インデックス内のページ分割操作の累積数。|  
|page_split_retry_count|**bigint**|ページ分割操作の再試行の累積数。|  
|key_split_count|**bigint**|インデックス内のキー分割の累積数。|  
|key_split_retry_count|**bigint**|キー分割操作の再試行の累積数。|  
|page_merge_count|**bigint**|インデックスのページ マージ操作の累積数。|  
|page_merge_retry_count|**bigint**|ページマージ操作の再試行の累積数。|  
|key_merge_count|**bigint**|インデックス内のキーマージ操作の累積数。|  
|key_merge_retry_count|**bigint**|キーマージ操作の再試行の累積数。|  
  
## <a name="permissions"></a>アクセス許可  
 現在のデータベースに対する VIEW DATABASE STATE 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [メモリ最適化テーブルの動的管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
