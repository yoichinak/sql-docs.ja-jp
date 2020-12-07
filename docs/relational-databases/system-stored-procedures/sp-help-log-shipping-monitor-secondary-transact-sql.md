---
description: sp_help_log_shipping_monitor_secondary (Transact-sql)
title: sp_help_log_shipping_monitor_secondary (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_monitor_secondary
- sp_help_log_shipping_monitor_secondary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_monitor_secondary
ms.assetid: 3ac091ea-c9a8-4c05-a0b6-1ccf4e001339
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e9bfac5c9cbb8594667f33a3abcc0a3a7561b49d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489362"
---
# <a name="sp_help_log_shipping_monitor_secondary-transact-sql"></a>sp_help_log_shipping_monitor_secondary (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  監視テーブルからセカンダリデータベースに関する情報を返します。  
  
 
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_log_shipping_monitor_secondary  
[ @secondary_server = ] 'secondary_server',  
[ @secondary_database = ] 'secondary_database'  
```  
  
## <a name="arguments"></a>引数  
`[ @secondary_server = ] 'secondary_server'` セカンダリサーバーの名前を指定します。 *secondary_server* は **sysname**であり、既定値はありません。  
  
`[ @secondary_database = ] 'secondary_database'` セカンダリデータベースの名前を指定します。 *secondary_database* は **sysname**であり、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列|説明|  
|------------|-----------------|  
|**secondary_server**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ログ配布構成におけるのセカンダリインスタンスの名前です。|  
|**secondary_database**|ログ配布構成のセカンダリデータベースの名前。|  
|**secondary_id**|ログ配布構成におけるセカンダリ サーバーの ID。|  
|**primary_server**|ログ配布構成における [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のプライマリ インスタンスの名前。|  
|**primary_database**|ログ配布構成のプライマリデータベースの名前。|  
|**restore_threshold**|復元操作の間に、アラートが生成されるまでの経過時間 (分単位)。|  
|**threshold_alert**|復元のしきい値を超えたときに発生する警告。|  
|**threshold_alert_enabled**|復元のしきい値の警告を有効にするかどうか。<br /><br /> 1 = 有効。<br /><br /> 0 = 無効です。|  
|**last_copied_file**|セカンダリ サーバーにコピーされた最後のバックアップ ファイルの名前。|  
|**last_copied_date**|セカンダリサーバーに最後にコピー操作を行った日時です。|  
|**last_copied_date_utc**|セカンダリサーバーへの最後のコピー操作の日時。協定世界時で表されます。|  
|**last_restored_file**|セカンダリデータベースに復元された最後のバックアップファイルのファイル名。|  
|**last_restored_date**|セカンダリデータベースに対する最後の復元操作の日時。|  
|**last_restored_date_utc**|セカンダリデータベースでの最後の復元操作の日時。協定世界時で表されます。|  
|**history_retention_period**|指定されたセカンダリデータベースのログ配布履歴レコードが保持されてから削除されるまでの時間 (分単位)。|  
  
## <a name="remarks"></a>解説  
 **sp_help_log_shipping_monitor_secondary** は、監視サーバーの **master** データベースから実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャを実行できるのは、 **sysadmin** 固定サーバーロールのメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
