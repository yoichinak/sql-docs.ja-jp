---
description: sp_add_schedule (Transact-SQL)
title: sp_add_schedule (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_schedule_TSQL
- sp_add_schedule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_schedule
ms.assetid: 9060aae3-3ddd-40a5-83bb-3ea7ab1ffbd7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ee456f7be6d59ded32a67908d69bf59028e931c6
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753838"
---
# <a name="sp_add_schedule-transact-sql"></a>sp_add_schedule (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  任意の数のジョブで使用できるスケジュールを作成します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_add_schedule [ @schedule_name = ] 'schedule_name'   
    [ , [ @enabled = ] enabled ]  
    [ , [ @freq_type = ] freq_type ]  
    [ , [ @freq_interval = ] freq_interval ]   
    [ , [ @freq_subday_type = ] freq_subday_type ]   
    [ , [ @freq_subday_interval = ] freq_subday_interval ]   
    [ , [ @freq_relative_interval = ] freq_relative_interval ]   
    [ , [ @freq_recurrence_factor = ] freq_recurrence_factor ]   
    [ , [ @active_start_date = ] active_start_date ]   
    [ , [ @active_end_date = ] active_end_date ]   
    [ , [ @active_start_time = ] active_start_time ]   
    [ , [ @active_end_time = ] active_end_time ]   
    [ , [ @owner_login_name = ] 'owner_login_name' ]  
    [ , [ @schedule_uid = ] schedule_uid OUTPUT ]  
    [ , [ @schedule_id = ] schedule_id OUTPUT ]
    [ , [ @originating_server = ] server_name ] /* internal */  
```  
  
## <a name="arguments"></a>引数  
`[ @schedule_name = ] 'schedule_name'` スケジュールの名前を指定します。 *schedule_name* は **sysname**であり、既定値はありません。  
  
`[ @enabled = ] enabled` スケジュールの現在の状態を示します。 *有効* になっているは **tinyint**,、既定値は **1** (有効) です。 **0**の場合、スケジュールは有効になりません。 スケジュールが有効になっていない場合、このスケジュールでジョブは実行されません。  
  
`[ @freq_type = ] freq_type` ジョブがいつ実行されるかを示す値です。 *freq_type* は **int**,、既定値は **0**,、これらの値のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**1**|1 度|  
|**4**|毎日|  
|**8**|週次|  
|**16**|月単位|  
|**32**|毎月 ( *freq_interval*を基準)|  
|**64**|SQL エージェントサービスの開始時に実行する|  
|**128**|コンピューターがアイドル状態のときに実行する ( [AZURE SQL Managed Instance](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)ではサポートされていません) |  
  
`[ @freq_interval = ] freq_interval` ジョブを実行する曜日。 *freq_interval* は **int**,、既定値は **1**,、 *freq_type*の値に依存します。  
  
|*Freq_type*の値|*Freq_interval*への影響|  
|---------------------------|--------------------------------|  
|**1** (1 回)|*freq_interval* は使用されていません。|  
|**4** (毎日)|*Freq_interval*日ごと。|  
|**8** (毎週)|*freq_interval* は次の1つまたは複数です (or 論理演算子と組み合わせて使用します)。<br /><br /> **1** = 日曜日<br /><br /> **2** = 月曜日<br /><br /> **4** = 火曜日<br /><br /> **8** = 水曜日<br /><br /> **16** = 木曜日<br /><br /> **32** = 金曜日<br /><br /> **64** = 土曜日|  
|**16** (毎月)|月の *freq_interval* 日。|  
|**32** (月単位)|*freq_interval* は次のいずれかです。<br /><br /> **1** = 日曜日<br /><br /> **2** = 月曜日<br /><br /> **3** = 火曜日<br /><br /> **4** = 水曜日<br /><br /> **5** = 木曜日<br /><br /> **6** = 金曜日<br /><br /> **7** = 土曜日<br /><br /> **8** = 日<br /><br /> **9** = 平日<br /><br /> **10** = 週末|  
|**64** (SQLServerAgent サービスの開始時)|*freq_interval* は使用されていません。|  
|**128**|*freq_interval* は使用されていません。|  
  
`[ @freq_subday_type = ] freq_subday_type`*Freq_subday_interval*の単位を指定します。 *freq_subday_type* は **int**,、既定値は **0**,、これらの値のいずれかを指定することができます。  
  
|値|説明 (単位)|  
|-----------|--------------------------|  
|**0x1**|指定された時間|  
|**0x2**|Seconds|  
|**0x4**|分|  
|**0x8**|時間|  
  
`[ @freq_subday_interval = ] freq_subday_interval` ジョブの各実行間に発生する *freq_subday_type* 期間の数。 *freq_subday_interval* は **int**,、既定値は **0**です。 注: 間隔は10秒より長くする必要があります。 *freq_subday_type*が**1**に等しい場合、 *freq_subday_interval*は無視されます。  
  
`[ @freq_relative_interval = ] freq_relative_interval`*Freq_interval*が 32 (月単位) の場合、各月における*freq_interval*のジョブの発生回数。 *freq_relative_interval* は **int**,、既定値は **0**,、これらの値のいずれかを指定することができます。 *freq_type*が32と等しくない場合、 *freq_relative_interval*は無視されます。  
  
|値|説明 (単位)|  
|-----------|--------------------------|  
|**1**|First|  
|**2**|Second|  
|**4**|Third|  
|**8**|4 番目|  
|**16**|Last (最後へ)|  
  
`[ @freq_recurrence_factor = ] freq_recurrence_factor` ジョブのスケジュールされた実行の間隔を週または月単位で指定します。 *freq_recurrence_factor* は *freq_type* が **8**、 **16**、または **32**の場合にのみ使用されます。 *freq_recurrence_factor* は **int**,、既定値は **0**です。  
  
`[ @active_start_date = ] active_start_date` ジョブの実行を開始できる日付。 *active_start_date* のデータ **型は int**で、既定値は NULL です。これは今日の日付を示します。 日付の形式は YYYYMMDD です。 *Active_start_date*が NULL でない場合、日付は19900101以上である必要があります。  
  
 スケジュールを作成したら、開始日を確認し、正しい日付であることを確認します。 詳細については、「 [ジョブにスケジュールを作成してアタッチする](../../ssms/agent/create-and-attach-schedules-to-jobs.md)」の「開始日のスケジュール設定」を参照してください。  
  
 週単位または月単位のスケジュールでは、エージェントは active_start_date が過去の場合は無視し、代わりに現在の日付を使用します。 Sp_add_schedule を使用して SQL エージェントのスケジュールを作成する場合は、ジョブの実行が開始される日付 active_start_date パラメーターを指定するオプションがあります。 スケジュールの種類が週単位または月単位で、active_start_date パラメーターが過去の日付に設定されている場合、active_start_date パラメーターは無視され、現在の日付が active_start_date に使用されます。  
  
`[ @active_end_date = ] active_end_date` ジョブの実行を停止できる日付。 *active_end_date* は **int**,、既定値は **99991231**,、9999年12月31日を示します。 YYYYMMDD として書式設定されます。  
  
`[ @active_start_time = ] active_start_time`*Active_start_date*から*active_end_date*までの任意の日にジョブの実行を開始する時刻。 *active_start_time* は **int**,、既定値は **000000**,、12:00:00 A.M. を示す を 24 時間形式で表したものです。HHMMSS 形式で入力する必要があります。  
  
`[ @active_end_time = ] active_end_time`*Active_start_date*から*active_end_date*までの任意の日にジョブの実行を終了する時刻。 *active_end_time* は **int**,、既定値は **235959**,、11:59:59 pm を示す を 24 時間形式で表したものです。HHMMSS 形式で入力する必要があります。  
  
`[ @owner_login_name = ] 'owner_login_name'` スケジュールを所有するサーバープリンシパルの名前。 *owner_login_name* は **sysname**で、既定値は NULL です。これは、スケジュールが作成者によって所有されていることを示します。  
  
`[ @schedule_uid = ] _schedule_uidOUTPUT` スケジュールの一意の識別子。 *schedule_uid* は、 **uniqueidentifier**型の変数です。  
  
`[ @schedule_id = ] _schedule_idOUTPUT` スケジュールの識別子。 *schedule_id* は **int**型の変数です。  
  
`[ @originating_server = ] server_name` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] は、ジョブを簡単に管理できるグラフィカルなツールです。ジョブのインフラストラクチャを作成し、管理するには、このツールを使用することをお勧めします。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、このストアド プロシージャを実行できるのは、 **sysadmin** 固定サーバー ロールのメンバーです。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
## <a name="examples"></a>例  
  
### <a name="a-creating-a-schedule"></a>A. スケジュールを作成する  
 次の例では、という名前のスケジュールを作成し `RunOnce` ます。 スケジュールは 1 回のみ、スケジュールが作成された日の `23:30` に実行されます。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_schedule  
    @schedule_name = N'RunOnce',  
    @freq_type = 1,  
    @active_start_time = 233000 ;  
  
GO  
```  
  
### <a name="b-creating-a-schedule-attaching-the-schedule-to-multiple-jobs"></a>B. スケジュールを作成し、複数のジョブにスケジュールをアタッチする  
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
 [スケジュールを作成してジョブにアタッチする](../../ssms/agent/create-and-attach-schedules-to-jobs.md)   
 [ジョブのスケジュール設定](../../ssms/agent/schedule-a-job.md)   
 [スケジュールを作成する](../../ssms/agent/create-a-schedule.md)   
 [Transact-sql&#41;&#40;のストアドプロシージャの SQL Server エージェント ](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_jobschedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql.md)   
 [sp_update_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_help_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
