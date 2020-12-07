---
description: sys.spatial_indexes (Transact-SQL)
title: spatial_indexes (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.spatial_indexes_TSQL
- spatial_indexes
- spatial_indexes_TSQL
- sys.spatial_indexes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.spatial_indexes catalog view
ms.assetid: 40e967d5-2e8d-45af-bf5e-5251493cf7cb
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 313e28bdda409b96059e95e8ea0f0fca9ef4a6cb
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539474"
---
# <a name="sysspatial_indexes-transact-sql"></a>sys.spatial_indexes (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  空間インデックスの主インデックス情報を表します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|\<inherited columns>||は [、列を継承](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)します。|  
|spatial_index_type|**tinyint**|空間インデックスの種類です。<br /><br /> 1 = 幾何学的空間インデックス<br /><br /> 2 = 地理的空間インデックス|  
|spatial_index_type_desc|**nvarchar(60)**|空間インデックスの説明を入力します。<br /><br /> GEOMETRY = 幾何学的空間インデックス<br /><br /> GEOGRAPHY = 地理的空間インデックス|  
|tessellation_scheme|**sysname**|テセレーション スキームの名前です。<br /><br /> GEOMETRY_GRID、GEOMETRY_AUTO_GRID、<br /><br /> GEOGRAPHY_GRID、GEOGRAPHY_AUTO_GRID<br /><br /> 注: テセレーションスキームの詳細については、「 [空間インデックスの概要](../../relational-databases/spatial/spatial-indexes-overview.md)」を参照してください。|  
|\<inherited columns>||は [、列を継承](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)します。<br /><br /> 継承された列 has_filter および filter_definition は、空間インデックスに固有の列の後に表示されます。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>参照  
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.spatial_index_tessellations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-spatial-index-tessellations-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [空間インデックスの概要](../../relational-databases/spatial/spatial-indexes-overview.md)  
  
  
