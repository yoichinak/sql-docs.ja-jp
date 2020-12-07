---
description: sys.dm_pdw_node_status (Transact-sql)
title: sys.dm_pdw_node_status (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8e263b65-81d0-49d0-8873-62ef424369d6
author: markingmyname
ms.author: maghan
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 267b2aa14e85f77af91a0cf1a5640a16ee158215
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035315"
---
# <a name="sysdm_pdw_node_status-transact-sql"></a>sys.dm_pdw_node_status (Transact-sql)

[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  すべてのアプライアンスノードのパフォーマンスと状態に関する追加情報 ( [sys.dm_pdw_nodes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)) を保持します。 アプライアンス内のノードごとに1行が一覧表示されます。  
  
|列名|データ型|説明|Range|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|ノードに関連付けられている一意の数値 id。<br /><br /> このビューのキー。|種類に関係なく、アプライアンス全体で一意です。|  
|process_id|**int**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|process_name|**nvarchar (255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|allocated_memory|**bigint**|このノードで割り当てられたメモリの合計。||  
|available_memory|**bigint**|このノードで使用可能なメモリの合計。||  
|process_cpu_usage|**bigint**|プロセス CPU 使用率の合計 (ティック単位)。||  
|total_cpu_usage|**bigint**|合計 CPU 使用率 (ティック単位)。||  
|thread_count|**bigint**|このノードで使用されているスレッドの合計数。||  
|handle_count|**bigint**|このノードで使用されているハンドルの合計数。||  
|total_elapsed_time|**bigint**|システムの開始または再起動からの経過時間の合計。|システムの開始または再起動からの経過時間の合計。 Total_elapsed_time が整数の最大値 (ミリ秒単位で24.8 日) を超えた場合、オーバーフローによる具体化エラーが発生します。<br /><br /> ミリ秒単位の最大値は24.8 日に相当します。|  
|is_available|**bit**|このノードが使用可能かどうかを示すフラグです。||  
|sent_time|**datetime**|ネットワークパッケージがこのノードによって最後に送信された時刻。||  
|received_time|**datetime**|ネットワークパッケージがこのノードによって最後に受信された時刻。||  
|error_id|**nvarchar (36)**|このノードで発生した最後のエラーの一意の識別子。||  
  
## <a name="see-also"></a>参照  
 [Azure Synapse Analytics と並列データウェアハウスの動的管理ビュー &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
