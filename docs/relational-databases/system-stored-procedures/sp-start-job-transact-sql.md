---
description: sp_start_job (Transact-sql)
title: sp_start_job (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_start_job
- sp_start_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_start_job
ms.assetid: 8a91df6a-eb84-4512-9a17-4a6e32a9538a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4e7a86d9ea25b4d9ae412b922cc6f36ddce27c20
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545942"
---
# <a name="sp_start_job-transact-sql"></a>sp_start_job (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]直ちにジョブを実行するようにエージェントに指示します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_start_job   
     {   [@job_name =] 'job_name'  
       | [@job_id =] job_id }  
     [ , [@error_flag =] error_flag]  
     [ , [@server_name =] 'server_name']  
     [ , [@step_name =] 'step_name']  
     [ , [@output_flag =] output_flag]  
```  
  
## <a name="arguments"></a>引数  
`[ @job_name = ] 'job_name'` 開始するジョブの名前を指定します。 *Job_id*または*job_name*のいずれかを指定する必要がありますが、両方を指定することはできません。 *job_name* は **sysname**,、既定値は NULL です。  
  
`[ @job_id = ] job_id` 開始するジョブの識別番号を指定します。 *Job_id*または*job_name*のいずれかを指定する必要がありますが、両方を指定することはできません。 *job_id* は **uniqueidentifier**,、既定値は NULL です。  
  
`[ @error_flag = ] error_flag` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @server_name = ] 'server_name'` ジョブを開始する対象サーバー。 *server_name* は **nvarchar (128)**,、既定値は NULL です。 *server_name* には、ジョブが現在対象となっている対象サーバーのいずれかを指定する必要があります。  
  
`[ @step_name = ] 'step_name'` ジョブの実行を開始するステップの名前です。 ローカルジョブにのみ適用されます。 *step_name* は **sysname**,、既定値は NULL です。  
  
`[ @output_flag = ] output_flag` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 このストアドプロシージャは **msdb** データベースにあります。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、 **sysadmin** 固定サーバーロールのメンバーは、このストアドプロシージャを実行できます。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
 **SQLAgentUserRole**と**SQLAgentReaderRole**のメンバーは、自分が所有するジョブのみを開始できます。 **Sqlagentoperatorrole**のメンバーは、他のユーザーによって所有されているものも含め、すべてのローカルジョブを開始できます。 **Sysadmin**のメンバーは、すべてのローカルジョブとマルチサーバージョブを開始できます。  
  
## <a name="examples"></a>例  
 次の例では、という名前のジョブを開始し `Weekly Sales Data Backup` ます。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_start_job N'Weekly Sales Data Backup' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_delete_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_help_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_stop_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-stop-job-transact-sql.md)   
 [sp_update_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
