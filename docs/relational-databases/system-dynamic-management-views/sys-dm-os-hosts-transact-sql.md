---
description: sys.dm_os_hosts (Transact-sql)
title: sys.dm_os_hosts (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sys.dm_os_hosts_TSQL
- dm_os_hosts
- dm_os_hosts_TSQL
- sys.dm_os_hosts
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_hosts dynamic management view
ms.assetid: a313ff3b-1fe9-421e-b94b-cea19c43b0e5
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: d82b85a23c67979e8f94a9358d0175d21193dc15
ms.sourcegitcommit: 9413ddd8071da8861715c721b923e52669a921d8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "101837599"
---
# <a name="sysdm_os_hosts-transact-sql"></a>sys.dm_os_hosts (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  のインスタンスに現在登録されているすべてのホストを返し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 このビューでは、ホストで使用されているリソースも返されます。  
  
> [!NOTE]  
>  またはからこれを呼び出すに [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] は [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 、 **sys.dm_pdw_nodes_os_hosts** という名前を使用します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**host_address**|**varbinary (8)**|ホスト オブジェクトの内部メモリ アドレス。|  
|**type**|**nvarchar(60)**|ホストされるコンポーネントの種類。 たとえば、次のように入力します。<br /><br /> SOSHOST_CLIENTID_SERVERSNI = SQL Server ネイティブインターフェイス<br /><br /> SOSHOST_CLIENTID_SQLOLEDB = SQL Server Native Client OLE DB プロバイダー<br /><br /> SOSHOST_CLIENTID_MSDART = Microsoft データアクセスの実行時|  
|**name**|**nvarchar(32)**|ホストの名前。|  
|**enqueued_tasks_count**|**int**|ホストによって [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のキューに挿入されたタスクの合計数。|  
|**active_tasks_count**|**int**|このホストがキューに配置した現在実行中のタスクの数。|  
|**completed_ios_count**|**int**|このホストで発行され、完了した i/o の合計数。|  
|**completed_ios_in_bytes**|**bigint**|このホストで完了した i/o の合計バイト数。|  
|**active_ios_count**|**int**|現在完了を待機しているこのホストに関連する i/o 要求の合計数。|  
|**default_memory_clerk_address**|**varbinary (8)**|このホストに関連付けられているメモリクラークオブジェクトのメモリアドレス。 詳細については、「 [sys.dm_os_memory_clerks &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)」を参照してください。|  
|**pdw_node_id**|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> このディストリビューションが配置されているノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可

で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   
SQL Database Basic、S0、S1 のサービス目標、およびエラスティックプール内のデータベースについては、 [サーバー管理者](/azure/azure-sql/database/logins-create-manage#existing-logins-and-user-accounts-after-creating-a-new-database) アカウントまたは [Azure Active Directory 管理者](/azure/azure-sql/database/authentication-aad-overview#administrator-structure) アカウントが必要です。 その他のすべての SQL Database サービスの目的で `VIEW DATABASE STATE` は、データベースで権限が必要になります。   

## <a name="remarks"></a>解説  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の実行可能なコンポーネント以外の OLE DB プロバイダーなどのコンポーネントが、メモリを割り当てたりノンプリエンプティブなスケジュールに参加することが許可されます。 これらのコンポーネントはによってホストされ、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] これらのコンポーネントによって割り当てられるすべてのリソースが追跡されます。 ホスティングによって、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の外部コンポーネントで使用されるリソースをより正確に把握できます。  
  
## <a name="relationship-cardinalities"></a>リレーションシップ基数  
  
|差出人|終了|Relationship|  
|----------|--------|------------------|  
|sys.dm_os_hosts. default_memory_clerk_address|sys.dm_os_memory_clerks。 memory_clerk_address|1対1|  
|sys.dm_os_hosts. host_address|sys.dm_os_memory_clerks。 host_address|1対1|  
  
## <a name="examples"></a>例  
 次の例では、ホストされるコンポーネントによってコミットされたメモリの合計量を確認します。  
  
||  
|-|  
|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。|  
  
```  
SELECT h.type, SUM(mc.pages_kb) AS commited_memory  
FROM sys.dm_os_memory_clerks AS mc   
INNER JOIN sys.dm_os_hosts AS h   
    ON mc.memory_clerk_address = h.default_memory_clerk_address  
GROUP BY h.type;  
```  
  
## <a name="see-also"></a>参照  

 [sys.dm_os_memory_clerks &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)   
 [SQL Server オペレーティングシステム関連の動的管理ビュー &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
