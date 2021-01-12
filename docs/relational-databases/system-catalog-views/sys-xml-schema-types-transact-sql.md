---
description: sys.xml_schema_types (Transact-sql)
title: sys.xml_schema_types (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_types_TSQL
- xml_schema_types_TSQL
- sys.xml_schema_types
- xml_schema_types
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_types catalog view
ms.assetid: 441ba49d-f778-4fa1-98c4-ced375a01a34
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 2bd282bdecec59df5c1edf611cf2e2a8d6cfa08c
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98097889"
---
# <a name="sysxml_schema_types-transact-sql"></a>sys.xml_schema_types (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **T** の **symbol_space** 型である XML スキーマコンポーネントごとに1行の値を返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**\<inherited columns>**||[sys.xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md)から列を継承します。|  
|**is_abstract**|**bit**|1 = 型は抽象型です。 この型の要素のすべてのインスタンスは、抽象型ではない派生型を示すために、 **xsi: type** を使用する必要があります。<br /><br /> 0 = 型は abstract ではありません  (既定値)。|  
|**allows_mixed_content**|**bit**|1 = 混合コンテンツは許可されます。<br /><br /> 0 = 混合コンテンツは許可されていません。 (既定値)。|  
|**is_extension_blocked**|**bit**|1 = **complexType** 定義の block 属性または祖先要素情報項目の **blockdefault** 属性 \<schema> が "extension" または "#all" に設定されている場合、型の拡張による置換はインスタンスでブロックされます。<br /><br /> 0 = 拡張による置き換えはブロックされません。|  
|**is_restriction_blocked**|**bit**|1 = **complexType** 定義の block 属性または祖先要素情報項目の **blockdefault** 属性 \<schema> が "restriction" または "#all" に設定されている場合、型の制限付きの置換はインスタンスでブロックされます。<br /><br /> 0 = 制約による置き換えはブロックされません  (既定値)。|  
|**is_final_extension**|**bit**|1 = **complexType** 定義の final 属性、または祖先要素情報項目の **finaldefault** 属性 \<schema> が "extension" または "#all" に設定されている場合、型の拡張による派生はブロックされます。<br /><br /> 0 = 拡張は許可されます  (既定値)。|  
|**is_final_restriction**|**bit**|1 = simple または **complexType** 定義の final 属性、または祖先要素情報項目の **finaldefault** 属性 \<schema> が "restriction" または "#all" に設定されている場合、型の制限による派生はブロックされます。<br /><br /> 0 = 制約は許可されます  (既定値)。|  
|**is_final_list_member**|**bit**|1 = この単純型は、リスト項目の型として使用できません。<br /><br /> 0 = この型は複合型、またはリスト項目の型として使用できます  (既定値)。|  
|**is_final_union_member**|**bit**|1 = この単純型は、共用体型のメンバー型として使用することはできません。<br /><br /> 0 = この型は複合型です。 または、共用体メンバー型として使用することもできます。 (既定値)。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Xml スキーマ &#40;XML 型システム&#41; カタログビュー &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
