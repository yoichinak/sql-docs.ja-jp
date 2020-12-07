---
description: sp_add_log_shipping_secondary_primary (Transact-SQL)
title: sp_add_log_shipping_secondary_primary (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_log_shipping_secondary_primary_TSQL
- sp_add_log_shipping_secondary_primary
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_shipping_secondary_primary
ms.assetid: bfbbbee2-c255-4a59-a963-47d6e980a8e2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e1123bfa1ce465989322c3b76a48da96c1fed7f7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464636"
---
# <a name="sp_add_log_shipping_secondary_primary-transact-sql"></a>sp_add_log_shipping_secondary_primary (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定したプライマリ データベースのセカンダリ サーバーに対して、プライマリ情報の設定、ローカルおよびリモート監視リンクの追加、コピー ジョブと復元ジョブの作成を行います。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_add_log_shipping_secondary_primary  
 [ @primary_server = ] 'primary_server',   
[ @primary_database = ] 'primary_database',  
[ @backup_source_directory = ] 'backup_source_directory' ,   
[ @backup_destination_directory = ] 'backup_destination_directory'  
[ @copy_job_name = ] 'copy_job_name'  
[ @restore_job_name = ] 'restore_job_name'  
[, [ @file_retention_period = ] 'file_retention_period']  
[, [ @monitor_server = ] 'monitor_server']  
[, [ @monitor_server_security_mode = ] 'monitor_server_security_mode']  
[, [ @monitor_server_login = ] 'monitor_server_login']  
[, [ @monitor_server_password = ] 'monitor_server_password']  
[, [ @copy_job_id = ] 'copy_job_id' OUTPUT ]  
[, [ @restore_job_id = ] 'restore_job_id' OUTPUT ]  
[, [ @secondary_id = ] 'secondary_id' OUTPUT]  
```  
  
## <a name="arguments"></a>引数  
`[ @primary_server = ] 'primary_server'`[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ログ配布構成におけるのプライマリインスタンスの名前。 *primary_server* は **sysname** であり、NULL にすることはできません。  
  
`[ @primary_database = ] 'primary_database'` プライマリサーバー上のデータベースの名前を指定します。 *primary_database* は **sysname**であり、既定値はありません。  
  
`[ @backup_source_directory = ] 'backup_source_directory'` プライマリサーバーからのトランザクションログバックアップファイルが格納されているディレクトリ。 *backup_source_directory* は **nvarchar (500)** であり、NULL にすることはできません。  
  
`[ @backup_destination_directory = ] 'backup_destination_directory'` バックアップファイルのコピー先となるセカンダリサーバー上のディレクトリ。 *backup_destination_directory* は **nvarchar (500)** であり、NULL にすることはできません。  
  
`[ @copy_job_name = ] 'copy_job_name'`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]トランザクションログバックアップをセカンダリサーバーにコピーするために作成されるエージェントジョブに使用する名前。 *copy_job_name* は **sysname** であり、NULL にすることはできません。  
  
`[ @restore_job_name = ] 'restore_job_name'` セカンダリ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースにバックアップを復元するセカンダリサーバー上のエージェントジョブの名前を指定します。 *restore_job_name* は **sysname** であり、NULL にすることはできません。  
  
`[ @file_retention_period = ] 'file_retention_period'` パラメーターで指定されたパスでバックアップファイルがセカンダリサーバーに保持される時間 (分単位)。この時間を経過すると、 @backup_destination_directory 削除されます。 *history_retention_period* は **int**,、既定値は NULL です。 値が指定されていない場合は、14420の値が使用されます。  
  
`[ @monitor_server = ] 'monitor_server'` 監視サーバーの名前を指定します。 *Monitor_server* は **sysname**であり、既定値はありません。 NULL にすることはできません。  
  
`[ @monitor_server_security_mode = ] 'monitor_server_security_mode'` 監視サーバーへの接続に使用されるセキュリティモード。  
  
 1 = Windows 認証。  
  
 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証。  
  
 *monitor_server_security_mode* は **ビット** であり、NULL にすることはできません。  
  
`[ @monitor_server_login = ] 'monitor_server_login'` 監視サーバーへのアクセスに使用するアカウントのユーザー名を示します。  
  
`[ @monitor_server_password = ] 'monitor_server_password'` 監視サーバーへのアクセスに使用するアカウントのパスワードを入力します。  
  
`[ @copy_job_id = ] 'copy_job_id' OUTPUT` セカンダリサーバー上のコピージョブに関連付けられている ID。 *copy_job_id* は **uniqueidentifier** であり、NULL にすることはできません。  
  
`[ @restore_job_id = ] 'restore_job_id' OUTPUT` セカンダリサーバー上の復元ジョブに関連付けられている ID。 *restore_job_id* は **uniqueidentifier** であり、NULL にすることはできません。  
  
`[ @secondary_id = ] 'secondary_id' OUTPUT` ログ配布構成におけるセカンダリサーバーの ID。 *secondary_id* は **uniqueidentifier** であり、NULL にすることはできません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 **sp_add_log_shipping_secondary_primary** は、セカンダリサーバーの **master** データベースから実行する必要があります。 このストアド プロシージャでは次の処理が行われます。  
  
1.  指定したプライマリ サーバーとプライマリ データベースのセカンダリ ID を生成する。  
  
2.  では、次のことが行われます。  

    1.  指定された引数を使用して **log_shipping_secondary** にセカンダリ ID のエントリを追加します。  
  
    2.  無効になったセカンダリ ID のコピー ジョブを作成する。  
  
    3.  **Log_shipping_secondary**エントリのコピージョブ id をコピージョブのジョブ id に設定します。  
  
    4.  セカンダリ ID に対して無効になっている復元ジョブを作成します。  
  
    5.  **Log_shipping_secondary**エントリの復元ジョブ id を、復元ジョブのジョブ id に設定します。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャを実行できるのは、 **sysadmin** 固定サーバーロールのメンバーだけです。  
  
## <a name="examples"></a>例  
 この例では、 **sp_add_log_shipping_secondary_primary** ストアドプロシージャを使用して、セカンダリサーバー上のプライマリデータベースの情報を設定する方法を示し [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] ます。  
  
```  
EXEC master.dbo.sp_add_log_shipping_secondary_primary   
@primary_server = N'TRIBECA'   
,@primary_database = N'AdventureWorks'   
,@backup_source_directory = N'\\tribeca\LogShipping'   
,@backup_destination_directory = N''   
,@copy_job_name = N''   
,@restore_job_name = N''   
,@file_retention_period = 1440   
,@monitor_server = N'ROCKAWAY'   
,@monitor_server_security_mode = 1   
,@copy_job_id = @LS_Secondary__CopyJobId OUTPUT   
,@restore_job_id = @LS_Secondary__RestoreJobId OUTPUT   
,@secondary_id = @LS_Secondary__SecondaryId OUTPUT ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
