---
description: sys.spatial_index_tessellations (Transact-SQL)
title: spatial_index_tessellations (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- spatial_index_tessellations
- sys.spatial_index_tessellations_TSQL
- spatial_index_tessellations_TSQL
- sys.spatial_index_tessellations
dev_langs:
- TSQL
helpviewer_keywords:
- sys.spatial_index_tessellations catalog view
ms.assetid: 8b17a9a4-b57f-4220-8138-fc73581b1670
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 783c73ba514e348cd515929ae988c4097225ec5b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539496"
---
# <a name="sysspatial_index_tessellations-transact-sql"></a>sys.spatial_index_tessellations (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

 各空間インデックスのテセレーション スキームおよびパラメーターに関する情報を表します。  
  
> [!NOTE]  
>  テセレーションについて詳しくは、「[空間インデックスの概要](../../relational-databases/spatial/spatial-indexes-overview.md)」をご覧ください。  
  

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|object_id|**int**|インデックスが定義されているオブジェクトの ID。 各 (object_id、index_id) ペアには、 [sys. spatial_indexes](../../relational-databases/system-catalog-views/sys-spatial-indexes-transact-sql.md)に対応するエントリがあります。|  
|index_id|**int**|インデックス付き列が定義されている空間インデックスの ID|  
|tessellation_scheme|**sysname**|テセレーションスキームの名前。次のいずれかです: GEOMETRY_GRID、GEOGRAPHY_GRID|  
|bounding_box_xmin|**float(53)**|境界ボックスの左下隅の x 座標。次のうちのどれかです: NULL = 特定のテセレーションスキームには適用されません (GEOGRAPHY_GRID など) *n* = tessellation_scheme が GEOMETRY_GRID 場合は、x 座標の最小値です。                     **注:** 境界ボックスパラメーターによって定義される座標は、 [空間参照識別子 (SRID)](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)に従って、各オブジェクトに対して解釈されます。|  
|bounding_box_ymin|**float(53)**|境界ボックスの左下隅の Y 座標 (次のいずれか): NULL = 特定のテセレーションスキームには適用されません (GEOGRAPHY_GRID など) *n* = tessellation_scheme が GEOMETRY_GRID 場合、y 座標の最小値|  
|bounding_box_xmax|**float(53)**|境界ボックスの右上隅の X 座標 (次のいずれか): NULL = 特定のテセレーションスキームには適用されません (GEOGRAPHY_GRID など) *n* = tessellation_scheme が GEOMETRY_GRID 場合、x 座標の最大値|  
|bounding_box_ymax|**float(53)**|境界ボックスの右上隅の Y 座標 (次のいずれか): NULL = 特定のテセレーションスキームには適用されません (GEOGRAPHY_GRID など) *n* = tessellation_scheme が GEOMETRY_GRID 場合、y 座標の最大値|  
|level_1_grid|**smallint**|最上位レベルのグリッドのグリッド密度です。 Tessellation_scheme が GEOMETRY_GRID または GEOGRAPHY_GRID の場合は、次のいずれかになります:16 = 4 ×4グリッド (低) 64 = 8 ×8グリッド (中) 256 = 16 x 16 グリッド (HIGH) NULL = 特定の空間インデックスの種類またはテセレーションスキームに適用されません。  新しい SQL Server 11 テセレーションが使用されると、NULL が返されます。|  
|level_1_grid_desc|**nvarchar(60)**|最上位レベルのグリッドのグリッド密度: 低中高 NULL = 特定の空間インデックスの種類またはテセレーションスキームには適用されません。  新しい SQL Server 11 テセレーションが使用されると、NULL が返されます。|  
|level_2_grid|**smallint**|第2レベルのグリッドのグリッド密度。 Tessellation_scheme が GEOMETRY_GRID または GEOGRAPHY_GRID の場合は、次のいずれかになります:16 = 4 ×4グリッド (低) 64 = 8 ×8グリッド (中) 256 = 16 x 16 グリッド (HIGH) NULL = 特定の空間インデックスの種類またはテセレーションスキームに適用されません。  新しい SQL Server 11 テセレーションが使用されると、NULL が返されます。|  
|level_2_grid_desc|**nvarchar(60)**|第2レベルのグリッドのグリッド密度: 低中高 NULL = 特定の空間インデックスの種類またはテセレーションスキームには適用されません。  新しい SQL Server 11 テセレーションが使用されると、NULL が返されます。|  
|level_3_grid|**smallint**|第3レベルのグリッドのグリッド密度。   Tessellation_scheme が GEOMETRY_GRID または GEOGRAPHY_GRID の場合は、次のいずれかになります:16 = 4 ×4グリッド (低) 64 = 8 ×8グリッド (中) 256 = 16 x 16 グリッド (HIGH) NULL = 特定の空間インデックスの種類またはテセレーションスキームに適用されません。  新しい SQL Server 11 テセレーションが使用されると、NULL が返されます。|  
|level_3_grid_desc|**nvarchar(60)**|第3レベルのグリッドのグリッド密度: 低中高 NULL = 特定の空間インデックスの種類またはテセレーションスキームには適用されません。  新しい SQL Server 11 テセレーションが使用されると、NULL が返されます。|  
|level_4_grid|**smallint**|第 4 レベルのグリッドのグリッド密度です。 Tessellation_scheme が GEOMETRY_GRID または GEOGRAPHY_GRID の場合、次のいずれかになります:16 = 4 ×4グリッド (LOW) 64 = 8 ×8グリッド (中) 256 = 16 ×16グリッド (HIGH) NULL = 特定の空間インデックスの種類またはテセレーションスキームに適用されません。  新しい SQL Server 11 テセレーションが使用されると、NULL が返されます。|  
|level_4_grid_desc|**nvarchar(60)**|第4レベルのグリッドのグリッド密度: < 低 MEDIUM 高 NULL = 特定の空間インデックスの種類またはテセレーションスキームには適用されません。  新しい SQL Server 11 テセレーションが使用されると、NULL が返されます。|  
|cells_per_object|**int**|空間オブジェクトごとのセル数。次のうちのどれかです: tessellation_scheme が GEOMETRY_GRID または GEOGRAPHY_GRID の場合、 *n* = オブジェクトあたりのセル数 NULL = 特定の空間インデックスの種類またはテセレーションスキームには適用できません|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [空間インデックスの概要](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.spatial_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-spatial-indexes-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
