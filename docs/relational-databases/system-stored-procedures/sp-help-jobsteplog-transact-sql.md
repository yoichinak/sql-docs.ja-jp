---
description: sp_help_jobsteplog (Transact-sql)
title: sp_help_jobsteplog (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobsteplog_TSQL
- sp_help_jobsteplog
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobsteplog
ms.assetid: 1a0be7b1-8f31-4b4c-aadb-586c0e00ed04
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4499ad9e2dd54e5592bd4ee9d3b22e3505e9d144
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547994"
---
# <a name="sp_help_jobsteplog-transact-sql"></a>sp_help_jobsteplog (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  特定のエージェントのジョブステップログに関するメタデータを返し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 **sp_help_jobsteplog** は実際のログを返しません。  

  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_jobsteplog { [ @job_id = ] 'job_id' | [ @job_name = ] 'job_name' }  
     [ , [ @step_id = ] step_id ]  
     [ , [ @step_name = ] 'step_name' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @job_id = ] 'job_id'` ジョブステップログ情報を返すジョブの識別番号を指定します。 *job_id* は **int**,、既定値は NULL です。  
  
`[ @job_name = ] 'job_name'` ジョブの名前。 *job_name* は **sysname**で、既定値は NULL です。  
  
> [!NOTE]  
>  *Job_id*または*job_name*のいずれかを指定する必要がありますが、両方を指定することはできません。  
  
`[ @step_id = ] step_id` ジョブのステップの識別番号を指定します。 含まれていない場合は、ジョブのすべての手順が含まれます。 *step_id* は **int**,、既定値は NULL です。  
  
`[ @step_name = ] 'step_name'` ジョブのステップの名前。 *step_name* は **sysname**,、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|ジョブの一意識別子。|  
|**job_name**|**sysname**|ジョブの名前。|  
|**step_id**|**int**|ジョブ内のステップの識別子。 たとえば、ステップがジョブの最初のステップである場合、その *step_id* は1になります。|  
|**step_name**|**sysname**|ジョブのステップの名前。|  
|**step_uid**|**uniqueidentifier**|ジョブ内のステップ (システムによって生成される) の一意の識別子。|  
|**date_created**|**datetime**|ステップが作成された日付。|  
|**date_modified**|**datetime**|ステップが最後に変更された日付。|  
|**log_size**|**float**|ジョブ ステップ ログのサイズ (MB 単位)。|  
|**出力**|**nvarchar(max)**|ジョブステップのログ出力。|  
  
## <a name="remarks"></a>解説  
 **sp_help_jobsteplog** は **msdb** データベースにあります。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、 **sysadmin** 固定サーバーロールのメンバーは、このストアドプロシージャを実行できます。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
 **SQLAgentUserRole**のメンバーは、自分が所有するジョブステップのログメタデータのみを表示できます。  
  
## <a name="examples"></a>例  
  
### <a name="a-returns-job-step-log-information-for-all-steps-in-a-specific-job"></a>A. 特定のジョブのすべてのステップに関するジョブステップログ情報を返します  
 次の例では、`Weekly Sales Data Backup` という名前のジョブに関する、すべてのジョブ ステップ ログ情報を返します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobsteplog  
    @job_name = N'Weekly Sales Data Backup' ;  
GO  
```  
  
### <a name="b-return-job-step-log-information-about-a-specific-job-step"></a>B. 特定のジョブ ステップに関するジョブ ステップ ログ情報を返す  
 次の例では、`Weekly Sales Data Backup` という名前のジョブ内にある最初のジョブ ステップに関するジョブ ステップ ログ情報を返します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobsteplog  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 1 ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_add_jobstep &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)   
 [sp_delete_jobstep &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_help_jobstep &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [sp_delete_jobstep &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_delete_jobsteplog &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobsteplog-transact-sql.md)   
 [Transact-sql&#41;&#40;のストアドプロシージャの SQL Server エージェント ](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)  
  
  
