---
description: sys.dm_pdw_os_event_logs (Transact-sql)
title: sys.dm_pdw_os_event_logs (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a0daa8cf-72e2-4349-8be1-d3cc0f9b1e02
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: '>= aps-pdw-2016'
ms.openlocfilehash: af5633fc5e1a169c71197ac77a715e4b28da2b57
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98092702"
---
# <a name="sysdm_pdw_os_event_logs-transact-sql"></a>sys.dm_pdw_os_event_logs (Transact-sql)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  異なるノード上のさまざまな Windows イベントログに関する情報を保持します。  
  
|列名|データ型|説明|Range|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|このログの基になっているアプライアンスノード。<br /><br /> このビューのキーは pdw_node_id と log_name によって形成されます。||  
|log_name|**nvarchar (255)**|Windows イベントログの名前。<br /><br /> このビューのキーは pdw_node_id と log_name によって形成されます。||  
|log_source|**nvarchar (255)**|Windows イベントログのソース名。||  
|event_id|**int**|イベントの ID。 一意ではありません。||  
|event_type|**nvarchar (255)**|重大度を識別するイベントの種類。|' Information '、' Warning '、' Error '|  
|event_message|**nvarchar (4000)**|イベントの詳細。||  
|generate_time|**datetime**|イベントが作成された時刻。||  
|write_time|**datetime**|イベントが実際にログに書き込まれた時刻。||  
  
 このビューで保持される最大行数の詳細については、「 [容量制限](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) 」トピックの「メタデータ」セクションを参照してください。 
  
## <a name="see-also"></a>参照  
 [Azure Synapse Analytics と並列データウェアハウスの動的管理ビュー &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
