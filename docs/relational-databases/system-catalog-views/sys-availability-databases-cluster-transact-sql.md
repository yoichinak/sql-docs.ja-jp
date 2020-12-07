---
description: availability_databases_cluster (Transact-sql)
title: availability_databases_cluster (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.availability_databases_cluster_TSQL
- sys.availability_databases_cluster
- availability_databases_cluster_TSQL
- availability_databases_cluster
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.availability_databases_cluster catalog view
- Availability Groups [SQL Server], databases
ms.assetid: 8d9c57e5-7f39-4315-b466-92748231140a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3d600d524c5bee67113c98065989b0706acbd0f4
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551505"
---
# <a name="sysavailability_databases_cluster-transact-sql"></a>availability_databases_cluster (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ローカルコピーデータベースが可用性グループにまだ参加しているかどうかに関係なく、Windows Server フェールオーバークラスタリング (WSFC) クラスター内の任意の Always On 可用性グループの可用性レプリカをホストしているのインスタンス上の可用性データベースごとに1行のデータを格納します。  
  
> [!NOTE]  
>  データベースを可用性グループに追加すると、プライマリ データベースは自動的にそのグループに参加します。 セカンダリ データベースを可用性グループに参加させるには、各セカンダリ レプリカでそのデータベースを準備する必要があります。   
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|可用性グループが存在する場合、データベースが参加している可用性グループの一意識別子。<br /><br /> NULL = データベースは可用性グループの可用性レプリカの一部ではありません。|  
|**group_database_id**|**uniqueidentifier**|データベースが参加している可用性グループ内のデータベースの一意の識別子 (存在する場合)。 **group_database_id** は、プライマリレプリカのこのデータベースと、データベースが可用性グループに参加しているすべてのセカンダリレプリカで同じです。<br /><br /> NULL = データベースは、どの可用性グループの可用性レプリカの一部でもありません。|  
|**database_name**|**sysname**|可用性グループに追加されたデータベースの名前。|  
  
## <a name="permissions"></a>アクセス許可  
 **Availability_databases_cluster**の呼び出し元がデータベースの所有者でない場合、対応する行を表示するために必要な最小限の権限は、ALTER any database または VIEW any database のサーバーレベルの権限、または**MASTER**データベースの CREATE database 権限です。  
  
## <a name="see-also"></a>参照  
 [sys.availability_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [dm_hadr_database_replica_states &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)   
 [dm_hadr_database_replica_cluster_states &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md)   
 [Always On 可用性グループの概要 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
