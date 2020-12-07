---
description: dm_db_xtp_hash_index_stats (Transact-sql)
title: dm_db_xtp_hash_index_stats (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_xtp_hash_index_stats
- sys.dm_db_xtp_hash_index_stats_TSQL
- dm_db_xtp_hash_index_stats
- dm_db_xtp_hash_index_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_hash_index_stats (dynamic management view)
ms.assetid: 45969884-cd61-48e8-aee5-c725c78e3e4c
author: markingmyname
ms.author: maghan
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5e8b28d292de4d860a8e46f7a679e42d99ac8c88
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542262"
---
# <a name="sysdm_db_xtp_hash_index_stats-transact-sql"></a>dm_db_xtp_hash_index_stats (Transact-sql)
[!INCLUDE[sql-asdb-asdbmi](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  これらの統計は、バケット数を理解してチューニングするために役立ちます。 また、インデックス キーに多数の重複があるケースを検出するためにも使用できます。  
  
 平均チェーン長が大きい場合は、同じバケットに多数の行がハッシュされていることを示します。 これは、次の場合に発生する可能性があります。  
  
-   空のバケットの数が少ない場合、またはチェーンの長さの平均値が最大値に近い場合は、バケット数の合計が少なすぎる可能性があります。 これにより、多くの異なるインデックスキーが同じバケットにハッシュされます。  
  
-   空のバケットの数が多い場合、またはチェーンの長さの最大値が平均値よりも高い場合、インデックス キーの値が重複していて行が多数あるか、キーの値にスキューがある可能性があります。 同じインデックスキー値を持つすべての行が同じバケットにハッシュされるため、そのバケットには長いチェーン長が存在します。  
  
長いチェーン長は、SELECT や INSERT など、個々の行に対するすべての DML 操作のパフォーマンスに大きな影響を与える可能性があります。 チェーンの長さが短く、空のバケット数が多いことは、bucket_count の値が高すぎることを意味します。 これにより、インデックス スキャンのパフォーマンスが低下します。  
  
> [!WARNING]
> **dm_db_xtp_hash_index_stats** は、テーブル全体をスキャンします。 そのため、データベースに大きなテーブルがある場合は、 **dm_db_xtp_hash_index_stats** に長時間かかることがあります。  
  
詳細については、「 [メモリ最適化テーブルのハッシュインデックス](../../relational-databases/sql-server-index-design-guide.md#hash_index)」を参照してください。  
  
|列名|種類|説明|  
|-----------------|----------|-----------------|  
|object_id|**int**|親テーブルのオブジェクト ID。|  
|xtp_object_id|**bigint**|メモリ最適化テーブルの ID。|  
|index_id|**int**|インデックス ID。|  
|total_bucket_count|**bigint**|インデックス内のハッシュ バケットの総数。|  
|empty_bucket_count|**bigint**|インデックス内の空のハッシュ バケットの数。|  
|avg_chain_length|**bigint**|インデックス内のすべてのハッシュバケットに対する行チェーンの平均の長さ。|  
|max_chain_length|**bigint**|ハッシュバケット内の行チェーンの最大長。|  
|xtp_object_id|**bigint**|メモリ最適化テーブルに対応するインメモリ OLTP オブジェクト ID。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW DATABASE STATE 権限が必要です。  

## <a name="examples"></a>例  
  
### <a name="a-troubleshooting-hash-index-bucket-count"></a>A. ハッシュ インデックスのバケット数のトラブルシューティング

次のクエリを使用して、既存のテーブルのハッシュインデックスバケット数のトラブルシューティングを行うことができます。 このクエリは、ユーザーテーブルのすべてのハッシュインデックスについて、空のバケットの割合とチェーン長に関する統計を返します。

```sql
  SELECT  
    QUOTENAME(SCHEMA_NAME(t.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(h.object_id)) as [table],   
    i.name                   as [index],   
    h.total_bucket_count,  
    h.empty_bucket_count,  
    FLOOR((  
      CAST(h.empty_bucket_count as float) /  
        h.total_bucket_count) * 100)  
                             as [empty_bucket_percent],  
    h.avg_chain_length,   
    h.max_chain_length  
  FROM sys.dm_db_xtp_hash_index_stats as h   
  INNER JOIN sys.indexes as i  
            ON h.object_id = i.object_id  
           AND h.index_id  = i.index_id  
    INNER JOIN sys.memory_optimized_tables_internal_attributes ia ON h.xtp_object_id=ia.xtp_object_id
    INNER JOIN sys.tables t on h.object_id=t.object_id
  WHERE ia.type=1
  ORDER BY [table], [index];  
``` 

このクエリの結果を解釈する方法の詳細については、「 [メモリ最適化テーブルのハッシュインデックスのトラブルシューティング](../../relational-databases/in-memory-oltp/hash-indexes-for-memory-optimized-tables.md) 」を参照してください。  

### <a name="b-hash-index-statistics-for-internal-tables"></a>B. 内部テーブルのハッシュインデックスの統計

一部の機能では、メモリ最適化テーブルの列ストアインデックスなど、ハッシュインデックスを利用する内部テーブルが使用されます。 次のクエリは、ユーザーテーブルにリンクされている内部テーブルのハッシュインデックスの統計を返します。

```sql
  SELECT  
    QUOTENAME(SCHEMA_NAME(t.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(h.object_id)) as [user_table],
    ia.type_desc as [internal_table_type],
    i.name                   as [index],   
    h.total_bucket_count,  
    h.empty_bucket_count,  
    h.avg_chain_length,   
    h.max_chain_length  
  FROM sys.dm_db_xtp_hash_index_stats as h   
  INNER JOIN sys.indexes as i  
            ON h.object_id = i.object_id  
           AND h.index_id  = i.index_id  
    INNER JOIN sys.memory_optimized_tables_internal_attributes ia ON h.xtp_object_id=ia.xtp_object_id
    INNER JOIN sys.tables t on h.object_id=t.object_id
  WHERE ia.type!=1
  ORDER BY [user_table], [internal_table_type], [index]; 
```

内部テーブルのインデックスの BUCKET_COUNT を変更することはできないため、このクエリの出力は有益であると見なされる必要があります。 必要な操作はありません。  

内部テーブルでハッシュインデックスを利用する機能を使用している場合を除き、このクエリは行を返すとは限りません。 次のメモリ最適化テーブルには、列ストアインデックスが含まれています。 このテーブルを作成すると、内部テーブルにハッシュインデックスが表示されます。

```sql
  CREATE TABLE dbo.table_columnstore
  (
    c1 INT NOT NULL PRIMARY KEY NONCLUSTERED,
    INDEX ix_columnstore CLUSTERED COLUMNSTORE
  ) WITH (MEMORY_OPTIMIZED=ON)
```

## <a name="see-also"></a>参照  
 [メモリ最適化テーブルの動的管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
