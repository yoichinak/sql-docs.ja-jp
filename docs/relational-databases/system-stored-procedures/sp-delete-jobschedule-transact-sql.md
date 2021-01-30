---
description: sp_delete_jobschedule (Transact-sql)
title: sp_delete_jobschedule (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sp_delete_jobschedule
- sp_delete_jobschedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_jobschedule
ms.assetid: 82fbb48b-603a-4016-a7fb-1ce17fb76919
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c06030d2cc646dd269a0b3cb6bf564ce9248c9de
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99195514"
---
# <a name="sp_delete_jobschedule-transact-sql"></a>sp_delete_jobschedule (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ジョブのスケジュールを削除します。  
  
 **sp_delete_jobschedule** は、旧バージョンとの互換性のためだけに用意されています。  
  
  
## <a name="remarks"></a>コメント  
 ジョブスケジュールをジョブとは別に管理できるようになりました。 ジョブからスケジュールを削除するには、 **sp_detach_schedule** を使用します。 スケジュールを削除するには、 **sp_delete_schedule** を使用します。  
  
> **注: sp_delete_jobschedule** では、複数のジョブにアタッチされているスケジュールはサポートされていません。 既存のスクリプトが **sp_delete_jobschedule** を呼び出して、複数のジョブにアタッチされているスケジュールを削除すると、エラーが返されます。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、このストアド プロシージャを実行できるのは、 **sysadmin** 固定サーバー ロールのメンバーです。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
 **Sysadmin** ロールのメンバーは、任意のジョブスケジュールを削除できます。 **Sysadmin** ロールのメンバーでないユーザーは、自分が所有しているジョブスケジュールのみを削除できます。  
  
## <a name="see-also"></a>参照  
 [sp_delete_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_detach_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)   
 [ジョブの表示または変更](../../ssms/agent/view-or-modify-jobs.md)   
 [sp_add_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_help_jobschedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-jobschedule-transact-sql.md)   
 [sp_update_jobschedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-jobschedule-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
