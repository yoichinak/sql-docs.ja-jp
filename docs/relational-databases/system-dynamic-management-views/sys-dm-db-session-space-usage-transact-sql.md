---
description: sys.dm_db_session_space_usage (Transact-SQL)
title: dm_db_session_space_usage (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/16/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_session_space_usage_TSQL
- dm_db_session_space_usage
- sys.dm_db_session_space_usage
- sys.dm_db_session_space_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_session_space_usage dynamic management view
ms.assetid: a67a6045-8e14-460a-9fe3-912b846c08c1
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 571b3a474e8b6f40745ca0534d40b76dea4dd0fb
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550329"
---
# <a name="sysdm_db_session_space_usage-transact-sql"></a>sys.dm_db_session_space_usage (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  データベースの各セッションで割り当てられ、割り当てが解除されたページ数を返します。  
  
> [!NOTE]  
>  このビューは、 [tempdb データベース](../../relational-databases/databases/tempdb-database.md)にのみ適用できます。  
  
> [!NOTE]  
>  またはからこれを呼び出すに [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] は [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 、 **dm_pdw_nodes_db_session_space_usage**という名前を使用します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**session_id**|**smallint**|セッション ID。<br /><br /> **session_id**は、 [sys. dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)の**session_id**にマップされます。|  
|**database_id**|**smallint**|データベース ID。|  
|**user_objects_alloc_page_count**|**bigint**|このセッションによってユーザーオブジェクトに対して予約または割り当てられたページ数。|  
|**user_objects_dealloc_page_count**|**bigint**|セッションで、ユーザー オブジェクトへの割り当てが解除され、予約されなくなったページの数。|  
|**internal_objects_alloc_page_count**|**bigint**|セッションで、内部オブジェクトに予約された、または割り当てられたページの数。|  
|**internal_objects_dealloc_page_count**|**bigint**|このセッションによって内部オブジェクト用に割り当て解除され、予約されなくなったページの数。|  
|**user_objects_deferred_dealloc_page_count**|**bigint**|遅延割り当て解除用にマークされているページの数。<br /><br /> **注:** およびのサービスパックで導入されました [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 。|  
|**pdw_node_id**|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> このディストリビューションが配置されているノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可  

で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium レベルでは、データベースの権限が必要です `VIEW DATABASE STATE` 。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Standard レベルおよび Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   

## <a name="remarks"></a>解説  
 IAM ページは、このビューによって報告された割り当て数または割り当て解除数に含まれていません。  
  
 ページ カウンターはセッションの開始時に 0 に初期化されます。 このカウンターによって、セッションで完了したタスクに割り当てられた、または割り当て解除されたページの合計数が記録されます。 カウンターはタスクが終了したときにだけ更新され、実行中のタスクは反映されません。  
  
 セッションでは、同時に複数の要求をアクティブにすることができます。 要求が並列クエリの場合、複数のスレッドやタスクを開始できます。  
  
 セッション、要求、およびタスクの詳細については、「 [sys. dm_exec_sessions &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)」 dm_exec_requests、「transact-sql [&#40;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)」、および「 [&#41;dm_os_tasks transact-sql &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)」を参照してください。  
  
## <a name="user-objects"></a>ユーザーオブジェクト  
 ユーザーオブジェクトページカウンターには、次のオブジェクトが含まれています。  
  
-   ユーザー定義テーブルとインデックス  
  
-   システムテーブルとインデックス  
  
-   グローバル一時テーブルとインデックス  
  
-   ローカル一時テーブルとインデックス  
  
-   テーブル変数  
  
-   テーブル値関数で返されるテーブル  
  
## <a name="internal-objects"></a>内部オブジェクト  
 内部オブジェクトは **tempdb**にのみ存在します。 内部オブジェクトページカウンターには、次のオブジェクトが含まれています。  
  
-   カーソルまたはスプール操作の作業テーブルと、一時的なラージオブジェクト (LOB) ストレージ  
  
-   ハッシュ結合などの操作用の作業ファイル  
  
-   並べ替え実行結果  
  
## <a name="physical-joins"></a>物理結合  
 ![sys.dm_db_session_space_usage の物理結合](../../relational-databases/system-dynamic-management-views/media/join-dm-db-session-space-usage-1.gif "sys.dm_db_session_space_usage の物理結合")  
  
## <a name="relationship-cardinalities"></a>リレーションシップ基数  
  
|From|終了|リレーションシップ|  
|----------|--------|------------------|  
|dm_db_session_space_usage。 session_id|dm_exec_sessions。 session_id|一対一|  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;データベース関連の動的管理ビュー ](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [dm_os_tasks &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)   
 [dm_db_task_space_usage &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md)   
 [sys.dm_db_file_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)  
  
  



