---
description: sp_change_log_shipping_secondary_primary (Transact-SQL)
title: sp_change_log_shipping_secondary_primary (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_change_log_shipping_secondary_primary
- sp_change_log_shipping_secondary_primary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_log_shipping_secondary_primary
ms.assetid: 5bcb4df7-6df3-4f2b-9207-b97b5addf2a6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7b17019380bc65d1b3d2fcdb16352fe32477c6bb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474506"
---
# <a name="sp_change_log_shipping_secondary_primary-transact-sql"></a>sp_change_log_shipping_secondary_primary (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  セカンダリデータベースの設定を変更します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_change_log_shipping_secondary_primary  
[ @primary_server = ] 'primary_server',  
[ @primary_database = ] 'primary_database',  
[, [ @backup_source_directory = ] 'backup_source_directory']  
[, [ @backup_destination_directory = ] 'backup_destination_directory']  
[, [ @file_retention_period = ] file_retention_period]  
[, [ @monitor_server_security_mode = ] monitor_server_security_mode]  
[, [ @monitor_server_login = ] 'monitor_server_login']  
[, [ @monitor_server_password = ] 'monitor_server_password']  
```  
  
## <a name="arguments"></a>引数  
`[ @primary_server = ] 'primary_server'`[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ログ配布構成におけるのプライマリインスタンスの名前。 *primary_server* は **sysname** であり、NULL にすることはできません。  
  
`[ @primary_database = ] 'primary_database'` プライマリサーバー上のデータベースの名前を指定します。 *primary_database* は **sysname**であり、既定値はありません。  
  
`[ @backup_source_directory = ] 'backup_source_directory'` プライマリサーバーからのトランザクションログバックアップファイルが格納されているディレクトリ。 *backup_source_directory* は **nvarchar (500)** であり、NULL にすることはできません。  
  
`[ @backup_destination_directory = ] 'backup_destination_directory'` バックアップファイルのコピー先となるセカンダリサーバー上のディレクトリ。 *backup_destination_directory* は **nvarchar (500)** であり、NULL にすることはできません。  
  
`[ @file_retention_period = ] 'file_retention_period'` 履歴を保持する時間の長さを分単位で指定します。 *history_retention_period* は **int**,、既定値は NULL です。 値が指定されていない場合は、14420の値が使用されます。  
  
`[ @monitor_server_security_mode = ] 'monitor_server_security_mode'` 監視サーバーへの接続に使用されるセキュリティモード。  
  
 1 = Windows 認証。  
  
 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証。 *monitor_server_security_mode* は **ビット** であり、NULL にすることはできません。  
  
`[ @monitor_server_login = ] 'monitor_server_login'` 監視サーバーへのアクセスに使用するアカウントのユーザー名を示します。  
  
`[ @monitor_server_password = ] 'monitor_server_password'` 監視サーバーへのアクセスに使用するアカウントのパスワードを入力します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 **sp_change_log_shipping_secondary_primary** は、セカンダリサーバーの **master** データベースから実行する必要があります。 このストアド プロシージャでは次の処理が行われます。  
  
1.  **Log_shipping_secondary**レコードの設定を必要に応じて変更します。  
  
2.  監視サーバーがセカンダリサーバーと異なる場合は、必要に応じて、指定された引数を使用して監視サーバー上の **log_shipping_monitor_secondary** の監視レコードを変更します。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャを実行できるのは、 **sysadmin** 固定サーバーロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
