---
description: log_shipping_monitor_secondary (Transact-sql)
title: log_shipping_monitor_secondary (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_monitor_secondary_TSQL
- log_shipping_monitor_secondary
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_monitor_secondary system table
ms.assetid: afbe1bb7-89a7-4020-9408-0af64a043c2e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 823295ed5746abcf0e02fca4680a196c8687bc86
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538300"
---
# <a name="log_shipping_monitor_secondary-transact-sql"></a>log_shipping_monitor_secondary (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ログ配布構成のセカンダリデータベースごとに1つの監視レコードを格納します。 このテーブルは、 **msdb** データベースに格納されます。  
  
 履歴と監視に関連するテーブルは、プライマリサーバーとセカンダリサーバーでも使用されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**secondary_server**|**sysname**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ログ配布構成におけるのセカンダリインスタンスの名前です。|  
|**secondary_database**|**sysname**|ログ配布構成のセカンダリデータベースの名前。|  
|**secondary_id**|**uniqueidentifier**|ログ配布構成におけるセカンダリ サーバーの ID。|  
|**primary_server**|**sysname**|ログ配布構成における [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のプライマリ インスタンスの名前。|  
|**primary_database**|**sysname**|ログ配布構成のプライマリデータベースの名前。|  
|**restore_threshold**|**int**|復元操作の間に、アラートが生成されるまでの経過時間 (分単位)。|  
|**threshold_alert**|**int**|復元のしきい値を超えたときに発生する警告。|  
|**threshold_alert_enabled**|**bit**|復元のしきい値の警告を有効にするかどうか。 1 = 有効。<br /><br /> 0 = 無効です。|  
|**last_copied_file**|**nvarchar (500)**|セカンダリ サーバーにコピーされた最後のバックアップ ファイルの名前。|  
|**last_copied_date**|**datetime**|セカンダリサーバーに最後にコピー操作を行った日時です。|  
|**last_copied_date_utc**|**datetime**|セカンダリサーバーへの最後のコピー操作の日時。協定世界時で表されます。|  
|**last_restored_file**|**nvarchar (500)**|セカンダリデータベースに復元された最後のバックアップファイルのファイル名。|  
|**last_restored_date**|**datetime**|セカンダリデータベースに対する最後の復元操作の日時。|  
|**last_restored_date_utc**|**datetime**|セカンダリデータベースでの最後の復元操作の日時。協定世界時で表されます。|  
|**last_restored_latency**|**int**|ログバックアップがプライマリで作成されてからセカンダリに復元されるまでの経過時間 (分単位)。<br /><br /> 初期値が NULL です。|  
|**history_retention_period**|**int**|指定されたセカンダリデータベースのログ配布履歴レコードが保持されてから削除されるまでの時間 (分単位)。|  
  
## <a name="remarks"></a>解説  
 リモート監視サーバーに格納されているだけでなく、セカンダリサーバーに関連する情報は、セカンダリサーバーの **log_shipping_monitor_secondary** テーブルにも格納されます。  
  
## <a name="see-also"></a>参照  
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_refresh_log_shipping_monitor &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [sp_add_log_shipping_secondary_database &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql.md)   
 [sp_change_log_shipping_secondary_database &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-change-log-shipping-secondary-database-transact-sql.md)   
 [sp_delete_log_shipping_secondary_database &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [sp_help_log_shipping_secondary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md)   
 [sp_help_log_shipping_monitor_secondary &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-secondary-transact-sql.md)   
 [sp_refresh_log_shipping_monitor &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [システム テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
