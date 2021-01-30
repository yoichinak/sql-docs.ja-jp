---
description: sys.dm_pdw_sys_info (Transact-sql)
title: sys.dm_pdw_sys_info (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: reference
dev_langs:
- TSQL
ms.assetid: 686976b4-2d5d-4d64-bf12-56eba1dc59b1
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest'
ms.openlocfilehash: 7d69c8c58f46d6fbbccc5ee98ead54f222b5e2a9
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99139078"
---
# <a name="sysdm_pdw_sys_info-transact-sql"></a>sys.dm_pdw_sys_info (Transact-sql)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  アプライアンスの全体的なアクティビティを反映するアプライアンスレベルのカウンターのセットを提供します。  
  
|列名|データ型|説明|Range|  
|-----------------|---------------|-----------------|-----------|  
|total_sessions|**int**|現在システム内にあるセッションの数。|0を max_active_sessions (下記参照)。|  
|idle_sessions|**int**|現在アイドル状態のセッションの数。||  
|active_requests|**int**|現在実行中のアクティブな要求の数。||  
|queued_requests|**int**|現在キューに置かれている要求の数。||  
|active_loads|**int**|システムで現在実行されている読み込みの数。||  
|queued_loads|**int**|実行を待機しているキューに置かれた読み込みの数。||  
|active_backups|**int**|現在実行中のバックアップの数。||  
|active_restores|**int**|現在実行中のバックアップ復元の数。||  
  
## <a name="see-also"></a>参照  
 [Azure Synapse Analytics と並列データウェアハウスの動的管理ビュー &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
