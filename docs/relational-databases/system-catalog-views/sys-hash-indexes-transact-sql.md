---
description: sys.hash_indexes (Transact-sql)
title: sys.hash_indexes (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sys.hash_indexes_TSQL
- hash_indexes
- sys.hash_indexes
- hash_indexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.hash_indexes catalog view
ms.assetid: d9e230fb-d3ff-486f-86ef-44898f0a703e
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: d0644ee943599ce3e34c408cf571543dd3692fcb
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99193839"
---
# <a name="syshash_indexes-transact-sql"></a>sys.hash_indexes (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在のハッシュインデックスとハッシュインデックスのプロパティが表示されます。 ハッシュインデックスは、 [インメモリ OLTP &#40;In-Memory 最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)でのみサポートされています。  
  
 Sys.hash_indexes ビューには、sys ビューと同じ列と、 **bucket_count** という名前の追加の列が含まれています。 Sys.hash_indexes ビューのその他の列の詳細については、「 [sys &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)」を参照してください。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**\<inherited columns>**||は [、SQL&#41;&#40;transact-sql ](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)の列を継承します。|  
|**bucket_count**|**int**|ハッシュインデックスのハッシュバケットの数。<br /><br /> 値を設定するためのガイドラインなど、bucket_count の値の詳細については、「 [transact-sql&#41;&#40;CREATE TABLE ](../../t-sql/statements/create-table-transact-sql.md)」を参照してください。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]. 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="examples"></a>例  
  
```  
SELECT object_name([object_id]) AS 'table_name', [object_id],  
     [name] AS 'index_name', [type_desc], [bucket_count]   
FROM sys.hash_indexes   
WHERE OBJECT_NAME([object_id]) = 'T1';  
```  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
