---
description: sp_help_log_shipping_primary_database (Transact-sql)
title: sp_help_log_shipping_primary_database (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_primary_database_TSQL
- sp_help_log_shipping_primary_database
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_primary_database
ms.assetid: e711b01c-ef29-4eb6-a016-0e647e337818
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b3dea602c3464fb4fee36281a2430f2fef39b7ec
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88493200"
---
# <a name="sp_help_log_shipping_primary_database-transact-sql"></a>sp_help_log_shipping_primary_database (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  プライマリデータベースの設定を取得します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_log_shipping_primary_database  
[ @database = ] 'database' OR  
[ @primary_id = ] 'primary_id'  
```  
  
## <a name="arguments"></a>引数  
`[ @database = ] 'database'` ログ配布プライマリデータベースの名前を指定します。 *データベースのデータ* 型は **sysname**で、既定値はありません。 NULL にすることはできません。  
  
`[ @primary_id = ] 'primary_id'` ログ配布構成のプライマリデータベースの ID。 *primary_id* は **uniqueidentifier** であり、NULL にすることはできません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|説明|  
|-----------------|-----------------|  
|**primary_id**|ログ配布構成のプライマリデータベースの ID。|  
|**primary_database**|ログ配布構成のプライマリデータベースの名前。|  
|**backup_directory**|プライマリサーバーからのトランザクションログバックアップファイルが格納されているディレクトリ。|  
|**backup_share**|バックアップディレクトリへのネットワークまたは UNC パス。|  
|**backup_retention_period**|バックアップ ディレクトリでログ バックアップ ファイルが保持される時間 (分単位)。この時間を過ぎるとファイルは削除されます。|  
|**backup_compression**|ログ配布構成で [バックアップの圧縮](../../relational-databases/backup-restore/backup-compression-sql-server.md)を使用するかどうかを示します。<br /><br /> **0** = 無効です。 ログ バックアップは圧縮されません。<br /><br /> **1** = 有効。 ログバックアップは常に圧縮します。<br /><br /> **2** = [ビューの設定 [] または [Backup Compression Default サーバー構成オプションの構成]](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)を使用します。 これが既定値です。<br /><br /> バックアップの圧縮は、(以降のバージョン) でのみサポートされてい [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] ます。 その他のエディションでは、値は常に 2 です。|  
|**backup_job_id**|プライマリ サーバー上のバックアップ ジョブに関連付けられている、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのジョブ ID。|  
|**monitor_server**|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]ログ配布構成で監視サーバーとして使用されているのインスタンスの名前。|  
|**monitor_server_security_mode**|監視サーバーへの接続に使用されるセキュリティモード。<br /><br /> 1 = [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 認証。<br /><br /> 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証。|  
|**backup_threshold**|バックアップ操作の間に、アラートが生成されるまでの経過時間 (分) です。|  
|**threshold_alert**|バックアップのしきい値を超えたときに発生するアラート。|  
|**threshold_alert_enabled**|バックアップしきい値アラートを有効にするかどうかを決定します。<br /><br /> **1** = 有効。<br /><br /> **0** = 無効です。|  
|**last_backup_file**|最新のトランザクションログバックアップの絶対パス。|  
|**last_backup_date**|最後のログ バックアップ操作の日時。|  
|**last_backup_date_utc**|プライマリデータベースでの最後のトランザクションログバックアップ操作の日時。協定世界時で表されます。|  
|**history_retention_period**|指定したプライマリ データベースでログ配布履歴レコードが保持される時間 (分単位)。この時間を過ぎるとレコードは削除されます。|  
  
## <a name="remarks"></a>解説  
 **sp_help_log_shipping_primary_database** は、プライマリサーバーの **master** データベースから実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャを実行できるのは、 **sysadmin** 固定サーバーロールのメンバーだけです。  
  
## <a name="examples"></a>例  
 この例では、 **sp_help_log_shipping_primary_database** を使用して、データベースのプライマリデータベースの設定を取得する方法を示し [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] ます。  
  
```  
EXEC master.dbo.sp_help_log_shipping_primary_database @database=N'AdventureWorks2012';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
