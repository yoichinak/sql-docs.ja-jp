---
description: sys.pdw_materialized_view_distribution_properties (Transact-sql) (プレビュー)
title: sys.pdw_materialized_view_distribution_properties (Transact-sql)
ms.custom: seo-dt-2019
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d62b0e25-3226-4f87-a10a-b3a0d9555e19
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: ad934310f5bd4b5628efdf28788eff9ac7aa2503
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036979"
---
# <a name="syspdw_materialized_view_distribution_properties-transact-sql-preview"></a>sys.pdw_materialized_view_distribution_properties (Transact-sql) (プレビュー)

[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

配布情報の具体化されたビューを表示します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------| 
|object_id|**int**|プロパティが指定された具体化されたビューの ID。| 
|distribution_policy |**tinyint**|2 = ハッシュ</br>4 = ROUND_ROBIN|  
|distribution_policy_desc |**nvarchar(60)**|HASH、ROUND_ROBIN|  
 
## <a name="permissions"></a>アクセス許可

VIEW DATABASE STATE 権限が必要です。
 
## <a name="see-also"></a>関連項目

[CREATE MATERIALIZED VIEW AS SELECT &#40;Transact-SQL&#41;](../../t-sql/statements/create-materialized-view-as-select-transact-sql.md?view=azure-sqldw-latest)   
[ALTER MATERIALIZED VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/alter-materialized-view-transact-sql.md?view=azure-sqldw-latest)   
[EXPLAIN &#40;Transact-SQL&#41;](../../t-sql/queries/explain-transact-sql.md?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_mappings &#40;Transact-SQL&#41;](./sys-pdw-materialized-view-mappings-transact-sql.md?view=azure-sqldw-latest)   
[DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-pdw-showmaterializedviewoverhead-transact-sql.md?view=azure-sqldw-latest)   
[Azure Synapse Analytics と Parallel Data Warehouse のカタログ ビュー](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[Azure Synapse Analytics でサポートされているシステム ビュー](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[Azure Synapse Analytics でサポートされている T-SQL ステートメント](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements)