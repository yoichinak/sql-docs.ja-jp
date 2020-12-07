---
description: dbo.sysjobsteps (Transact-SQL)
title: dbo.sysjobsteps (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysjobsteps
- dbo.sysjobsteps_TSQL
- sysjobsteps
- sysjobsteps_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobsteps system table
ms.assetid: 978b8205-535b-461c-91f3-af9b08eca467
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a2f6fa46b0057680453b443186f6a4828195ab4a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544579"
---
# <a name="dbosysjobsteps-transact-sql"></a>dbo.sysjobsteps (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントによって実行されるジョブ内の各ステップに関する情報を格納します。 このテーブルは、 **msdb** データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|ジョブの ID。|  
|**step_id**|**int**|ジョブ ステップの ID。|  
|**step_name**|**sysname**|ジョブステップの名前。|  
|**サブ**|**nvarchar(40)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントがジョブ ステップを実行するために使用するサブシステムの名前。|  
|**command**|**nvarchar(max)**|**サブシステム**によって実行されるコマンドです。|  
|**flags**|**int**|予約済み。|  
|**additional_parameters**|**ntext**|予約済み。|  
|**cmdexec_success_code**|**int**|**CmdExec**サブシステムのステップによって返された、成功を示すエラーレベルの値。|  
|**on_success_action**|**tinyint**|ステップが正常に実行されたときに実行されるアクション。<br /><br /> **1** = (既定値) 正常に終了します。<br /><br /> **2** = 失敗で終了<br /><br /> **3** = 次の手順に進む<br /><br /> **4** = ステップに進む _on_success_step_id_|
|**on_success_step_id**|**int**|ステップが正常に実行されたときに実行する次のステップの ID。|  
|**on_fail_action**|**tinyint**|ステップが正常に実行されなかった場合に実行されるアクション。<br /><br /> **1** = 正常に終了します。<br /><br /> **2** = (既定) エラーで終了します。<br /><br /> **3** = 次の手順に進む<br /><br /> **4** = ステップに進む _on_fail_step_id_|
|**on_fail_step_id**|**int**|ステップが正常に実行されないときに実行する次のステップの ID。|  
|**server**|**sysname**|予約済み。|  
|**database_name**|**sysname**|**サブシステム**が TSQL の場合に**コマンド**が実行されるデータベースの名前。|  
|**database_user_name**|**sysname**|ステップの実行時に使用されるアカウントを持つデータベースユーザーの名前。|  
|**retry_attempts**|**int**|ステップが失敗した場合の再試行回数。|  
|**retry_interval**|**int**|再試行の間に待機する時間。|  
|**os_run_priority**|**int**|予約済み。|  
|**output_file_name**|**nvarchar(200)**|**サブシステム**が TSQL、PowerShell、または**CmdExec**の場合に、ステップの出力が保存されるファイルの名前 _。_|  
|**last_run_outcome**|**int**|ジョブ ステップの前回の実行結果。<br /><br /> **0** = 失敗<br /><br /> **1** = 成功<br /><br /> **2** = 再試行<br /><br /> **3** = キャンセル<br /><br /> **5** = 不明|  
|**last_run_duration**|**int**|最後に実行されたときのステップの期間 (hhmmss)。|  
|**last_run_retries**|**int**|最後にジョブステップを実行したときの再試行回数。|  
|**last_run_date**|**int**|ステップの実行を最後に開始した日付 (yyyymmdd)。|  
|**last_run_time**|**int**|ステップの実行を最後に開始した時刻 (hhmmss)。|  
|**proxy_id**|**int**|ジョブステップのプロキシ。|  
|**step_uid**|**uniqueidentifier**|ジョブステップの識別子。|  
  
## <a name="see-also"></a>参照  
 [SQL Server エージェントテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)  
  
  
