---
description: sp_change_log_shipping_secondary_database (Transact-SQL)
title: sp_change_log_shipping_secondary_database (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_change_log_shipping_secondary_database
- sp_change_log_shipping_secondary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_log_shipping_secondary_database
ms.assetid: 3ebcf2f1-980f-4543-a84b-fbaeea54eeac
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5fc10c705564c88fe157860d00a61fa5ea682cc0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88486285"
---
# <a name="sp_change_log_shipping_secondary_database-transact-sql"></a>sp_change_log_shipping_secondary_database (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  セカンダリデータベースの設定を変更します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_change_log_shipping_secondary_database  
[ @secondary_database = ] 'secondary_database',  
[, [ @restore_delay = ] 'restore_delay']  
[, [ @restore_all = ] 'restore_all']  
[, [ @restore_mode = ] 'restore_mode']  
[, [ @disconnect_users = ] 'disconnect_users']  
[, [ @block_size = ] 'block_size']  
[, [ @buffer_count = ] 'buffer_count']  
[, [ @max_transfer_size = ] 'max_transfer_size']  
[, [ @restore_threshold = ] 'restore_threshold']   
[, [ @threshold_alert = ] 'threshold_alert']   
[, [ @threshold_alert_enabled = ] 'threshold_alert_enabled']   
[, [ @history_retention_period = ] 'history_retention_period']  
```  
  
## <a name="arguments"></a>引数  
`[ @restore_delay = ] 'restore_delay'` 指定されたバックアップファイルを復元する前に、セカンダリサーバーが待機する時間 (分単位)。 *restore_delay* は **int** であり、NULL にすることはできません。 既定値は 0 です。  
  
`[ @restore_all = ] 'restore_all'` 1に設定すると、復元ジョブの実行時に、使用可能なすべてのトランザクションログバックアップがセカンダリサーバーによって復元されます。 それ以外の場合は、1つのファイルが復元された後に停止します。 *restore_all* は **ビット** であり、NULL にすることはできません。  
  
`[ @restore_mode = ] 'restore_mode'` セカンダリデータベースの復元モード。  
  
 0 = NORECOVERY でログを復元。  
  
 1 = スタンバイ状態のログを復元します。  
  
 *restore* は **ビット** であり、NULL にすることはできません。  
  
`[ @disconnect_users = ] 'disconnect_users'` 1に設定すると、復元操作の実行時にユーザーがセカンダリデータベースから切断されます。 既定値は 0 です。 *disconnect_users* は **ビット** であり、NULL にすることはできません。  
  
`[ @block_size = ] 'block_size'` バックアップデバイスのブロックサイズとして使用されるサイズ (バイト単位)。 *block_size* は **int** で、既定値は-1 です。  
  
`[ @buffer_count = ] 'buffer_count'` バックアップまたは復元操作によって使用されるバッファーの合計数。 *buffer_count* は **int** で、既定値は-1 です。  
  
`[ @max_transfer_size = ] 'max_transfer_size'` によってバックアップデバイスに発行される入力要求または出力要求の最大サイズ (バイト単位) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 *max_transfersize* は **int** であり、NULL を指定できます。  
  
`[ @restore_threshold = ] 'restore_threshold'` 復元操作の間に、アラートが生成されるまでの経過時間 (分単位)。 *restore_threshold* は **int** であり、NULL にすることはできません。  
  
`[ @threshold_alert = ] 'threshold_alert'` 復元のしきい値を超えたときに発生する警告を指定します。 *threshold_alert* は **int**,、既定値は14420です。  
  
`[ @threshold_alert_enabled = ] 'threshold_alert_enabled'`*Restore_threshold*を超えたときにアラートを生成するかどうかを指定します。 1 = 有効。0 = 無効です。 *threshold_alert_enabled* は **ビット** であり、NULL にすることはできません。  
  
`[ @history_retention_period = ] 'history_retention_period'` 履歴を保持する時間の長さを分単位で指定します。 *history_retention_period* は **int**です。値が指定されていない場合は、1440の値が使用されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 **sp_change_log_shipping_secondary_database** は、セカンダリサーバーの **master** データベースから実行する必要があります。 このストアド プロシージャでは次の処理が行われます。  
  
1.  必要に応じて **log_shipping_secondary_database** レコードの設定を変更します。  
  
2.  必要に応じて、指定された引数を使用して、セカンダリサーバー上の **log_shipping_monitor_secondary** のローカル監視レコードを変更します。  

## <a name="permissions"></a>アクセス許可  
 このプロシージャを実行できるのは、 **sysadmin** 固定サーバーロールのメンバーだけです。  
  
## <a name="examples"></a>例  
 この例では、 **sp_change_log_shipping_secondary_database** を使用してデータベース **LogShipAdventureWorks**のセカンダリデータベースパラメーターを更新する方法を示します。  
  
```  
EXEC master.dbo.sp_change_log_shipping_secondary_database   
 @secondary_database =  'LogShipAdventureWorks'  
,  @restore_delay = 0  
,  @restore_all = 1  
,  @restore_mode = 0  
,  @disconnect_users = 0  
,  @threshold_alert = 14420  
,  @threshold_alert_enabled = 1  
,  @history_retention_period = 14420;  
```  
  
## <a name="see-also"></a>参照  
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
