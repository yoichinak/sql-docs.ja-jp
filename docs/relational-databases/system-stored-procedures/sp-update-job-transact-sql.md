---
description: sp_update_job (Transact-SQL)
title: sp_update_job (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_job
- sp_update_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_job
ms.assetid: cbdfea38-9e42-47f3-8fc8-5978b82e2623
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 494e284bb9df06094116d075979673bf2b033dea
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551200"
---
# <a name="sp_update_job-transact-sql"></a>sp_update_job (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ジョブの属性を変更します。  
  

  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_update_job [ @job_id =] job_id | [@job_name =] 'job_name'  
     [, [@new_name =] 'new_name' ]   
     [, [@enabled =] enabled ]  
     [, [@description =] 'description' ]   
     [, [@start_step_id =] step_id ]  
     [, [@category_name =] 'category' ]   
     [, [@owner_login_name =] 'login' ]  
     [, [@notify_level_eventlog =] eventlog_level ]  
     [, [@notify_level_email =] email_level ]  
     [, [@notify_level_netsend =] netsend_level ]  
     [, [@notify_level_page =] page_level ]  
     [, [@notify_email_operator_name =] 'operator_name' ]  
     [, [@notify_netsend_operator_name =] 'netsend_operator' ]  
     [, [@notify_page_operator_name =] 'page_operator' ]  
     [, [@delete_level =] delete_level ]   
     [, [@automatic_post =] automatic_post ]  
```  
  
## <a name="arguments"></a>引数  
`[ @job_id = ] job_id` 更新するジョブの識別番号を指定します。 *job_id*は **uniqueidentifier**です。  
  
`[ @job_name = ] 'job_name'` ジョブの名前。 *job_name* は **nvarchar (128)** です。  
  
> **注:***Job_id*または*job_name*のいずれかを指定する必要がありますが、両方を指定することはできません。  
  
`[ @new_name = ] 'new_name'` ジョブの新しい名前を指定します。 *new_name* は **nvarchar (128)** です。  
  
`[ @enabled = ] enabled` ジョブが有効 (**1**) か無効 (**0**) かを指定します。 *有効* なは **tinyint**です。  
  
`[ @description = ] 'description'` ジョブの説明。 *説明* は **nvarchar (512)** です。  
  
`[ @start_step_id = ] step_id` ジョブに対して実行する最初のステップの識別番号を指定します。 *step_id* は **int**です。  
  
`[ @category_name = ] 'category'` ジョブのカテゴリ。 *category* は **nvarchar (128)** です。  
  
`[ @owner_login_name = ] 'login'` ジョブを所有するログインの名前です。 *ログイン* は **nvarchar (128)** 固定サーバーロール **sysadmin** のメンバーだけがジョブの所有権を変更できます。  
  
`[ @notify_level_eventlog = ] eventlog_level` このジョブの Microsoft Windows アプリケーションログにエントリを配置するタイミングを指定します。 *eventlog_level*は **int**,、これらの値のいずれかを指定できます。  
  
|[値]|説明 (アクション)|  
|-----------|----------------------------|  
|**0**|行わない|  
|**1**|成功時|  
|**2**|失敗時|  
|**3**|Always (常に)|  
  
`[ @notify_level_email = ] email_level` このジョブの完了時に電子メールを送信するタイミングを指定します。 *email_level*は **int**です。 *email_level*は *eventlog_level*と同じ値を使用します。  
  
`[ @notify_level_netsend = ] netsend_level` このジョブの完了時にネットワークメッセージを送信するタイミングを指定します。 *netsend_level*は **int**です。 *netsend_level*は *eventlog_level*と同じ値を使用します。  
  
`[ @notify_level_page = ] page_level` このジョブの完了時にページを送信するタイミングを指定します。 *page_level* は **int**です。 *page_level*は *eventlog_level*と同じ値を使用します。  
  
`[ @notify_email_operator_name = ] 'operator_name'`*Email_level*に達したときに電子メールを送信するオペレーターの名前。 *email_name* は **nvarchar (128)** です。  
  
`[ @notify_netsend_operator_name = ] 'netsend_operator'` ネットワークメッセージの送信先オペレーターの名前。 *netsend_operator* は **nvarchar (128)** です。  
  
`[ @notify_page_operator_name = ] 'page_operator'` ページを送信するオペレーターの名前。 *page_operator* は **nvarchar (128)** です。  
  
`[ @delete_level = ] delete_level` いつジョブを削除するかを指定します。 *delete_value*は **int**です。 *delete_level*は *eventlog_level*と同じ値を使用します。  
  
`[ @automatic_post = ] automatic_post` 確保.  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_update_job** は、 **msdb** データベースから実行する必要があります。  
  
 **sp_update_job** は、パラメーター値が指定されている設定のみを変更します。 パラメーターを省略した場合は、現在の設定が保持されます。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、 **sysadmin** 固定サーバーロールのメンバーは、このストアドプロシージャを実行できます。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
 **Sysadmin**のメンバーだけが、このストアドプロシージャを使用して、他のユーザーが所有するジョブの属性を編集できます。  
  
## <a name="examples"></a>例  
 次の例では、ジョブの名前、説明、および有効な状態を変更し `NightlyBackups` ます。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_job  
    @job_name = N'NightlyBackups',  
    @new_name = N'NightlyBackups -- Disabled',  
    @description = N'Nightly backups disabled during server migration.',  
    @enabled = 0 ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [sp_delete_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_help_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
