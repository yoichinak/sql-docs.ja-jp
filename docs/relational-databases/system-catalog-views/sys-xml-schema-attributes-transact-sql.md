---
description: sys.xml_schema_attributes (Transact-SQL)
title: sys.xml_schema_attributes (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xml_schema_attributes_TSQL
- xml_schema_attributes
- sys.xml_schema_attributes_TSQL
- sys.xml_schema_attributes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_attributes catalog view
ms.assetid: dd0c98aa-5e72-4df6-96d9-482786c8dbb1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a64481a5e3ab55a489d173dfd88f295a09aa9dfd
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546723"
---
# <a name="sysxml_schema_attributes-transact-sql"></a>sys.xml_schema_attributes (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  属性である XML スキーマコンポーネントごとに 1**行のを返します。の** **symbol_space**です。  

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**\<inherited columns>**|--|[sys.xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md)から継承します。|  
|**is_default_fixed**|**bit**|1 = 既定値は固定値です。 この値を XML インスタンスでオーバーライドすることはできません。<br /><br /> 0 = デフォルト値は属性の固定値ではありません  (既定値)。|  
|**must_be_qualified**|**bit**|1 = 属性には明示的に名前空間の修飾名を追加する必要があります。<br /><br /> 0 = 属性には暗黙的に名前空間の修飾名を追加できます  (既定値)。|  
|**default_value**|**nvarchar**<br /><br /> **(4000)**|属性の既定値。 既定値が指定されていない場合は NULL になります。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Xml スキーマ &#40;XML 型システム&#41; カタログビュー &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
