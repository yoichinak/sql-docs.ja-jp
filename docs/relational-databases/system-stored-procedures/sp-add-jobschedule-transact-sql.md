---
description: sp_add_jobschedule (Transact-SQL)
title: sp_add_jobschedule (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 07/28/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_jobschedule
- sp_add_jobschedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_jobschedule
ms.assetid: ffce19d9-d1d6-45b4-89fd-ad0f60822ba0
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b474931aad2958a4ddba3bccb20773e7f36fd0e7
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753824"
---
# <a name="sp_add_jobschedule-transact-sql"></a>sp_add_jobschedule (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  SQL エージェントジョブのスケジュールを作成します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
  > [!IMPORTANT]  
  > 現在、[Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance) によって、すべてではありませんが、ほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、[Azure SQL Managed Instance と SQL Server の T-SQL の相違点](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)に関するページを参照してください。

## <a name="syntax"></a>構文  
  
```  
  
sp_add_jobschedule [ @job_id = ] job_id, | [ @job_name = ] 'job_name', [ @name = ] 'name'  
     [ , [ @enabled = ] enabled_flag ]  
     [ , [ @freq_type = ] frequency_type ]  
     [ , [ @freq_interval = ] frequency_interval ]  
     [ , [ @freq_subday_type = ] frequency_subday_type ]  
     [ , [ @freq_subday_interval = ] frequency_subday_interval ]  
     [ , [ @freq_relative_interval = ] frequency_relative_interval ]  
     [ , [ @freq_recurrence_factor = ] frequency_recurrence_factor ]  
     [ , [ @active_start_date = ] active_start_date ]  
     [ , [ @active_end_date = ] active_end_date ]  
     [ , [ @active_start_time = ] active_start_time ]  
     [ , [ @active_end_time = ] active_end_time ]  
     [ , [ @schedule_id = ] schedule_id OUTPUT ]
     [ , [ @schedule_uid = ] _schedule_uid OUTPUT ]
```  
  
## <a name="arguments"></a>引数  
`[ @job_id = ] job_id` スケジュールを追加するジョブの識別番号を指定します。 *job_id* は **uniqueidentifier**,、既定値はありません。  
  
`[ @job_name = ] 'job_name'` スケジュールを追加するジョブの名前。 *job_name* は **nvarchar (128)**,、既定値はありません。  
  
> [!NOTE]  
>  *Job_id*または*job_name*のいずれかを指定する必要がありますが、両方を指定することはできません。  
  
`[ @name = ] 'name'` スケジュールの名前。 *名前* は **nvarchar (128)**,、既定値はありません。  
  
`[ @enabled = ] enabled_flag` スケジュールの現在の状態を示します。 *enabled_flag* は **tinyint**,、既定値は **1** (有効) です。 **0**の場合、スケジュールは有効になりません。 スケジュールを無効にすると、ジョブは実行されません。  
  
`[ @freq_type = ] frequency_type` ジョブがいつ実行されるかを示す値。 *frequency_type* は **int**,、既定値は **0**,、値は次のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**1**|1 度|  
|**4**|毎日|  
|**8**|週次|  
|**16**|月単位|  
|**32**|毎月、frequency_interval を基準と *します。*|  
|**64**|エージェントサービスが開始されたときに実行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。|  
|**128**|コンピューターがアイドル状態のときに実行します。|  
  
`[ @freq_interval = ] frequency_interval` ジョブが実行された日。 *frequency_interval* は **int**で、既定値は0です。次の表に示すように、 *frequency_type* の値に依存します。  
  
|値|結果|  
|-----------|------------|  
|**1** (1 回)|*frequency_interval* は使用されていません。|  
|**4** (毎日)|*Frequency_interval*日ごと。|  
|**8** (毎週)|*frequency_interval* は次の1つまたは複数です (or 論理演算子と組み合わせて使用します)。<br /><br /> 1 = 日曜日<br /><br /> 2 = 月曜日<br /><br /> 4 = 火曜日<br /><br /> 8 = 水曜日<br /><br /> 16 = 木曜日<br /><br /> 32 = 金曜日<br /><br /> 64 = 土曜日|  
|**16** (毎月)|月の *frequency_interval* 日。|  
|**32** (月単位)|*frequency_interval* は次のいずれかです。<br /><br /> 1 = 日曜日<br /><br /> 2 = 月曜日<br /><br /> 3 = 火曜日<br /><br /> 4 = 水曜日<br /><br /> 5 = 木曜日<br /><br /> 6 = 金曜日<br /><br /> 7 = 土曜日<br /><br /> 8 = 日<br /><br /> 9 = 平日<br /><br /> 10 = 週末|  
|**64** (エージェントサービスが開始されたとき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] )|*frequency_interval* は使用されていません。|  
|**128**|*frequency_interval* は使用されていません。|  
  
