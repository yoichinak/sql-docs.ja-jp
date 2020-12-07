---
description: log_shipping_secondary_databases (Transact-sql)
title: log_shipping_secondary_databases (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_secondary_databases_TSQL
- log_shipping_secondary_databases
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_secondary_databases system table
ms.assetid: ba2374af-86b8-480c-a10c-51e7c4e3ae23
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5160975171ab32f0c44d807ec445eeaabc5ff4c2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540351"
---
# <a name="log_shipping_secondary_databases-transact-sql"></a>log_shipping_secondary_databases (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ログ配布構成のセカンダリデータベースごとに1つのレコードを格納します。 このテーブルは、 **msdb** データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**secondary_database**|**sysname**|ログ配布構成のセカンダリデータベースの名前。|  
|**secondary_id**|**uniqueidentifier**|ログ配布構成におけるセカンダリ サーバーの ID。|  
|**restore_delay**|**int**|指定されたバックアップファイルを復元する前に、セカンダリサーバーが待機する時間 (分単位)。 既定値は、0 分です。|  
|**restore_all**|**bit**|1に設定すると、復元ジョブの実行時に、使用可能なすべてのトランザクションログバックアップがセカンダリサーバーによって復元されます。 それ以外の場合は、1つのファイルが復元された後に停止します。|  
|**restore_mode**|**bit**|セカンダリデータベースの復元モード。<br /><br /> 0 = with NORECOVERY を使用してログを復元します。<br /><br /> 1 = スタンバイ状態のログを復元します。|  
|**disconnect_users**|**bit**|1に設定すると、復元操作の実行時に、ユーザーはセカンダリデータベースから切断されます。 既定値は0です。|  
|**block_size**|**int**|バックアップデバイスのブロックサイズとして使用されるサイズ (バイト単位)。|  
|**buffer_count**|**int**|バックアップまたは復元操作によって使用されるバッファーの合計数。|  
|**max_transfer_size**|**int**|によって [!INCLUDE[msCoName](../../includes/msconame-md.md)] バックアップデバイスに発行される入力要求または出力要求の最大サイズ (バイト単位) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|**last_restored_file**|**nvarchar (500)**|セカンダリデータベースに復元された最後のバックアップファイルのファイル名。|  
|**last_restored_date**|**datetime**|セカンダリデータベースに対する最後の復元操作の日時。|  
  
## <a name="see-also"></a>参照  
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_add_log_shipping_secondary_database &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql.md)   
 [sp_delete_log_shipping_secondary_database &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [sp_help_log_shipping_secondary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md)   
 [log_shipping_secondary &#40;Transact-SQL&#41;](../../relational-databases/system-tables/log-shipping-secondary-transact-sql.md)   
 [システム テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
