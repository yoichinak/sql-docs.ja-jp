---
description: log_shipping_monitor_error_detail (Transact-SQL)
title: log_shipping_monitor_error_detail (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_monitor_error_detail_TSQL
- log_shipping_monitor_error_detail
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_monitor_error_detail system table
ms.assetid: 0c38a625-60d2-4ee2-bcf3-2ba367914220
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0f606f93697308a690451583267a5d77383fa723
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547187"
---
# <a name="log_shipping_monitor_error_detail-transact-sql"></a>log_shipping_monitor_error_detail (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ログ配布ジョブのエラーの詳細を格納します。 このテーブルは、 **msdb** データベースに格納されます。  
  
 履歴と監視に関連するテーブルは、プライマリサーバーとセカンダリサーバーでも使用されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**agent_id**|**uniqueidentifier**|バックアップ用のプライマリ ID、またはコピーまたは復元用のセカンダリ ID。|  
|**agent_type**|**tinyint**|ログ配布ジョブの種類です。<br /><br /> 0 = バックアップ。<br /><br /> 1 = コピー。<br /><br /> 2 = 復元します。|  
|**session_id**|**int**|バックアップ/コピー/復元/ジョブのセッション ID。|  
|**database_name**|**sysname**|このエラーレコードに関連付けられているデータベースの名前。 バックアップ用のプライマリデータベース、復元用のセカンダリデータベース、またはコピー用に空。|  
|**sequence_number**|**int**|複数のレコードにまたがるエラーの正しい順序を示す増分番号。|  
|**log_time**|**datetime**|レコードが作成された日時。|  
|**log_time_utc**|**datetime**|レコードが作成された日付と時刻。協定世界時で表されます。|  
|**message**|**nvarchar**|メッセージ テキスト。|  
|**source**|**nvarchar**|エラー メッセージまたはイベントのソース。|  
|**help_url**|**nvarchar**|URL (使用可能な場合)。エラーに関する詳細情報が表示されます。|  
  
## <a name="remarks"></a>解説  
 このテーブルには、ログ配布エージェントに関するエラーの詳細が格納されます。 各エラーは一連の例外として記録され、 エージェントセッションごとに複数のエラー (シーケンス) が存在する場合があります。  
  
 リモート監視サーバーに格納されているだけでなく、プライマリサーバーに関連する情報が **log_shipping_monitor_error_detail** テーブルのプライマリサーバーに格納されます。また、セカンダリサーバーに関連する情報は、セカンダリサーバーの **log_shipping_monitor_error_detail** テーブルにも格納されます。  
  
 エージェントセッションを識別するには、列 **agent_id**、 **agent_type**、および **session_id**を使用します。 **Log_time**で並べ替え、ログに記録された順序でエラーを確認します。  
  
## <a name="see-also"></a>参照  
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [log_shipping_monitor_history_detail &#40;Transact-sql&#41;](../../relational-databases/system-tables/log-shipping-monitor-history-detail-transact-sql.md)   
 [sp_cleanup_log_shipping_history &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md)   
 [sp_delete_log_shipping_primary_database &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [sp_delete_log_shipping_secondary_database &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [sp_refresh_log_shipping_monitor &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [システム テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
