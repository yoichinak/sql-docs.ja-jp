---
description: sys.selective_xml_index_paths (Transact-sql)
title: sys.selective_xml_index_paths (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- xml_schema_attributes_TSQL
- xml_schema_attributes
- sys.xml_schema_attributes_TSQL
- sys.xml_schema_attributes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_attributes catalog view
ms.assetid: 07a73d71-ec3e-4894-947a-5859ca62c606
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 4a768ded6ef89a54f35e7ce30a64bc3dd6e277ac
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99182467"
---
# <a name="sysselective_xml_index_paths-transact-sql"></a>sys.selective_xml_index_paths (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Service Pack 1 以降で使用でき [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ます。 sys.selective_xml_index_paths の各行は、特定の選択的 xml インデックスの1つの昇格されたパスを表します。  
  
 次のステートメントを使用して、テーブル T の xmlcol に対して選択的 XML インデックスを作成すると、  
  
```  
CREATE SELECTIVE XML INDEX sxi1 ON T(xmlcol)   
FOR ( path1 = '/a/b/c' AS XQUERY 'xs:string',  
      path2 = '/a/b/d' AS XQUERY 'xs:double'  
    )  
```  
  
 Sys.selective_xml_index_paths には、インデックス sxi1 に対応する2つの新しい行があります。  

  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|XML 列を含むテーブルの ID。|  
|**index_id**|**int**|選択的 xml インデックスの一意の id。|  
|**path_id**|**int**|上位変換された XML パス ID。|  
|**path**|**nvarchar (4000)**|上位変換されたパス。 たとえば、'/a/b/c/d/e ' のようになります。|  
|**name**|**sysname**|パス名。|  
|**path_type**|**tinyint**|0 = XQUERY<br /><br /> 1 = SQL|  
|**path_type_desc**|**sysname**|**Path_type** 値 ' XQUERY ' または ' SQL ' に基づいています。|  
|**xml_component_id**|**int**|データベース内の XML スキーマコンポーネントの一意の ID。|  
|**xquery_type_description**|**nvarchar (4000)**|指定された XSD 型の名前。|  
|**is_xquery_type_inferred**|**bit**|1 = 型は推論されます。|  
|**xquery_max_length**|**smallint**|最大長 (XSD 型の文字で表される)。|  
|**is_xquery_max_length_inferred**|**bit**|1 = 最大長は推論されます。|  
|**is_node**|**bit**|0 = node() ヒントが存在しない。<br /><br /> 1 = node () 最適化ヒントが適用されました。|  
|**system_type_id**|**tinyint**|列のシステム型の ID。|  
|**user_type_id**|**tinyint**|列のユーザー型の ID。|  
|**max_length**|**smallint**|型の最大長 (バイト単位)。<br /><br /> -1 の場合、列のデータ型は varchar(max)、nvarchar(max)、varbinary(max)、または xml です。|  
|**有効桁数 (precision)**|**tinyint**|型が数値型の場合は、最大有効桁数。 それ以外の場合は0です。|  
|**scale**|**tinyint**|数値ベースの場合の型の最大小数点以下桁数。 それ以外の場合は、0 に設定されます。|  
|**collation_name**|**sysname**|型が文字型の場合は、照合順序名。 それ以外の場合は NULL。|  
|**is_singleton**|**bit**|0 = シングルトンヒントが存在しません。<br /><br /> 1 = SINGLETON 最適化ヒントが適用される。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Xml スキーマ &#40;XML 型システム&#41; カタログビュー &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
