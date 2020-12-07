---
description: sys.dm_exec_compute_node_status (Transact-sql)
title: sys.dm_exec_compute_node_status (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DM_EXEC_COMPUTE_NODE_STATUS_TSQL
- DM_EXEC_COMPUTE_NODE_STATUS
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- dm_exec_compute_node_status
- sys.dm_exec_compute_node_status management view
ms.assetid: b606f91f-3a08-4a4f-bb57-32ae155b3738
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5ba6ccebd6274fc77b12a64b365f4c56ef9783c2
ms.sourcegitcommit: 32135463a8494d9ed1600a58f51819359e3c09dc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2020
ms.locfileid: "91834169"
---
# <a name="sysdm_exec_compute_node_status-transact-sql"></a>sys.dm_exec_compute_node_status (Transact-sql)
[!INCLUDE [sqlserver2016-asa-pdw](../../includes/applies-to-version/sqlserver2016-asa-pdw.md)]

  すべての PolyBase ノードのパフォーマンスと状態に関する追加情報を保持します。 ノードごとに1行を一覧表示します。  
  
|列名|データ型|説明|Range|  
|-----------------|---------------|-----------------|-----------|  
|compute_node_id|`int`|ノードに関連付けられている一意の数値 id。|種類に関係なく、スケールアウトクラスター全体で一意です。|  
|process_id|`int`|||  
|process_name|`nvarchar(255)`|ノードの論理名。|適切な長さの任意の文字列。|  
|allocated_memory|`bigint`|このノードで割り当てられたメモリの合計。||  
|available_memory|`bigint`|このノードで使用可能なメモリの合計。||  
|process_cpu_usage|`bigint`|プロセス CPU 使用率の合計 (ティック単位)。||  
|total_cpu_usage|`bigint`|合計 CPU 使用率 (ティック単位)。||  
|thread_count|`bigint`|このノードで使用されているスレッドの合計数。||  
|handle_count|`bigint`|このノードで使用されているハンドルの合計数。||  
|total_elapsed_time|`bigint`|システムの開始または再起動からの経過時間の合計。|システムの開始または再起動からの経過時間の合計。 Total_elapsed_time が整数の最大値 (ミリ秒単位で24.8 日) を超えた場合、オーバーフローによる具体化エラーが発生します。ミリ秒単位の最大値は24.8 日に相当します。|  
|is_available|`bit`|このノードが使用可能かどうかを示すフラグです。||  
|sent_time|`datetime`|最後にネットワークパッケージが送信された時刻||  
|received_time|`datetime`|ネットワークパッケージがこのノードによって最後に送信された時刻。||  
|error_id|`nvarchar(36)`|このノードで発生した最後のエラーの一意の識別子。||
|compute_pool_id|`int`|プールの一意の識別子。|

## <a name="see-also"></a>参照  
 [動的管理ビューを使用した PolyBase のトラブルシューティング](/previous-versions/sql/sql-server-2016/mt146389(v=sql.130))   
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;データベース関連の動的管理ビュー ](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
