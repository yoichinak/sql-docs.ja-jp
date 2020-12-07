---
description: sys.xml_schema_elements (Transact-SQL)
title: sys.xml_schema_elements (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_elements
- sys.xml_schema_elements_TSQL
- xml_schema_elements
- xml_schema_elements_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_elements catalog view
ms.assetid: 190ed0cd-0c5e-4607-9db4-9e77cacf17d7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 008fb9d5d8beb5f746d02be3357eb1e73ae58ea9
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543967"
---
# <a name="sysxml_schema_elements-transact-sql"></a>sys.xml_schema_elements (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **E**の**symbol_space**型である XML スキーマコンポーネントごとに1行の値を返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**\<inherited columns>**|**--**|[sys.xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md)から列を継承します。|  
|**is_default_fixed**|**bit**|1 = 既定値は固定値です。 この値を XML インスタンスでオーバーライドすることはできません。<br /><br /> 0 = 既定値は、要素の固定値ではありません。 (既定)|  
|**is_abstract**|**bit**|1 = 要素は abstract であり、インスタンス ドキュメント内では使用できません。 要素の代替グループのメンバーは、インスタンス ドキュメント内に表示される必要があります。<br /><br /> 0 = 要素は abstract ではありません。 (既定)|  
|**is_nillable**|**bit**|1 = 要素は nillable です。<br /><br /> 0 = 要素は nillable ではありません  (既定値)。|  
|**must_be_qualified**|**bit**|1 = 要素は、明示的に名前空間を修飾する必要があります。<br /><br /> 0 = 要素には暗黙的に名前空間の修飾名が追加されます  (既定値)。|  
|**is_extension_blocked**|**bit**|1 = 拡張型のインスタンスへの置換はブロックされます。<br /><br /> 0 = 拡張型による置換は許可されます。 (既定値)。|  
|**is_restriction_blocked**|**bit**|1 = 制限型のインスタンスへの置換はブロックされます。<br /><br /> 0 = 制限型による置換は許可されます。 (既定値)。|  
|**is_substitution_blocked**|**bit**|1 = 代替グループのインスタンスは使用できません。<br /><br /> 0 = 代替グループによる置換は許可されています。 (既定値)。|  
|**is_final_extension**|**bit**|1 = 拡張型のインスタンスへの置換は許可されません。<br /><br /> 0 = 拡張型のインスタンスへの置換は許可されます  (既定値)。|  
|**is_final_restriction**|**bit**|1 = 制限型のインスタンスへの置換は許可されていません。<br /><br /> 0 = 制限型のインスタンスでの置換は許可されます。 (既定値)。|  
|**default_value**|**nvarchar (4000)**|要素の既定値。 既定値が指定されていない場合は NULL です。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Xml スキーマ &#40;XML 型システム&#41; カタログビュー &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
