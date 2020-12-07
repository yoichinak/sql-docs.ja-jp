---
description: MSdistribution_agents (Transact-SQL)
title: MSdistribution_agents (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdistribution_agents_TSQL
- MSdistribution_agents
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistribution_agents system table
ms.assetid: 0e8f0653-1351-41d1-95d2-40f6d5a050ca
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f2433e5dcc96cc8b60adbc231a4f40e5a726dc62
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547159"
---
# <a name="msdistribution_agents-transact-sql"></a>MSdistribution_agents (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSdistribution_agents**テーブルには、ローカルディストリビューターで実行されているディストリビューションエージェントごとに1つの行が含まれています。 このテーブルは、ディストリビューションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ディストリビューションエージェントの ID。|  
|**name**|**nvarchar (100)**|ディストリビューションエージェントの名前。|  
|**publisher_database_id**|**int**|パブリッシャーデータベースの ID。|  
|**publisher_id**|**smallint**|パブリッシャーの ID。|  
|**publisher_db**|**sysname**|パブリッシャーデータベースの名前。|  
|**レプリケーション**|**sysname**|パブリケーションの名前を指定します。|  
|**subscriber_id**|**smallint**|既知のエージェントだけが使用するサブスクライバーの ID。 匿名のエージェントに対しては、予約済みとなります。|  
|**subscriber_db**|**sysname**|サブスクリプションデータベースの名前。|  
|**subscription_type**|**int**|サブスクリプションの種類。<br /><br /> **0** = プッシュ。<br /><br /> **1** = プル。<br /><br /> **2** = 匿名。|  
|**local_job**|**bit**|ローカルディストリビューターに SQL Server エージェントジョブがあるかどうかを示します。|  
|**job_id**|**binary(16)**|ジョブの識別番号を指定します。|  
|**subscription_guid**|**binary(16)**|エージェントのサブスクリプションの GUID 値。|  
|**profile_id**|**int**|[MSagent_profiles &#40;transact-sql&#41;](../../relational-databases/system-tables/msagent-profiles-transact-sql.md)テーブルの構成 ID。|  
|**anonymous_subid**|**uniqueidentifier**|匿名エージェントの ID。|  
|**subscriber_name**|**sysname**|匿名エージェントでのみ使用されるサブスクライバーの名前。|  
|**virtual_agent_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**anonymous_agent_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**creation_date**|**datetime**|分布またはマージエージェントが作成された日時。|  
|**queue_id**|**sysname**|キュー更新サブスクリプションのキューを検索する識別子。 キューに登録されていないサブスクリプションの場合、値は NULL になります。 [!INCLUDE[msCoName](../../includes/msconame-md.md)]メッセージキューベースのパブリケーションの場合、この値は、サブスクリプションに使用するキューを一意に識別する GUID です。 SQL Server ベースのキューパブリケーションの場合、列には **SQL**という値が含まれます。<br /><br /> 注: [!INCLUDE[msCoName](../../includes/msconame-md.md)] メッセージキューの使用は推奨されておらず、サポートされなくなりました。|  
|**queue_status**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**offload_enabled**|**bit**|エージェントをリモートからアクティブ化できるかどうかを示します。<br /><br /> **0** は、エージェントをリモートでアクティブ化できないことを示します。<br /><br /> **1** は、エージェントをリモートでアクティブにすること、および *offload_server* プロパティで指定されたリモートコンピューターで実行することを指定します。|  
|**offload_server**|**sysname**|リモートエージェントのアクティブ化に使用するサーバーのネットワーク名。|  
|**dts_package_name**|**sysname**|DTS パッケージの名前です。 たとえば、 **DTSPub_Package**という名前のパッケージの場合は、を指定し `@dts_package_name = N'DTSPub_Package'` ます。|  
|**dts_package_password**|**nvarchar (524)**|パッケージのパスワード。|  
|**dts_package_location**|**int**|パッケージの場所です。 パッケージの場所には、 **ディストリビューター** または **サブスクライバー**を指定できます。|  
|**sid**|**varbinary(85)**|最初の実行時の、ディストリビューション エージェントまたはマージ エージェントのセキュリティ識別番号 (SID) です。|  
|**queue_server**|**sysname**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**subscriber_security_mode**|**smallint**|サブスクライバーへの接続時にエージェントによって使用されるセキュリティモード。次のいずれかになります。<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server 認証<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 認証。|  
|**subscriber_login**|**sysname**|サブスクライバーへの接続時に使用されるログインです。|  
|**subscriber_password**|**nvarchar (524)**|サブスクライバーに接続するときに使用するパスワードの暗号化された値。|  
|**reset_partial_snapshot_progress**|**bit**|部分的にダウンロードされたスナップショットを破棄して、スナップショットプロセス全体を再び開始できるかどうかを指定します。|  
|**job_step_uid**|**uniqueidentifier**|エージェントを開始する SQL Server エージェントジョブステップの一意の ID。|  
|**subscriptionstreams**|**tinyint**|変更のバッチをサブスクライバーに並列的に適用するために、ディストリビューション エージェントごとに許可される接続の数を設定します。 サポートされている値の範囲は 1 ～ 64 です。|  
|**memory_optimized**|**bit**|1は、サブスクライバーがメモリ最適化テーブルに使用できることを示します。|  
|**job_login**|**sysname**||  
|**job_password**|**nvarchar (524)**||  
  
## <a name="see-also"></a>参照  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
