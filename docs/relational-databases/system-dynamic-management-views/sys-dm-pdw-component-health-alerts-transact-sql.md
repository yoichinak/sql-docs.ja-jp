---
description: sys.dm_pdw_component_health_alerts (Transact-sql)
title: sys.dm_pdw_component_health_alerts (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 88f05392-1e97-4693-ba60-a4910af3c000
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: '>= aps-pdw-2016'
ms.openlocfilehash: 83a3a237da01eb677ef8282940b334fa28b42637
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98093985"
---
# <a name="sysdm_pdw_component_health_alerts-transact-sql"></a>sys.dm_pdw_component_health_alerts (Transact-sql)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  以前に発行されたアラートをアプライアンスコンポーネントに格納します。  
  
|列名|データ型|説明|Range|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|ノードの一意識別子 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 。<br /><br /> pdw_node_id、component_id、component_instance_id、alert_id、および alert_instance_id を使用して、このビューのキーを形成します。|NOT NULL|  
|component_id|**int**|コンポーネントの ID。 「 [Sys.pdw_health_components &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)」を参照してください。<br /><br /> pdw_node_id、component_id、component_instance_id、alert_id、および alert_instance_id を使用して、このビューのキーを形成します。|NOT NULL|  
|component_instance_id|**nvarchar (255)**|pdw_node_id、component_id、component_instance_id、alert_id、および alert_instance_id を使用して、このビューのキーを形成します。|NOT NULL|  
|alert_id|**int**|アラートの種類の ID。 「 [Sys.pdw_health_alerts &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md)」を参照してください。<br /><br /> pdw_node_id、component_id、component_instance_id、alert_id、および alert_instance_id を使用して、このビューのキーを形成します。|NOT NULL|  
|alert_instance_id|**nvarchar (36)**|指定された警告のインスタンスを識別します。<br /><br /> pdw_node_id、component_id、component_instance_id、alert_id、および alert_instance_id を使用して、このビューのキーを形成します。|NOT NULL|  
|previous_value|**nvarchar (255)**|アラートの種類が StatusChange の場合に使用します。 これは、以前のコンポーネントの状態です。 種類がしきい値のアラートの値は NULL です。 アラートの種類の一覧については、「 [sys.pdw_health_alerts &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) 」を参照してください。|NULL|  
|current_value|**nvarchar (255)**|アラートの種類が StatusChange の場合に使用します。 これは、現在のコンポーネントのステータスです。 種類がしきい値のアラートの値は NULL です。 アラートの種類の一覧については、「 [sys.pdw_health_alerts &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) 」を参照してください。|NULL|  
|create_time|**datetime**|アラートが生成された日時。|NOT NULL|  
  
## <a name="see-also"></a>参照  
 [Azure Synapse Analytics と並列データウェアハウスの動的管理ビュー &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
