---
description: sp_help_log_shipping_monitor (Transact-SQL)
title: sp_help_log_shipping_monitor (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_monitor_TSQL
- sp_help_log_shipping_monitor
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_monitor
ms.assetid: a4e96c45-6dcd-471a-a494-b5c619459855
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: fa34a789b4993b8eaf14123b2f9a4bffb477ed39
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474224"
---
# <a name="sp_help_log_shipping_monitor-transact-sql"></a>sp_help_log_shipping_monitor (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  プライマリ、セカンダリ、または監視サーバーに登録されているプライマリデータベースとセカンダリデータベースの状態などの情報を含む結果セットを返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_log_shipping_monitor  
```  
  
## <a name="arguments"></a>引数  
 [なし] :  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**status**|**bit**|ログ配布データベースのエージェントに関する全般的な状態。<br /><br /> **0** = 正常かつエージェントなしのエラー。<br /><br /> **1** = それ以外の場合は。|  
|**is_primary**|**bit**|この行がプライマリ データベースのものかどうか。<br /><br /> **1** = プライマリデータベースの行です。<br /><br /> **0** = セカンダリデータベースの行です。|  
|**server**|**sysname**|このデータベースが存在するプライマリまたはセカンダリ サーバーの名前。|  
|**database_name**|**sysname**|データベース名です。|  
|**time_since_last_backup**|**int**|前回のログバックアップ以降の時間の長さ (分単位)。<br /><br /> NULL = 情報が利用できないか、または関連性がありません。|  
|**last_backup_file**|**nvarchar (500)**|前回正常に作成されたログ バックアップ ファイルの名前。<br /><br /> NULL = 情報が利用できないか、または関連性がありません。|  
|**backup_threshold**|**int**|前回のバックアップが行われてから、threshold_alert エラーが発生するまでの期間 (分単位)。 **backup_threshold** は **int**,、既定値は **60 分**です。<br /><br /> NULL = 情報が利用できないか、または関連性がありません。<br /><br /> この値は [sp_add_log_shipping_primary_database &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md)を使用して変更できます。|  
|**is_backup_alert_enabled**|**bit**|**Backup_threshold**を超えたときにアラートを生成するかどうかを指定します。 **1 (既定**値) の値は、警告が発生することを意味します。<br /><br /> NULL = 情報が利用できないか、または関連性がありません。<br /><br /> この値は [sp_add_log_shipping_primary_database &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md)を使用して変更できます。|  
|**time_since_last_copy**|**int**|前回のログ バックアップがコピーされてから経過した時間 (分単位)。<br /><br /> NULL = 情報が利用できないか、または関連性がありません。|  
|**last_copied_file**|**nvarchar (500)**|最後に正常にコピーされたログバックアップファイルの名前。<br /><br /> NULL = 情報が利用できないか、または関連性がありません。|  
|**time_since_last_restore**|**int**|前回のログバックアップが復元されてからの時間の長さ (分単位)。<br /><br /> NULL = 情報が利用できないか、または関連性がありません。|  
|**last_restored_file**|**nvarchar (500)。**|最後に正常に復元されたログバックアップファイルの名前。<br /><br /> NULL = 情報が利用できないか、または関連性がありません。|  
|**last_restored_latency**|**int**|前回のバックアップが作成されてからバックアップが復元されるまでの時間 (分単位)。<br /><br /> NULL = 情報が利用できないか、または関連性がありません。|  
|**restore_threshold**|**int**|復元操作の間に、アラートが生成されるまでの経過時間 (分単位)。 **restore_threshold** を NULL にすることはできません。|  
|**is_restore_alert_enabled**|**bit**|**Restore_threshold**を超えたときにアラートを生成するかどうかを指定します。 **1 (既定**値) の値は、警告が発生することを意味します。<br /><br /> NULL = 情報が利用できないか、または関連性がありません。<br /><br /> 復元のしきい値を設定するには、 [sp_add_log_shipping_secondary_database](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql.md)を使用します。|  
  
## <a name="remarks"></a>解説  
 **sp_help_log_shipping_monitor** は、監視サーバーの **master** データベースから実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 **sysadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="see-also"></a>参照  
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
