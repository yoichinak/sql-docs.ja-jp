---
description: MSsubscriber_schedule (Transact-sql)
title: MSsubscriber_schedule (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsubscriber_schedule
- MSsubscriber_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscriber_schedule system table
ms.assetid: ff428306-0ef4-49a3-b536-07ccdf6e2196
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6f65d855a118031fd34bcf69257a90bca6e41933
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540897"
---
# <a name="mssubscriber_schedule-transact-sql"></a>MSsubscriber_schedule (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSsubscriber_schedule**テーブルには、パブリッシャーとサブスクライバーのペアごとに、既定のマージおよびトランザクション同期のスケジュールが含まれています。 このテーブルは、ディストリビューションデータベースに格納されます。  
  
> [!NOTE]
>  このシステムテーブルは非推奨とされており、以前のバージョンのをサポートするために保持されてい [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|パブリッシャーの名前です。|  
|**サブスクライバ**|**sysname**|サブスクライバーの名前です。|  
|**agent_type**|**smallint**|エージェントの種類。<br /><br /> 0 = ディストリビューション エージェント<br /><br /> 1 = マージエージェント。|  
|**frequency_type**|**int**|ディストリビューションエージェントのスケジュールを設定する頻度。<br /><br /> **1** = 1 回。<br /><br /> **2** = 要求時。<br /><br /> **4** = 毎日。<br /><br /> **8** = 週単位。<br /><br /> **16** = 月単位。<br /><br /> **32** = 毎月の相対。<br /><br /> **64** = 自動開始。<br /><br /> **128** = 定期的。|  
|**frequency_interval**|**int**|**Frequency_type**によって設定された頻度に適用する値。|  
|**frequency_relative_interval**|**int**|ディストリビューション エージェントの日付。<br /><br /> **1** = 最初。<br /><br /> **2** = 秒。<br /><br /> **4** = 3 番目。<br /><br /> **8** = 4 番目。<br /><br /> **16** = 最後。|  
|**frequency_recurrence_factor**|**int**|**Frequency_type**によって使用される繰り返し係数。|  
|**frequency_subday**|**int**|定義した期間にスケジュールを組み直す頻度。<br /><br /> **1** = 1 回。<br /><br /> **2** = 秒。<br /><br /> **4** = 分。<br /><br /> **8** = 時間。|  
|**frequency_subday_interval**|**int**|**Frequency_subday**の間隔。|  
|**active_start_time_of_day**|**int**|ディストリビューションエージェントを最初にスケジュール設定する時刻を HHMMSS 形式で指定します。|  
|**active_end_time_of_day**|**int**|ディストリビューション エージェントのスケジュールの終了時刻。HHMMSS の形式で表されます。|  
|**active_start_date**|**int**|ディストリビューション エージェントのスケジュールの開始日。YYYYMMDD の形式で表されます。|  
|**active_end_date**|**int**|ディストリビューションエージェントのスケジュール設定を停止する日付。形式は YYYYMMDD です。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
