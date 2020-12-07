---
description: sys.pdw_nodes_pdw_physical_databases (Transact-sql)
title: sys.pdw_nodes_pdw_physical_databases (Transact-sql)
ms.custom: seo-dt-2019
ms.date: 03/09/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 70e0939d-4d97-4ae0-ba16-934e0a80e718
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 3f4b29984f962f2ec4f542a57cd604c619a78c6a
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036715"
---
# <a name="syspdw_nodes_pdw_physical_databases-transact-sql"></a>sys.pdw_nodes_pdw_physical_databases (Transact-sql)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  コンピューティングノードの物理データベースごとに1行のデータを格納します。 物理データベース情報を集計して、データベースに関する詳細情報を取得します。 情報を結合するには、を `sys.pdw_nodes_pdw_physical_databases` `sys.pdw_database_mappings` テーブルとテーブルに結合し `sys.databases` ます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|database_id|**int**|データベースのオブジェクト ID。 この値は、 [transact-sql&#41;ビュー &#40;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) の database_id と同じではないことに注意してください。|  
|physical_name|**sysname**|シェル/コンピューティングノード上のデータベースの物理名。 この値は、 [transact-sql&#41;ビュー &#40;sys.pdw_database_mappings ](../../relational-databases/system-catalog-views/sys-pdw-database-mappings-transact-sql.md) の [physical_name] 列の値と同じです。|  
|pdw_node_id|**int**|ノードに関連付けられている一意の数値 id。|  
  
## <a name="examples-sspdw"></a>例: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-returning"></a>A. 不正  
 次のクエリでは、master の各データベースの名前と ID、および各計算ノードの対応するデータベース名が返されます。  
  
```  
SELECT D.database_id AS DBID_in_master, D.name AS UserDatabaseName,   
PD.pdw_node_id AS NodeID, DM.physical_name AS PhysDBName   
FROM sys.databases AS D  
JOIN sys.pdw_database_mappings AS DM  
    ON D.database_id = DM.database_id  
JOIN sys.pdw_nodes_pdw_physical_databases AS PD  
    ON DM.physical_name = PD.physical_name  
ORDER BY D.database_id, PD.pdw_node_ID;  
```  
  
### <a name="b-using-syspdw_nodes_pdw_physical_databases-to-gather-detailed-object-information"></a>B. Sys.pdw_nodes_pdw_physical_databases を使用した詳細なオブジェクト情報の収集  
 次のクエリは、インデックスに関する情報を表示し、データベース内のオブジェクトにオブジェクトが属しているデータベースに関する有用な情報を格納します。  
  
```  
SELECT D.name AS UserDatabaseName, D.database_id AS DBIDinMaster,  
DM.physical_name AS PhysDBName, PD.pdw_node_id AS NodeID,   
IU.object_id, IU.index_id, IU.user_seeks, IU.user_scans, IU.user_lookups, IU.user_updates  
FROM sys.databases AS D  
JOIN sys.pdw_database_mappings AS DM  
    ON D.database_id = DM.database_id  
JOIN sys.pdw_nodes_pdw_physical_databases AS PD  
    ON DM.physical_name = PD.physical_name  
JOIN sys.dm_pdw_nodes_db_index_usage_stats AS IU  
    ON PD.database_id = IU.database_id  
ORDER BY D.database_id, IU.object_id, IU.index_id, PD.pdw_node_ID;  
```  
  
### <a name="c-using-syspdw_nodes_pdw_physical_databases-to-determine-the-encryption-state"></a>C. Sys.pdw_nodes_pdw_physical_databases を使用して暗号化の状態を確認する  
 次のクエリは、AdventureWorksPDW2012 データベースの暗号化の状態を提供します。  
  
```  
WITH dek_encryption_state AS   
(  
    SELECT ISNULL(db_map.database_id, dek.database_id) AS database_id, encryption_state  
    FROM sys.dm_pdw_nodes_database_encryption_keys AS dek  
        INNER JOIN sys.pdw_nodes_pdw_physical_databases AS node_db_map  
            ON dek.database_id = node_db_map.database_id AND dek.pdw_node_id = node_db_map.pdw_node_id  
        LEFT JOIN sys.pdw_database_mappings AS db_map  
            ON node_db_map .physical_name = db_map.physical_name  
        INNER JOIN sys.dm_pdw_nodes AS nodes  
            ON nodes.pdw_node_id = dek.pdw_node_id  
    WHERE dek.encryptor_thumbprint <> 0x  
)  
SELECT TOP 1 encryption_state  
       FROM  dek_encryption_state  
       WHERE dek_encryption_state.database_id = DB_ID('AdventureWorksPDW2012 ')  
       ORDER BY (CASE encryption_state WHEN 3 THEN -1 ELSE encryption_state END) DESC;  
```  
  
## <a name="see-also"></a>参照  
 [Azure Synapse Analytics と Parallel Data Warehouse のカタログ ビュー](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.pdw_database_mappings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-database-mappings-transact-sql.md)  
  
  

