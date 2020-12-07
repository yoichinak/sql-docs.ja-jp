---
description: sys.pdw_health_component_groups (Transact-sql)
title: sys.pdw_health_component_groups (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: 5ba27432-7a29-4420-b73d-def621c0b3ac
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8ac09a94a4821713bd1ef3cb2c852251d9b811c9
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036786"
---
# <a name="syspdw_health_component_groups-transact-sql"></a>sys.pdw_health_component_groups (Transact-sql)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  コンポーネントとデバイスの論理グループに関する情報を格納します。  
  
|列名|データ型|説明|Range|  
|-----------------|---------------|-----------------|-----------|  
|group_id|**int**|コンポーネントとデバイスの一意の識別子。<br /><br /> このビューのキー。|NOT NULL|  
|group_name|**nvarchar (255)**|コンポーネントとデバイスの論理グループ名。|NOT NULL|  
  
## <a name="see-also"></a>参照  
 [Azure Synapse Analytics と Parallel Data Warehouse のカタログ ビュー](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