`[ @freq_subday_type = ] frequency_subday_type`*Frequency_subday_interval*の単位を指定します。 *frequency_subday_type* は **int**,、既定値はありませんは、次のいずれかの値を指定します。  
  
|値|説明 (単位)|  
|-----------|--------------------------|  
|**0x1**|指定された時間|  
|**0x4**|分|  
|**0x8**|時間|  
  
`[ @freq_subday_interval = ] frequency_subday_interval` ジョブの各実行間に発生する *frequency_subday_type* 期間の数。 *frequency_subday_interval* は **int**,、既定値は0です。  
  
`[ @freq_relative_interval = ] frequency_relative_interval`*Frequency_type*が**32** (月単位) に設定されている場合に、 *frequency_interval*をさらに定義します。  
  
 *frequency_relative_interval* は **int**,、既定値はありませんは、次のいずれかの値を指定します。  
  
|値|説明 (単位)|  
|-----------|--------------------------|  
|**1**|First|  
|**2**|Second|  
|**4**|Third|  
|**8**|4 番目|  
|**16**|Last (最後へ)|  
  
 *frequency_relative_interval* は、間隔の発生を示します。 たとえば、 *frequency_relative_interval* が **2**に設定され、 *frequency_type* が **32**に設定され、 *frequency_interval* が **3**に設定されている場合、スケジュールされたジョブは毎月第2火曜日に発生します。  
  
`[ @freq_recurrence_factor = ] frequency_recurrence_factor` スケジュールされたジョブの実行間隔 (週単位または月単位)。 *frequency_recurrence_factor* は、 *frequency_type* が **8**、 **16**、または **32**に設定されている場合にのみ使用されます。 *frequency_recurrence_factor* は **int**,、既定値は0です。  
  
`[ @active_start_date = ] active_start_date` ジョブの実行を開始できる日付。 *active_start_date* は **int**,、既定値はありません。 日付の形式は YYYYMMDD です。 *Active_start_date*が設定されている場合、日付は19900101以上である必要があります。  
  
 スケジュールを作成したら、開始日を確認し、正しい日付であることを確認します。 詳細については、「 [ジョブにスケジュールを作成してアタッチする](../../ssms/agent/create-and-attach-schedules-to-jobs.md)」の「開始日のスケジュール設定」を参照してください。  
  
`[ @active_end_date = ] active_end_date` ジョブの実行を停止できる日付。 *active_end_date* は **int**,、既定値はありません。 日付の形式は YYYYMMDD です。  
  
`[ @active_start_time = ] active_start_time`*Active_start_date*から*active_end_date*までの任意の日にジョブの実行を開始する時刻。 *active_start_time* は **int**,、既定値はありません。 時刻は、24時間制の HHMMSS 形式に設定されます。  
  
`[ @active_end_time = active_end_time_`*Active_start_date*から*active_end_date*までの任意の日にジョブの実行を終了する時刻。 *active_end_time* は **int**,、既定値はありません。 時刻は、24時間制の HHMMSS 形式に設定されます。  
  
`[ @schedule_id = schedule_idOUTPUT` スケジュールが正常に作成された場合に、スケジュールに割り当てられた識別番号を指定します。 *schedule_id* は **int**型の出力変数で、既定値はありません。  
  
`[ @schedule_uid = ] _schedule_uidOUTPUT` スケジュールの一意の識別子。 *schedule_uid* は、 **uniqueidentifier**型の変数です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 ジョブスケジュールをジョブとは別に管理できるようになりました。 ジョブにスケジュールを追加するには、 **sp_add_schedule** を使用してスケジュールを作成し、 **sp_attach_schedule** してスケジュールをジョブにアタッチします。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、このストアド プロシージャを実行できるのは、 **sysadmin** 固定サーバー ロールのメンバーです。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
 
 ## <a name="example"></a>例
 次の例では、毎週土曜日の 2:00 AM に実行するジョブスケジュールをに割り当て `SaturdayReports` ます。
```sql  
EXEC msdb.dbo.sp_add_jobschedule 
        @job_name = N'SaturdayReports', -- Job name
        @name = N'Weekly_Sat_2AM',  -- Schedule name
        @freq_type = 8, -- Weekly
        @freq_interval = 64, -- Saturday
        @freq_recurrence_factor = 1, -- every week
        @active_start_time = 20000 -- 2:00 AM
```
  
## <a name="see-also"></a>参照  
 [スケジュールを作成してジョブにアタッチする](../../ssms/agent/create-and-attach-schedules-to-jobs.md)   
 [ジョブのスケジュール設定](../../ssms/agent/schedule-a-job.md)   
 [スケジュールを作成する](../../ssms/agent/create-a-schedule.md)   
 [Transact-sql&#41;&#40;のストアドプロシージャの SQL Server エージェント ](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_update_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_help_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
