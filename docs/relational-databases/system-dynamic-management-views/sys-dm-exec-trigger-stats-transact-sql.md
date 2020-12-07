---
description: sys.dm_exec_trigger_stats (Transact-SQL)
title: dm_exec_trigger_stats (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/03/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_trigger_stats
- dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_trigger_stats dynamic management function
ms.assetid: 863498b4-849c-434d-b748-837411458738
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 11498cce396d85bc35a7b15dcb441e303c30d196
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543965"
---
# <a name="sysdm_exec_trigger_stats-transact-sql"></a>sys.dm_exec_trigger_stats (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  キャッシュされたトリガーの集計パフォーマンス統計を返します。 このビューには、トリガーごとに 1 行が含まれており、その行の有効期間はトリガーがキャッシュに残っている間です。 つまり、トリガーがキャッシュから削除されると、対応する行もこのビューから削除されます。 その時点で、**sys.dm_exec_query_stats** と同様にパフォーマンス統計 SQL トレース イベントが発生します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|トリガーが存在するデータベースの ID。|  
|**object_id**|**int**|トリガーのオブジェクト ID 番号。|  
|**type**|**char(2)**|次のいずれかのオブジェクトの種類。<br /><br /> TA = アセンブリ (CLR) トリガー<br /><br /> TR = SQL トリガー|  
|**Type_desc**|**nvarchar(60)**|オブジェクトの種類の説明。<br /><br /> CLR_TRIGGER<br /><br /> SQL_TRIGGER|  
|**sql_handle**|**varbinary(64)**|これを使用すると、このトリガー内から実行された **dm_exec_query_stats** のクエリと関連付けることができます。|  
|**plan_handle**|**varbinary(64)**|インメモリ プランの識別子。 この識別子は一時的なもので、プランがキャッシュに残っている間だけ一定の値になります。 この値は、 **dm_exec_cached_plans** 動的管理ビューで使用できます。|  
|**cached_time**|**datetime**|トリガーがキャッシュに追加された時刻。|  
|**last_execution_time**|**datetime**|前回トリガーが実行された時刻。|  
|**execution_count**|**bigint**|トリガーが最後にコンパイルされてから実行された回数。|  
|**total_worker_time**|**bigint**|コンパイル後にこのトリガーの実行で消費された CPU 時間の合計 (マイクロ秒単位)。|  
|**last_worker_time**|**bigint**|トリガーを前回実行したときに使用された CPU 時間 (マイクロ秒単位)。|  
|**min_worker_time**|**bigint**|このトリガーが1回の実行で消費した最大 CPU 時間 (マイクロ秒単位)。|  
|**max_worker_time**|**bigint**|このトリガーが1回の実行で消費した最大 CPU 時間 (マイクロ秒単位)。|  
|**total_physical_reads**|**bigint**|コンパイル後にこのトリガーの実行で行われた物理読み取りの合計数。|  
|**last_physical_reads**|**bigint**|トリガーを前回実行したときに実行された物理読み取りの数。|  
|**min_physical_reads**|**bigint**|このトリガーの1回の実行で行われた物理読み取りの最小数。|  
|**max_physical_reads**|**bigint**|このトリガーの1回の実行で行われた物理読み取りの最大数。|  
|**total_logical_writes**|**bigint**|コンパイル後にこのトリガーの実行によって実行された論理書き込みの合計数。|  
|**last_logical_writes**|**bigint**|トリガーが最後に実行されたときに実行された論理書き込みの数。|  
|**min_logical_writes**|**bigint**|このトリガーの1回の実行で行われた論理書き込みの最小数。|  
|**max_logical_writes**|**bigint**|このトリガーの1回の実行で行われた論理書き込みの最大数。|  
|**total_logical_reads**|**bigint**|コンパイル後にこのトリガーの実行で行われた論理読み取りの合計数。|  
|**last_logical_reads**|**bigint**|トリガーが最後に実行されたときに実行された論理読み取りの数。|  
|**min_logical_reads**|**bigint**|このトリガーの1回の実行で行われた論理読み取りの最小数。|  
|**max_logical_reads**|**bigint**|このトリガーの1回の実行で行われた論理読み取りの最大数。|  
|**total_elapsed_time**|**bigint**|このトリガーの実行完了までの経過時間の合計 (マイクロ秒単位)。|  
|**last_elapsed_time**|**bigint**|このトリガーの前回の実行完了までの経過時間 (マイクロ秒単位)。|  
|**min_elapsed_time**|**bigint**|このトリガーの実行完了までの最小経過時間 (マイクロ秒単位)。|  
|**max_elapsed_time**|**bigint**|このトリガーの実行完了までの最大経過時間 (マイクロ秒単位)。| 
|**total_spills**|**bigint**|コンパイル後にこのトリガーの実行によって書き込まれたページの合計数。<br /><br /> **適用対象**: CU3 以降 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]|  
|**last_spills**|**bigint**|最後にトリガーが実行されたときに書き込まれたページの数。<br /><br /> **適用対象**: CU3 以降 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]|  
|**min_spills**|**bigint**|このトリガーによって1回の実行中に書き込まれたページの最小数。<br /><br /> **適用対象**: CU3 以降 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]|  
|**max_spills**|**bigint**|このトリガーによって1回の実行中に書き込まれたページの最大数。<br /><br /> **適用対象**: CU3 以降 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]|  
|**total_page_server_reads**|**bigint**|コンパイル後にこのトリガーの実行によって実行されたページサーバー読み取りの合計数。<br /><br /> **適用対象**: Azure SQL Database ハイパースケール|  
|**last_page_server_reads**|**bigint**|最後にトリガーを実行したときに実行されたページサーバーの読み取り回数。<br /><br /> **適用対象**: Azure SQL Database ハイパースケール|  
|**min_page_server_reads**|**bigint**|このトリガーの1回の実行で行われた、ページサーバーの読み取りの最小数。<br /><br /> **適用対象**: Azure SQL Database ハイパースケール|  
|**max_page_server_reads**|**bigint**|このトリガーの1回の実行で行われた、ページサーバーの読み取りの最大数。<br /><br /> **適用対象**: Azure SQL Database ハイパースケール|  

  
## <a name="remarks"></a>解説  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] では、動的管理ビューは、データベースの包含に影響する情報を公開することも、ユーザーがアクセスできる他のデータベースに関する情報を公開することもできません。 この情報を公開しないように、接続されたテナントに属していないデータを含むすべての行がフィルターで除外されます。  

ビュー内の統計は、クエリが完了したときに更新されます。  
  
## <a name="permissions"></a>アクセス許可  

で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium レベルでは、データベースの権限が必要です `VIEW DATABASE STATE` 。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Standard レベルおよび Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   
  
## <a name="examples"></a>例  
 次の例では、平均経過時間で識別される上位 5 つのトリガーに関する情報を返します。  
  
```sql  
SELECT TOP 5 d.object_id, d.database_id, DB_NAME(database_id) AS 'database_name',   
    OBJECT_NAME(object_id, database_id) AS 'trigger_name', d.cached_time,  
    d.last_execution_time, d.total_elapsed_time,   
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],   
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_trigger_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## <a name="see-also"></a>参照  
[実行関連の動的管理ビューおよび関数 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
[dm_exec_sql_text &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
[dm_exec_query_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
[dm_exec_procedure_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)   
[sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
  
