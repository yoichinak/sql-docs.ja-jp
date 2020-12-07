---
description: sys.dm_hadr_availability_replica_states (Transact-SQL)
title: dm_hadr_availability_replica_states (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_hadr_availability_replica_states
- sys.dm_hadr_availability_replica_states_TSQL
- sys.dm_hadr_availability_replica_states
- dm_hadr_availability_replica_states_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_availability_replica_states dynamic management view
ms.assetid: d2e678bb-51e8-4a61-b223-5c0b8d08b8b1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 347d05c0bfc37b1c14fddb728df5508e062cb13d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546563"
---
# <a name="sysdm_hadr_availability_replica_states-transact-sql"></a>sys.dm_hadr_availability_replica_states (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ローカル レプリカごとに 1 行のデータと、ローカル レプリカと同じ AlwaysOn 可用性グループに含まれるリモート レプリカごとに 1 行のデータを返します。 各行には、特定のレプリカの状態に関する情報が含まれています。  
  
> [!IMPORTANT]  
>  特定の可用性グループ内のすべてのレプリカに関する情報を取得するには、プライマリレプリカをホストしているサーバーインスタンスの dm_hadr_availability_replica_states をクエリし **ます** 。 可用性グループのセカンダリ レプリカをホストしているサーバー インスタンスに対してクエリを実行した場合、この動的管理ビューはその可用性グループのローカル情報のみを返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|レプリカの一意識別子。|  
|**group_id**|**uniqueidentifier**|可用性グループの一意識別子。|  
|**is_local**|**bit**|レプリカがローカルであるかどうか。次のいずれかになります。<br /><br /> 0 = ローカルサーバーインスタンスによってホストされるプライマリレプリカを持つ可用性グループ内のリモートセカンダリレプリカを示します。 この値は、プライマリレプリカの場所でのみ発生します。<br /><br /> 1 = ローカルレプリカを示します。 セカンダリ レプリカの場合、これはそのレプリカが属する可用性グループに対して使用できる唯一の値です。|  
|**role**|**tinyint**|[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]ローカルレプリカまたは接続されているリモートレプリカの現在のロール。次のいずれかになります。<br /><br /> 0 = 解決中<br /><br /> 1 = プライマリ<br /><br /> 2 = セカンダリ<br /><br /> [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] のロールについては、「[Always On 可用性グループの概要 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)」を参照してください。|  
|**role_desc**|**nvarchar(60)**|**ロール**の説明。次のいずれかになります。<br /><br /> 修復<br /><br /> PRIMARY<br /><br /> SECONDARY|  
|**operational_state**|**tinyint**|レプリカの現在の操作状態。次のいずれかになります。<br /><br /> 0 = フェールオーバー保留中<br /><br /> 1 = 保留中<br /><br /> 2 = オンライン<br /><br /> 3 = オフライン<br /><br /> 4 = 失敗<br /><br /> 5 = 失敗、クォーラムなし<br /><br /> NULL = レプリカがローカルでない<br /><br /> 詳細については、このトピックの「 [役割と操作状態](#RolesAndOperationalStates)」を参照してください。|  
|**動作 \_ 状態の説明 \_**|**nvarchar(60)**|**動作 \_ 状態**の説明。次のいずれかになります。<br /><br /> PENDING_FAILOVER<br /><br /> PENDING<br /><br /> ONLINE<br /><br /> OFFLINE<br /><br /> FAILED<br /><br /> FAILED_NO_QUORUM<br /><br /> NULL|  
|**回復の \_ 正常性**|**tinyint**|[Dm_hadr_database_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)動的管理ビューの [**データベースの \_ 状態**] 列のロールアップ。 使用可能な値とその説明を次に示します。<br /><br /> 0: 処理中です。  少なくとも1つの結合されたデータベースのデータベース状態がオンライン以外です (**データベースの \_ 状態** が0ではありません)。<br /><br /> 1: オンライン。 すべての結合されたデータベースのデータベースの状態がオンラインになっています (**database_state** は0です)。<br /><br /> NULL: **is_local** = 0|  
|**recovery_health_desc**|**nvarchar(60)**|**Recovery_health**の説明。次のいずれかになります。<br /><br /> ONLINE_IN_PROGRESS<br /><br /> ONLINE<br /><br /> NULL|  
|**同期の \_ 正常性**|**tinyint**|すべての参加している可用性データベース (*レプリカ*とも呼ばれます) とレプリカの可用性モード (同期コミットモードまたは非同期コミットモード) のデータベース同期状態 (**synchronization_state**) のロールアップを反映します。 ロールアップには、レプリカ上のデータベースに対する正常な累積状態が反映されます。 使用可能な値とその説明を次に示します。<br /><br /> 0: 異常です。   少なくとも1つの結合されたデータベースが未同期状態です。<br /><br /> 1: 部分的に正常です。 一部のレプリカが目標の同期状態ではありません: 同期コミット レプリカは SYNCHRONIZED である必要があり、非同期コミット レプリカは SYNCHRONIZING である必要があります。<br /><br /> 2: 正常。 すべてのレプリカが目標の同期状態です。同期コミットレプリカは同期され、非同期コミットレプリカは同期されています。|  
|**synchronization_health_desc**|**nvarchar(60)**|**Synchronization_health**の説明。次のいずれかになります。<br /><br /> NOT_HEALTHY<br /><br /> PARTIALLY_HEALTHY<br /><br /> 戻ら|  
|**connected_state**|**tinyint**|セカンダリレプリカが現在プライマリレプリカに接続されているかどうか。 次に、使用可能な値とその説明を示します。<br /><br /> 0: 切断されました。 切断された状態への可用性レプリカの応答は、そのロールによって異なります。プライマリレプリカでは、セカンダリレプリカが切断された場合、プライマリレプリカでセカンダリデータベースが同期されていないとマークされ、セカンダリが再接続するのを待機します。セカンダリレプリカでは、切断されていることを検出すると、セカンダリレプリカはプライマリレプリカへの再接続を試みます。<br /><br /> 1: 接続されています。<br /><br /> 各プライマリ レプリカでは、同じ可用性グループに含まれるすべてのセカンダリ レプリカの接続状態を追跡します。 セカンダリ レプリカでは、プライマリ レプリカの接続状態のみを追跡します。|  
|**connected_state_desc**|**nvarchar(60)**|**Connection_state**の説明。次のいずれかになります。<br /><br /> DISCONNECTED<br /><br /> CONNECTED|  
|**last_connect_error_number**|**int**|最後の接続エラーの番号。|  
|**last_connect_error_description**|**nvarchar(1024)**|**Last_connect_error_number**メッセージのテキスト。|  
|**last_connect_error_timestamp**|**datetime**|**Last_connect_error_number**エラーが発生した日時を示す日付と時刻のタイムスタンプ。|  
  
##  <a name="roles-and-operational-states"></a><a name="RolesAndOperationalStates"></a> 役割と操作状態  
 ロール ( **ロール**) は、特定の可用性レプリカの状態と、動作状態 ( **operational_state**) を反映します。これは、レプリカが可用性レプリカのすべてのデータベースに対するクライアント要求を処理する準備ができているかどうかを示します。 各ロールで実行できる操作状態の概要を次に示します。解決、プライマリ、およびセカンダリです。  
  
 **解決中:** 可用性レプリカが解決中のロールに含まれる場合、次の表に示す操作状態が考えられます。  
  
|動作状態|説明|  
|-----------------------|-----------------|  
|PENDING_FAILOVER|可用性グループに対するフェールオーバー コマンドを処理しています。|  
|OFFLINE|WSFC クラスターおよびローカル メタデータ内の可用性レプリカのすべての構成データが更新されたが、可用性グループには現在プライマリ レプリカがありません。|  
|FAILED|WSFC クラスターから情報を取得しようとしているときに、読み取りエラーが発生しました。|  
|FAILED_NO_QUORUM|ローカルの WSFC ノードに、クォーラムがありません。 これは、推定された状態です。|  
  
 **プライマリ:** 可用性レプリカがプライマリロールを実行している場合は、現在プライマリレプリカです。 次の表に、可能な操作状態を示します。  
  
|動作状態|説明|  
|-----------------------|-----------------|  
|PENDING|これは一時的な状態ですが、ワーカーを使用して要求を処理できない場合、プライマリ レプリカがこの状態になることがあります。|  
|ONLINE|可用性グループリソースがオンラインで、すべてのデータベースワーカースレッドが取得されました。|  
|FAILED|可用性レプリカは、WSFC クラスターに対して読み取りまたは書き込みを行うことができません。|  
  
 **セカンダリ:** セカンダリロールを実行している可用性レプリカは、現在セカンダリレプリカです。 次の表に、可能な操作状態を示します。  
  
|動作状態|説明|  
|-----------------------|-----------------|  
|ONLINE|ローカル セカンダリ レプリカがプライマリ レプリカに接続されています。|  
|FAILED|ローカル セカンダリ レプリカが WSFC クラスターに対して読み取りまたは書き込みを行うことができません。|  
|NULL|プライマリ レプリカでは、行がセカンダリ レプリカに関係する場合に、この値が返されます。|  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [可用性グループの監視 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
