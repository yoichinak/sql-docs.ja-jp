---
description: sys.pdw_nodes_partitions (Transact-sql)
title: sys.pdw_nodes_partitions (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: b4216752-4813-4b2c-b259-7d8ffc6cc190
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: ff60a994457c8836446520aae7772f2ab6150a46
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036725"
---
# <a name="syspdw_nodes_partitions-transact-sql"></a>sys.pdw_nodes_partitions (Transact-sql)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  すべてのテーブルのパーティションごとに1行のデータを格納し、データベース内のほとんどの種類のインデックスを格納 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] します。 すべてのテーブルとインデックスには、明示的にパーティション分割されているかどうかにかかわらず、少なくとも1つのパーティションが含まれます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|partition_id|**bigint**|パーティションの ID。 データベース内で一意です。|  
|object_id|**int**|このパーティションが所属するオブジェクトの ID です。 すべてのテーブルまたはビューは、少なくとも1つのパーティションで構成されます。|  
|index_id|**int**|このパーティションが所属するオブジェクト内のインデックスの ID です。|  
|partition_number|**int**|所有しているインデックスまたはヒープ内の1から始まるパーティション番号。 の場合 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 、この列の値は1です。|  
|hobt_id|**bigint**|このパーティションの行を含むデータヒープまたは B ツリー (HoBT) の ID。|  
|rows|**bigint**|このパーティション内の行の概数です。 |  
|data_compression|**int**|各パーティションの圧縮の状態を示します。<br /><br /> 0 = NONE<br /><br /> 1 = 行<br /><br /> 2 = ページ<br /><br /> 3 = 列ストア|  
|data_compression_desc|**nvarchar(60)**|各パーティションの圧縮の状態を示します。 指定できる値は、[なし]、[行]、および [ページ] です。|  
|pdw_node_id|**int**|ノードの一意識別子 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 。|  
  
## <a name="permissions"></a>アクセス許可  
 `CONTROL SERVER` 権限が必要です。  
  
## <a name="examples-sssdwfull-and-sspdw"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  

### <a name="example-a-display-rows-in-each-partition-within-each-distribution"></a>例 A: 各ディストリビューション内の各パーティションに行を表示する 

**適用対象:** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]
 
各ディストリビューション内の各パーティションの行数を表示するには、 [DBCC PDW_SHOWPARTITIONSTATS (SQL Server PDW)](../../t-sql/database-console-commands/dbcc-pdw-showpartitionstats-transact-sql.md) を使用します。

### <a name="example-b-uses-system-views-to-view-rows-in-each-partition-of-each-distribution-of-a-table"></a>例 B: システムビューを使用して、テーブルの各ディストリビューションの各パーティションの行を表示する

**適用対象:** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]
 
このクエリは、テーブルの各ディストリビューションの各パーティションの行数を返し `myTable` ます。  
 
```sql  
SELECT o.name, pnp.index_id, pnp.partition_id, pnp.rows,   
    pnp.data_compression_desc, pnp.pdw_node_id  
FROM sys.pdw_nodes_partitions AS pnp  
JOIN sys.pdw_nodes_tables AS NTables  
    ON pnp.object_id = NTables.object_id  
AND pnp.pdw_node_id = NTables.pdw_node_id  
JOIN sys.pdw_table_mappings AS TMap  
    ON NTables.name = TMap.physical_name 
    AND substring(TMap.physical_name,40, 10) = pnp.distribution_id 
JOIN sys.objects AS o  
    ON TMap.object_id = o.object_id  
WHERE o.name = 'myTable'  
ORDER BY o.name, pnp.index_id, pnp.partition_id;  
```    
  
## <a name="see-also"></a>参照  
 [Azure Synapse Analytics と Parallel Data Warehouse のカタログ ビュー](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  

