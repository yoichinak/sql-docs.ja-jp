---
description: sp_help_jobstep (Transact-sql)
title: sp_help_jobstep (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobstep_TSQL
- sp_help_jobstep
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobstep
ms.assetid: 4a13b804-45f2-4f82-987f-42d9a57dd6db
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 24ec19dc231ce2fedf3a3562312ddc0bf7311e39
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535246"
---
# <a name="sp_help_jobstep-transact-sql"></a>sp_help_jobstep (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  エージェントサービスが自動化された活動を実行するために使用するジョブのステップに関する情報を返し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_jobstep { [ @job_id = ] 'job_id' | [ @job_name = ] 'job_name' }  
     [ , [ @step_id = ] step_id ]   
     [ , [ @step_name = ] 'step_name' ]   
     [ , [ @suffix = ] suffix ]   
```  
  
## <a name="arguments"></a>引数  
`[ @job_id = ] 'job_id'` ジョブ情報を返すジョブの識別番号を指定します。 *job_id* は **uniqueidentifier**,、既定値は NULL です。  
  
`[ @job_name = ] 'job_name'` ジョブの名前。 *job_name* は **sysname**で、既定値は NULL です。  
  
> [!NOTE]  
>  *Job_id*または*job_name*のいずれかを指定する必要がありますが、両方を指定することはできません。  
  
`[ @step_id = ] step_id` ジョブのステップの識別番号を指定します。 含まれていない場合は、ジョブのすべての手順が含まれます。 *step_id* は **int**,、既定値は NULL です。  
  
`[ @step_name = ] 'step_name'` ジョブのステップの名前。 *step_name* は **sysname**,、既定値は NULL です。  
  
`[ @suffix = ] suffix` 出力の **flags** 列にテキストの説明を追加するかどうかを示すフラグです。 *サフィックス*は **ビット**,、既定値は **0**です。 *サフィックス*が**1**の場合は、説明が追加されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**step_id**|**int**|ステップの一意識別子。|  
|**step_name**|**sysname**|ジョブのステップの名前。|  
|**サブ**|**nvarchar(40)**|ステップ コマンドを実行するサブシステム。|  
|**command**|**nvarchar(max)**|コマンドを実行します。|  
|**flags**|**int**|ステップの動作を制御する値のビットマスク。|  
|**cmdexec_success_code**|**int**|**CmdExec**ステップの場合、これは成功したコマンドのプロセス終了コードです。|  
|**on_success_action**|**tinyint**|ステップが成功した場合に実行するアクション:<br /><br /> **1** = 成功を報告するジョブを終了します。<br /><br /> **2** = エラーを報告するジョブを終了します。<br /><br /> **3** = 次の手順に進みます。<br /><br /> **4** = ステップに進みます。|  
|**on_success_step_id**|**int**|**On_success_action**が4の場合は、次に実行する手順を示します。|  
|**on_fail_action**|**tinyint**|ステップが失敗した場合の対処方法。 値は **on_success_action**と同じです。|  
|**on_fail_step_id**|**int**|**On_fail_action**が4の場合は、次に実行する手順を示します。|  
|**server**|**sysname**|予約済み。|  
|**database_name**|**sysname**|[!INCLUDE[tsql](../../includes/tsql-md.md)] ステップの場合は、コマンドを実行するデータベース。|  
|**database_user_name**|**sysname**|[!INCLUDE[tsql](../../includes/tsql-md.md)] ステップの場合は、コマンドを実行するデータベース ユーザー コンテキスト。|  
|**retry_attempts**|**int**|正常に実行できない場合にコマンドを再試行する最大回数。|  
|**retry_interval**|**int**|再試行の間隔 (分)。|  
|**os_run_priority**|**int**|予約済み。|  
|**output_file_name**|**nvarchar(200)**|コマンドの出力の書き込み先のファイル ( [!INCLUDE[tsql](../../includes/tsql-md.md)] 、 **CmdExec**、および **PowerShell** の手順のみ)。|  
|**last_run_outcome**|**int**|最後に実行したときのステップの結果。<br /><br /> **0** = 失敗<br /><br /> **1** = 成功<br /><br /> **2** = 再試行<br /><br /> **3** = キャンセル<br /><br /> **5** = 不明|  
|**last_run_duration**|**int**|最後に実行されたときのステップの期間 (hhmmss)。|  
|**last_run_retries**|**int**|最後にステップを実行したときにコマンドが再試行された回数。|  
|**last_run_date**|**int**|ステップの実行を最後に開始した日付。|  
|**last_run_time**|**int**|ステップの実行を最後に開始した時刻。|  
|**proxy_id**|**int**|ジョブステップのプロキシ。|  
  
## <a name="remarks"></a>解説  
 **sp_help_jobstep** は **msdb** データベースにあります。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、 **sysadmin** 固定サーバーロールのメンバーは、このストアドプロシージャを実行できます。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
 **SQLAgentUserRole**のメンバーは、自分が所有しているジョブのジョブステップのみを表示できます。  
  
## <a name="examples"></a>例  
  
### <a name="a-return-information-for-all-steps-in-a-specific-job"></a>A. 特定のジョブのすべてのステップに関する情報を返す  
 次の例では、`Weekly Sales Data Backup` という名前のジョブに関する、すべてのジョブ ステップを返します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobstep  
    @job_name = N'Weekly Sales Data Backup' ;  
GO  
```  
  
### <a name="b-return-information-about-a-specific-job-step"></a>B. 特定のジョブステップに関する情報を返す  
 次の例では、という名前のジョブの最初のジョブステップに関する情報を返し `Weekly Sales Data Backup` ます。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobstep  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 1 ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_add_jobstep &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)   
 [sp_delete_jobstep &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_help_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_update_jobstep &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
