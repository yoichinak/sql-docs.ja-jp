---
description: sp_detach_schedule (Transact-SQL)
title: sp_detach_schedule (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sp_detach_schedule
- sp_detach_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_detach_schedule
ms.assetid: 9a1fc335-1bef-4638-a33a-771c54a5dd19
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 513287fadf671cc645ffa210e96f56615e237983
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99200746"
---
# <a name="sp_detach_schedule-transact-sql"></a>sp_detach_schedule (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  スケジュールとジョブ間の関連付けを削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_detach_schedule   
     { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,  
       { [ @schedule_id = ] schedule_id | [ @schedule_name = ] 'schedule_name' } ,  
     [ @delete_unused_schedule = ] delete_unused_schedule   
```  
  
## <a name="arguments"></a>引数  
`[ @job_id = ] job_id` スケジュールを削除するジョブの識別番号を指定します。 *job_id* は **uniqueidentifier**,、既定値は NULL です。  
  
`[ @job_name = ] 'job_name'` スケジュールを削除するジョブの名前を指定します。 *job_name* は **sysname**,、既定値は NULL です。  
  
> [!NOTE]  
>  *Job_id* または *job_name* のいずれかを指定する必要がありますが、両方を指定することはできません。  
  
`[ @schedule_id = ] schedule_id` ジョブから削除するスケジュールの識別番号を指定します。 *schedule_id* は **int**,、既定値は NULL です。  
  
`[ @schedule_name = ] 'schedule_name'` ジョブから削除するスケジュールの名前を指定します。 *schedule_name* は **sysname**,、既定値は NULL です。  
  
> [!NOTE]  
>  *Schedule_id* または *schedule_name* のいずれかを指定する必要がありますが、両方を指定することはできません。  
  
`[ @delete_unused_schedule = ] delete_unused_schedule` 未使用のジョブスケジュールを削除するかどうかを指定します。 *delete_unused_schedule* の部分は **ビット** で、既定値は **0** です。これは、ジョブが参照していない場合でも、すべてのスケジュールが保持されることを意味します。 **1** に設定すると、ジョブが参照していない場合、未使用のジョブスケジュールが削除されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="permissions"></a>アクセス許可  
 既定では、このストアド プロシージャを実行できるのは、 **sysadmin** 固定サーバー ロールのメンバーです。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 ジョブの所有者はスケジュールにジョブをアタッチし、スケジュールの所有者でなくてもジョブをスケジュールからデタッチできることに注意してください。 ただし、呼び出し元がスケジュールの所有者でない限り、デタッチによってジョブが存在しない場合、スケジュールを削除することはできません。  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、ユーザーがスケジュールを所有しているかどうかが判断されます。 **Sysadmin** 固定サーバーロールのメンバーだけが、別のユーザーが所有するジョブからスケジュールをデタッチできます。  
  
## <a name="examples"></a>例  
 次の例では、スケジュールとジョブの関連付けを削除し `'NightlyJobs'` `'BackupDatabase'` ます。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_detach_schedule  
    @job_name = 'BackupDatabase',  
    @schedule_name = 'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_add_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)  
  
  
