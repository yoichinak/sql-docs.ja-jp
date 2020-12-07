---
description: managed_backup。 sp_backup_config_schedule (Transact-sql)
title: managed_backup。 sp_backup_config_schedule (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 02/20/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_backup_config_schedule_TSQL
- managed_backup.sp_backup_config_schedule
- managed_backup.sp_backup_config_schedule_TSQL
- sp_backup_config_schedule
dev_langs:
- TSQL
helpviewer_keywords:
- managed_backup.sp_backup_config_schedule
- sp_backup_config_schedule
ms.assetid: 82541160-d1df-4061-91a5-6868dd85743a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 23f1f96ff6d41412e8606e67aacfdc42d9afabc4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88486305"
---
# <a name="managed_backupsp_backup_config_schedule-transact-sql"></a>managed_backup。 sp_backup_config_schedule (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  の自動またはカスタムスケジュールオプションを構成 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] します。  
    
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```vb  
EXEC managed_backup.sp_backup_config_schedule   
    [@database_name = ] 'database_name'
    ,[@scheduling_option = ] {'Custom' | 'System'}  
    ,[@full_backup_freq_type = ] {'Daily' | 'Weekly'}  
    ,[@days_of_week = ] 'days_of_the_week'  
    ,[@backup_begin_time = ] 'begin time of the backup window'  
    ,[@backup_duration = ] 'backup window length'  
    ,[@log_backup_freq = ] 'frequency of log backup'  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a> 引数  
 @database_name  
 特定のデータベースでマネージバックアップを有効にするためのデータベース名。 NULL または * の場合、このマネージバックアップはサーバー上のすべてのデータベースに適用されます。  
  
 @scheduling_option  
 システム制御のバックアップスケジュールには ' System ' を指定してください。 他の paratmeters によって定義されたカスタムスケジュールには、' Custom ' を指定します。  
  
 @full_backup_freq_type  
 マネージバックアップ操作の頻度の種類。 ' Daily ' または ' Weekly ' に設定できます。  
  
 @days_of_week  
 が毎週に設定されている場合のバックアップの曜日 @full_backup_freq_type 。 ' Monday ' のような完全な文字列名を指定してください。  複数の曜日名をパイプで区切って指定することもできます。 例: N'Monday |水曜日 |金曜日  
  
 @backup_begin_time  
 バックアップウィンドウの開始時刻。 バックアップは、との組み合わせによって定義される時間枠の外側では開始されません @backup_begin_time @backup_duration 。  
  
 @backup_duration  
 バックアップ時間枠の期間。 とで定義された時間枠でバックアップが完了する保証はないことに注意 @backup_begin_time @backup_duration してください。 この時間枠内に開始され、ウィンドウの期間を超えるバックアップ操作は取り消されません。  
  
 @log_backup_freq  
 これにより、トランザクションログバックアップの頻度が決まります。 これらのバックアップは、データベースバックアップに指定されたスケジュールではなく、一定の間隔で行われます。 @log_backup_freq は数分または数時間で指定でき `0:00` 、ログバックアップがないことを示します。 ログバックアップを無効にすることは、単純復旧モデルのデータベースにのみ適しています。  
  
> [!NOTE]  
>  復旧モデルが単純から完全に変更された場合は、log_backup_freq をから `0:00` 0 以外の値に再構成する必要があります。  
  
## <a name="return-code-value"></a>リターン コード値  
 0 (成功) または 1 (失敗)  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>アクセス許可  
 **Db_backupoperator**データベースロールのメンバーシップ、 **ALTER ANY CREDENTIAL**権限、および**Sp_delete_backuphistory**ストアドプロシージャに対する**EXECUTE**権限が必要です。  
  
## <a name="see-also"></a>関連項目  
 [managed_backup。 sp_backup_config_basic (Transact-sql)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)   
 [managed_backup.sp_backup_config_advanced &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)  
  
  
