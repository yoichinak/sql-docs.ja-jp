---
description: sp_help_schedule (Transact-sql)
title: sp_help_schedule (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_schedule
- sp_help_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_schedule
ms.assetid: b2fc4ce1-0a8e-44d2-b206-7dc7b258d8c9
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9e6dbddc56d00732495bce71b7c05c79f76adb20
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538818"
---
# <a name="sp_help_schedule-transact-sql"></a>sp_help_schedule (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  スケジュールに関する情報を一覧表示します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_schedule   
     [ @schedule_id = ] id ,  
     [ @schedule_name = ] 'schedule_name'   
     [ , [ @attached_schedules_only = ] attached_schedules_only ]  
     [ , [ @include_description = ] include_description ]  
```  
  
## <a name="arguments"></a>引数  
`[ @schedule_id = ] id` 一覧表示するスケジュールの識別子を設定します。 *schedule_name* は **int**,、既定値はありません。 *Schedule_id*または*schedule_name*のいずれかを指定できます。  
  
`[ @schedule_name = ] 'schedule_name'` 一覧表示するスケジュールの名前を指定します。 *schedule_name* は **sysname**であり、既定値はありません。 *Schedule_id*または*schedule_name*のいずれかを指定できます。  
  
`[ @attached_schedules_only = ] attached_schedules_only ]` ジョブがアタッチされているスケジュールのみを表示するかどうかを指定します。 *attached_schedules_only* は **ビット**,、既定値は **0**です。 *Attached_schedules_only*が**0**の場合、すべてのスケジュールが表示されます。 *Attached_schedules_only*が**1**の場合、結果セットには、ジョブにアタッチされているスケジュールのみが含まれます。  
  
`[ @include_description = ] include_description` 結果セットに説明を含めるかどうかを指定します。 *include_description* は **ビット**,、既定値は **0**です。 *Include_description*が**0**の場合、結果セットの*schedule_description*列にはプレースホルダーが含まれます。 *Include_description*が**1**の場合、スケジュールの説明が結果セットに含まれます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 このプロシージャは、次の結果セットを返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|スケジュールの識別子番号。|  
|**schedule_uid**|**uniqueidentifier**|スケジュールの識別子。|  
|**schedule_name**|**sysname**|スケジュールの名前。|  
|**有効**|**int**|スケジュールが有効になっている (**1**) か、有効でない (**0**) かを指定します。|  
|**freq_type**|**int**|ジョブをいつ実行するかを示す値。<br /><br /> **1** = 1 回<br /><br /> **4** = 日単位<br /><br /> **8** = 週単位<br /><br /> **16** = 月単位<br /><br /> **32** = 毎月、 **freq_interval**に対して相対的<br /><br /> **64** = SQLServerAgent サービスの開始時に実行します。|  
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
|**schedule_description**|**nvarchar (4000)**|スケジュールの英語の説明 (要求された場合)。|  
|**job_count**|**int**|このスケジュールを参照するジョブの数を返します。|  
  
## <a name="remarks"></a>解説  
 パラメーターを指定しない場合、 **sp_help_schedule** インスタンス内のすべてのスケジュールに関する情報が一覧表示されます。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、 **sysadmin** 固定サーバーロールのメンバーは、このストアドプロシージャを実行できます。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
 **SQLAgentUserRole**のメンバーは、自分が所有しているスケジュールのみを表示できます。  
  
## <a name="examples"></a>例  
  
### <a name="a-listing-information-for-all-schedules-in-the-instance"></a>A. インスタンスのすべてのスケジュールに関する情報を一覧表示する  
 次の例では、インスタンスのすべてのスケジュールに関する情報を一覧表示します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_schedule ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-schedule"></a>B. 特定のスケジュールの情報を一覧表示する  
 次の例では、`NightlyJobs` というスケジュールに関する情報を一覧表示します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_schedule  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_add_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_detach_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)  
  
  
