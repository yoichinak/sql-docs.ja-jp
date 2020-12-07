---
description: sys.dm_pdw_nodes_database_encryption_keys (Transact-sql)
title: sys.dm_pdw_nodes_database_encryption_keys (Transact-sql)
ms.custom: seo-dt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: e7fd02b2-5d7e-4816-a0af-b58ae2ac3f7a
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 5e8a399d58c4ffa4f61e9509bd243f7e9c71275e
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037725"
---
# <a name="sysdm_pdw_nodes_database_encryption_keys-transact-sql"></a>sys.dm_pdw_nodes_database_encryption_keys (Transact-sql)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  データベースの暗号化の状態と、それに関連付けられているデータベース暗号化キーに関する情報を返します。 **sys.dm_pdw_nodes_database_encryption_keys** は、各ノードにこの情報を提供します。 データベース暗号化の詳細については、「 [Transparent Data Encryption (SQL Server PDW)](../../analytics-platform-system/transparent-data-encryption.md)」を参照してください。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|database_id|**int**|各ノード上の物理データベースの ID。|  
|encryption_state|**int**|このノードのデータベースが暗号化されているか、暗号化されていないかを示します。<br /><br /> 0 = データベース暗号化キーは存在しません。暗号化は行われません。<br /><br /> 1 = 暗号化されていない<br /><br /> 2 = 暗号化が進行中<br /><br /> 3 = 暗号化<br /><br /> 4 = キーの変更中<br /><br /> 5 = 暗号化解除中<br /><br /> 6 = 保護の変更中 (データベース暗号化キーを暗号化する証明書が変更されています)|  
|create_date|**datetime**|暗号化キーが作成された日付が表示されます。|  
|regenerate_date|**datetime**|暗号化キーが再生成された日付が表示されます。|  
|modify_date|**datetime**|暗号化キーが変更された日付が表示されます。|  
|set_date|**datetime**|暗号化キーがデータベースに適用された日付が表示されます。|  
|opened_date|**datetime**|データベースキーが最後に開かれた日時を表示します。|  
|key_algorithm|**varchar (?)**|キーに使用されるアルゴリズムが表示されます。|  
|key_length|**int**|キーの長さを表示します。|  
|encryptor_thumbprint|**varbin**|暗号化のサムプリントを表示します。|  
|percent_complete|**real**|データベース暗号化状態の変更の完了率。 状態の変更がない場合、これは0になります。|  
|node_id|**int**|ノードに関連付けられている一意の数値 id。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="examples-sssdwfull-and-sspdw"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 次の例では、 `sys.dm_pdw_nodes_database_encryption_keys` 他のシステムテーブルと結合して、TDE で保護されたデータベースの各ノードの暗号化状態を示しています。  
  
```  
SELECT D.database_id AS DBIDinMaster, D.name AS UserDatabaseName,   
PD.pdw_node_id AS NodeID, DM.physical_name AS PhysDBName,   
keys.encryption_state  
FROM sys.dm_pdw_nodes_database_encryption_keys AS keys  
JOIN sys.pdw_nodes_pdw_physical_databases AS PD  
    ON keys.database_id = PD.database_id AND keys.pdw_node_id = PD.pdw_node_id  
JOIN sys.pdw_database_mappings AS DM  
    ON DM.physical_name = PD.physical_name  
JOIN sys.databases AS D  
    ON D.database_id = DM.database_id  
ORDER BY D.database_id, PD.pdw_node_ID;  
```  
  
## <a name="see-also"></a>参照  
 [Azure Synapse Analytics と並列データウェアハウスの動的管理ビュー &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-encryption-key-transact-sql.md)   
 [ALTER DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-encryption-key-transact-sql.md)   
 [DROP DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-encryption-key-transact-sql.md)  
  
  

