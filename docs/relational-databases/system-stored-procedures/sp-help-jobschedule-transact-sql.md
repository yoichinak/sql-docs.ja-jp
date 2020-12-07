---
description: sp_help_jobschedule (Transact-sql)
title: sp_help_jobschedule (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobschedule
- sp_help_jobschedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobschedule
ms.assetid: 2cded902-9272-4667-ac4b-a4f95a9f008e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5d74890ab154700159fcf6ca086f88cd2ac57409
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538826"
---
# <a name="sp_help_jobschedule-transact-sql"></a>sp_help_jobschedule (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  自動化された [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 活動を実行するためにによって使用されるジョブのスケジュールに関する情報を返します。  
 
 
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_jobschedule { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }  
     [ , [ @schedule_name = ] 'schedule_name' ]  
     [ , [ @schedule_id = ] schedule_id ]  
     [ , [ @include_description = ] include_description ]  
```  
  
## <a name="arguments"></a>引数  
`[ @job_id = ] job_id` ジョブの識別番号を指定します。 *job_id*は **uniqueidentifier**,、既定値は NULL です。  
  
`[ @job_name = ] 'job_name'` ジョブの名前。 *job_name*は **sysname**,、既定値は NULL です。  
  
> [!NOTE]
> *Job_id*または*job_name*のいずれかを指定する必要がありますが、両方を指定することはできません。

`[ @schedule_name = ] 'schedule_name'` ジョブのスケジュールアイテムの名前。 *schedule_name*は **sysname**,、既定値は NULL です。  
  
`[ @schedule_id = ] schedule_id` ジョブのスケジュールアイテムの識別番号を指定します。 *schedule_id*は **int**,、既定値は NULL です。  
  
`[ @include_description = ] include_description` スケジュールの説明を結果セットに含めるかどうかを指定します。 *include_description* は **ビット**,、既定値は **0**です。 *Include_description*が**0**の場合は、スケジュールの説明が結果セットに含まれません。 *Include_description*が**1**の場合、スケジュールの説明が結果セットに含まれます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|スケジュールの識別子番号。|  
|**schedule_name**|**sysname**|スケジュールの名前。|  
|**有効**|**int**|スケジュールが有効になっている (**1**) か、有効でない (**0**) かを指定します。|  
|**freq_type**|**int**|ジョブをいつ実行するかを示す値。<br /><br /> **1** = 1 回<br /><br /> **4** = 日単位<br /><br /> **8** = 週単位<br /><br /> **16** = 月単位<br /><br /> **32** = 毎月、 **freq_interval**に対して相対的<br /><br /> **64** = **SQLServerAgent** サービスの開始時に実行します。|  
|**freq_interval**|**int**|ジョブが実行された日。 値は **freq_type**の値によって異なります。 詳細については、「 [sp_add_schedule &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)」を参照してください。|  
|**freq_subday_type**|**int**|**Freq_subday_interval**の単位。 詳細については、「 [sp_add_schedule &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)」を参照してください。|  
|**freq_subday_interval**|**int**|ジョブの各実行間に発生する **freq_subday_type** 期間の数。 詳細については、「 [sp_add_schedule &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)」を参照してください。|  
|**freq_relative_interval**|**int**|スケジュールされたジョブの各月の **freq_interval** の発生。 詳細については、「 [sp_add_schedule &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)」を参照してください。|  
|**freq_recurrence_factor**|**int**|スケジュールされたジョブの実行間隔 (月数)。|  
|**active_start_date**|**int**|スケジュールをアクティブにした日付。|  
|**active_end_date**|**int**|スケジュールの終了日。|  
|**active_start_time**|**int**|スケジュールの開始時刻。|  
|**active_end_time**|**int**|スケジュールを終了する時刻。|  
|**date_created**|**datetime**|スケジュールが作成された日付。|  
|**schedule_description**|**nvarchar (4000)**|**msdb.dbo.sysスケジュール**の値から派生したスケジュールの英語の説明。 *Include_description*が**0**の場合、この列には説明が要求されていないことを示すテキストが含まれます。|  
|**next_run_date**|**int**|スケジュールによってジョブが次に実行される日付。|  
|**next_run_time**|**int**|スケジュールによってジョブが次に実行される時刻。|  
|**schedule_uid**|**uniqueidentifier**|スケジュールの識別子。|  
|**job_count**|**int**|返されたジョブの数。|  
  
> **注: sp_help_jobschedule**は**dbo.sysjobschedules**から値を返し、 **msdb**のシステムテーブルを**dbo.sys**します。 **sysjobschedules** 20 分ごとに更新をスケジュールします。 これは、このストアドプロシージャによって返される値に影響を与える可能性があります。  
  
## <a name="remarks"></a>解説  
 **Sp_help_jobschedule**のパラメーターは、特定の組み合わせでのみ使用できます。 *Schedule_id*が指定されている場合、 *job_id*も*job_name*も指定できません。 それ以外の場合は、 *job_id* パラメーターまたは *job_name* パラメーターを *schedule_name*と共に使用できます。  
  
## <a name="permissions"></a>アクセス許可  
 **sysadmin** 固定サーバー ロールのメンバーシップが必要です。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
 **SQLAgentUserRole**のメンバーは、自分が所有するジョブスケジュールのプロパティのみを表示できます。  
  
## <a name="examples"></a>例  
  
### <a name="a-returning-the-job-schedule-for-a-specific-job"></a>A. 特定のジョブのジョブ スケジュールを返す  
 次の例では、という名前のジョブのスケジュール情報が返され `BackupDatabase` ます。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobschedule  
    @job_name = N'BackupDatabase' ;  
GO  
```  
  
### <a name="b-returning-the-job-schedule-for-a-specific-schedule"></a>B. 特定のスケジュールのジョブスケジュールを返す  
 次の例では、`NightlyJobs` という名前のスケジュールと、`RunReports` という名前のジョブの情報を返します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobschedule   
    @job_name = N'RunReports',  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
### <a name="c-returning-the-job-schedule-and-schedule-description-for-a-specific-schedule"></a>C. 特定のスケジュールのジョブスケジュールとスケジュールの説明を返す  
 次の例では、`NightlyJobs` という名前のスケジュールと、`RunReports` という名前のジョブの情報を返します。 返される結果セットには、スケジュールの説明が含まれます。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobschedule  
    @job_name = N'RunReports',  
    @schedule_name = N'NightlyJobs',  
    @include_description = 1 ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_add_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_update_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
