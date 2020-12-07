---
description: sys.dm_hadr_cluster (Transact-SQL)
title: dm_hadr_cluster (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 01/31/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_cluster
- dm_hadr_cluster_HADR
- sys.dm_hadr_cluster_TSQL
- dm_hadr_cluster
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_cluster catalog view
- Availability Groups [SQL Server], WSFC clusters
ms.assetid: 13ce70e4-9d43-4a80-a826-099e6213bf85
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b8bc19f3e73c00c2148cba2fb0381d73a36d6eb2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89533083"
---
# <a name="sysdm_hadr_cluster-transact-sql"></a>sys.dm_hadr_cluster (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  が有効になっているのインスタンスをホストする Windows Server フェールオーバークラスタリング (WSFC) ノードに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] wsfc クォーラムがある場合、dm_hadr_cluster は、クラスター名とクォーラムに関する情報を公開する行を返します **。** WSFC ノードにクォーラムがない場合、行は返されません。  
 > [!TIP]
 > 以降で [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] は、この動的管理ビューは Always On 可用性グループに加えて Always On フェールオーバークラスターインスタンスをサポートしています。

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**cluster_name**|**nvarchar(128)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に対応した [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] のインスタンスをホストする WSFC クラスターの名前。|  
|**quorum_type**|**tinyint**|この WSFC クラスターで使用されるクォーラムの種類。次のいずれかになります。<br /><br /> 0 = ノード マジョリティ。 このクォーラム構成では、ノードの半分 (切り上げ) から1を引いた数の障害に耐えることができます。 たとえば、7 つのノードから成るクラスターの場合、このクォーラム構成では 3 つのノードの障害に対する耐性があります。<br /><br /> 1 = ノードおよびディスク マジョリティ。 ディスク監視がオンラインのままの場合、このクォーラム構成では、クラスター内の半数のノード (切り上げ) の障害に耐えることができます。 たとえば、ディスク監視がオンラインの6ノードクラスターでは、3つのノード障害が発生する可能性があります。 ディスク監視がオフラインになった場合、または障害が発生した場合、このクォーラム構成では、ノードの半分 (切り上げ) から1を引いた障害に耐えることができます。 たとえば、障害が発生したディスク監視を使用する6ノードクラスターでは、2つ (3-1 = 2) のノード障害が発生する可能性があります。<br /><br /> 2 = ノードおよびファイル共有マジョリティ。 このクォーラム構成は "ノードおよびディスク マジョリティ" と同じように動作しますが、ディスク監視の代わりにファイル共有監視を使用します。<br /><br /> 3 = マジョリティなし: ディスクのみ。 クォーラムディスクがオンラインの場合、このクォーラム構成では、1つを除くすべてのノードの障害に耐えることができます。<br /><br /> 4 = 不明なクォーラム。 クラスターに不明なクォーラムがあります。<br /><br /> 5 = クラウド監視。 クラスターは、クォーラムの判別に Microsoft Azure を利用します。 クラウド監視が利用可能な場合、クラスターはノードの半分 (切り上げ) の障害に耐えることができます。|  
|**quorum_type_desc**|**varchar (50)**|**Quorum_type**の説明。次のいずれかになります。<br /><br /> NODE_MAJORITY<br /><br /> NODE_AND_DISK_MAJORITY<br /><br /> NODE_AND_FILE_SHARE_MAJORITY<br /><br /> NO_MAJORITY: _DISK_ONLY <br /><br /> UNKNOWN_QUORUM <br /><br /> CLOUD_WITNESS|  
|**quorum_state**|**tinyint**|WSFC クォーラムの状態。次のいずれかになります。<br /><br /> 0 = 不明なクォーラムの状態<br /><br /> 1 = 通常のクォーラム<br /><br /> 2 = 強制クォーラム|  
|**quorum_state_desc**|**varchar (50)**|**Quorum_state**の説明。次のいずれかになります。<br /><br /> UNKNOWN_QUORUM_STATE<br /><br /> NORMAL_QUORUM<br /><br /> FORCED_QUORUM|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [Always On 可用性グループの動的管理ビューおよび関数 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [AlwaysOn 可用性グループのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Transact-sql&#41;&#40;可用性グループの監視 ](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [sys.dm_hadr_cluster_members &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql.md)  
  
  
