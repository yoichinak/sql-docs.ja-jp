---
description: エンタープライズ全体におけるジョブの管理
title: エンタープライズ全体におけるジョブの管理
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- multiserver job management [SQL Server]
- jobs [SQL Server Agent], modifying
- modifying jobs
- SQL Server Agent jobs, modifying
- target servers [SQL Server], job changes
ms.assetid: 4fe7f6c6-f89b-4430-979c-4994a5dcf7a6
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e54498ffd749417a6ae4991cfcdaeeb1c91a85d8
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036533"
---
# <a name="manage-jobs-across-an-enterprise"></a>エンタープライズ全体におけるジョブの管理
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 現在、[Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance) によって、すべてではありませんが、ほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、[Azure SQL Managed Instance と SQL Server の T-SQL の相違点](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)に関するページを参照してください。

[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用せずにマルチサーバー ジョブ定義を変更した場合は、ターゲット サーバーが更新済みジョブを再びダウンロードできるように、その変更をダウンロード一覧に通知する必要があります。 ターゲット サーバーが最新のジョブ定義を確実に持つように、マルチサーバー ジョブを更新した後で INSERT 命令を次のように通知します。  
  
```  
EXECUTE sp_post_msx_operation 'INSERT', 'JOB', '<job id>'  
```  
  
マルチサーバー ジョブが変更されたことをターゲット サーバーに通知するには、次のいずれかのプロシージャを使用した後で前述のコマンドを呼び出す必要があります。  
  
-   [sp_add_jobstep (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)  
  
-   [sp_update_jobstep (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md)  
  
-   [sp_delete_jobstep (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)  
  
-   [イベントの管理](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
-   [sp_detach_schedule (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)  
  
    > [!NOTE]  
    > **sp_update_job** または **sp_delete_job** を呼び出した後で **sp_post_msx_operation**を呼び出す必要はありません。この 2 つのストアド プロシージャは、必要な変更をダウンロード一覧に自動的に通知するためです。  
  
エンタープライズ全体でジョブを管理するための一般的なタスクは次のとおりです。  
  
**ターゲット サーバーの状態を確認するには**  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-help-targetserver-transact-sql.md)  
  
-   [SQL Server 管理オブジェクト (SMO)](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
**ジョブのターゲット サーバーを変更するには**  
  
-   [SQL Server Management Studio](../../ssms/agent/modify-the-target-servers-for-a-job.md)  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)  
  
-   [SQL Server 管理オブジェクト (SMO)](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
**ターゲット サーバーの場所を変更するには**  
  
-   [SQL Server Management Studio](../../ssms/agent/specify-a-target-server-s-location-sql-server-management-studio.md)  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql.md)  
  
-   [SQL Server 管理オブジェクト (SMO)](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
**ターゲット サーバーのクロックを同期するには**  
  
-   [SQL Server Management Studio](../../ssms/agent/synchronize-target-server-clocks-sql-server-management-studio.md)  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql.md)  
  
**ターゲット サーバーからマスター サーバーにポーリングさせるには**  
  
-   [SQL Server Management Studio](../../ssms/agent/force-a-target-server-to-poll-the-master-server.md)  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-post-msx-operation-transact-sql.md)  
  
## <a name="see-also"></a>参照  
[イベントの管理](../../ssms/agent/manage-events.md)  
