---
description: SQL Server エージェントのストアド プロシージャ (Transact-SQL)
title: SQL Server エージェントストアドプロシージャ (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- system stored procedures [SQL Server], SQL Server Agent
- SQL Server Agent, stored procedures
ms.assetid: 9c8de925-928b-460c-9455-779c4c37b966
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b81d3535d2ea6a8abf18083f8d6c13d0f6ce8697
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545876"
---
# <a name="sql-server-agent-stored-procedures-transact-sql"></a>SQL Server エージェントのストアド プロシージャ (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、スケジュールが設定された作業やイベントにより実行される作業を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントで管理する場合に、次のシステム ストアド プロシージャを使用できます。  

:::row:::
    :::column:::
        [sp_add_alert](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)

        [sp_add_category](../../relational-databases/system-stored-procedures/sp-add-category-transact-sql.md)

        [sp_add_job](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)

        [sp_add_jobschedule](../../relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql.md)

        [sp_add_jobserver](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)

        [sp_add_jobstep](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)

        [sp_add_notification](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)

        [sp_add_operator](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)

        [sp_add_schedule](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)

        [sp_add_targetservergroup](../../relational-databases/system-stored-procedures/sp-add-targetservergroup-transact-sql.md)

        [sp_add_targetsvrgrp_member](../../relational-databases/system-stored-procedures/sp-add-targetsvrgrp-member-transact-sql.md)

        [sp_apply_job_to_targets](../../relational-databases/system-stored-procedures/sp-apply-job-to-targets-transact-sql.md)

        [sp_attach_schedule](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)

        [sp_cycle_agent_errorlog](../../relational-databases/system-stored-procedures/sp-cycle-agent-errorlog-transact-sql.md)

        [sp_cycle_errorlog](../../relational-databases/system-stored-procedures/sp-cycle-errorlog-transact-sql.md)

        [sp_delete_alert](../../relational-databases/system-stored-procedures/sp-delete-alert-transact-sql.md)

        [sp_delete_category](../../relational-databases/system-stored-procedures/sp-delete-category-transact-sql.md)

        [sp_delete_job](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)

        [sp_delete_jobschedule](../../relational-databases/system-stored-procedures/sp-delete-jobschedule-transact-sql.md)

        [sp_delete_jobserver](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)

        [sp_delete_jobstep](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)

        [sp_delete_jobsteplog](../../relational-databases/system-stored-procedures/sp-delete-jobsteplog-transact-sql.md)

        [sp_delete_notification](../../relational-databases/system-stored-procedures/sp-delete-notification-transact-sql.md)

        [sp_delete_operator](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)

        [sp_delete_proxy](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)

        [sp_delete_schedule](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)

        [sp_delete_targetserver](../../relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql.md)

        [sp_delete_targetservergroup](../../relational-databases/system-stored-procedures/sp-delete-targetservergroup-transact-sql.md)

        [sp_delete_targetsvrgrp_member](../../relational-databases/system-stored-procedures/sp-delete-targetsvrgrp-member-transact-sql.md)

        [sp_detach_schedule](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)

        [sp_enum_login_for_proxy](../../relational-databases/system-stored-procedures/sp-enum-login-for-proxy-transact-sql.md)

        [sp_enum_proxy_for_subsystem](../../relational-databases/system-stored-procedures/sp-enum-proxy-for-subsystem-transact-sql.md)

        [sp_enum_sqlagent_subsystems](../../relational-databases/system-stored-procedures/sp-enum-sqlagent-subsystems-transact-sql.md)

        [sp_grant_proxy_to_subsystem](../../relational-databases/system-stored-procedures/sp-grant-proxy-to-subsystem-transact-sql.md)

        [sp_grant_login_to_proxy](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)

        [sp_help_alert](../../relational-databases/system-stored-procedures/sp-help-alert-transact-sql.md)

        [sp_help_category](../../relational-databases/system-stored-procedures/sp-help-category-transact-sql.md)

        [sp_help_downloadlist](../../relational-databases/system-stored-procedures/sp-help-downloadlist-transact-sql.md)

        [sp_help_job](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)
    :::column-end:::
    :::column:::
        [sp_help_jobactivity](../../relational-databases/system-stored-procedures/sp-help-jobactivity-transact-sql.md)

        [sp_help_jobcount](../../relational-databases/system-stored-procedures/sp-help-jobcount-transact-sql.md)

        [sp_help_jobhistory](../../relational-databases/system-stored-procedures/sp-help-jobhistory-transact-sql.md)

        [sp_help_jobs_in_schedule](../../relational-databases/system-stored-procedures/sp-help-jobs-in-schedule-transact-sql.md)

        [sp_help_jobschedule](../../relational-databases/system-stored-procedures/sp-help-jobschedule-transact-sql.md)

        [sp_help_jobserver](../../relational-databases/system-stored-procedures/sp-help-jobserver-transact-sql.md)

        [sp_help_jobstep](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)

        [sp_help_jobsteplog](../../relational-databases/system-stored-procedures/sp-help-jobsteplog-transact-sql.md)

        [sp_help_notification](../../relational-databases/system-stored-procedures/sp-help-notification-transact-sql.md)

        [sp_help_operator](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)

        [sp_help_proxy](../../relational-databases/system-stored-procedures/sp-help-proxy-transact-sql.md)

        [sp_help_schedule](../../relational-databases/system-stored-procedures/sp-help-schedule-transact-sql.md)

        [sp_help_targetserver](../../relational-databases/system-stored-procedures/sp-help-targetserver-transact-sql.md)

        [sp_help_targetservergroup](../../relational-databases/system-stored-procedures/sp-help-targetservergroup-transact-sql.md)

        [sp_manage_jobs_by_login](../../relational-databases/system-stored-procedures/sp-manage-jobs-by-login-transact-sql.md)

        [sp_msx_defect](../../relational-databases/system-stored-procedures/sp-msx-defect-transact-sql.md)

        [sp_msx_enlist](../../relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql.md)

        [sp_msx_get_account](../../relational-databases/system-stored-procedures/sp-msx-get-account-transact-sql.md)

        [sp_msx_set_account](../../relational-databases/system-stored-procedures/sp-msx-set-account-transact-sql.md)

        [sp_notify_operator](../../relational-databases/system-stored-procedures/sp-notify-operator-transact-sql.md)

        [sp_post_msx_operation](../../relational-databases/system-stored-procedures/sp-post-msx-operation-transact-sql.md)

        [sp_purge_jobhistory](../../relational-databases/system-stored-procedures/sp-purge-jobhistory-transact-sql.md)

        [sp_remove_job_from_targets](../../relational-databases/system-stored-procedures/sp-remove-job-from-targets-transact-sql.md)

        [sp_resync_targetserver](../../relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql.md)

        [sp_revoke_login_from_proxy](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)

        [sp_revoke_proxy_from_subsystem](../../relational-databases/system-stored-procedures/sp-revoke-proxy-from-subsystem-transact-sql.md)

        [sp_start_job](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)

        [sp_stop_job](../../relational-databases/system-stored-procedures/sp-stop-job-transact-sql.md)

        [sp_update_alert](../../relational-databases/system-stored-procedures/sp-update-alert-transact-sql.md)

        [sp_update_category](../../relational-databases/system-stored-procedures/sp-update-category-transact-sql.md)

        [sp_update_job](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)

        [sp_update_jobschedule](../../relational-databases/system-stored-procedures/sp-update-jobschedule-transact-sql.md)

        [sp_update_jobstep](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md)

        [sp_update_notification](../../relational-databases/system-stored-procedures/sp-update-notification-transact-sql.md)

        [sp_update_operator](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)

        [sp_update_proxy](../../relational-databases/system-stored-procedures/sp-update-proxy-transact-sql.md)

        [sp_update_schedule](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)

        [sp_update_targetservergroup](../../relational-databases/system-stored-procedures/sp-update-targetservergroup-transact-sql.md)
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
