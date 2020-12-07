---
description: sp_help_jobs_in_schedule (Transact-sql)
title: sp_help_jobs_in_schedule (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobs_in_schedule_TSQL
- sp_help_jobs_in_schedule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobs_in_schedule
ms.assetid: 1168aa2c-136b-4ba3-b18e-9070d95a26fa
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9d8a9251e807be429bfb0881afc711880520f9f7
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538855"
---
# <a name="sp_help_jobs_in_schedule-transact-sql"></a>sp_help_jobs_in_schedule (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  特定のスケジュールがアタッチされているジョブに関する情報を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_jobs_in_schedule   
     [ @schedule_name = ] 'schedule_name' ,  
     [ @schedule_id = ] schedule_id   
```  
  
## <a name="arguments"></a>引数  
`[ @schedule_id = ] schedule_id` 情報を一覧表示するスケジュールの識別子を設定します。 *schedule_id* は **int**,、既定値はありません。 *Schedule_id*または*schedule_name*のいずれかを指定できます。  
  
`[ @schedule_name = ] 'schedule_name'` 情報を一覧表示するスケジュールの名前を指定します。 *schedule_name* は **sysname**であり、既定値はありません。 *Schedule_id*または*schedule_name*のいずれかを指定できます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 次の結果セットを返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|ジョブの一意の ID。|  
|**originating_server**|**nvarchar(30)**|ジョブの送信元のサーバーの名前。|  
|**name**|**sysname**|ジョブの名前。|  
|**有効**|**tinyint**|ジョブの実行が有効かどうかを示します。|  
|**description**|**nvarchar(512)**|ジョブの説明。|  
|**start_step_id**|**int**|実行を開始するジョブのステップの ID。|  
|**category**|**sysname**|ジョブ カテゴリ。|  
|**責任**|**sysname**|ジョブ所有者。|  
|**notify_level_eventlog**|**int**|どのような場合に、通知イベントを Microsoft Windows アプリケーションログに記録するかを示すビットマスク。 次のいずれかの値を指定します。<br /><br /> **0** = なし<br /><br /> **1** = ジョブが成功した場合<br /><br /> **2** = ジョブが失敗したとき<br /><br /> **3** = ジョブが完了するたびに (ジョブの結果に関係なく)|  
|**notify_level_email**|**int**|どのような場合に、ジョブの完了時に通知電子メールを送信するのかを示すビットマスク。 指定できる値は、 **notify_level_eventlog**の場合と同じです。|  
|**notify_level_netsend**|**int**|どのような場合に、ジョブの完了時にネットワーク メッセージを送信するのかを示すビットマスク。 指定できる値は、 **notify_level_eventlog**の場合と同じです。|  
|**notify_level_page**|**int**|どのような場合に、ジョブの完了時にページを送信するのかを示すビットマスク。 指定できる値は、 **notify_level_eventlog**の場合と同じです。|  
|**notify_email_operator**|**sysname**|通知するオペレーターの電子メール名。|  
|**notify_netsend_operator**|**sysname**|ネットワークメッセージを送信するときに使用するコンピューターまたはユーザーの名前。|  
|**notify_page_operator**|**sysname**|ページを送信するときに使用するコンピューターまたはユーザーの名前。|  
|**delete_level**|**int**|どのような場合に、ジョブの完了時にジョブを削除するかを示すビットマスク。 指定できる値は、 **notify_level_eventlog**の場合と同じです。|  
|**date_created**|**datetime**|ジョブが作成された日付。|  
|**date_modified**|**datetime**|ジョブが最後に変更された日付。|  
|**version_number**|**int**|ジョブのバージョン (ジョブを変更するたびに自動的に更新されます)。|  
|**last_run_date**|**int**|ジョブの実行を最後に開始した日付。|  
|**last_run_time**|**int**|ジョブの実行を最後に開始した時刻。|  
|**last_run_outcome**|**int**|最後に実行したときのジョブの結果:<br /><br /> **0** = 失敗<br /><br /> **1** = 成功<br /><br /> **3** = キャンセル<br /><br /> **5** = 不明|  
|**next_run_date**|**int**|ジョブが次に実行されるようにスケジュールされている日付。|  
|**next_run_time**|**int**|ジョブの次回実行予定時刻。|  
|**next_run_schedule_id**|**int**|次回の実行スケジュールの識別番号。|  
|**current_execution_status**|**int**|現在の実行状態です。|  
|**current_execution_step**|**sysname**|ジョブの現在の実行ステップ。|  
|**current_retry_attempt**|**int**|ジョブが実行中で、ステップが再試行されている場合は、これが現在の再試行です。|  
|**has_step**|**int**|ジョブに含まれるジョブステップの数。|  
|**has_schedule**|**int**|ジョブのジョブ スケジュール数。|  
|**has_target**|**int**|ジョブのターゲット サーバー数。|  
|**type**|**int**|ジョブの種類:<br /><br /> **1** = ローカルジョブ。<br /><br /> **2** = マルチサーバージョブ。<br /><br /> **0** = ジョブに対象サーバーがありません。|  
  
## <a name="remarks"></a>解説  
 この手順では、指定したスケジュールに関連付けられているジョブに関する情報を一覧表示します。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、 **sysadmin** 固定サーバーロールのメンバーは、このストアドプロシージャを実行できます。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
 **SQLAgentUserRole**のメンバーは、自分が所有しているジョブの状態のみを表示できます。  
  
## <a name="examples"></a>例  
 次の例では、`NightlyJobs` スケジュールにアタッチされたジョブを一覧表示します。  
  
```  
USE msdb ;  
GO  
  
EXEC sp_help_jobs_in_schedule  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のストアドプロシージャの SQL Server エージェント ](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_detach_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)  
  
  
