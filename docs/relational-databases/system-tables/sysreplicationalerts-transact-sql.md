---
description: sysreplicationalerts (Transact-SQL)
title: sysreplicationalerts (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysreplicationalerts_TSQL
- sysreplicationalerts
dev_langs:
- TSQL
helpviewer_keywords:
- sysreplicationalerts system table
ms.assetid: 6ed15828-8cca-4cf0-b2ff-1ecd0d8db11a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cce33fa91f6ea11cda33e622edd39ec764b2c2ce
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537820"
---
# <a name="sysreplicationalerts-transact-sql"></a>sysreplicationalerts (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  レプリケーションの警告が発生する原因となった条件に関する情報が含まれます。 このテーブルは、 **msdb** データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**alert_id**|**int**|警告の ID。|  
|**status**|**int**|ユーザー定義の値です。<br /><br /> **0** = サービス解除。<br /><br /> **1** = サービス。|  
|**agent_type**|**int**|エージェントのタイプです。<br /><br /> **1** = スナップショットエージェント。<br /><br /> **2** = ログリーダーエージェント。<br /><br /> **3** = ディストリビューションエージェント。<br /><br /> **4** = マージエージェント。|  
|**agent_id**|**int**|テーブル **MSsnapshot_agents**、 **MSlogreader_agents**、 **MSdistribution_agents**、または **MSmerge_agents**のエージェント ID。|  
|**error_id**|**int**|**MSrepl_errors**に格納されているエラーの ID。|  
|**alert_error_code**|**int**|このレコードをログに記録するときに発生する警告のメッセージ ID。|  
|**time**|**datetime**|レコードが挿入された時刻。|  
|**publisher**|**sysname**|この警告を発生したエージェントに関係するパブリッシャー名です。|  
|**publisher_db**|**sysname**|この警告を発生したエージェントに関連付けられているパブリッシャーデータベース。|  
|**レプリケーション**|**sysname**|この警告を発生したエージェントに関係するパブリケーションです。|  
|**publication_type**|**int**|パブリケーションの種類です。<br /><br /> **0** = スナップショット。<br /><br /> **1** = トランザクション。<br /><br /> **2** = Merge。|  
|**サブスクライバ**|**sysname**|この警告を発生したエージェントに関連付けられているサブスクライバーの名前。|  
|**subscriber_db**|**sysname**|この警告を発生したエージェントに関連付けられているサブスクライバーデータベースの名前。|  
|**記事**|**sysname**|この警告を発生したエージェントに関連付けられているアーティクルの名前。|  
|**destination_object**|**sysname**|警告に関連付けられているサブスクリプションテーブルの名前。|  
|**source_object**|**sysname**|警告に関連付けられているパブリッシュ済みテーブルの名前。|  
|**alert_error_text**|**ntext**|警告のテキスト。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
