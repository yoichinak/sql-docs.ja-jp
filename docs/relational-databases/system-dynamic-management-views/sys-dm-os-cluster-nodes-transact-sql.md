---
description: sys.dm_os_cluster_nodes (Transact-SQL)
title: sys.dm_os_cluster_nodes (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_cluster_nodes_TSQL
- dm_os_cluster_nodes_TSQL
- dm_os_cluster_nodes
- sys.dm_os_cluster_nodes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_cluster_nodes dynamic management view
ms.assetid: 92fa804e-2d08-42c6-a36f-9791544b1d42
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 532af156f9d22773a0946fff0706179e96207e84
ms.sourcegitcommit: 32135463a8494d9ed1600a58f51819359e3c09dc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2020
ms.locfileid: "91834259"
---
# <a name="sysdm_os_cluster_nodes-transact-sql"></a>sys.dm_os_cluster_nodes (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  フェールオーバークラスターインスタンス構成内のノードごとに1行の値を返します。 現在のインスタンスがフェールオーバークラスターインスタンスの場合は、このフェールオーバークラスターインスタンス (以前の "仮想サーバー") が定義されているノードの一覧を返します。 現在のサーバー インスタンスがフェールオーバー クラスター インスタンスではない場合は、空の行セットを返します。  
  
> **注:** またはからこれを呼び出すに [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] は [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 、 **sys.dm_pdw_nodes_os_cluster_nodes**という名前を使用します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**ノード**|**sysname**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]フェールオーバークラスターインスタンス (仮想サーバー) 構成のノードの名前。|  
|status|**int**|フェールオーバークラスターインスタンス内のノードの状態 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] : 0、1、2、3、-1。 詳細については、「 [Getclusternodestate 関数](/windows/win32/api/clusapi/nf-clusapi-getclusternodestate)」を参照してください。|  
|status_description|**nvarchar (20)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスター ノードの状態の説明。<br /><br /> 0 = up<br /><br /> 1 = ダウン<br /><br /> 2 = 一時停止<br /><br /> 3 = 結合<br /><br /> -1 = 不明|  
|is_current_owner|bit|1は、このノードがフェールオーバークラスターリソースの現在の所有者であることを示し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。|  
|pdw_node_id|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> このディストリビューションが配置されているノードの識別子。|  
  
## <a name="remarks"></a>注釈  
 フェールオーバー クラスタリングが有効な場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンス (仮想サーバー) 構成の一部として指定されているフェールオーバー クラスター内のどのノードでも実行できます。  
  
> **注:** このビューは fn_virtualservernodes 関数を置き換えます。これは今後のリリースで非推奨とされる予定です。  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、sys を使用します。 dm_os_cluster_nodes を使用して、クラスター化されたサーバー インスタンスの割り当てノードを返します。  
  
```  
SELECT NodeName, status, status_description, is_current_owner   
FROM sys.dm_os_cluster_nodes;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|NodeName|status|status_description|is_current_owner|  
|--------------|------------|-------------------------|------------------------|  
|node1|0|up|1|  
|node2|0|up|0|  
|Node3|1|ダウン|0|  
  
## <a name="see-also"></a>参照  
 [sys.dm_os_cluster_properties &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-properties-transact-sql.md)   
 [sys.dm_io_cluster_shared_drives &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-shared-drives-transact-sql.md)   
 [sys.fn_virtualservernodes &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-virtualservernodes-transact-sql.md)   
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
