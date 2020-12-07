---
description: dm_exec_query_resource_semaphores (Transact-sql)
title: dm_exec_query_resource_semaphores (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_query_resource_semaphores_TSQL
- dm_exec_query_resource_semaphores_TSQL
- sys.dm_exec_query_resource_semaphores
- dm_exec_query_resource_semaphores
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_resource_semaphores dynamic management view
ms.assetid: e43a2aa9-dd52-4c89-911e-1a7d05f7ffbb
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6d782c81ce803441e91d6008ae5b0117522c3286
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548562"
---
# <a name="sysdm_exec_query_resource_semaphores-transact-sql"></a>dm_exec_query_resource_semaphores (Transact-sql)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  現在のクエリのリソースセマフォの状態に関する情報を返し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ますです。 **dm_exec_query_resource_semaphores** は、一般的なクエリ実行メモリの状態を提供し、システムが十分なメモリにアクセスできるかどうかを判断できます。 このビューは、サーバーのメモリステータスの完全な画像を提供するために、dm_os_memory_clerks から取得したメモリ情報を補完し [ます](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md) 。 **dm_exec_query_resource_semaphores** は、通常のリソースセマフォに対して1つの行を返し、小さいクエリのリソースセマフォ用に別の行を返します。 小規模クエリセマフォには、次の2つの要件があります。  
  
-   要求されたメモリ許可は 5 MB 未満である必要があります  
  
-   クエリコストは、3コスト単位未満にする必要があります  
  
> [!NOTE]  
>  またはからこれを呼び出すに [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] は [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 、 **dm_pdw_nodes_exec_query_resource_semaphores**という名前を使用します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**resource_semaphore_id**|**smallint**|リソースセマフォの一意でない ID。 通常のリソースセマフォの場合は0、小さいクエリのリソースセマフォの場合は1。|  
|**target_memory_kb**|**bigint**|使用状況のターゲットをキロバイト単位で付与します。|  
|**max_target_memory_kb**|**bigint**|最大許容対象メモリ (KB 単位)。 小さいクエリのリソースセマフォの場合は NULL です。|  
|**total_memory_kb**|**bigint**|リソースセマフォによって保持されているメモリ (kb 単位)。 システムでメモリ不足が発生している場合、または強制最小メモリが頻繁に許可されている場合、この値は **target_memory_kb** または **max_target_memory_kb** の値よりも大きくなる可能性があります。 合計メモリは、使用可能なメモリと許可されているメモリの合計です。|  
|**available_memory_kb**|**bigint**|新しい許可で使用可能なメモリ (kb 単位)。|  
|**granted_memory_kb**|**bigint**|許可されたメモリの合計 (kb 単位)。|  
|**used_memory_kb**|**bigint**|許可されるメモリの一部をキロバイト単位で物理的に使用します。|  
|**grantee_count**|**int**|許可が満たされているアクティブなクエリの数。|  
|**waiter_count**|**int**|許可条件が満たされるのを待機しているクエリの数。|  
|**timeout_error_count**|**bigint**|サーバーが起動した後のタイムアウト エラーの合計数。 小さいクエリのリソースセマフォの場合は NULL です。|  
|**forced_grant_count**|**bigint**|サーバーが起動してからの強制された最小メモリ許可の合計数。 小さいクエリのリソースセマフォの場合は NULL です。|  
|**pool_id**|**int**|このリソースセマフォが属するリソースプールの ID。|  
|**pdw_node_id**|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> このディストリビューションが配置されているノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可  

で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium レベルでは、データベースの権限が必要です `VIEW DATABASE STATE` 。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Standard レベルおよび Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   
  
## <a name="remarks"></a>解説  
 ORDER BY または集計を含む動的管理ビューを使用するクエリでは、メモリ使用量が増加し、トラブルシューティングの問題に寄与する可能性があります。  
  
 トラブルシューティングには**dm_exec_query_resource_semaphores**を使用しますが、今後のバージョンのを使用するアプリケーションには含めないでください。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 データベース管理者は、リソース ガバナー機能を使用することで、サーバー リソースを最大 64 個までのリソース プールに分散できます。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降では、各プールが小規模の独立したサーバー インスタンスのように動作し、2 つのセマフォを必要とします。  
  
## <a name="see-also"></a>参照  
 [実行関連の動的管理ビューおよび関数 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_query_memory_grants &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)  
  
  


