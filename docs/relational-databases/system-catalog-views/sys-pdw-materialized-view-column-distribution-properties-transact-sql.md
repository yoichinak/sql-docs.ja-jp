---
title: sys.pdw_materialized_view_column_distribution_properties (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: jrasnick
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d62b0e25-3226-4f87-a10a-b3a0d9555e19
author: XiaoyuL-Preview
ms.author: xiaoyul
manager: craigg
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 144ae511f6074dc06cb0c5fe73c0e0042cc94a9a
ms.sourcegitcommit: e4b241fd92689c2aa6e1f5e625874bd0b807dd01
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/04/2019
ms.locfileid: "67566674"
---
# <a name="syspdwmaterializedviewcolumndistributionproperties-transact-sql-preview"></a>sys.pdw_materialized_view_column_distribution_properties (TRANSACT-SQL) (プレビュー)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

具体化されたビューの列の分布情報を表示します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|object_id|**int**|列が所属するオブジェクトの ID。 |  
|column_id|**int**|列の ID。|  
|distribution_ordinal|**tinyint**|0 = ディストリビューション列ではありません。</br> 1 = SQL Data Warehouse には、具体化されたビューを配布するこの列を使用しています。|
 
## <a name="permissions"></a>アクセス許可 

VIEW DATABASE STATE 権限が必要です。
 
## <a name="see-also"></a>関連項目

[MATERIALIZED VIEW AS を SELECT 作成&#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-materialized-view-as-select-transact-sql?view=azure-sqldw-latest)   
[ALTER MATERIALIZED VIEW &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/alter-materialized-view-transact-sql?view=azure-sqldw-latest)   
[説明&#40;TRANSACT-SQL&#41;](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_distribution_properties &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_mappings &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-mappings-transact-sql?view=azure-sqldw-latest)   
[DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD &#40;TRANSACT-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-pdw-showmaterializedviewoverhead-transact-sql?view=azure-sqldw-latest)   
[SQL Data Warehouse と Parallel Data Warehouse カタログ ビュー](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[Azure SQL Data Warehouse でサポートされるシステム ビュー](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[Azure SQL Data Warehouse でサポートされる T-SQL ステートメント](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements)