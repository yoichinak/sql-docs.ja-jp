---
description: dm_os_process_memory (Transact-sql)
title: dm_os_process_memory (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_process_memory_TSQL
- dm_os_process_memory_TSQL
- dm_os_process_memory
- sys.dm_os_process_memory
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_process_memory dynamic management view
ms.assetid: e838130c-95d4-4605-9e3b-eb0ab71cd250
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4234894d907a383902a00a659e954ccfea2ff74c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539319"
---
# <a name="sysdm_os_process_memory-transact-sql"></a>dm_os_process_memory (Transact-sql)
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセス空間から生じる大半のメモリ割り当ては、こうした割り当ての追跡と管理を可能にするインターフェイスを通じて制御されます。 ただし、メモリ割り当てが、内部のメモリ管理ルーチンをバイパスする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アドレス空間で実行される場合もあります。 値は、ベースとなるオペレーティング システムを通じて取得されます。 これらのメソッドは、ロックされ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] たページまたは大きいページ割り当てを調整する場合を除き、内部のメソッドによって操作されることはありません。  
  
 メモリサイズを示すすべての戻り値は、キロバイト (KB) 単位で表示されます。 列**total_virtual_address_space_reserved_kb**は、 **sys. dm_os_sys_info**からの**virtual_memory_in_bytes**と重複しています。  
  
 次の表は、プロセス アドレス空間の全体像を表したものです。  
  
> [!NOTE]  
>  またはからこれを呼び出すに [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] は [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 、 **dm_pdw_nodes_os_process_memory**という名前を使用します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**physical_memory_in_use_kb**|**bigint**|オペレーティング システムから報告されたプロセス ワーキング セットに、ラージ ページ API を使用して追跡された割り当てを加えた値 (KB 単位) を示します。 NULL 値は許可されません。|  
|**large_page_allocations_kb**|**bigint**|ラージページ Api を使用して割り当てられた物理メモリを指定します。 NULL 値は許可されません。|  
|**locked_page_allocations_kb**|**bigint**|メモリ内でロックされているメモリページを指定します。 NULL 値は許可されません。|  
|**total_virtual_address_space_kb**|**bigint**|仮想アドレス空間のユーザーモード部分の合計サイズを示します。 NULL 値は許可されません。|  
|**virtual_address_space_reserved_kb**|**bigint**|プロセスによって予約されている仮想アドレス空間の合計サイズを示します。 NULL 値は許可されません。|  
|**virtual_address_space_committed_kb**|**bigint**|コミットまたは物理ページにマップされた予約済みの仮想アドレス空間の量を示します。 NULL 値は許可されません。|  
|**virtual_address_space_available_kb**|**bigint**|現在利用可能な仮想アドレス空間の量を示します。 NULL 値は許可されません。<br /><br /> **注:** 割り当ての粒度よりも小さい空き領域が存在する可能性があります。 これらの領域は割り当てに利用できません。|  
|**page_fault_count**|**bigint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のプロセスに起因するページ違反の数を示します。 NULL 値は許可されません。|  
|**memory_utilization_percentage**|**int**|ワーキングセット内のコミット済みメモリの割合を指定します。 NULL 値は許可されません。|  
|**available_commit_limit_kb**|**bigint**|プロセスによってコミット可能なメモリの量を示します。 NULL 値は許可されません。|  
|**process_physical_memory_low**|**bit**|プロセスが物理メモリの不足の通知に応答していることを示します。 NULL 値は許可されません。|  
|**process_virtual_memory_low**|**bit**|仮想メモリ不足の状態が検出されたことを示します。 NULL 値は許可されません。|  
|**pdw_node_id**|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> このディストリビューションが配置されているノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可  
 で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium レベルでは、データベースの権限が必要です `VIEW DATABASE STATE` 。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Standard レベルおよび Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [SQL Server オペレーティングシステム関連の動的管理ビュー &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


