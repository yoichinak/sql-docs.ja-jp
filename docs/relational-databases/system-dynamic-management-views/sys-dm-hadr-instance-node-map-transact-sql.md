---
description: dm_hadr_instance_node_map (Transact-sql)
title: dm_hadr_instance_node_map (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sys.dm_hadr_instance_node_map_TSQL
- sys.sys.dm_hadr_instance_node_map
- sys.dm_hadr_instance_node_map_TSQL
- sys.dm_hadr_instance_node_map
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC
- sys.sys.dm_hadr_instance_node_map dynamic management view
ms.assetid: ccfaf62c-9f87-43cf-a5e7-8942e91dd041
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 08d928613751650b4943604aa6caed52ccc26b85
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548493"
---
# <a name="sysdm_hadr_instance_node_map-transact-sql"></a>dm_hadr_instance_node_map (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Always On 可用性グループに参加している可用性レプリカをホストするのすべてのインスタンスについて [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、は、サーバーインスタンスをホストする Windows Server フェールオーバークラスター (WSFC) ノードの名前を返します。 この動的管理ビューには、次の用途があります。  
  
-   この動的管理ビューは、同一の WSFC ノードでホストされている複数の可用性レプリカを持つ可用性グループを検出するために役に立ちます。これはサポート外の構成であり、可用性グループが間違って構成されているときに FCI フェールオーバーが発生した場合にこの状態になることがあります。 詳細については、「[フェールオーバー クラスタリングと Always On 可用性グループ #40;SQL Server&#41;](../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)」を参照してください。  
  
-   複数の SQL Server インスタンスが同じ WSFC ノードでホストされている場合、リソース DLL はこの動的管理ビューを使用して、接続先ののインスタンスを決定し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
   
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**ag_resource_id**|**nvarchar (256)**|WSFC 内のリソースとしての可用性グループの一意の ID。|  
|**instance_name**|**nvarchar (256)**|名前-*サーバー* / *インスタンス*-可用性グループのレプリカをホストするサーバーインスタンス。|  
|**node_name**|**nvarchar (256)**|WSFC ノードの名前。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [Always On 可用性グループの動的管理ビューおよび関数 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [AlwaysOn 可用性グループのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Transact-sql&#41;&#40;可用性グループの監視 ](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性グループ &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
