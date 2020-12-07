---
description: sys.xml_schema_component_placements (Transact-sql)
title: sys.xml_schema_component_placements (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_component_placements
- xml_schema_component_placements_TSQL
- xml_schema_component_placements
- sys.xml_schema_component_placements_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_component_placements catalog view
ms.assetid: 2d3c8828-e4b3-423d-bf11-990464c1341b
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: b4b971fe631671d193340fc3c68b8e4e235c178f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88400708"
---
# <a name="sysxml_schema_component_placements-transact-sql"></a>sys.xml_schema_component_placements (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  XML スキーマコンポーネントの配置ごとに1行の値を返します。  
   
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**xml_component_id**|**int**|この配置を所有する XML スキーマコンポーネントの ID。|  
|**placement_id**|**int**|配置の ID。 配置を所有する XML スキーマ コンポーネント内で一意です。|  
|**placed_xml_component_id**|**int**|配置された XML スキーマコンポーネントの ID。|  
|**is_default_fixed**|**bit**|1 = 既定値は固定値です。 この値を XML インスタンスでオーバーライドすることはできません。<br /><br /> 0 = 値はオーバーライドされる場合があります (既定)|  
|**min_occurrences**|**int**|配置されたコンポーネントの最小数。|  
|**max_occurrences**|**int**|配置されたコンポーネントの最大数。|  
|**default_value**|**nvarchar (4000)**|既定値が指定されている場合。 既定値が指定されていない場合は NULL になります。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Xml スキーマ &#40;XML 型システム&#41; カタログビュー &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
