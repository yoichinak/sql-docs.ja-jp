---
description: MSsubscription_agents (Transact-sql)
title: MSsubscription_agents (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsubscription_agents
- MSsubscription_agents_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscription_agents system table
ms.assetid: 86ad5891-0bef-4963-9381-7d5b45245a0c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e92e0e3476aa377577d00fca63a8348c47d09002
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540861"
---
# <a name="mssubscription_agents-transact-sql"></a>MSsubscription_agents (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSsubscription_agents**テーブルは、更新可能なサブスクリプションのディストリビューションエージェントおよびトリガーによって、サブスクリプションのプロパティを追跡するために使用されます。 このテーブルは、サブスクリプションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|行の ID。|  
|**publisher**|**sysname**|パブリッシャーの名前です。|  
|**publisher_db**|**sysname**|パブリケーションデータベースの名前です。|  
|**レプリケーション**|**sysname**|パブリケーションの名前を指定します。|  
|**subscription_type**|**int**|サブスクリプションのタイプです。<br /><br /> 0 = プッシュ。<br /><br /> 1 = プル<br /><br /> 2 = プル匿名。|  
|**queue_id**|**sysname**|[!INCLUDE[msCoName](../../includes/msconame-md.md)]パブリッシャーのメッセージキューの ID。 SQL ベースのキュー更新の場合、 *queue_id*は**sql**に設定されます。|  
|**update_mode**|**tinyint**|更新の種類。<br /><br /> **0** = 読み取り専用。<br /><br /> **1** = 即時更新。<br /><br /> **2** = メッセージキューを使用した更新がキューに登録されました。<br /><br /> **3** = メッセージキューを使用して、フェールオーバーとしてキュー更新を使用する即時更新。<br /><br /> **4** = SQL Server キューを使用したキュー更新。<br /><br /> **5** = キュー更新フェールオーバーを使用した即時更新。 SQL Server キューを使用します。|  
|**failover_mode**|**bit**|更新のフェールオーバー タイプが選択された場合、そのタイプは次のいずれかです。<br /><br /> **0** = 即時更新が使用されています。 フェールオーバーが有効になっていません。<br /><br /> **1** = キュー更新が使用されています。 フェールオーバーが有効になっています。 フェールオーバーに使用されるキューは、 *update_mode* 値に指定されます。|  
|**spid**|**int**|現在実行中または実行直後のディストリビューションエージェントによって使用される接続のシステムプロセス ID。|  
|**login_time**|**datetime**|現在実行中または実行直後のディストリビューションエージェント接続の日付と時刻。|  
|**allow_subscription_copy**|**bit**|サブスクリプションデータベースをコピーする機能が許可されるかどうかを指定します。|  
|**attach_state**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**attach_version**|**binary(16)**|アタッチされたサブスクリプションのバージョンを表す一意の識別子。|  
|**last_sync_status**|**int**|現在実行されている、または実行したばかりのディストリビューションエージェントの最終実行状態。 ステータスの値が示す内容は次のとおりです。<br /><br /> **1** = 開始しました。<br /><br /> **2** = 成功しました。<br /><br /> **3** = 実行中です。<br /><br /> **4** = アイドル状態。<br /><br /> **5** = 再試行します。<br /><br /> **6** = 失敗。|  
|**last_sync_summary**|**sysname**|現在実行中または実行直後のディストリビューションエージェントの最後のメッセージ。 ステータスの値が示す内容は次のとおりです。<br /><br /> **開始.**<br /><br /> **行わ.**<br /><br /> **進行中です。**<br /><br /> **退席.**<br /><br /> **再試行.**<br /><br /> **オーバー.**|  
|**last_sync_time**|**datetime**|*Last_sync_summary*列と*last_sync_status*列が更新された日付と時刻。 SqlServer エージェントサービスジョブとして実行されているプルまたは匿名ディストリビューションエージェントは、これらの列を更新しません。 この場合、履歴情報がジョブ履歴テーブルに代わりに記録されます。|  
|**queue_server**|**sysname**|内部使用のみです。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーションビュー &#40;Transact-sql&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helppullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)  
  
  
