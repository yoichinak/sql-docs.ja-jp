---
description: sp_delete_job (Transact-SQL)
title: sp_delete_job (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_job
- sp_delete_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_job
ms.assetid: b85db6e4-623c-41f1-9643-07e5ea38db09
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3d4ded9ec986afc467534c3053e17831147bc404
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541850"
---
# <a name="sp_delete_job-transact-sql"></a>sp_delete_job (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ジョブを削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_delete_job { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,  
     [ , [ @originating_server = ] 'server' ]   
     [ , [ @delete_history = ] delete_history ]  
     [ , [ @delete_unused_schedule = ] delete_unused_schedule ]  
```  
  
## <a name="arguments"></a>引数  
`[ @job_id = ] job_id` 削除するジョブの識別番号を指定します。 *job_id* は **uniqueidentifier**,、既定値は NULL です。  
  
`[ @job_name = ] 'job_name'` 削除するジョブの名前を指定します。 *job_name* は **sysname**,、既定値は NULL です。  
  
> [!NOTE]  
>  *Job_id*または*job_name*のいずれかを指定する必要があります。両方を指定することはできません。  
  
`[ @originating_server = ] 'server'` 内部使用。  
  
`[ @delete_history = ] delete_history` ジョブの履歴を削除するかどうかを指定します。 *delete_history* は **ビット**,、既定値は **1**です。 *Delete_history*が**1**の場合、ジョブのジョブ履歴は削除されます。 *Delete_history*が**0**の場合、ジョブ履歴は削除されません。  
  
 ジョブが削除され、履歴が削除されていない場合、ジョブの履歴情報はエージェントのグラフィカルユーザーインターフェイスのジョブ履歴に表示されません [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が、情報は**msdb**データベースの**sysjobhistory**テーブルに残ります。  
  
`[ @delete_unused_schedule = ] delete_unused_schedule` 他のジョブにアタッチされていない場合に、このジョブにアタッチされているスケジュールを削除するかどうかを指定します。 *delete_unused_schedule* は **ビット**,、既定値は **1**です。 *Delete_unused_schedule*が**1**の場合、そのスケジュールを参照するジョブが他にない場合、このジョブにアタッチされているスケジュールは削除されます。 *Delete_unused_schedule*が**0**の場合、スケジュールは削除されません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 ** \@ Originating_server**引数は、内部使用のために予約されています。  
  
 ** \@ Delete_unused_schedule**引数は、どのジョブにもアタッチされていないスケジュールを自動的に削除することによって、以前のバージョンの SQL Server との下位互換性を提供します。 このパラメーターでは、既定で互換動作が設定されることに注意してください。 ジョブにアタッチされていないスケジュールを保持するには、 ** \@ delete_unused_schedule**引数として値**0**を指定する必要があります。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] は、ジョブを簡単に管理できるグラフィカルなツールです。ジョブのインフラストラクチャを作成し、管理するには、このツールを使用することをお勧めします。  
  
 このストアド プロシージャでは、メンテナンス プランやメンテナンス プランの一部であるジョブを削除できません。 代わりに [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、メンテナンス プランを削除します。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、 **sysadmin** 固定サーバーロールのメンバーは、このストアドプロシージャを実行できます。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
 **sp_delete_job** を実行して任意のジョブを削除できるのは、 **sysadmin** 固定サーバー ロールのメンバーです。 **sysadmin** 固定サーバー ロールのメンバーでないユーザーは、自分が所有するジョブのみを削除できます。  
  
## <a name="examples"></a>例  
 次の例では、ジョブ `NightlyBackups` を削除します。  
  
```  
USE msdb ;  
GO  
  
EXEC sp_delete_job  
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [sp_help_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_update_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
