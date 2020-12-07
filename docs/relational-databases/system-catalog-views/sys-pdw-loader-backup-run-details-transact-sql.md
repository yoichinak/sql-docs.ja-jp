---
description: sys.pdw_loader_backup_run_details (Transact-sql)
title: sys.pdw_loader_backup_run_details (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 04fc004f-ee15-4d7a-be08-78357aa99b55
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 243bbff033bfa3b9327227da6fdbf200d28e1ee5
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92034811"
---
# <a name="syspdw_loader_backup_run_details-transact-sql"></a>sys.pdw_loader_backup_run_details (Transact-sql)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  の詳細な情報については [sys.pdw_loader_backup_runs &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)に関する情報以外に、での進行中のバックアップと復元操作、およびで [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] の進行中および完了したバックアップ、復元、および読み込み操作に関する情報が含まれてい [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] ます。 情報は、システムの再起動の間で永続化します。  
  
|列名|データ型|説明|Range|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|特定のバックアップまたは復元の実行の一意の識別子。<br /><br /> このビューのキーは run_id と pdw_node_id によって形成されます。||  
|pdw_node_id|**int**|このレコードが詳細を保持するアプライアンスノードの一意識別子。<br /><br /> このビューのキーは run_id と pdw_node_id によって形成されます。|[Transact-sql&#41;&#40;sys.dm_pdw_nodes](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)の node_id を参照してください。|  
|status|**nvarchar (16)**|実行の現在の状態。|' 取り消された '、' COMPLETED '、' FAILED '、' QUEUED '、' RUNNING '|  
|start_time|**datetime**|この特定のノードで操作が開始された時刻。||  
|end_time|**datetime**|この特定のノードで操作が終了した時刻 (存在する場合)。||  
|total_elapsed_time|**int**|この特定のノードで操作が実行されていた合計時間。|Total_elapsed_time が整数の最大値 (ミリ秒単位で24.8 日) を超えた場合、オーバーフローによる具体化エラーが発生します。<br /><br /> ミリ秒単位の最大値は24.8 日に相当します。|  
|progress|**int**|比率で表された操作の進行状況。|0 から 100|  
  
## <a name="see-also"></a>参照  
 [Azure Synapse Analytics と Parallel Data Warehouse のカタログ ビュー](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
