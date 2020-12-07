---
description: sp_help_jobserver (Transact-sql)
title: sp_help_jobserver (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobserver
- sp_help_jobserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobserver
ms.assetid: 57971787-f9f5-4199-9f64-c2b61a308906
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7e59691a44353826f47550bb67c7a7872fcc4200
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546099"
---
# <a name="sp_help_jobserver-transact-sql"></a>sp_help_jobserver (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定されたジョブのサーバーに関する情報を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_jobserver  
     { [ @job_id = ] job_id   
     | [ @job_name = ] 'job_name' }  
     [ , [ @show_last_run_details = ] show_last_run_details ]  
```  
  
## <a name="arguments"></a>引数  
`[ @job_id = ] job_id` 情報を返すジョブの識別番号を指定します。 *job_id* は **uniqueidentifier**,、既定値は NULL です。  
  
`[ @job_name = ] 'job_name'` 情報を返すジョブの名前を指定します。 *job_name* は **sysname**,、既定値は NULL です。  
  
> [!NOTE]  
>  *Job_id*または*job_name*のいずれかを指定する必要がありますが、両方を指定することはできません。  
  
`[ @show_last_run_details = ] show_last_run_details` 最後に実行された実行情報が結果セットに含まれるかどうかを示します。 *show_last_run_details* は **tinyint**,、既定値は **0**です。 **0** には最後の実行情報は含まれず、 **1** はです。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|対象サーバーの識別番号。|  
|**server_name**|**nvarchar(30)**|対象サーバーのコンピューター名。|  
|**enlist_date**|**datetime**|対象サーバーをマスターサーバーに参加させた日付。|  
|**last_poll_date**|**datetime**|対象サーバーが最後にマスターサーバーをポーリングした日付。|  
  
 *Show_last_run_details*を**1**に設定して**sp_help_jobserver**を実行した場合、結果セットにはこれらの列が追加されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**last_run_date**|**int**|ターゲット サーバーでジョブの実行を最後に開始した日付。|  
|**last_run_time**|**int**|このサーバーでジョブの実行を最後に開始した時刻。|  
|**last_run_duration**|**int**|対象サーバーで最後に実行されたジョブの期間 (秒単位)。|  
|**last_outcome_message**|**nvarchar(1024)**|ジョブの最終結果を説明します。|  
|**last_run_outcome**|**int**|このサーバーで最後に実行されたときのジョブの結果:<br /><br /> **0** = 失敗<br /><br /> **1** = 成功<br /><br /> **3** = キャンセル<br /><br /> **5** = 不明|  
  
## <a name="permissions"></a>アクセス許可  
 既定では、 **sysadmin** 固定サーバーロールのメンバーは、このストアドプロシージャを実行できます。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
 **SQLAgentUserRole**のメンバーは、自分が所有しているジョブの情報のみを表示できます。  
  
## <a name="examples"></a>例  
 次の例では、ジョブに関する情報 (最終実行情報を含む) が返され `NightlyBackups` ます。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobserver  
    @job_name = N'NightlyBackups',  
    @show_last_run_details = 1 ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_add_jobserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_delete_jobserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
