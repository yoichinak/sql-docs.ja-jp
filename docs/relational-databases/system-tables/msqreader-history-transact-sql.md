---
description: MSqreader_history (Transact-sql)
title: MSqreader_history (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- MSqreader_history
- MSqreader_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSqreader_history system table
ms.assetid: c5c91d39-513c-4a77-870b-c8ef74a1cd6b
author: cawrites
ms.author: chadam
ms.openlocfilehash: 7c158b9c035f14f7904a828c7a3628494096ddb2
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99182602"
---
# <a name="msqreader_history-transact-sql"></a>MSqreader_history (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSqreader_history** テーブルには、ローカルディストリビューターに関連付けられているキューリーダーエージェントの履歴行が含まれています。 このテーブルは、ディストリビューションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|キュー リーダー エージェントの ID|  
|**publication_id**|**int**|パブリケーションの ID です。|  
|**runstatus**|**int**|エージェントの実行状態。<br /><br /> **1** = 開始します。<br /><br /> **2** = 成功します。<br /><br /> **3** = 実行中です。<br /><br /> **4** = アイドル状態。<br /><br /> **5** = 再試行します。<br /><br /> **6** = 失敗。|  
|**start_time**|**datetime**|エージェントセッションが開始された日付と時刻。|  
|**time**|**datetime**|最後にメッセージがログに記録された日時。|  
|**duration**|**int**|ログに記録されたセッションのアクティビティの経過時間 (秒単位)。|  
|**コメント**|**nvarchar (255)**|説明のテキスト。|  
|**transaction_id**|**nvarchar(40)**|メッセージと共に格納されるトランザクション ID (該当する場合)。|  
|**transaction_status**|**int**|トランザクションの状態。|  
|**transactions_processed**|**int**|セッションで処理されたトランザクションの累積数。|  
|**commands_processed**|**int**|セッション中に処理されたコマンド数の累計。|  
|**delivery_rate**|**float(53)**|1秒間に配信されたコマンドの平均数。|  
|**transaction_rate**|**float(53)**|処理されたトランザクションの比率。|  
|**サブスクライバ**|**sysname**|サブスクライバーの名前です。|  
|**subscriberdb**|**sysname**|サブスクリプションデータベースの名前。|  
|**error_id**|**int**|0以外の値を指定すると、エラーメッセージが表示され [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。|  
|**timestamp**|**timestamp**|テーブルの timestamp 列。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
