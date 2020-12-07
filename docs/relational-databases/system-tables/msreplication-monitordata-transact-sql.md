---
description: MSreplication_monitordata (Transact-SQL)
title: MSreplication_monitordata (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSreplication_monitordata_TSQL
- MSreplication_monitordata
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_monitordata system table
ms.assetid: 843d3ffd-a1ef-4fd5-a744-c2252199793e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: dde16569f96619778a3a3cd6a246f58482b9947d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540891"
---
# <a name="msreplication_monitordata-transact-sql"></a>MSreplication_monitordata (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSreplication_monitordata**テーブルには、レプリケーションモニターによって使用されるキャッシュデータと、監視対象のサブスクリプションごとに1行のデータが含まれています。 このテーブルは、ディストリビューションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**lastrefresh**|**datetime**|モニターデータが更新された日付と時刻。|  
|**computetime**|**int**|モニターデータの計算に要した時間 (秒) です。|  
|**publication_id**|**int**|パブリケーション ID です。|  
|**publisher**|**sysname**|パブリッシャーの名前です。|  
|**publisher_srvid**|**int**|パブリッシャーのサーバー ID です。|  
|**publisher_db**|**sysname**|パブリケーションデータベースの名前です。|  
|**レプリケーション**|**sysname**|パブリケーションの名前を指定します。|  
|**publication_type**|**int**|パブリケーションの種類。次のいずれかの値を指定できます。<br /><br /> **0** = トランザクションパブリケーション<br /><br /> **1** = スナップショットパブリケーション<br /><br /> **2** = マージパブリケーション|  
|**agent_type**|**int**|レプリケーション エージェントの種類です。次のいずれかの値をとります。<br /><br /> **1** = スナップショットエージェント<br /><br /> **2** = ログリーダーエージェント<br /><br /> **3** = ディストリビューションエージェント<br /><br /> **4** = マージエージェント<br /><br /> **9** = キューリーダーエージェント|  
|**agent_id**|**int**|レプリケーションエージェントの ID です。|  
|**agent_name**|**sysname**|レプリケーションエージェントジョブの名前です。|  
|**job_id**|**uniqueidentifier**|レプリケーションエージェントジョブの GUID。|  
|**status**|**int**|レプリケーションエージェントの状態。次のいずれかの値を指定できます。<br /><br /> **1** = 開始<br /><br /> **2** = 成功<br /><br /> **3** = 実行中<br /><br /> **4** = アイドル<br /><br /> **5** = 再試行中<br /><br /> **6** = 失敗|  
|**isagentrunningnow**|**bit**|エージェントジョブが現在実行されているかどうかを示すフラグ。値 **1** は、ジョブが実行されていることを意味します。|  
|**warning**|**int**|サブスクリプションによって生成されるしきい値警告です。次の 1 つ以上の値の論理和演算をとります。<br /><br /> **1** = 有効期限-トランザクションパブリケーションへのサブスクリプションが、保有期間の割合として、許容されるしきい値を超える保有期間を超えました。<br /><br /> **2** = 待機時間-トランザクションパブリッシャーからサブスクライバーへのデータのレプリケートにかかった時間が、秒単位のしきい値を超えています。<br /><br /> **4** = mergeexpiration-マージパブリケーションに対するサブスクリプションが、保有期間の割合として許容されるしきい値を超える保有期間を超えました。 8 = mergefastrunduration。高速ネットワーク接続上で、マージ サブスクリプションの同期の完了にかかった時間が、秒単位のしきい値を超過しました。<br /><br /> **16** = mergeslowrunduration-低速またはダイヤルアップネットワーク接続を介して、マージサブスクリプションの同期の完了にかかった時間が、秒単位のしきい値を超えています。<br /><br /> **32** = mergefastrunspeed-高速ネットワーク接続上で、マージサブスクリプションの同期中の行の配信率が、1秒あたりの行数でのしきい値の比率を維持できませんでした。<br /><br /> **64** = mergeslowrunspeed-低速またはダイヤルアップネットワーク接続を介して、マージサブスクリプションの同期中の行の配信率が、1秒あたりの行数でしきい値を維持できませんでした。|  
|**last_distsync**|**datetime**|ディストリビューションエージェント実行された最後の日付と時刻。|  
|**agentstoptime**|**datetime**|エージェントが停止された日時です。|  
|**distdb**|**sysname**|サブスクリプションのディストリビューションデータベースの名前。|  
|**保有**|**int**|パブリケーションの保有期間です。|  
|**time_stamp**|**datetime**|内部使用のみ。|  
|**worst_latency**|**int**|トランザクションパブリケーションのログリーダーまたはディストリビューションエージェントによって反映されたデータ変更の待機時間の最大値 (秒単位)。|  
|**best_latency**|**int**|トランザクションパブリケーションのログリーダーまたはディストリビューションエージェントによって反映されたデータ変更の最小待機時間 (秒単位)。|  
|**avg_latency**|**int**|トランザクションパブリケーションのログリーダーまたはディストリビューションエージェントによって反映されたデータ変更の平均待機時間 (秒単位)。|  
|**cur_latency**|**int**|現在の実行中にログリーダーまたはディストリビューションエージェントによって反映されたデータ変更の待機時間 (秒単位)。|  
|**worst_runspeedPerf**|**int**|マージパブリケーションの最長同期時間|  
|**best_runspeedPerf**|**int**|マージパブリケーションの最短同期時間|  
|**average_runspeedPerf**|**int**|マージパブリケーションの平均同期時間|  
|**mergePerformance**|**int**|サブスクリプションに対するすべての同期と比較した前回の同期のパフォーマンスです。前回の同期の配信速度を前回までのすべての配信速度の平均で割った値に基づいて算出されます。|  
|**mergelatestsessionrunduration**|**int**|最後に実行されたマージエージェントの実行時間。|  
|**mergelatestsessionrunspeed**|**float(53)**|マージエージェント実行された最新の配信率です。|  
|**mergelatestsessionconnectiontype**|**int**|最新のマージエージェントセッションに使用される接続。次のいずれかの値を指定できます。<br /><br /> **1** = ローカルエリアネットワーク (LAN)<br /><br /> **2** = ダイヤルアップネットワーク接続|  
|**retention_period_unit**|**tinyint**|保有期間を定義するときに使用する単位を指定します。次のいずれかの値をとります。<br /><br /> **1** = 週<br /><br /> **2** = 月<br /><br /> **3** = 年|  
  
## <a name="see-also"></a>参照  
 [プログラムによるレプリケーションの監視](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)   
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーションビュー &#40;Transact-sql&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_replmonitorhelpsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelpsubscription-transact-sql.md)   
 [sp_replmonitorhelppublication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelppublication-transact-sql.md)   
 [sp_replmonitorhelppublisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelppublisher-transact-sql.md)   
 [sp_replmonitorhelpmergesession &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql.md)   
 [sp_replmonitorhelppublicationthresholds &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelppublicationthresholds-transact-sql.md)   
 [sp_replmonitorhelpmergesessiondetail &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql.md)  
  
  
