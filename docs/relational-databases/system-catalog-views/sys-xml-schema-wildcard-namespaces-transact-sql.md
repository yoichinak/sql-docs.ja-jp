---
description: sys.xml_schema_wildcard_namespaces (Transact-sql)
title: sys.xml_schema_wildcard_namespaces (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- xml_schema_wildcard_namespaces_TSQL
- xml_schema_wildcard_namespaces
- sys.xml_schema_wildcard_namespaces_TSQL
- sys.xml_schema_wildcard_namespaces
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_wildcard_namespaces catalog view
ms.assetid: a3caa932-41c7-48a9-9b2d-ff090afbb66b
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 0cfc70cf32e186afe3d08dc1a2edbf5802a614f6
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99199793"
---
# <a name="sysxml_schema_wildcard_namespaces-transact-sql"></a>sys.xml_schema_wildcard_namespaces (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  XML スキーマワイルドカードの列挙された名前空間ごとに1行の値を返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**xml_component_id**|**int**|このが適用される XML スキーマコンポーネント (ワイルドカード) の ID。|  
|**namespace**|**nvarchar (4000)**|XML ワイルドカードによって使用される名前空間の名前または URI。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Xml スキーマ &#40;XML 型システム&#41; カタログビュー &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
