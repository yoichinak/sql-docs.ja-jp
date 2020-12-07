---
description: dm_exec_background_job_queue (Transact-sql)
title: dm_exec_background_job_queue (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_background_job_queue
- sys.dm_exec_background_job_queue_TSQL
- dm_exec_background_job_queue_TSQL
- sys.dm_exec_background_job_queue
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_background_job_queue dynamic management function
ms.assetid: 05d9884f-b74c-4e3c-a23b-c90c1ea5ef02
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4499bbffd3e5b14eb870db2bf55e639188c08912
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89534126"
---
# <a name="sysdm_exec_background_job_queue-transact-sql"></a>dm_exec_background_job_queue (Transact-sql)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  非同期 (バックグラウンド) 実行用にスケジュールされているクエリプロセッサジョブごとに1行の値を返します。  
  
> **注:** またはからこれを呼び出すに **[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]** は **[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]** 、 **dm_pdw_nodes_exec_background_job_queue**という名前を使用します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**time_queued**|**datetime**|ジョブがキューに追加された時刻。|  
|**job_id**|**int**|ジョブ識別子。|  
|**database_id**|**int**|ジョブを実行するデータベース。|  
|**object_id1**|**int**|値はジョブの種類によって異なります。 詳細については、「解説」を参照してください。|  
|**object_id2**|**int**|値はジョブの種類によって異なります。 詳細については、「解説」を参照してください。|  
|**object_id3**|**int**|値はジョブの種類によって異なります。 詳細については、「解説」を参照してください。|  
|**object_id4**|**int**|値はジョブの種類によって異なります。 詳細については、「解説」を参照してください。|  
|**error_code**|**int**|エラーによりジョブが再挿入された場合は、エラーコード。 ジョブが中断したか、取得されていないか、完了している場合は NULL です。|  
|**request_type**|**smallint**|ジョブ要求の種類。|  
|**retry_count**|**smallint**|ジョブがキューから選択され、リソース不足またはその他の理由により再挿入された回数。|  
|**in_progress**|**smallint**|ジョブが実行を開始したかどうかを示します。<br /><br /> 1 = 開始<br /><br /> 0 = 待機中|  
|**session_id**|**smallint**|セッション識別子。|  
|**pdw_node_id**|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> このディストリビューションが配置されているノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可

で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium レベルでは、データベースの権限が必要です `VIEW DATABASE STATE` 。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Standard レベルおよび Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   
  
## <a name="remarks"></a>解説  
 このビューは、統計の非同期更新ジョブに関する情報のみを返します。 統計の非同期更新の詳細については、「 [統計](../../relational-databases/statistics/statistics.md)」を参照してください。  
  
 **Object_id4**を通じて**object_id1**の値は、ジョブ要求の種類によって異なります。 次の表は、それぞれのジョブの種類の列に関する説明です。  
  
|要求の種類|object_id1|object_id2|object_id3|object_id4|  
|------------------|-----------------|-----------------|-----------------|-----------------|  
|統計の非同期更新|テーブルまたはビュー ID|統計 ID|使用されていない|使用されていない|  
  
## <a name="examples"></a>例  
 次の例では、のインスタンス内の各データベースについて、バックグラウンドキューにあるアクティブな非同期ジョブの数を返し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
```  
SELECT DB_NAME(database_id) AS [Database], COUNT(*) AS [Active Async Jobs]  
FROM sys.dm_exec_background_job_queue  
WHERE in_progress = 1  
GROUP BY database_id;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [実行関連の動的管理ビューおよび関数 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [統計](../../relational-databases/statistics/statistics.md)   
 [KILL STATS JOB &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-stats-job-transact-sql.md)  
  
  



