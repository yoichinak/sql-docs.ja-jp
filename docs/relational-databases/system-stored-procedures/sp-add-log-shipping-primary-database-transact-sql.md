---
description: sp_add_log_shipping_primary_database (Transact-SQL)
title: sp_add_log_shipping_primary_database (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_log_shipping_primary_database
- sp_add_log_shipping_primary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_shipping_primary_database
ms.assetid: 69531611-113f-46b5-81a6-7bf496d0353c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0ed823f2b6564593388893db74866931bc1c0c93
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464664"
---
# <a name="sp_add_log_shipping_primary_database-transact-sql"></a>sp_add_log_shipping_primary_database (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  バックアップ ジョブ、ローカル監視レコード、リモート監視レコードを含め、ログ配布構成のプライマリ データベースを設定します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_add_log_shipping_primary_database [ @database = ] 'database',   
[ @backup_directory = ] 'backup_directory',   
[ @backup_share = ] 'backup_share',   
[ @backup_job_name = ] 'backup_job_name',   
[, [ @backup_retention_period = ] backup_retention_period]  
[, [ @monitor_server = ] 'monitor_server']  
[, [ @monitor_server_security_mode = ] monitor_server_security_mode]  
[, [ @monitor_server_login = ] 'monitor_server_login']  
[, [ @monitor_server_password = ] 'monitor_server_password']  
[, [ @backup_threshold = ] backup_threshold ]   
[, [ @threshold_alert = ] threshold_alert ]   
[, [ @threshold_alert_enabled = ] threshold_alert_enabled ]   
[, [ @history_retention_period = ] history_retention_period ]  
[, [ @backup_job_id = ] backup_job_id OUTPUT ]  
[, [ @primary_id = ] primary_id OUTPUT]  
[, [ @backup_compression = ] backup_compression_option ]  
  
```  
  
## <a name="arguments"></a>引数  
`[ @database = ] 'database'` ログ配布プライマリデータベースの名前を指定します。 *データベースのデータ* 型は **sysname**で、既定値はありません。 NULL にすることはできません。  
  
`[ @backup_directory = ] 'backup_directory'` プライマリサーバー上のバックアップフォルダーへのパスを示します。 *backup_directory* は **nvarchar (500)** で、既定値はありません。 NULL にすることはできません。  
  
`[ @backup_share = ] 'backup_share'` プライマリサーバー上のバックアップディレクトリへのネットワークパスを示します。 *backup_share* は **nvarchar (500)** で、既定値はありません。 NULL にすることはできません。  
  
`[ @backup_job_name = ] 'backup_job_name'` バックアップをバックアップフォルダーにコピーする、プライマリサーバー上の SQL Server エージェントジョブの名前を指定します。 *backup_job_name* は **sysname** であり、NULL にすることはできません。  
  
`[ @backup_retention_period = ] backup_retention_period` プライマリサーバー上のバックアップディレクトリにログバックアップファイルを保持する時間を分単位で示します。 *backup_retention_period* は **int**,、既定値はありません、NULL にすることはできません。  
  
`[ @monitor_server = ] 'monitor_server'` 監視サーバーの名前を指定します。 *Monitor_server* は **sysname**であり、既定値はありません。 NULL にすることはできません。  
  
`[ @monitor_server_security_mode = ] monitor_server_security_mode` 監視サーバーへの接続に使用されるセキュリティモード。  
  
 1 = Windows 認証。  
  
 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証。 *monitor_server_security_mode* は **ビット** であり、NULL にすることはできません。  
  
`[ @monitor_server_login = ] 'monitor_server_login'` 監視サーバーへのアクセスに使用するアカウントのユーザー名を示します。  
  
`[ @monitor_server_password = ] 'monitor_server_password'` 監視サーバーへのアクセスに使用するアカウントのパスワードを入力します。  
  
`[ @backup_threshold = ] backup_threshold`*Threshold_alert*エラーが発生する前に、前回のバックアップ後の分単位の時間を示します。 *backup_threshold* は **int**,、既定値は60分です。  
  
`[ @threshold_alert = ] threshold_alert` バックアップのしきい値を超えたときに発生する警告を指定します。 *threshold_alert* は **int**,、既定値は14420です。  
  
`[ @threshold_alert_enabled = ] threshold_alert_enabled`*Backup_threshold*を超えたときにアラートを生成するかどうかを指定します。 値 0 (既定値) を指定すると、警告が無効になり、生成されなくなります。 *threshold_alert_enabled* は **ビット**です。  
  
`[ @history_retention_period = ] history_retention_period` 履歴を保持する時間の長さを分単位で指定します。 *history_retention_period* は **int**,、既定値は NULL です。 値が指定されていない場合は、14420の値が使用されます。  
  
`[ @backup_job_id = ] backup_job_id OUTPUT`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]プライマリサーバー上のバックアップジョブに関連付けられているエージェントジョブ ID。 *backup_job_id* は **uniqueidentifier** であり、NULL にすることはできません。  
  
`[ @primary_id = ] primary_id OUTPUT` ログ配布構成のプライマリデータベースの ID。 *primary_id* は **uniqueidentifier** であり、NULL にすることはできません。  
  
`[ @backup_compression = ] backup_compression_option` ログ配布構成で [バックアップの圧縮](../../relational-databases/backup-restore/backup-compression-sql-server.md)を使用するかどうかを指定します。 このパラメーターは [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (またはそれ以降のバージョン) でのみサポートされます。  
  
 0 = 無効です。 ログ バックアップは圧縮されません。  
  
 1 = 有効。 ログバックアップは常に圧縮します。  
  
 2 = [ビューの設定 [] または [backup compression Default サーバー構成オプションの構成]](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)を使用します。 これが既定値です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 **sp_add_log_shipping_primary_database** は、プライマリサーバーの **master** データベースから実行する必要があります。 このストアドプロシージャは、次の機能を実行します。  
  
1.  プライマリ ID を生成し、指定された引数を使用して **log_shipping_primary_databases** テーブルにプライマリデータベースのエントリを追加します。  
  
2.  無効になっているプライマリデータベースのバックアップジョブを作成します。  
  
3.  **Log_shipping_primary_databases**エントリのバックアップジョブ id をバックアップジョブのジョブ id に設定します。  
  
4.  指定された引数を使用して、プライマリサーバーのテーブル **log_shipping_monitor_primary** にローカル監視レコードを追加します。  
  
5.  監視サーバーがプライマリサーバーと異なる場合は、によって、指定された引数を使用して監視サーバーの **log_shipping_monitor_primary** に監視レコードが追加されます。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャを実行できるのは、 **sysadmin** 固定サーバーロールのメンバーだけです。  
  
## <a name="examples"></a>例  
 次の例では、ログ配布構成のプライマリ データベースとして、データベース [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] を追加します。  
  
```  
DECLARE @LS_BackupJobId AS uniqueidentifier ;  
DECLARE @LS_PrimaryId AS uniqueidentifier ;  
  
EXEC master.dbo.sp_add_log_shipping_primary_database   
@database = N'AdventureWorks'   
,@backup_directory = N'c:\lsbackup'   
,@backup_share = N'\\tribeca\lsbackup'   
,@backup_job_name = N'LSBackup_AdventureWorks'   
,@backup_retention_period = 1440  
,@monitor_server = N'rockaway'   
,@monitor_server_security_mode = 1   
,@backup_threshold = 60   
,@threshold_alert = 0   
,@threshold_alert_enabled = 0   
,@history_retention_period = 1440   
,@backup_job_id = @LS_BackupJobId OUTPUT   
,@primary_id = @LS_PrimaryId OUTPUT   
,@overwrite = 1   
,@backup_compression = 0;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
