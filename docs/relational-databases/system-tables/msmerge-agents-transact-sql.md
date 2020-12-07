---
description: MSmerge_agents (Transact-sql)
title: MSmerge_agents (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_agents
- MSmerge_agents_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_agents system table
ms.assetid: 639d2ebb-2c37-4fe0-b14b-1637bc5fc221
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0dd3ef69b380122d173436e19ae42ed3227b30e5
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545696"
---
# <a name="msmerge_agents-transact-sql"></a>MSmerge_agents (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_agents**テーブルには、サブスクライバーで実行されているマージエージェントごとに1つの行が含まれています。 このテーブルは、ディストリビューションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|マージエージェントの ID。|  
|**name**|**nvarchar (100)**|マージエージェントの名前。|  
|**publisher_id**|**smallint**|パブリッシャーの ID。|  
|**publisher_db**|**sysname**|パブリッシャーデータベースの名前。|  
|**レプリケーション**|**sysname**|パブリケーションの名前を指定します。|  
|**subscriber_id**|**smallint**|サブスクライバーの ID です。|  
|**subscriber_db**|**sysname**|サブスクリプションデータベースの名前。|  
|**local_job**|**bit**|ローカル ディストリビューターに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブがあるかどうかを示します。|  
|**job_id**|**binary(16)**|ジョブの識別番号を指定します。|  
|**profile_id**|**int**|**MSagent_profiles**テーブルの構成 ID。|  
|**anonymous_subid**|**uniqueidentifier**|匿名エージェントの ID。|  
|**subscriber_name**|**sysname**|サブスクライバーの名前です。|  
|**creation_date**|**datetime**|分布またはマージエージェントが作成された日付と時刻。|  
|**offload_enabled**|**bit**|エージェントをリモートでアクティブ化できることを指定します。<br /><br /> **0** を指定すると、エージェントをリモートでアクティブにすることはできません。<br /><br /> **1** は、エージェントをリモートでアクティブにし、offload_server プロパティで指定されたリモートコンピューターでアクティブにすることを指定します。|  
|**offload_server**|**sysname**|リモートエージェントのアクティブ化に使用するサーバーのネットワーク名を指定します。|  
|**sid**|**varbinary(85)**|最初の実行時の、ディストリビューション エージェントまたはマージ エージェントのセキュリティ識別番号 (SID) です。|  
|**subscriber_security_mode**|**smallint**|サブスクライバーへの接続時にエージェントによって使用されるセキュリティモード。次のいずれかになります。<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証。<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 認証。|  
|**subscriber_login**|**sysname**|サブスクライバーへの接続時に使用されるログインです。|  
|**subscriber_password**|**nvarchar (524)**|サブスクライバーへの接続時に使用されるパスワードの暗号化された値です。|  
|**publisher_security_mode**|**smallint**|パブリッシャーに接続するときにエージェントによって使用されるセキュリティモード。次のいずれかになります。<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証。<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 認証。|  
|**publisher_login**|**sysname**|パブリッシャーに接続するときに使用されるログインです。|  
|**publisher_password**|**nvarchar (524)**|パブリッシャーに接続するときに使用されるパスワードの暗号化された値。|  
|**job_step_uid**|**uniqueidentifier**|エージェントが起動される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブ ステップの一意な ID|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
