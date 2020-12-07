---
description: sys.pdw_replicated_table_cache_state (Transact-SQL)
title: sys.pdw_replicated_table_cache_state (Transact-SQL)
ms.custom: seo-dt-2019
ms.date: 07/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 19a5132bd78b3cc1cca48be193b34126a9f83c3e
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036897"
---
# <a name="syspdw_replicated_table_cache_state-transact-sql"></a>sys.pdw_replicated_table_cache_state (Transact-SQL)
[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

  **Object_id**によって、レプリケートされたテーブルに関連付けられたキャッシュの状態を返します。  
  
|列名|データ型|説明|Range|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|テーブルのオブジェクト ID。 「 [Sys &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)」を参照してください。<br /><br /> **object_id** は、このビューのキーです。||  
|state|**nvarchar(40)**|このテーブルのレプリケートされたテーブルのキャッシュ状態です。|' NotReady '、' Ready '|  
  
## <a name="example"></a>例
この例では、sys.pdw_replicated_table_cache_state を sys. tables と結合して、レプリケートされたテーブルキャッシュのテーブル名と状態を取得します。

```sql
SELECT t.[name], p.[object_id], p.[state]
  FROM sys.pdw_replicated_table_cache_state p 
  JOIN sys.tables t ON t.object_id = p.object_id
```



## <a name="next-steps"></a>次の手順  
 Azure Synapse Analytics と Parallel Data Warehouse のすべてのカタログビューの一覧については、「 [Azure Synapse analytics と並列データウェアハウスのカタログビュー](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)」を参照してください。   
  
