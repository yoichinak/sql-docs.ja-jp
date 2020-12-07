---
description: sys.dm_xtp_gc_stats (Transact-SQL)
title: dm_xtp_gc_stats (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_xtp_gc_stats
- dm_xtp_gc_stats_TSQL
- sys.dm_xtp_gc_stats_TSQL
- sys.dm_xtp_gc_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xtp_gc_stats dynamic management view
ms.assetid: 8287d611-50e3-43e1-ba8d-3e3793d3ba0e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e69ed7bc99077962489a81e44484fb2a90b33b70
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543810"
---
# <a name="sysdm_xtp_gc_stats-transact-sql"></a>sys.dm_xtp_gc_stats (Transact-SQL)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  ガベージコレクションプロセスの現在の動作に関する情報 (全体的な統計情報) を提供 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] します。  
  
 行は、通常のトランザクション処理の一部として、またはメインのガベージコレクションスレッド (アイドルワーカーと呼ばれます) によってガベージコレクトされます。 ユーザートランザクションがコミットされると、ガベージコレクションキュー dm_xtp_gc_queue_stats (デキュー[&#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xtp-gc-queue-stats-transact-sql.md)) から1つの作業項目がされます。 ガベージ コレクションが可能であってもメイン ユーザー トランザクションでアクセスされなかった行のガベージ コレクションは、ダスティ コーナー スキャン (使用頻度が低いインデックスの領域のスキャン) の一環としてアイドル ワーカーによって実行されます。  
  
 詳細については、「[インメモリ OLTP &#40;インメモリ最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)」を参照してください。  
  
|列名|種類|説明|  
|-----------------|----------|-----------------|  
|rows_examined|**bigint**|サーバーの起動後にガベージコレクションサブシステムによって検査された行の数。|  
|rows_no_sweep_needed|**bigint**|ダスティコーナースキャンなしで削除された行の数。|  
|rows_first_in_bucket|**bigint**|ガベージ コレクションによって検査された、ハッシュ バケットの最初の行であった行の数。|  
|rows_first_in_bucket_removed|**bigint**|削除されたハッシュバケットの最初の行であるガベージコレクションによって検査された行の数。|  
|rows_marked_for_unlink|**bigint**|ガベージ コレクションによって検査された、ref_count が =0 のインデックスで既に unlinked としてマークされていた行の数。|  
|parallel_assist_count|**bigint**|ユーザー トランザクションで処理された行の数。|  
|idle_worker_count|**bigint**|アイドル状態のワーカーによって処理されたガベージ行の数。|  
|sweep_scans_started|**bigint**|ガベージコレクションサブシステムによって実行されたダスティコーナースキャンの数。|  
|sweep_scans_retries|**bigint**|ガベージコレクションサブシステムによって実行されたダスティコーナースキャンの数。|  
|sweep_rows_touched|**bigint**|ダスティコーナー処理によって読み取られた行。|  
|sweep_rows_expiring|**bigint**|ダスティコーナー処理によって読み取られた、期限切れの行。|  
|sweep_rows_expired|**bigint**|ダスティ コーナー処理によって読み取られた、期限切れの行。|  
|sweep_rows_expired_removed|**bigint**|ダスティコーナー処理によって削除された期限切れの行。|  
  
## <a name="permissions"></a>アクセス許可  
 インスタンスに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="usage-scenario"></a>使用シナリオ  
 出力例を次に示します。  
  
```  
rows_examined        rows_no_sweep_needed rows_first_in_bucket rows_first_in_bucket_removed  
280085               209512               69905  
rows_first_in_bucket_removed rows_marked_for_unlink parallel_assist_count idle_worker_count  
69905                        0                      8953  
  
idle_worker_count    sweep_scans_started  sweep_scan_retries   sweep_rows_touched  
10306473             670                  0                    1343  
  
sweep_rows_expiring  sweep_rows_expired   sweep_rows_expired_removed  
               0                 673673  
```  
  
## <a name="see-also"></a>参照  
 [メモリ最適化テーブルの動的管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
