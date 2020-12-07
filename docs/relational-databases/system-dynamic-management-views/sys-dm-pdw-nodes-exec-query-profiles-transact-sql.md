---
title: sys.dm_pdw_nodes_exec_query_profiles (Transact-sql) |Microsoft Docs
description: クエリの実行中にリアルタイムのデータウェアハウスのクエリの進行状況を監視するために使用できる動的管理ビュー。
ms.custom: ''
ms.date: 10/14/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ''
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 591bba14af18f8c622ffa5547339fd0024cf4445
ms.sourcegitcommit: 76ab3b57718341c6057613c9bd38cf82fb17786e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92059520"
---
# <a name="sysdm_pdw_nodes_exec_query_profiles-transact-sql"></a>sys.dm_pdw_nodes_exec_query_profiles (Transact-sql)

[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

クエリの実行中にリアルタイムのデータウェアハウスのクエリの進行状況を監視します。   
  
## <a name="table-returned"></a>返されたテーブル
  
返されるカウンターは、スレッドごとの演算子ごとになります。 結果は動的であり、 `SET STATISTICS XML ON` クエリの終了時にのみ出力を作成するなど、既存のオプションの結果とは一致しません。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|pdw_node_id|**int**|ノードに関連付けられている一意の数値 ID。|
|session_id|**smallint**|このクエリが実行されるセッションを識別します。 dm_exec_sessions.session_id を参照します。|  
|request_id|**int**|ターゲット要求を識別します。 Dm_exec_sessions request_id を参照します。|  
|sql_handle|**varbinary(64)**|クエリが含まれているバッチまたはストアドプロシージャを一意に識別するトークンです。 Dm_exec_query_stats を参照します。|  
|plan_handle|**varbinary(64)**|は、実行され、そのプランがプランキャッシュに存在するか、現在実行中のバッチのクエリ実行プランを一意に識別するトークンです。 Dm_exec_query_stats plan_handle を参照します。|  
|physical_operator_name|**nvarchar (256)**|物理操作名。|  
|node_id|**int**|クエリ ツリー内の演算子ノードを識別します。|  
|thread_id|**int**|同じクエリ演算子ノードに属している (並列クエリの) スレッドを識別します。|  
|task_address|**varbinary (8)**|このスレッドが使用している SQLOS タスクを識別します。 Dm_os_tasks task_address を参照します。|  
|row_count|**bigint**|これまでに演算子によって返された行の数。|  
|rewind_count|**bigint**|これまでの巻き戻しの数。|  
|rebind_count|**bigint**|これまでの再バインドの数。|  
|end_of_scan_count|**bigint**|これまでのスキャンの終了の数。|  
|estimate_row_count|**bigint**|予測行数。 実際の row_count に estimated_row_count と比較すると便利な場合があります。|  
|first_active_time|**bigint**|演算子が最初に呼び出されたときの時間 (ミリ秒単位)。|  
|last_active_time|**bigint**|演算子が最後に呼び出された時刻 (ミリ秒単位)。|  
|open_time|**bigint**|開いたときのタイムスタンプ (ミリ秒単位)。|  
|first_row_time|**bigint**|最初の行が開かれたときのタイムスタンプ (ミリ秒単位)。|  
|last_row_time|**bigint**|最後の行を開いたときのタイムスタンプ (ミリ秒単位)。|  
|close_time|**bigint**|終了時のタイムスタンプ (ミリ秒単位)。|  
|elapsed_time_ms|**bigint**|これまでのターゲットノードの操作で使用された経過時間の合計 (ミリ秒単位)。|  
|cpu_time_ms|**bigint**|これまでのターゲットノードの操作で使用された合計 CPU 時間 (ミリ秒)。|  
|database_id|**smallint**|読み取りおよび書き込みが実行されたオブジェクトを含むデータベースの ID。|  
|object_id|**int**|読み取りおよび書き込みが実行されたオブジェクトの識別子。 sys.objects.object_id を参照します。|  
|index_id|**int**|行セットが開かれている対象のインデックス (ある場合)。|  
|scan_count|**bigint**|これまでのテーブル/インデックス スキャンの数。|  
|logical_read_count|**bigint**|これまでの論理読み取りの数。|  
|physical_read_count|**bigint**|これまでの物理読み取りの数。|  
|read_ahead_count|**bigint**|これまでの先読みの数。|  
|write_page_count|**bigint**|書き込むによるこれまでのページ書き込み回数。|  
|lob_logical_read_count|**bigint**|これまでの LOB 論理読み取り数。|  
|lob_physical_read_count|**bigint**|これまでの LOB 物理読み取りの数。|  
|lob_read_ahead_count|**bigint**|これまでの LOB 先読みの数。|  
|segment_read_count|**int**|これまでのセグメント先行読み取りの数。|  
|segment_skip_count|**int**|これまでにスキップされたセグメントの数。| 
|actual_read_row_count|**bigint**|残存述語が適用される前に演算子によって読み取られた行の数。| 
|estimated_read_row_count|**bigint**|**適用対象:** SP1 以降 [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 。 <br/>残存述語が適用される前に、演算子によって読み取られると推定される行の数。|  
  
## <a name="remarks"></a>解説

[Sys.dm_exec_query_profiles](./sys-dm-exec-query-profiles-transact-sql.md?view=sql-server-ver15)の同じ解説が適用されます。  

## <a name="permissions"></a>アクセス許可  
 サーバーに対する `VIEW SERVER STATE` 権限が必要です。  

## <a name="see-also"></a>関連項目

 [Azure Synapse Analytics と並列データウェアハウスの動的管理ビュー &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
   

 ## <a name="next-steps"></a>次のステップ 

Azure Synapse Analytics の開発の概要] (/azure/sql-data-warehouse/sql-data-warehouse-overview-develop) をご説明します。