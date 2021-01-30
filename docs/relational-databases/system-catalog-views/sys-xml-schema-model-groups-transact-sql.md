---
description: sys.xml_schema_model_groups (Transact-sql)
title: sys.xml_schema_model_groups (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sys.xml_schema_model_groups
- xml_schema_model_groups
- sys.xml_schema_model_groups_TSQL
- xml_schema_model_groups_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_model_groups catalog view
ms.assetid: 566556dc-a8c8-465c-9196-c7e0ae092a8a
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 0d2cd070f8e293fc764a996faafab42e8c21a437
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99199839"
---
# <a name="sysxml_schema_model_groups-transact-sql"></a>sys.xml_schema_model_groups (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  モデルグループであり、 **Symbol_space** **M**. の XML スキーマコンポーネントごとに1行の値を返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**\<inherited columns>**||[sys.xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md)から列を継承します。|  
|**compositor**|**char(1)**|グループのコンポジターの種類。<br /><br /> A = XSD \<all> グループ<br /><br /> C = XSD \<choice> グループ<br /><br /> S = XSD \<sequence> グループ|  
|**compositor_desc**|**nvarchar (60)**|グループのコンポジターの種類の説明。<br /><br /> XSD_ALL_GROUP<br /><br /> XSD_CHOICE_GROUP<br /><br /> XSD_SEQUENCE_GROUP|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Xml スキーマ &#40;XML 型システム&#41; カタログビュー &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
