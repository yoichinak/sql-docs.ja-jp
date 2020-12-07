---
description: sys.dm_hadr_cluster_members (Transact-SQL)
title: dm_hadr_cluster_members (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 01/31/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_cluster_members_TSQL
- sys.dm_hadr_cluster_members
- dm_hadr_cluster_members_TSQL
- dm_hadr_cluster_members
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.dm_hadr_cluster_members catalog view
ms.assetid: feb20b3a-8835-41d3-9a1c-91d3117bc170
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9c7e182c4b8efb2ecc882c0e81bb1c1863b310a1
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546572"
---
# <a name="sysdm_hadr_cluster_members-transact-sql"></a>sys.dm_hadr_cluster_members (Transact-SQL)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  が有効になっているのローカルインスタンスをホストする WSFC ノードに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] wsfc クォーラムがある場合、はクォーラムを構成するメンバーごとに1行の値を返し、それぞれの状態を返します。 これには、クラスター内のすべてのノード ( **Clusterenum** 関数によって CLUSTER_ENUM_NODE の種類で返されます) とディスクまたはファイル共有監視 (存在する場合) が含まれます。 特定のメンバーに対して返される行には、そのメンバーの状態に関する情報が含まれています。 たとえば、1つのノードがダウンしているノードが5つあるノードクラスターの場合、クォーラムを持つノード上に存在するが有効になっているサーバーインスタンスから **sys. dm_hadr_cluster_members** を照会すると、dm_hadr_cluster_members には、 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] ダウンノードの状態が "NODE_DOWN" として反映され **ます** 。  
  
 WSFC ノードにクォーラムが存在しない場合、行は返されません。  
  
 次の事項を確認するには、この動的管理ビューを使用します。  
  
-   WSFC クラスターで現在実行されているノード  
  
-   マジョリティ ノードのクォーラムが失われるまでに、WSFC クラスターがあと何回の障害に耐えられるか。  

 > [!TIP]
 > 以降で [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] は、この動的管理ビューは Always On 可用性グループに加えて Always On フェールオーバークラスターインスタンスをサポートしています。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**member_name**|**nvarchar(128)**|メンバー名。コンピューター名、ドライブ文字、ファイル共有パスのいずれかになります。|  
|**member_type**|**tinyint**|メンバーの種類。次のいずれかになります。<br /><br /> 0 = WSFC ノード<br /><br /> 1 = ディスク監視<br /><br /> 2 = ファイル共有監視<br /><br /> 3 = クラウド監視|  
|**member_type_desc**|**nvarchar (50)**|**Member_type**の説明。次のいずれかになります。<br /><br /> CLUSTER_NODE<br /><br /> DISK_WITNESS<br /><br /> FILE_SHARE_WITNESS<br /><br /> CLOUD_WITNESS|  
|**member_state**|**tinyint**|メンバーの状態。次のいずれかになります。<br /><br /> 0 = オフライン<br /><br /> 1 = オンライン|  
|**member_state_desc**|**nvarchar(60)**|**Member_state**の説明。次のいずれかになります。<br /><br /> UP<br /><br /> DOWN|  
|**number_of_quorum_votes**|**tinyint**|このクォーラム メンバーが保有するクォーラムの投票数。 マジョリティなし: ディスクのみのクォーラムの場合、この値は既定で0に設定されます。 その他のクォーラムの種類の場合、この値は既定で 1 になります。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="examples"></a>例  
  
## <a name="see-also"></a>参照  
 [Always On 可用性グループの動的管理ビューおよび関数 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [AlwaysOn 可用性グループのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Transact-sql&#41;&#40;可用性グループの監視 ](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性グループ &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
