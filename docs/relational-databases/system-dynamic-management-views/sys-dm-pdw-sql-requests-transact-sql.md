---
description: sys.dm_pdw_sql_requests (Transact-sql)
title: sys.dm_pdw_sql_requests (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 44e19609-902c-46cf-acdf-19ea75011365
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 3bbf99db3971ecb9979c1ef234d1f57c1761afa9
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035205"
---
# <a name="sysdm_pdw_sql_requests-transact-sql"></a>sys.dm_pdw_sql_requests (Transact-sql)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  クエリの SQL ステップの一部として、すべての SQL Server クエリディストリビューションに関する情報を保持します。  
  
|列名|データ型|説明|Range|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|この SQL クエリディストリビューションが属するクエリの一意識別子。<br /><br /> request_id、step_index、および distribution_id は、このビューのキーを形成します。|[Transact-sql&#41;&#40;sys.dm_pdw_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)の request_id を参照してください。|  
|step_index|**int**|この分布が含まれるクエリステップのインデックス。<br /><br /> request_id、step_index、および distribution_id は、このビューのキーを形成します。|[Transact-sql&#41;&#40;sys.dm_pdw_request_steps](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)の step_index を参照してください。|  
|pdw_node_id|**int**|このクエリの分布が実行されるノードの一意の識別子。|[Transact-sql&#41;&#40;sys.dm_pdw_nodes](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)の node_id を参照してください。|  
|distribution_id|**int**|このクエリの分布が実行されるディストリビューションの一意識別子。<br /><br /> request_id、step_index、および distribution_id は、このビューのキーを形成します。|[Transact-sql&#41;&#40;sys.pdw_distributions](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md)の distribution_id を参照してください。 配布スコープではなく、ノードスコープで実行される要求の場合は-1 に設定します。|  
|status|**nvarchar(32)**|クエリの分布の現在の状態。|保留中、実行中、失敗、取り消し済み、完了、中止、キャンセル送信|  
|error_id|**nvarchar (36)**|このクエリの分布に関連付けられているエラーの一意識別子 (存在する場合)。|[Transact-sql&#41;&#40;sys.dm_pdw_errors](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md)の error_id を参照してください。 エラーが発生しなかった場合は、NULL に設定します。|  
|start_time|**datetime**|クエリの配布が実行を開始した時刻。|小さいまたは現在の時刻に等しいが、このクエリのディストリビューションが属しているクエリステップの start_time 以上|  
|end_time|**datetime**|このクエリの分布が実行を完了した時刻、が取り消された、または失敗した時刻。|開始時刻が大きいか等しいか、またはクエリの分布が実行中またはキューに置かれている場合は NULL に設定します。|  
|total_elapsed_time|**int**|クエリの分布が実行されている時間をミリ秒単位で表します。|0以上です。 完了、失敗、または取り消されたクエリのディストリビューションの start_time と end_time の差分と同じです。<br /><br /> Total_elapsed_time が整数の最大値を超えた場合、total_elapsed_time は引き続き最大値になります。 この条件により、"最大値を超えました。" という警告が生成されます。<br /><br /> ミリ秒単位の最大値は24.8 日に相当します。|  
|row_count|**bigint**|このクエリの分布によって変更または読み取られた行の数。|CREATE TABLE や DROP TABLE などのデータを変更または返さない操作の場合は-1。|  
|調べる|**int**|クエリの配布を実行している SQL Server インスタンスのセッション id。||  
|command|**nvarchar (4000)**|このクエリの配布用のコマンドのフルテキストです。|任意の有効なクエリまたは要求文字列。|  
  
 このビューで保持される最大行数の詳細については、「 [容量制限](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) 」トピックの「メタデータ」セクションを参照してください。  
  
## <a name="see-also"></a>参照  
 [Azure Synapse Analytics と並列データウェアハウスの動的管理ビュー &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
