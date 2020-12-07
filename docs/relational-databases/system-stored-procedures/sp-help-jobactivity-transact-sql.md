---
description: sp_help_jobactivity (Transact-SQL)
title: sp_help_jobactivity (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobactivity_TSQL
- sp_help_jobactivity
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobactivity
ms.assetid: d344864f-b4d3-46b1-8933-b81dec71f511
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e137d556413057b409d67c8ead14530d224241e0
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549704"
---
# <a name="sp_help_jobactivity-transact-sql"></a>sp_help_jobactivity (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブのランタイム状態に関する情報を一覧表示します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_jobactivity { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }  
     [ , [ @session_id = ] session_id ]  
```  
  
## <a name="arguments"></a>引数  
`[ @job_id = ] job_id` ジョブの識別番号を指定します。 *job_id*は **uniqueidentifier**,、既定値は NULL です。  
  
`[ @job_name = ] 'job_name'` ジョブの名前。 *job_name*は **sysname**,、既定値は NULL です。  
  
> [!NOTE]  
>  *Job_id*または*job_name*のいずれかを指定する必要がありますが、両方を指定することはできません。  
  
`[ @session_id = ] session_id` 情報を報告するセッション id。 *session_id* は **int**,、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 次の結果セットを返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|エージェントセッションの識別番号。|  
|**job_id**|**uniqueidentifier**|ジョブの識別子。|  
|**job_name**|**sysname**|ジョブの名前。|  
|**run_requested_date**|**datetime**|ジョブの実行が要求された日付。|  
|**run_requested_source**|**sysname**|ジョブを実行する要求のソース。 つぎのいずれかです。<br /><br /> **1** = スケジュールに基づいて実行<br /><br /> **2** = 警告に応答して実行する<br /><br /> **3** = スタートアップ時に実行<br /><br /> **4** = ユーザーによる実行<br /><br /> **6** = CPU のアイドルスケジュールに基づいて実行|  
|**queued_date**|**datetime**|要求がキューに登録された日付。 ジョブが直接実行された場合は NULL になります。|  
|**start_execution_date**|**datetime**|ジョブが実行可能なスレッドに割り当てられた日時。|  
|**last_executed_step_id**|**int**|最後に実行されたジョブステップのステップ ID です。|  
|**last_exectued_step_date**|**datetime**|最後にジョブ ステップを開始した日付。|  
|**stop_execution_date**|**datetime**|ジョブが停止した日付。|  
|**next_scheduled_run_date**|**datetime**|ジョブが次に実行されるようにスケジュールされている場合。|  
|**job_history_id**|**int**|ジョブ履歴テーブル内のジョブ履歴の識別子。|  
|**message**|**nvarchar(1024)**|ジョブの前回の実行中に生成されたメッセージ。|  
|**run_status**|**int**|ジョブの最後の実行から返された状態:<br /><br /> **0** = エラー失敗<br /><br /> **1** = 成功<br /><br /> **3** = キャンセル<br /><br /> **5** = 不明な状態|  
|**operator_id_emailed**|**int**|ジョブの完了時に電子メールの通知を受けたオペレーターの ID 番号。|  
|**operator_id_netsent**|**int**|ジョブの完了時に **net send** によって通知されたオペレーターの ID 番号。|  
|**operator_id_paged**|**int**|ジョブの完了時に、ポケットベルの通知を受けたオペレーターの ID 番号。|  
  
## <a name="remarks"></a>解説  
 このプロシージャでは、ジョブに関する現在の状態のスナップショットが生成されます。 返される結果は、要求が処理された時点の情報を表します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントサービスが開始されるたびに、エージェントによってセッション id が作成されます。 セッション id は、テーブル **msdb.dbo.sysのセッション**に格納されます。  
  
 *Session_id*が指定されていない場合は、最新のセッションに関する情報が一覧表示されます。  
  
 *Job_name*または*job_id*が指定されていない場合は、すべてのジョブの情報が一覧表示されます。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、 **sysadmin** 固定サーバーロールのメンバーは、このストアドプロシージャを実行できます。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
 他のユーザーが所有するジョブのアクティビティを表示できるのは、 **sysadmin** のメンバーだけです。  
  
## <a name="examples"></a>例  
 次の例では、現在のユーザーが表示する権限を持っているすべてのジョブのアクティビティを一覧表示します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobactivity ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のストアドプロシージャの SQL Server エージェント ](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)  
  
  
