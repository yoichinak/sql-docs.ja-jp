---
description: sp_attach_schedule (Transact-SQL)
title: sp_attach_schedule (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_attach_schedule_TSQL
- sp_attach_schedule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_attach_schedule
ms.assetid: 80c80eaf-cf23-4ed8-b8dd-65fe59830dd1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 939c8d25428c4ff2afa7249fcb215229226e3d88
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539152"
---
# <a name="sp_attach_schedule-transact-sql"></a>sp_attach_schedule (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ジョブのスケジュールを設定します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_attach_schedule  
     { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,   
     { [ @schedule_id = ] schedule_id   
     | [ @schedule_name = ] 'schedule_name' }  
```  
  
## <a name="arguments"></a>引数  
`[ @job_id = ] job_id` スケジュールを追加するジョブのジョブ識別番号を指定します。 *job_id*は **uniqueidentifier**,、既定値は NULL です。  
  
`[ @job_name = ] 'job_name'` スケジュールを追加するジョブの名前を指定します。 *job_name*は **sysname**,、既定値は NULL です。  
  
> [!NOTE]  
>  *Job_id*または*job_name*のいずれかを指定する必要がありますが、両方を指定することはできません。  
  
`[ @schedule_id = ] schedule_id` ジョブに設定するスケジュールの識別番号を指定します。 *schedule_id*は **int**,、既定値は NULL です。  
  
`[ @schedule_name = ] 'schedule_name'` ジョブに設定するスケジュールの名前を指定します。 *schedule_name*は **sysname**,、既定値は NULL です。  
  
> [!NOTE]  
>  *Schedule_id*または*schedule_name*のいずれかを指定する必要がありますが、両方を指定することはできません。  
  
## <a name="remarks"></a>解説  
 スケジュールとジョブの所有者は同じである必要があります。  
  
 スケジュールは複数のジョブに対して設定できます。 ジョブは、複数のスケジュールで実行できます。  
  
 このストアドプロシージャは、 **msdb** データベースから実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、 **sysadmin** 固定サーバーロールのメンバーは、このストアドプロシージャを実行できます。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 ジョブの所有者はスケジュールにジョブをアタッチし、スケジュールの所有者でなくてもジョブをスケジュールからデタッチできることに注意してください。 ただし、呼び出し元がスケジュールの所有者でない限り、デタッチによってジョブが存在しない場合、スケジュールを削除することはできません。  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、ユーザーがジョブとスケジュールの両方を所有しているかどうかを確認します。  
  
## <a name="examples"></a>例  
 次の例では、という名前のスケジュールを作成し `NightlyJobs` ます。 このスケジュールを使用するジョブは、毎日、サーバーの時間が `01:00` になると実行されます。 この例では、スケジュールをジョブ `BackupDatabase` とジョブにアタッチし `RunReports` ます。  
  
> [!NOTE]  
>  この例では、ジョブ `BackupDatabase` とジョブが既に存在していることを前提としてい `RunReports` ます。  
  
```  
USE msdb ;  
GO  
  
EXEC sp_add_schedule  
    @schedule_name = N'NightlyJobs' ,  
    @freq_type = 4,  
    @freq_interval = 1,  
    @active_start_time = 010000 ;  
GO  
  
EXEC sp_attach_schedule  
   @job_name = N'BackupDatabase',  
   @schedule_name = N'NightlyJobs' ;  
GO  
  
EXEC sp_attach_schedule  
   @job_name = N'RunReports',  
   @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_add_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_detach_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)  
  
  
