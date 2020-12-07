---
description: sys.dm_os_memory_clerks (Transact-SQL)
title: dm_os_memory_clerks (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_memory_clerks
- sys.dm_os_memory_clerks
- dm_os_memory_clerks_TSQL
- sys.dm_os_memory_clerks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_clerks dynamic management view
ms.assetid: 1d556c67-5c12-46d5-aa8c-7ec1bb858df7
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2f5841aab34fbea23d3933f918c2ab9298594c81
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550274"
---
# <a name="sysdm_os_memory_clerks-transact-sql"></a>sys.dm_os_memory_clerks (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  のインスタンスで現在アクティブなすべてのメモリクラークのセットを返し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
> [!NOTE]  
>  またはからこれを呼び出すに [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] は [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 、 **dm_pdw_nodes_os_memory_clerks**という名前を使用します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**memory_clerk_address**|**varbinary (8)**|メモリ クラークの一意のメモリ アドレスを指定します。 これは主キー列です。 NULL 値は許可されません。|  
|**type**|**nvarchar(60)**|メモリクラークの種類を指定します。 各クラークには、CLR Clerks MEMORYCLERK_SQLCLR などの特定の種類があります。 NULL 値は許可されません。|  
|**name**|**nvarchar (256)**|このメモリ クラークに内部的に割り当てられた名前を指定します。 コンポーネントは、特定の種類の複数のメモリクラークを持つことができます。 同じ種類のメモリ クラークを識別するために、コンポーネントで特定の名前を選択して使用することもできます。 NULL 値は許可されません。|  
|**memory_node_id**|**smallint**|メモリノードの ID を指定します。 NULL 値は許可されません。|  
|**single_pages_kb**|**bigint**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] から [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|  
|**pages_kb**|**bigint**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> このメモリクラークに割り当てられたページメモリの量をキロバイト (KB) 単位で指定します。 NULL 値は許可されません。|  
|**multi_pages_kb**|**bigint**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] から [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /><br /> 割り当てられた複数ページメモリの量 (KB 単位)。 これは、メモリノードの複数ページアロケーターを使用して割り当てられたメモリの量です。 このメモリは、バッファー プール外に割り当てられ、メモリ ノードの仮想アロケーターを利用します。 NULL 値は許可されません。|  
|**virtual_memory_reserved_kb**|**bigint**|メモリクラークによって予約されている仮想メモリの量を指定します。 NULL 値は許可されません。|  
|**virtual_memory_committed_kb**|**bigint**|メモリクラークによってコミットされる仮想メモリの量を指定します。 コミット済みのメモリ量は、予約済みのメモリ量よりも常に少ない状態である必要があります。 NULL 値は許可されません。|  
|**awe_allocated_kb**|**bigint**|オペレーティングシステムによってページングされていない物理メモリ内のメモリの量をキロバイト (KB) 単位で指定します。 NULL 値は許可されません。|  
|**shared_memory_reserved_kb**|**bigint**|メモリクラークによって予約されている共有メモリの量を指定します。 共有メモリおよびファイル マッピングで使用するために予約されるメモリの量です。 NULL 値は許可されません。|  
|**shared_memory_committed_kb**|**bigint**|メモリ クラークによってコミット済みの共有メモリの量を指定します。 NULL 値は許可されません。|  
|**page_size_in_bytes**|**bigint**|このメモリ クラークのページ割り当ての粒度を指定します。 NULL 値は許可されません。|  
|**page_allocator_address**|**varbinary (8)**|ページアロケーターのアドレスを指定します。 このアドレスは、メモリクラークに対して一意であり、 **dm_os_memory_objects** で使用して、この clerk にバインドされているメモリオブジェクトを見つけることができます。 NULL 値は許可されません。|  
|**host_address**|**varbinary (8)**|このメモリ クラークのホストのメモリ アドレスを指定します。 詳細については、「 [sys. dm_os_hosts &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-hosts-transact-sql.md)」を参照してください。 Native Client などのコンポーネントは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ホストインターフェイスを介してメモリリソースにアクセスします。<br /><br /> 0x00000000 = メモリ クラークは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に属します。<br /><br /> NULL 値は許可されません。|  
|**pdw_node_id**|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> このディストリビューションが配置されているノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可 

で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium レベルでは、データベースの権限が必要です `VIEW DATABASE STATE` 。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Standard レベルおよび Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   
  
## <a name="remarks"></a>解説  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メモリマネージャーは、3層階層で構成されます。 階層の最下部には、メモリノードがあります。 中間レベルは、メモリクラーク、メモリキャッシュ、およびメモリプールで構成されます。 最上位の階層はメモリ オブジェクトから成ります。 これらのオブジェクトは、一般的に、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスでメモリを割り当てる場合に使用されます。  
  
 メモリノードは、低レベルのアロケーターのインターフェイスと実装を提供します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部では、メモリ クラークのみがメモリ ノードにアクセスできます。 メモリクラークはメモリノードインターフェイスにアクセスしてメモリを割り当てます。 また、メモリノードは、診断の clerk を使用して割り当てられたメモリを追跡します。 大量のメモリを割り当てるすべてのコンポーネントは、独自のメモリクラークを作成し、clerk インターフェイスを使用してすべてのメモリを割り当てる必要があります。 通常、コンポーネントは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の起動時に、それぞれに対応したクラークを作成します。  
  
## <a name="see-also"></a>参照  

 [SQL Server オペレーティングシステム関連の動的管理ビュー &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [dm_exec_query_memory_grants &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [dm_exec_query_plan &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)   
 [dm_exec_sql_text &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)  
  
  


