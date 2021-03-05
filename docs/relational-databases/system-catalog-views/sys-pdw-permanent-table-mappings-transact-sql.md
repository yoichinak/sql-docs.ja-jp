---
title: sys.pdw_permanent_table_mappings (Transact-sql)
description: '**Object_id** によって、永続的なユーザーテーブルを内部オブジェクト名に結び付けます。'
ms.custom: ''
ms.date: 07/24/2020
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: reference
dev_langs:
- TSQL
author: mstehrani
ms.author: emtehran
monikerRange: = azure-sqldw-latest
ms.openlocfilehash: ab6ec23c35f9766a82e9a0c07f31433b2cbbc2ce
ms.sourcegitcommit: ca81fc9e45fccb26934580f6d299feb0b8ec44b7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102186590"
---
# <a name="syspdw_permanent_table_mappings-transact-sql"></a>sys.pdw_permanent_table_mappings (Transact-sql)
[!INCLUDE [applies-to-version/asa](../../includes/applies-to-version/asa.md)]

**Object_id** によって、永続的なユーザーテーブルを内部オブジェクト名に結び付けます。  
  
> [!NOTE]
> **sys.pdw_permanent_table_mappings** は、永続的なテーブルへのマッピングを保持し、一時テーブルまたは外部テーブルマッピングを含みません。

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|physical_name|**nvarchar (36)**|テーブルの物理名。<br /><br /> このビューのキーは **physical_name** と **object_id** によって形成されます。||  
|object_id|**int**|テーブルのオブジェクト ID。 「 [Sys &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)」を参照してください。<br /><br /> このビューのキーは **physical_name** と **object_id** によって形成されます。||  
  
## <a name="see-also"></a>関連項目  
 [Azure Synapse Analytics と Parallel Data Warehouse のカタログ ビュー](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [sys.pdw_index_mappings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-index-mappings-transact-sql.md)  
  
  
