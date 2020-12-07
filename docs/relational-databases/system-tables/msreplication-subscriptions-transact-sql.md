---
description: MSreplication_subscriptions (Transact-SQL)
title: MSreplication_subscriptions (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSreplication_subscriptions
- MSreplication_subscriptions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_subscriptions system table
ms.assetid: fd0c5843-4e9b-4448-8bfb-0a4067d1d8d1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b89aee32b5ea431da77043938104960d4d353b74
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551034"
---
# <a name="msreplication_subscriptions-transact-sql"></a>MSreplication_subscriptions (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSreplication_subscriptions**テーブルには、ローカルサブスクライバーデータベースにサービスを提供している各ディストリビューションエージェントについて、1行のレプリケーション情報が含まれています。 このテーブルは、サブスクリプションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|パブリッシャーの名前です。|  
|**publisher_db**|**sysname**|パブリッシャーデータベースの名前。|  
|**レプリケーション**|**sysname**|パブリケーションの名前を指定します。|  
|**independent_agent**|**bit**|このパブリケーションに対してスタンドアロンのディストリビューションエージェントがあるかどうかを示します。|  
|**subscription_type**|**int**|サブスクリプションの種類。<br /><br /> 0 = プッシュ。<br /><br /> 1 = プル<br /><br /> 2 = 匿名。|  
|**distribution_agent**|**sysname**|ディストリビューションエージェントの名前。|  
|**Time**|**smalldatetime**|ディストリビューションエージェントによって最後に更新された時刻。|  
|**description**|**nvarchar (255)**|サブスクリプションの説明。|  
|**transaction_timestamp**|**varbinary(16)**|内部使用のみ。|  
|**update_mode**|**tinyint**|更新の種類。|  
|**agent_id**|**binary(16)**|エージェントの ID。|  
|**subscription_guid**|**binary(16)**|パブリケーションにおけるサブスクリプションのバージョンを表すグローバル識別子。|  
|**subid**|**binary(16)**|匿名サブスクリプションのグローバル識別子。|  
|**immediate_sync**|**bit**|スナップショットエージェントが実行されるたびに同期ファイルが作成または再作成されるかどうかを示します。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーションビュー &#40;Transact-sql&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
