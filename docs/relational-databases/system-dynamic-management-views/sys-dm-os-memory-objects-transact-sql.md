---
description: dm_os_memory_objects (Transact-sql)
title: dm_os_memory_objects (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_memory_objects
- sys.dm_os_memory_objects
- sys.dm_os_memory_objects_TSQL
- dm_os_memory_objects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_objects dynamic management view
ms.assetid: 5688bcf8-5da9-4ff9-960b-742b671d7096
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 42e6d315d2a3450223e7a5d9f1a6d9e75ac5d4b6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539369"
---
# <a name="sysdm_os_memory_objects-transact-sql"></a>dm_os_memory_objects (Transact-sql)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  現在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって割り当てられているメモリ オブジェクトを返します。 **Dm_os_memory_objects**を使用すると、メモリの使用量を分析し、メモリリークの可能性を特定できます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**memory_object_address**|**varbinary (8)**|メモリオブジェクトのアドレス。 NULL 値は許可されません。|  
|**parent_address**|**varbinary (8)**|親メモリ オブジェクトのアドレス。 NULL 値が許可されます。|  
|**pages_allocated_count**|**int**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] から [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /><br /> メモリ オブジェクトによって割り当てられているページ数。 NULL 値は許可されません。|  
|**pages_in_bytes**|**bigint**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> メモリオブジェクトのこのインスタンスによって割り当てられたメモリの量 (バイト単位)。 NULL 値は許可されません。|  
|**creation_options**|**int**|内部使用のみです。 NULL 値が許可されます。|  
|**bytes_used**|**bigint**|内部使用のみです。 NULL 値が許可されます。|  
|**type**|**nvarchar(60)**|メモリ オブジェクトの種類。<br /><br /> これは、このメモリオブジェクトが属するコンポーネント、またはメモリオブジェクトの関数を示します。 NULL 値が許可されます。|  
|**name**|**varchar(128)**|内部使用のみです。 NULL 値は許可されます。|  
|**memory_node_id**|**smallint**|メモリ オブジェクトが使用しているメモリ ノードの ID。 NULL 値は許可されません。|  
|**creation_time**|**datetime**|内部使用のみです。 NULL 値が許可されます。|  
|**max_pages_allocated_count**|**int**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] から [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /><br /> このメモリオブジェクトによって割り当てられたページの最大数。 NULL 値は許可されません。|  
|**page_size_in_bytes**|**int**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> メモリ オブジェクトによって割り当てられているのページのサイズ (バイト単位)。 NULL 値は許可されません。|  
|**max_pages_in_bytes**|**bigint**|このメモリオブジェクトによって使用されるメモリの最大量。 NULL 値は許可されません。|  
|**page_allocator_address**|**varbinary (8)**|ページアロケーターのメモリアドレス。 NULL 値は許可されません。 詳細については、「 [sys. dm_os_memory_clerks &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)」を参照してください。|  
|**creation_stack_address**|**varbinary (8)**|内部使用のみです。 NULL 値が許可されます。|  
|**sequence_num**|**int**|内部使用のみです。 NULL 値が許可されます。|  
|**partition_type**|**int**|**適用対象**: [!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] 以降。<br /><br /> パーティションの種類。<br /><br /> 0-パーティション分割が不可能なメモリオブジェクト<br /><br /> 1-分割できないメモリオブジェクト (現在パーティション分割されていません)<br /><br /> 2-分割されたメモリオブジェクト。 NUMA ノードによってパーティション分割されます。 1つの NUMA ノードを持つ環境では、これは1に相当します。<br /><br /> 3-CPU でパーティション分割された、パーティション分割されたメモリオブジェクト。|  
|**contention_factor**|**real**|**適用対象**: [!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] 以降。<br /><br /> このメモリオブジェクトの競合を指定する値。0は競合しないことを意味します。 値は、指定された数のメモリ割り当てがその期間中に競合を反映したときに更新されます。 スレッドセーフなメモリオブジェクトにのみ適用されます。|  
|**waiting_tasks_count**|**bigint**|**適用対象**: [!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] 以降。<br /><br /> このメモリオブジェクトで待機している回数。 このカウンターは、メモリオブジェクトからメモリが割り当てられるたびにインクリメントされます。 インクリメントは、このメモリオブジェクトへのアクセスを現在待機しているタスクの数です。 スレッドセーフなメモリオブジェクトにのみ適用されます。 これは、正確性を保証せずに、ベストエフォートの値です。|  
|**exclusive_access_count**|**bigint**|**適用対象**: [!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] 以降。<br /><br /> このメモリオブジェクトに排他的にアクセスする頻度を指定します。 スレッドセーフなメモリオブジェクトにのみ適用されます。  これは、正確性を保証せずに、ベストエフォートの値です。|  
|**pdw_node_id**|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> このディストリビューションが配置されているノードの識別子。|  
  
 **partition_type**、 **contention_factor**、 **waiting_tasks_count**、および **exclusive_access_count** は、にまだ実装されていません [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] 。  
  
## <a name="permissions"></a>アクセス許可

で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium レベルでは、データベースの権限が必要です `VIEW DATABASE STATE` 。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Standard レベルおよび Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   

## <a name="remarks"></a>解説  
 メモリ オブジェクトはヒープであり、 割り当ての粒度はメモリ クラークよりも細かくなります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントでは、メモリ クラークの代わりにメモリ オブジェクトが使用されます。 メモリオブジェクトは、メモリクラークのページアロケーターインターフェイスを使用してページを割り当てます。 メモリオブジェクトは、仮想または共有メモリインターフェイスを使用しません。 割り当てパターンに応じて、コンポーネントでは各種メモリ オブジェクトを作成し、任意のサイズの領域を割り当てることができます。  
  
 メモリオブジェクトの一般的なページサイズは 8 KB です。 ただし、増分メモリオブジェクトのページサイズは、512バイトから 8 KB の範囲で指定できます。  
  
> [!NOTE]  
>  ページサイズが最大割り当てではありません。 メモリ クラークによって実装されたページ アロケーターでサポートされている割り当ての粒度です。 メモリ オブジェクトから、8 KB を超える割り当てを要求することができます。  
  
## <a name="examples"></a>例  
 次の例では、それぞれのメモリ オブジェクトの種類によって割り当てられたメモリのサイズを返します。  
  
```  
SELECT SUM (pages_in_bytes) as 'Bytes Used', type   
FROM sys.dm_os_memory_objects  
GROUP BY type   
ORDER BY 'Bytes Used' DESC;  
GO  
```  
  
## <a name="see-also"></a>参照  
  [SQL Server オペレーティングシステム関連の動的管理ビュー &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [dm_os_memory_clerks &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)  
  
  


