---
description: sys.dm_broker_queue_monitors (Transact-SQL)
title: dm_broker_queue_monitors (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_broker_queue_monitors
- sys.dm_broker_queue_monitors_TSQL
- dm_broker_queue_monitors_TSQL
- sys.dm_broker_queue_monitors
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_broker_queue_monitors dynamic management view
ms.assetid: 401207dc-ef4a-4a3f-879c-76dcbb52d6bc
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 15090a3b52be40dba3735bb0b10ef185efe5de2b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551310"
---
# <a name="sysdm_broker_queue_monitors-transact-sql"></a>sys.dm_broker_queue_monitors (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  インスタンス内のキュー モニターごとに 1 行のデータを返します。 キューモニターは、キューのアクティブ化を管理します。  
  

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|モニターが監視するキューを含むデータベースのオブジェクト識別子。 NULLABLE.|  
|**queue_id**|**int**|モニターが監視するキューのオブジェクト識別子。 NULLABLE.|  
|**状態**|**nvarchar(32)**|モニターの状態。 NULLABLE. これは、次のいずれかになります。<br /><br /> **INACTIVE**<br /><br /> **NOTIFIED**<br /><br /> **RECEIVES_OCCURRING**|  
|**last_empty_rowset_time**|**datetime**|キューからの受信によって空の結果が返された最後の時刻。 NULLABLE.|  
|**last_activated_time**|**datetime**|キュー モニターによってストアド プロシージャがアクティブ化された前回の時刻。 NULLABLE.|  
|**tasks_waiting**|**int**|このキューの RECEIVE ステートメント内で現在待機しているセッションの数。 NULLABLE.<br /><br /> 注: この数には、キューモニターがセッションを開始したかどうかに関係なく、receive ステートメントを実行するすべてのセッションが含まれます。 これは、RECEIVE と共に WAITFOR を使用する場合に該当します。 基本的に、これらのタスクは、メッセージがキューに到着するのを待機しています。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-current-status-queue-monitor"></a>A. 現在のステータスキューモニタ  
 このシナリオでは、すべてのメッセージキューの現在の状態が表示されます。  
  
```  
SELECT t1.name AS [Service_Name],  t3.name AS [Schema_Name],  t2.name AS [Queue_Name],    
CASE WHEN t4.state IS NULL THEN 'Not available'   
ELSE t4.state   
END AS [Queue_State],    
CASE WHEN t4.tasks_waiting IS NULL THEN '--'   
ELSE CONVERT(VARCHAR, t4.tasks_waiting)   
END AS tasks_waiting,   
CASE WHEN t4.last_activated_time IS NULL THEN '--'   
ELSE CONVERT(varchar, t4.last_activated_time)   
END AS last_activated_time ,    
CASE WHEN t4.last_empty_rowset_time IS NULL THEN '--'   
ELSE CONVERT(varchar,t4.last_empty_rowset_time)   
END AS last_empty_rowset_time,   
(   
SELECT COUNT(*)   
FROM sys.transmission_queue t6   
WHERE (t6.from_service_name = t1.name) ) AS [Tran_Message_Count]   
FROM sys.services t1    INNER JOIN sys.service_queues t2   
ON ( t1.service_queue_id = t2.object_id )     
INNER JOIN sys.schemas t3 ON ( t2.schema_id = t3.schema_id )    
LEFT OUTER JOIN sys.dm_broker_queue_monitors t4   
ON ( t2.object_id = t4.queue_id  AND t4.database_id = DB_ID() )    
INNER JOIN sys.databases t5 ON ( t5.database_id = DB_ID() );  
```  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Service Broker 関連の動的管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
  

