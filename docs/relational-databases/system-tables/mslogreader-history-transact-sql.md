---
description: MSlogreader_history (Transact-SQL)
title: MSlogreader_history (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSlogreader_history_TSQL
- MSlogreader_history
dev_langs:
- TSQL
helpviewer_keywords:
- MSlogreader_history system table
ms.assetid: 2e399fa1-3591-4c1c-96b7-7964fe82c7c4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ae2abdcaf4014df405ebf6dcefff8e2207530a93
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545741"
---
# <a name="mslogreader_history-transact-sql"></a>MSlogreader_history (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSlogreader_history**テーブルには、ローカルディストリビューターに関連付けられているログリーダーエージェントの履歴行が含まれています。 このテーブルは、ディストリビューションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|ログリーダーエージェントの ID。|  
|**runstatus**|**int**|実行ステータスです。<br /><br /> 1 = 開始します。<br /><br /> 2 = 成功します。<br /><br /> 3 = 実行中<br /><br /> 4 = アイドル状態。<br /><br /> 5 = 再試行<br /><br /> 6 = 失敗|  
|**start_time**|**datetime**|ジョブの実行開始時刻です。|  
|**time**|**datetime**|メッセージがログに記録される時刻。|  
|**duration**|**int**|メッセージ セッションの実行時間 (秒) です。|  
|**コメント**|**nvarchar (255)**|メッセージ テキスト。|  
|**xact_seqno**|**varbinary(16)**|最後に処理されたトランザクション シーケンス番号です。|  
|**delivery_time**|**int**|最初のトランザクションが配信された時刻。|  
|**delivered_transactions**|**int**|セッションで配信されたトランザクションの合計数。|  
|**delivered_commands**|**int**|セッションで配信されたコマンドの合計数。|  
|**average_commands**|**int**|セッションで配信されたコマンドの平均数。|  
|**delivery_rate**|**float**|1秒間に配信された平均コマンド。|  
|**delivery_latency**|**int**|コマンドがパブリッシュされたデータベースに入ってからディストリビューションデータベースに入ってくるまでの待機時間。 単位はミリ秒。|  
|**error_id**|**int**|**MSrepl_error**システムテーブル内のエラーの ID。|  
|**timestamp**|**timestamp**|このテーブルのタイムスタンプ列です。|  
|**updateable_row**|**bit**|履歴行を上書きできる場合は、 **1** に設定します。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
