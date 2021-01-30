---
description: sys.sql_dependencies (Transact-sql)
title: sys.sql_dependencies (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sql_dependencies
- sql_dependencies_TSQL
- sys.sql_dependencies_TSQL
- sys.sql_dependencies
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sql_dependencies catalog view
ms.assetid: 1779aa87-a0b8-470a-a286-d7cc0b93ad2e
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 2032bc1ba6658b18649f5908bebd4ae9405522b9
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99150708"
---
# <a name="syssql_dependencies-transact-sql"></a>sys.sql_dependencies (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  参照先エンティティの依存関係ごとに1行の値を格納します。参照先のエンティティ [!INCLUDE[tsql](../../includes/tsql-md.md)] は、他の参照元オブジェクトを定義する式またはステートメントで参照されます。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) を使用してください。  

  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**class**|**tinyint**|参照先エンティティのクラスを識別します。<br /><br /> 0 = オブジェクトまたは列 (非スキーマバインド参照のみ)<br /><br /> 1 = オブジェクトまたは列 (スキーマバインド参照)<br /><br /> 2 = 型 (スキーマバインド参照)<br /><br /> 3 = XML スキーマコレクション (スキーマバインド参照)<br /><br /> 4 = パーティション関数 (スキーマ バインド参照)|  
|**class_desc**|**nvarchar(60)**|参照先エンティティのクラスの説明です。<br /><br /> **OBJECT_OR_COLUMN_REFERENCE_NON_SCHEMA_BOUND**<br /><br /> **OBJECT_OR_COLUMN_REFERENCE_SCHEMA_BOUND**<br /><br /> **TYPE_REFERENCE**<br /><br /> **XML_SCHEMA_COLLECTION_REFERENCE**<br /><br /> **PARTITION_FUNCTION_REFERENCE**|  
|**object_id**|**int**|参照しているオブジェクトの ID。|  
|**column_id**|**int**|参照元 ID が列である場合は、参照している列の ID です。それ以外の場合は0です。|  
|**referenced_major_id**|**int**|に従って、クラスの値によって解釈される、参照先エンティティの ID。<br /><br /> 0、1 = オブジェクトまたは列のオブジェクト ID。<br /><br /> 2 = 型 ID<br /><br /> 3 = XML スキーマ コレクション ID|  
|**referenced_minor_id**|**int**|次に示すように、クラスの値によって解釈される、参照先エンティティのマイナー ID。<br /><br /> この値は、class の値によって異なります。<br /><br /> 0、 **referenced_minor_id** は列 id です。または、列でない場合は0になります。<br /><br /> 1, **referenced_minor_id** は列 id です。または、列でない場合は0になります。<br /><br /> それ以外の場合は、 **referenced_minor_id** = 0 です。|  
|**is_selected**|**bit**|オブジェクトまたは列が選択されています。|  
|**is_updated**|**bit**|オブジェクトまたは列が更新されます。|  
|**is_select_all**|**bit**|オブジェクトが SELECT * 句で使用されています (オブジェクトレベルのみ)。|  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [SQL Server システム カタログに対するクエリに関してよく寄せられる質問](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
