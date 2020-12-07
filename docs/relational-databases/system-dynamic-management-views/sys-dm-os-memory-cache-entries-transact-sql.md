---
description: dm_os_memory_cache_entries (Transact-sql)
title: dm_os_memory_cache_entries (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_memory_cache_entries
- sys.dm_os_memory_cache_entries
- dm_os_memory_cache_entries_TSQL
- sys.dm_os_memory_cache_entries_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_cache_entries dynamic management view
ms.assetid: dd32be6b-10d1-4059-b4fd-0bf817f40d54
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b29f7d03fc23fdb0d204de5f2f3cbd15bd6f74a7
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542153"
---
# <a name="sysdm_os_memory_cache_entries-transact-sql"></a>dm_os_memory_cache_entries (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で、キャッシュ内のすべてのエントリに関する情報を返します。 このビューを使用して、関連付けられているオブジェクトに対するキャッシュエントリをトレースします。 このビューを使用して、キャッシュエントリの統計情報を取得することもできます。  
  
> [!NOTE]  
>  またはからこれを呼び出すに [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] は [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 、 **dm_pdw_nodes_os_memory_cache_entries**という名前を使用します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary (8)**|キャッシュのアドレス。 NULL 値は許可されません。|  
|**name**|**nvarchar (256)**|キャッシュの名前。 NULL 値は許可されません。|  
|**type**|**varchar(60)**|キャッシュの種類。 NULL 値は許可されません。|  
|**entry_address**|**varbinary (8)**|キャッシュエントリの記述子のアドレス。 NULL 値は許可されません。|  
|**entry_data_address**|**varbinary (8)**|キャッシュエントリ内のユーザーデータのアドレス。<br /><br /> 0x00000000 = エントリ データ アドレスは使用できません。<br /><br /> NULL 値は許可されません。|  
|**in_use_count**|**int**|このキャッシュエントリの同時実行ユーザー数。 NULL 値は許可されません。|  
|**is_dirty**|**bit**|このキャッシュ エントリが削除対象としてマークされているかどうかを示します。 1 = 削除用にマークされています。 NULL 値は許可されません。|  
|**disk_ios_count**|**int**|このエントリが作成されたときに発生した i/o の数。 NULL 値は許可されません。|  
|**context_switches_count**|**int**|このエントリの作成中に発生したコンテキストスイッチの数。 NULL 値は許可されません。|  
|**original_cost**|**int**|エントリの元のコスト。 この値は、発生した i/o の数、CPU 命令のコスト、およびエントリによって消費されるメモリの量を概算したものです。 コストが大きいほど、アイテムがキャッシュから削除される可能性は低くなります。 NULL 値は許可されません。|  
|**current_cost**|**int**|キャッシュエントリの現在のコスト。 この値はエントリの削除プロセス中に更新されます。 現在のコストは、エントリの再利用時に元の値にリセットされます。 NULL 値は許可されません。|  
|**memory_object_address**|**varbinary (8)**|関連付けられているメモリオブジェクトのアドレス。 NULL 値が許可されます。|  
|**pages_allocated_count**|**bigint**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] から [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /><br /> キャッシュ エントリを格納する 8 KB ページの数。 NULL 値は許可されません。|  
|**pages_kb**|**bigint**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> このキャッシュエントリで使用されるメモリの量 (KB 単位)。  NULL 値は許可されません。|  
|**entry_data**|**nvarchar(2048)**|キャッシュされたエントリのシリアル化された表現。 この情報は、キャッシュストアに依存します。 NULL 値が許可されます。|  
|**pool_id**|**int**|**適用対象**: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 以降。<br /><br /> エントリに関連付けられているリソースプール id。 NULL 値が許可されます。<br /><br /> katmai|  
|**pdw_node_id**|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> このディストリビューションが配置されているノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可 

で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium レベルでは、データベースの権限が必要です `VIEW DATABASE STATE` 。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Standard レベルおよび Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   

## <a name="see-also"></a>参照  
 
  [SQL Server オペレーティングシステム関連の動的管理ビュー &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


