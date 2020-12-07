---
description: sys.xml_indexes (Transact-sql)
title: sys.xml_indexes (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.xml_indexes_TSQL
- xml_indexes_TSQL
- sys.xml_indexes
- xml_indexes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_indexes catalog view
ms.assetid: 3408de72-b067-4fda-b5d5-8e856dfd9db3
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1ceda15c69bd989172ad3fbb05e8c696fd9750aa
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546727"
---
# <a name="sysxml_indexes-transact-sql"></a>sys.xml_indexes (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  XML インデックスごとに1行の値を返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**\<inherited columns>**||は [、列を継承](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)します。|  
|**using_xml_index_id**|**int**|NULL = プライマリ XML インデックス<br /><br /> Null 以外 = セカンダリ XML インデックス。<br /><br /> Null 以外の場合は、プライマリ XML インデックスへの自己結合参照です。|  
|**secondary_type**|**char(1)**|セカンダリインデックスの説明を入力してください:<br /><br /> P = PATH セカンダリ XML インデックス<br /><br /> V = VALUE セカンダリ XML インデックス<br /><br /> R = PROPERTY セカンダリ XML インデックス<br /><br /> NULL = プライマリ XML インデックス|  
|**secondary_type_desc**|**nvarchar(60)**|セカンダリインデックスの説明を入力してください:<br /><br /> PATH = PATH セカンダリ XML インデックス<br /><br /> VALUE = VALUE セカンダリ XML インデックス<br /><br /> プロパティ = プロパティセカンダリ xml インデックス。<br /><br /> NULL = プライマリ XML インデックス|  
|**xml_index_type**|**tinyint**|インデックスの種類:<br /><br /> 0 = プライマリ XML インデックス<br /><br /> 1 = セカンダリ XML インデックス<br /><br /> 2 = 選択的な XML インデックス<br /><br /> 3 = 選択的セカンダリ XML インデックス|  
|**xml_index_type_description**|**nvarchar(60)**|インデックスの種類の説明:<br /><br /> PRIMARY_XML<br /><br /> セカンダリ XML インデックス<br /><br /> 選択的な XML インデックス<br /><br /> 選択的セカンダリ XML インデックス|  
|**path_id**|**int**|セカンダリ選択的 XML インデックスを除くすべての XML インデックスに対して NULL です。<br /><br /> それ以外の場合は、選択的セカンダリ XML インデックスを構築する上位変換されたパスの ID です。 この値は、sys.selective_xml_index_paths システム ビューからの path_id と同じ値です。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
