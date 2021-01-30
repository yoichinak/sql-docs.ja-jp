---
description: sys.dm_pdw_os_performance_counters (Transact-sql)
title: sys.dm_pdw_os_performance_counters (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
dev_langs:
- TSQL
ms.assetid: 0673a8f8-8bed-41eb-8959-a9e3e9e03a65
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: '>= aps-pdw-2016'
ms.openlocfilehash: ea7840aa8514bd3bdbc03004e551c66ad01944fb
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99140138"
---
# <a name="sysdm_pdw_os_performance_counters-transact-sql"></a>sys.dm_pdw_os_performance_counters (Transact-sql)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  のノードの Windows パフォーマンスカウンターに関する情報が含まれてい [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] ます。  
  
|列名|データ型|説明|Range|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|カウンターを含むノードの ID。<br /><br /> このビューのキーは pdw_node_id と counter_name によって形成されます。|[Transact-sql&#41;&#40;sys.dm_pdw_nodes](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)の node_id を参照してください。|  
|counter_name|**nvarchar (255)**|Windows パフォーマンスカウンターの名前。||  
|counter_category|**nvarchar (255)**|Windows パフォーマンスカウンターカテゴリの名前。||  
|instance_name|**nvarchar (255)**|カウンターの特定のインスタンスの名前。||  
|counter_value|**10進数 (38, 10)**|カウンターの現在の値。||  
|last_update_time|**Datetime2 (3)**|値が最後に更新されたときのタイムスタンプ。||  
  
## <a name="see-also"></a>参照  
 [Azure Synapse Analytics と並列データウェアハウスの動的管理ビュー &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
