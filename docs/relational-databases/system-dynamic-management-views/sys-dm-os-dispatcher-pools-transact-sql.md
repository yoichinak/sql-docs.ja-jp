---
description: sys.dm_os_dispatcher_pools (Transact-SQL)
title: dm_os_dispatcher_pools (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_dispatcher_pools_TSQL
- dm_os_dispatcher_pools
- sys.dm_os_dispatcher_pools
- sys.dm_os_dispatcher_pools_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- extended events [SQL Server], views
- sys.dm_os_dispatcher_pools DMV
ms.assetid: b9edbc83-c6bc-4753-9bb5-a454cfe7d6bf
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a1810098b53ab87f98687a767f384674fcdaa8bc
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89531902"
---
# <a name="sysdm_os_dispatcher_pools-transact-sql"></a>sys.dm_os_dispatcher_pools (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  セッション ディスパッチャー プールに関する情報を返します。 ディスパッチャープールは、バックグラウンド処理を実行するためにシステムコンポーネントによって使用されるスレッドプールです。  
  
> [!NOTE]  
>  またはからこれを呼び出すに [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] は [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 、 **dm_pdw_nodes_os_dispatcher_pools**という名前を使用します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|dispatcher_pool_address|**varbinary (8)**|ディスパッチャープールのアドレス。 dispatcher_pool_address は一意です。 NULL 値は許可されません。|  
|型|**nvarchar (256)**|ディスパッチャープールの種類。 NULL 値は許可されません。 ディスパッチャープールには、次の2種類があります。<br /><br /> DISP_POOL_XE_ENGINE<br /><br /> DISP_POOL_XE_SESSION<br /><br /> DMV で完全な一覧を照会する|  
|name|**nvarchar (256)**|ディスパッチャー プールの名前。 NULL 値は許可されません。|  
|dispatcher_count|**int**|アクティブなディスパッチャースレッドの数。 NULL 値は許可されません。|  
|dispatcher_ideal_count|**int**|ディスパッチャープールが使用できるようになるディスパッチャースレッドの数。 NULL 値は許可されません。|  
|dispatcher_timeout_ms|**int**|ディスパッチャーが終了する前に新しい作業を待機する時間 (ミリ秒単位)。 NULL 値は許可されません。|  
|dispatcher_waiting_count|**int**|アイドル状態のディスパッチャー スレッドの数。 NULL 値は許可されません。|  
|queue_length|**int**|ディスパッチャープールによって処理されるのを待機している作業項目の数。 NULL 値は許可されません。|  
|pdw_node_id|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> このディストリビューションが配置されているノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可

で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium レベルでは、データベースの権限が必要です `VIEW DATABASE STATE` 。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Standard レベルおよび Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   

## <a name="see-also"></a>参照  
  
  


