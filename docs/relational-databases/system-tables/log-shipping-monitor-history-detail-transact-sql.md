---
description: log_shipping_monitor_history_detail (Transact-SQL)
title: log_shipping_monitor_history_detail (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_monitor_history_detail_TSQL
- log_shipping_monitor_history_detail
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_monitor_history_detail system table
ms.assetid: 7080c888-323b-4206-a1ab-e6c51f9e2579
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 515a2b38f10beca9c4797ce02d48387bfa662707
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544553"
---
# <a name="log_shipping_monitor_history_detail-transact-sql"></a>log_shipping_monitor_history_detail (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ログ配布ジョブの履歴の詳細を格納します。 このテーブルは、 **msdb** データベースに格納されます。  
  
 履歴と監視に関連するテーブルは、プライマリサーバーとセカンダリサーバーでも使用されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**agent_id**|**uniqueidentifier**|バックアップ用のプライマリ ID、またはコピーまたは復元用のセカンダリ ID。|  
|**agent_type**|**tinyint**|ログ配布ジョブの種類です。<br /><br /> 0 = バックアップ。<br /><br /> 1 = コピー。<br /><br /> 2 = 復元します。|  
|**session_id**|**int**|バックアップ/コピー/復元/ジョブのセッション ID。|  
|**database_name**|**sysname**|このレコードに関連付けられているデータベースの名前。 バックアップ用のプライマリデータベース、復元用のセカンダリデータベース、またはコピー用に空。|  
|**session_status**|**tinyint**|セッションの状態。<br /><br /> 0 = 開始<br /><br /> 1 = 実行中。<br /><br /> 2 = 成功。<br /><br /> 3 = エラー。<br /><br /> 4 = 警告|  
|**log_time**|**datetime**|レコードが作成された日時。|  
|**log_time_utc**|**datetime**|レコードが作成された日付と時刻。協定世界時で表されます。|  
|**message**|**nvarchar(max)**|メッセージ テキスト。|  
  
## <a name="remarks"></a>解説  
 このテーブルには、ログ配布エージェントの履歴の詳細が含まれています。 エージェントセッションを識別するには、列 **agent_id**、 **agent_type**、および **session_id**を使用します。 エージェントセッションの履歴の詳細を表示するには、 **log_time**で並べ替えます。  
  
 リモート監視サーバーに格納されているだけでなく、プライマリサーバーに関連する情報が **log_shipping_monitor_history_detail** テーブルのプライマリサーバーに格納されます。また、セカンダリサーバーに関連する情報は、セカンダリサーバーの **log_shipping_monitor_history_detail** テーブルにも格納されます。  
  
## <a name="see-also"></a>参照  
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_delete_log_shipping_primary_database &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [sp_cleanup_log_shipping_history &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md)   
 [sp_refresh_log_shipping_monitor &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [sp_delete_log_shipping_secondary_database &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [システムテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)   
 [log_shipping_monitor_error_detail &#40;Transact-sql&#41;](../../relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql.md)  
  
  
