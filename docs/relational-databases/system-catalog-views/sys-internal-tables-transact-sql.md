---
description: internal_tables (Transact-sql)
title: internal_tables (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.internal_tables
- internal_tables
- sys.internal_tables_TSQL
- internal_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- internal tables
- sys.internal_tables catalog view
ms.assetid: a5821c70-f150-4676-8476-3a31f7403dca
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c46f6a7f66ff9dfba0ebf9a7b4dfe4e39eef7033
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548736"
---
# <a name="sysinternal_tables-transact-sql"></a>internal_tables (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  内部テーブルであるオブジェクトごとに1行の値を返します。 内部テーブルは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] さまざまな機能をサポートするためにによって自動的に生成されます。 たとえば、プライマリ XML インデックスを作成すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 細分化 xml ドキュメントデータを保持する内部テーブルがによって自動的に作成されます。 内部テーブルは、各データベースの **sys** スキーマに表示され、システムによって生成される一意の名前を持ちます。たとえば、 **xml_index_nodes_2021582240_32001** や **queue_messages_1977058079**  
  
 内部テーブルにはユーザーがアクセスできるデータは含まれず、スキーマは固定され、unalterable ます。 内部テーブルの名前を [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントで参照することはできません。 たとえば、SELECT FROM などのステートメントを実行することはできません \* *\<sys.internal_table_name>* 。 ただし、カタログ ビューにクエリを実行して、内部テーブルのメタデータを表示することはできます。  
  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**\<Columns inherited from sys.objects>**||このビューが継承する列の一覧については、「 [sys. objects &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)」を参照してください。|  
|**internal_type**|**tinyint**|内部テーブルの種類。<br /><br /> 3 = **query_disk_store_query_hints**<br /><br /> 4 = **query_disk_store_query_template_parameterization**<br /><br /> 6 = **query_disk_store_wait_stats**<br /><br /> 201 = **queue_messages**<br /><br /> 202 = **xml_index_nodes**<br /><br /> 203 = **fulltext_catalog_freelist**<br /><br /> 205 = **query_notification**<br /><br /> 206 = **service_broker_map**<br /><br /> 207 = **extended_indexes** (空間インデックスなど)<br /><br /> 208 = **filestream_tombstone**<br /><br /> 209 = **change_tracking**<br /><br /> 210 = **tracked_committed_transactions**<br /><br /> 220 = **contained_features**<br /><br /> 225 = **filetable_updates**<br /><br /> 236 = **selective_xml_index_node_table**<br /><br /> 240 = **query_disk_store_query_text**<br /><br /> 241 = **query_disk_store_query**<br /><br /> 242 = **query_disk_store_plan**<br /><br /> 243 = **query_disk_store_runtime_stats**<br /><br /> 244 = **query_disk_store_runtime_stats_interval**<br /><br /> 245 = **query_context_settings**|  
|**internal_type_desc**|**nvarchar(60)**|内部テーブルの種類の説明。<br /><br /> QUERY_DISK_STORE_QUERY_HINTS<br /><br /> QUERY_DISK_STORE_QUERY_TEMPLATE_PARAMETERIZATION<br /><br /> QUERY_DISK_STORE_WAIT_STATS<br /><br /> QUEUE_MESSAGES<br /><br /> XML_INDEX_NODES<br /><br /> FULLTEXT_CATALOG_FREELIST<br /><br /> FULLTEXT_CATALOG_MAP<br /><br /> QUERY_NOTIFICATION<br /><br /> SERVICE_BROKER_MAP<br /><br /> EXTENDED_INDEXES<br /><br /> FILESTREAM_TOMBSTONE<br /><br /> CHANGE_TRACKING<br /><br /> TRACKED_COMMITTED_TRANSACTIONS<br /><br /> CONTAINED_FEATURES<br /><br /> FILETABLE_UPDATES<br /><br /> SELECTIVE_XML_INDEX_NODE_TABLE<br /><br /> QUERY_DISK_STORE_QUERY_TEXT<br /><br /> QUERY_DISK_STORE_QUERY<br /><br /> QUERY_DISK_STORE_PLAN<br /><br /> QUERY_DISK_STORE_RUNTIME_STATS<br /><br /> QUERY_DISK_STORE_RUNTIME_STATS_INTERVAL<br /><br /> QUERY_CONTEXT_SETTINGS|  
|**parent_id**|**int**|スキーマスコープであるかどうかに関係なく、親の ID。 それ以外の場合は、親が存在しない場合は0です。<br /><br /> **queue_messages**  = キューの**object_id**<br /><br /> **xml_index_nodes**  = xml インデックスの**object_id**<br /><br /> **fulltext_catalog_freelist**  = フルテキストカタログの**fulltext_catalog_id**<br /><br /> **fulltext_index_map**  = フルテキストインデックスの**object_id**<br /><br /> **query_notification**、または **service_broker_map** = 0<br /><br /> **extended_indexes**  = 空間インデックスなどの拡張インデックスの**object_id**<br /><br /> テーブル追跡が有効になっているテーブルの**object_id** = **change_tracking**|  
|**parent_minor_id**|**int**|親のマイナー ID。<br /><br /> **xml_index_nodes**  = XML インデックスの**index_id**<br /><br /> **extended_indexes**  = 空間インデックスなどの拡張インデックスの**index_id**<br /><br /> 0 = **queue_messages**、 **fulltext_catalog_freelist**、 **fulltext_index_map**、 **query_notification**、 **service_broker_map**、または **change_tracking**|  
|**lob_data_space_id**|**int**|0以外の値は、このテーブルのラージオブジェクト (LOB) データを保持するデータ領域 (ファイルグループまたはパーティション構成) の ID です。|  
|**filestream_data_space_id**|**int**|将来使用するために予約されています。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="remarks"></a>解説  
 内部テーブルは、親エンティティと同じファイル グループに配置されます。 後半の例 F で示すカタログ クエリを使用して、内部テーブルが行内データ、行外データ、およびラージ オブジェクト (LOB) データに使用するページ数を返すことができます。  
  
 [Sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)システムプロシージャを使用すると、内部テーブルの領域使用量データを返すことができます。 **sp_spaceused** は、次の方法で内部テーブルの領域をレポートします。  
  
-   キュー名を指定すると、キューに関連付けられた基になる内部テーブルが参照され、そのストレージ使用量がレポートされます。  
  
-   XML インデックス、空間インデックス、およびフルテキストインデックスの内部テーブルによって使用されるページは、 **index_size** 列に含まれています。 テーブルまたはインデックス付きビュー名が指定されている場合、そのオブジェクトの XML インデックス、空間インデックス、およびフルテキストインデックスのページは、 **予約済み** の列と **index_size**に含まれます。  
  
## <a name="examples"></a>例  
 次の例では、カタログ ビューを使用して内部テーブルのメタデータにクエリを実行する方法について説明します。  
  
### <a name="a-show-internal-tables-that-inherit-columns-from-the-sysobjects-catalog-view"></a>A. [列を継承する内部テーブルを表示する] カタログビュー  
  
```  
SELECT * FROM sys.objects WHERE type = 'IT';  
```  
  
### <a name="b-return-all-internal-table-metadata-including-that-which-is-inherited-from-sysobjects"></a>B. すべての内部テーブルのメタデータ (sys. オブジェクトから継承されたものを含む) を返します。  
  
```  
SELECT * FROM sys.internal_tables;  
```  
  
### <a name="c-return-internal-table-columns-and-column-data-types"></a>C. 内部テーブルの列と列のデータ型を返す  
  
```  
SELECT SCHEMA_NAME(itab.schema_id) AS schema_name  
    ,itab.name AS internal_table_name  
    ,typ.name AS column_data_type   
    ,col.*  
FROM sys.internal_tables AS itab  
JOIN sys.columns AS col ON itab.object_id = col.object_id  
JOIN sys.types AS typ ON typ.user_type_id = col.user_type_id  
ORDER BY itab.name, col.column_id;  
```  
  
### <a name="d-return-internal-table-indexes"></a>D. 内部テーブルのインデックスを返す  
  
```  
SELECT SCHEMA_NAME(itab.schema_id) AS schema_name  
    , itab.name AS internal_table_name  
    , idx.*  
FROM sys.internal_tables AS itab  
JOIN sys.indexes AS idx ON itab.object_id = idx.object_id  
ORDER BY itab.name, idx.index_id;  
```  
  
### <a name="e-return-internal-table-statistics"></a>E. 内部テーブルの統計を返す  
  
```  
SELECT SCHEMA_NAME(itab.schema_id) AS schema_name  
    ,itab.name AS internal_table_name  
    , s.*  
FROM sys.internal_tables AS itab  
JOIN sys.stats AS s ON itab.object_id = s.object_id  
ORDER BY itab.name, s.stats_id;  
```  
  
### <a name="f-return-internal-table-partition-and-allocation-unit-information"></a>F. 内部テーブルのパーティションとアロケーションユニットの情報を返す  
  
```  
SELECT SCHEMA_NAME(itab.schema_id) AS schema_name  
    ,itab.name AS internal_table_name  
    ,idx.name AS heap_or_index_name  
    ,p.*  
    ,au.*  
FROM sys.internal_tables AS itab  
JOIN sys.indexes AS idx  
--     JOIN to the heap or the clustered index  
    ON itab.object_id = idx.object_id AND idx.index_id IN (0,1)  
JOIN   sys.partitions AS p   
    ON p.object_id = idx.object_id AND p.index_id = idx.index_id  
JOIN   sys.allocation_units AS au  
--     IN_ROW_DATA (type 1) and ROW_OVERFLOW_DATA (type 3) => JOIN to partition's Hobt  
--     else LOB_DATA (type 2) => JOIN to the partition ID itself.  
ON au.container_id =    
    CASE au.type   
        WHEN 2 THEN p.partition_id   
        ELSE p.hobt_id   
    END  
ORDER BY itab.name, idx.index_id;  
```  
  
### <a name="g-return-internal-table-metadata-for-xml-indexes"></a>G. XML インデックスに関する内部テーブルのメタデータを返す  
  
```  
SELECT t.name AS parent_table  
    ,t.object_id AS parent_table_id  
    ,it.name AS internal_table_name  
    ,it.object_id AS internal_table_id  
    ,xi.name AS primary_XML_index_name  
    ,xi.index_id as primary_XML_index_id  
FROM sys.internal_tables AS it  
JOIN sys.tables AS t   
    ON it.parent_id = t.object_id  
JOIN sys.xml_indexes AS xi   
    ON it.parent_id = xi.object_id  
    AND it.parent_minor_id  = xi.index_id  
WHERE it.internal_type_desc = 'XML_INDEX_NODES';  
GO  
```  
  
### <a name="h-return-internal-table-metadata-for-service-broker-queues"></a>H. Service Broker キューに関する内部テーブルのメタデータを返す  
  
```  
SELECT q.name AS queue_name  
    ,q.object_id AS queue_id  
    ,it.name AS internal_table_name  
    ,it.object_id AS internal_table_id  
FROM sys.internal_tables AS it  
JOIN sys.service_queues  AS  q ON it.parent_id = q.object_id  
WHERE it.internal_type_desc = 'QUEUE_MESSAGES';  
GO  
```  
  
## <a name="i-return-internal-table-metadata-for-all-service-broker-services"></a>I. すべての Service Broker サービスに関する内部テーブルのメタデータを返す  
  
```  
SELECT *   
FROM tempdb.sys.internal_tables   
WHERE internal_type_desc = 'SERVICE_BROKER_MAP';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
