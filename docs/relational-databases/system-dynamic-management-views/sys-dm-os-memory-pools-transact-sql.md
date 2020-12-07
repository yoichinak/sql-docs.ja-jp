---
description: dm_os_memory_pools (Transact-sql)
title: dm_os_memory_pools (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_pools_TSQL
- dm_os_memory_pools
- dm_os_memory_pools_TSQL
- sys.dm_os_memory_pools
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_pools dynamic management view
ms.assetid: 1ef053f3-c6f3-456e-82b6-26e4bd630d46
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 24ac0a1611d9b5996f2181a4d2c533bc2972bc86
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536990"
---
# <a name="sysdm_os_memory_pools-transact-sql"></a>dm_os_memory_pools (Transact-sql)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  のインスタンス内のオブジェクトストアごとに1行の値を返し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 このビューを使用すると、キャッシュメモリの使用状況を監視し、無効なキャッシュ動作を識別できます。  
  
> [!NOTE]  
>  またはからこれを呼び出すに [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] は [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 、 **dm_pdw_nodes_os_memory_pools**という名前を使用します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**memory_pool_address**|**varbinary (8)**|メモリ プールを表すエントリのメモリ アドレス。 NULL 値は許可されません。|  
|**pool_id**|**int**|プールのセット内にある特定プールの ID。 NULL 値は許可されません。|  
|**type**|**nvarchar(60)**|オブジェクトプールの種類。 NULL 値は許可されません。 詳細については、「 [sys. dm_os_memory_clerks &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)」を参照してください。|  
|**name**|**nvarchar (256)**|システムによって割り当てられた、メモリ オブジェクトの名前。 NULL 値は許可されません。|  
|**max_free_entries_count**|**bigint**|プールに含めることができる空きエントリの最大数。 NULL 値は許可されません。|  
|**free_entries_count**|**bigint**|現在プール内にある空きエントリ数。 NULL 値は許可されません。|  
|**removed_in_all_rounds_count**|**bigint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの起動後、プールから削除されたエントリ数。 NULL 値は許可されません。|  
|**pdw_node_id**|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> このディストリビューションが配置されているノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可

で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium レベルでは、データベースの権限が必要です `VIEW DATABASE STATE` 。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Standard レベルおよび Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   

## <a name="remarks"></a>解説  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントは、共通のプールフレームワークを使用して、同種のステートレスなデータをキャッシュすることがあります。 プール フレームワークは、キャッシュ フレームワークよりも単純です。 プール内のすべてのエントリが等しいと見なされます。 内部的には、プールはメモリ クラークであり、メモリ クラークが使用される場所で使用できます。  
  
## <a name="see-also"></a>参照  
 
  [SQL Server オペレーティングシステム関連の動的管理ビュー &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


