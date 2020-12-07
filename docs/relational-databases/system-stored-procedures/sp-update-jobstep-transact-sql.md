---
description: sp_update_jobstep (Transact-SQL)
title: sp_update_jobstep (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_jobstep
- sp_update_jobstep_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_jobstep
ms.assetid: e158802c-c347-4a5d-bf75-c03e5ae56e6b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 52b17f706b53c05074fdcb21bf5e566df3d1d165
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549504"
---
# <a name="sp_update_jobstep-transact-sql"></a>sp_update_jobstep (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  自動化された処理の実行に使用するジョブのステップに関する設定を変更します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_update_jobstep   
     {   [@job_id =] job_id   
       | [@job_name =] 'job_name' } ,  
     [@step_id =] step_id  
     [ , [@step_name =] 'step_name' ]  
     [ , [@subsystem =] 'subsystem' ]   
     [ , [@command =] 'command' ]  
     [ , [@additional_parameters =] 'parameters' ]  
     [ , [@cmdexec_success_code =] success_code ]  
     [ , [@on_success_action =] success_action ]   
     [ , [@on_success_step_id =] success_step_id ]  
     [ , [@on_fail_action =] fail_action ]   
     [ , [@on_fail_step_id =] fail_step_id ]  
     [ , [@server =] 'server' ]   
     [ , [@database_name =] 'database' ]  
     [ , [@database_user_name =] 'user' ]   
     [ , [@retry_attempts =] retry_attempts ]  
     [ , [@retry_interval =] retry_interval ]   
     [ , [@os_run_priority =] run_priority ]  
     [ , [@output_file_name =] 'file_name' ]   
     [ , [@flags =] flags ]  
     [ ,  {   [ @proxy_id = ] proxy_id   
            | [ @proxy_name = ] 'proxy_name' }   
```  
  
## <a name="arguments"></a>引数  
`[ @job_id = ] job_id` ステップが属するジョブの識別番号を指定します。 *job_id*は **uniqueidentifier**,、既定値は NULL です。 *Job_id*または*job_name*のいずれかを指定する必要がありますが、両方を指定することはできません。  
  
`[ @job_name = ] 'job_name'` ステップが属するジョブの名前です。 *job_name*は **sysname**,、既定値は NULL です。 *Job_id*または*job_name*のいずれかを指定する必要がありますが、両方を指定することはできません。  
  
`[ @step_id = ] step_id` 変更するジョブステップの識別番号を指定します。 この数を変更することはできません。 *step_id*は **int**,、既定値はありません。  
  
`[ @step_name = ] 'step_name'` ステップの新しい名前を指定します。 *step_name*は **sysname**,、既定値は NULL です。  
  
`[ @subsystem = ] 'subsystem'`*コマンド*を実行するために Microsoft SQL Server エージェントによって使用されるサブシステムです。 *サブシステム* は **nvarchar (40)**,、既定値は NULL です。  
  
`[ @command = ] 'command'`*サブシステム*を介して実行されるコマンドです。 *コマンド* は **nvarchar (max)**,、既定値は NULL です。  
  
`[ @additional_parameters = ] 'parameters'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @cmdexec_success_code = ] success_code`*コマンド*が正常に実行されたことを示すために、 **CmdExec**サブシステムコマンドによって返される値。 *success_code* は **int**,、既定値は NULL です。  
  
`[ @on_success_action = ] success_action` ステップが成功した場合に実行するアクション。*success_action* は **tinyint**,、既定値は NULL の場合、これらの値のいずれかを指定できます。  
  
|[値]|説明 (アクション)|  
|-----------|----------------------------|  
|**1**|正常に終了します。|  
|**2**|失敗した状態で終了|  
|**3**|次のステップに進む|  
|**4**|手順 success_step_id に進み *ます。*|  
  
`[ @on_success_step_id = ] success_step_id` ステップが成功し *success_action* が **4**の場合に実行する、このジョブのステップの識別番号を指定します。 *success_step_id* は **int**,、既定値は NULL です。  
  
`[ @on_fail_action = ] fail_action` ステップが失敗した場合に実行するアクション。 *fail_action* は **tinyint**,、既定値は NULL の場合、これらの値のいずれかを指定できます。  
  
|[値]|説明 (アクション)|  
|-----------|----------------------------|  
|**1**|正常に終了します。|  
|**2**|失敗した状態で終了|  
|**3**|次のステップに進む|  
|**4**|手順 *fail_step_id * * に進みます。*|  
  
`[ @on_fail_step_id = ] fail_step_id` ステップが失敗し、 *fail_action* が **4**の場合に実行する、このジョブのステップの識別番号を指定します。 *fail_step_id* は **int**,、既定値は NULL です。  
  
`[ @server = ] 'server'`[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]*サーバー*は**nvarchar (128)**,、既定値は NULL です。  
  
`[ @database_name = ] 'database'` ステップを実行するデータベースの名前です [!INCLUDE[tsql](../../includes/tsql-md.md)] 。 *データベース*は **sysname**です。 角かっこ ([]) で囲まれた名前は使用できません。 既定値は NULL です。  
  
`[ @database_user_name = ] 'user'` ステップの実行時に使用するユーザーアカウントの名前 [!INCLUDE[tsql](../../includes/tsql-md.md)] 。 *user*の部分は **sysname**で、既定値は NULL です。  
  
`[ @retry_attempts = ] retry_attempts` このステップが失敗した場合に使用する再試行回数。 *retry_attempts*は **int**,、既定値は NULL です。  
  
`[ @retry_interval = ] retry_interval` 再試行の間隔 (分) です。 *retry_interval* は **int**,、既定値は NULL です。  
  
`[ @os_run_priority = ] run_priority` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @output_file_name = ] 'file_name'` このステップの出力が保存されるファイルの名前。 *file_name* は **nvarchar (200)**,、既定値は NULL です。 このパラメーターは、[!INCLUDE[tsql](../../includes/tsql-md.md)] サブシステムまたは CmdExec サブシステム上で実行されるコマンドに対してのみ有効です。  
  
 Output_file_name を NULL に戻すには、 *output_file_name* を空の文字列 (' ') または空白文字の文字列に設定する必要がありますが、 **CHAR (32)** 関数は使用できません。 たとえば、次のように、この引数に空の文字列を設定します。  
  
 **@output_file_name = ' '**  
  
`[ @flags = ] flags` 動作を制御するオプション。 *フラグ* は **int**,、これらの値のいずれかを指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**0** (既定値)|出力ファイルを上書きします。|  
|**2**|出力ファイルに追加|  
|**4**|Transact-SQL ジョブ ステップの出力をステップ履歴に書き込む|  
|**8**|テーブルにログを書き込む (既存の履歴を上書きする)|  
|**16**|ログをテーブルに書き込む (既存の履歴に追加する)|  
  
`[ @proxy_id = ] proxy_id` ジョブステップを実行するプロキシの ID 番号を指定します。 *proxy_id* の型は **int**で、既定値は NULL です。 *Proxy_id*が指定されておらず、 *proxy_name*が指定されておらず、 *user_name*が指定されていない場合、ジョブステップはエージェントのサービスアカウントとして実行され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
`[ @proxy_name = ] 'proxy_name'` ジョブステップを実行するプロキシの名前を指定します。 *proxy_name* の型は **sysname**で、既定値は NULL です。 *Proxy_id*が指定されておらず、 *proxy_name*が指定されておらず、 *user_name*が指定されていない場合、ジョブステップはエージェントのサービスアカウントとして実行され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_update_jobstep** は、 **msdb** データベースから実行する必要があります。  
  
 ジョブ ステップを更新すると、ジョブのバージョン番号が増えます。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、 **sysadmin** 固定サーバーロールのメンバーは、このストアドプロシージャを実行できます。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
 他のユーザーが所有するジョブステップを更新できるのは、 **sysadmin** のメンバーだけです。  
  
 ジョブステップがプロキシへのアクセスを必要とする場合、ジョブステップの作成者は、そのジョブステップのプロキシへのアクセス権を持っている必要があります。 Transact-SQL を除くすべてのサブシステムでは、プロキシ アカウントが必要です。 **Sysadmin**のメンバーは、すべてのプロキシにアクセスでき、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロキシにエージェントサービスアカウントを使用できます。  
  
## <a name="examples"></a>例  
 次の例では、ジョブの最初のステップの再試行回数を変更し `Weekly Sales Data Backup` ます。 この例を実行すると、再試行回数は `10` 回になります。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_jobstep  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 1,  
    @retry_attempts = 10 ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [ジョブの表示または変更](../../ssms/agent/view-or-modify-jobs.md)   
 [sp_delete_jobstep &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_help_jobstep &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
