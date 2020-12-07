---
description: sp_change_log_shipping_primary_database (Transact-SQL)
title: sp_change_log_shipping_primary_database (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_change_log_shipping_primary_database
- sp_change_log_shipping_primary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_log_shipping_primary_database
ms.assetid: 8c9dce6b-d2a3-4ca7-a832-8f59a5adb214
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 070065ae6e621c5ea52bf4be50ac0cc99af089f3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474510"
---
# <a name="sp_change_log_shipping_primary_database-transact-sql"></a>sp_change_log_shipping_primary_database (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  プライマリデータベースの設定を変更します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_change_log_shipping_primary_database [ @database = ] 'database'  
[, [ @backup_directory = ] 'backup_directory']   
[, [ @backup_share = ] 'backup_share']   
[, [ @backup_retention_period = ] 'backup_retention_period']  
[, [ @monitor_server_security_mode = ] 'monitor_server_security_mode']  
[, [ @monitor_server_login = ] 'monitor_server_login']  
[, [ @monitor_server_password = ] 'monitor_server_password']  
[, [ @backup_threshold = ] 'backup_threshold']   
[, [ @threshold_alert = ] 'threshold_alert']   
[, [ @threshold_alert_enabled = ] 'threshold_alert_enabled']   
[, [ @history_retention_period = ] 'history_retention_period']  
[, [ @backup_compression = ] backup_compression_option ]   
```  
  
## <a name="arguments"></a>引数  
`[ @database = ] 'database'` プライマリサーバー上のデータベースの名前を指定します。 *primary_database* は **sysname**であり、既定値はありません。  
  
`[ @backup_directory = ] 'backup_directory'` プライマリサーバー上のバックアップフォルダーへのパスを示します。 *backup_directory* は **nvarchar (500)** で、既定値はありません。 NULL にすることはできません。  
  
`[ @backup_share = ] 'backup_share'` プライマリサーバー上のバックアップディレクトリへのネットワークパスを示します。 *backup_share* は **nvarchar (500)** で、既定値はありません。 NULL にすることはできません。  
  
`[ @backup_retention_period = ] 'backup_retention_period'` プライマリサーバー上のバックアップディレクトリにログバックアップファイルを保持する時間を分単位で示します。 *backup_retention_period* は **int**,、既定値はありません、NULL にすることはできません。  
  
`[ @monitor_server_security_mode = ] 'monitor_server_security_mode'` 監視サーバーへの接続に使用されるセキュリティモード。  
  
 1 = Windows 認証。  
  
 0 = SQL Server 認証。  
  
 *monitor_server_security_mode* は **ビット** であり、NULL にすることはできません。  
  
`[ @monitor_server_login = ] 'monitor_server_login'` 監視サーバーへのアクセスに使用するアカウントのユーザー名を示します。  
  
`[ @monitor_server_password = ] 'monitor_server_password'` 監視サーバーへのアクセスに使用するアカウントのパスワードを入力します。  
  
`[ @backup_threshold = ] 'backup_threshold'`*Threshold_alert*エラーが発生する前に、前回のバックアップ後の分単位の時間を示します。 *backup_threshold* は **int**,、既定値は60分です。  
  
`[ @threshold_alert = ] 'threshold_alert'` バックアップのしきい値を超えたときに発生するアラート。 *threshold_alert* は **int** であり、NULL にすることはできません。  
  
`[ @threshold_alert_enabled = ] 'threshold_alert_enabled'`*Backup_threshold*を超えたときにアラートを生成するかどうかを指定します。  
  
 1 = 有効。  
  
 0 = 無効です。  
  
 *threshold_alert_enabled* は **ビット** であり、NULL にすることはできません。  
  
`[ @history_retention_period = ] 'history_retention_period'` 履歴を保持する時間の長さを分単位で指定します。 *history_retention_period* は **int**です。値が指定されていない場合は、14420が使用されます。  
  
`[ @backup_compression = ] backup_compression_option` ログ配布構成で [バックアップの圧縮](../../relational-databases/backup-restore/backup-compression-sql-server.md)を使用するかどうかを指定します。 このパラメーターは [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (またはそれ以降のバージョン) でのみサポートされます。  
  
 0 = 無効です。 ログ バックアップは圧縮されません。  
  
 1 = 有効。 ログバックアップは常に圧縮します。  
  
 2 = [ビューの設定 [] または [backup compression Default サーバー構成オプションの構成]](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)を使用します。 これが既定値です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 **sp_change_log_shipping_primary_database** は、プライマリサーバーの **master** データベースから実行する必要があります。 このストアド プロシージャでは次の処理が行われます。  
  
1.  必要に応じて、 **log_shipping_primary_database** レコードの設定を変更します。  
  
2.  必要に応じて、指定された引数を使用して、プライマリサーバー上の **log_shipping_monitor_primary** のローカルレコードを変更します。  
  
3.  監視サーバーがプライマリサーバーと異なる場合は、必要に応じて、指定された引数を使用して、監視サーバー上の **log_shipping_monitor_primary** のレコードを変更します。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャを実行できるのは、 **sysadmin** 固定サーバーロールのメンバーだけです。  
  
## <a name="examples"></a>例  
 この例では、 **sp_change_log_shipping_primary_database** を使用して、プライマリデータベースに関連付けられている設定を更新する方法を示し [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] ます。  
  
```  
EXEC master.dbo.sp_change_log_shipping_primary_database   
 @database = N'AdventureWorks'   
, @backup_directory = N'c:\LogShipping'   
, @backup_share = N'\\tribeca\LogShipping'   
, @backup_retention_period = 1440   
, @backup_threshold = 60   
, @threshold_alert = 0   
, @threshold_alert_enabled = 1   
, @history_retention_period = 1440   
,@monitor_server_security_mode = 1  
,@backup_compression = 1;  
```  
  
## <a name="see-also"></a>参照  
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [システムストアドプロシージャ &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [log_shipping_primary_databases &#40;Transact-SQL&#41;](../../relational-databases/system-tables/log-shipping-primary-databases-transact-sql.md)  
  
  
