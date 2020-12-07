---
description: sys.dm_exec_text_query_plan (Transact-SQL)
title: dm_exec_text_query_plan (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_text_query_plan
- sys.dm_exec_text_query_plan_TSQL
- dm_exec_text_query_plan_TSQL
- sys.dm_exec_text_query_plan
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_text_query_plan dynamic management function
ms.assetid: 9d5e5f59-6973-4df9-9eb2-9372f354ca57
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 51e2ee0d9867f952b219434ff59432732a96ddd6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539442"
---
# <a name="sysdm_exec_text_query_plan-transact-sql"></a>sys.dm_exec_text_query_plan (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

[!INCLUDE[tsql](../../includes/tsql-md.md)] バッチ、またはバッチ内の特定のステートメントのプラン表示をテキスト形式で返します。 プラン ハンドルで指定するクエリ プランは、キャッシュ内のもの、または現在実行中のものを指定できます。 このテーブル値関数は、 [transact-sql&#41;&#40;dm_exec_query_plan ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)に似ていますが、次の点が異なります。  
  
-   クエリ プランの出力がテキスト形式で返される。  
-   クエリ プランの出力のサイズに制限がない。  
-   バッチ内の個々のステートメントを指定できる。  
  
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降)、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sys.dm_exec_text_query_plan   
(   
    plan_handle   
    , { statement_start_offset | 0 | DEFAULT }  
        , { statement_end_offset | -1 | DEFAULT }  
)  
```  
  
## <a name="arguments"></a>引数  
*plan_handle*  
は、実行され、そのプランがプランキャッシュに存在するか、現在実行中のバッチのクエリ実行プランを一意に識別するトークンです。 *plan_handle* は **varbinary (64)** です。   

*Plan_handle*は、次の動的管理オブジェクトから取得できます。 
  
-   [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
-   [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  

-   [dm_exec_procedure_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  

-   [dm_exec_trigger_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)  
  
*statement_start_offset* |0 |標準  
バッチまたは保存されるオブジェクトのテキスト内での、行が示すクエリの開始位置 (バイト単位) を示します。 *statement_start_offset* は **int**です。値0はバッチの先頭を示します。 既定値は 0 です。  
  
ステートメントの開始オフセットは、次の動的管理オブジェクトから取得できます。  
  
-  [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-  [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
*statement_end_offset* |-1 |標準  
バッチまたは保存されるオブジェクトのテキスト内での、行が示すクエリの終了位置 (バイト単位) を示します。  
  
*statement_start_offset* は **int**です。  
  
値 -1 はバッチの最後を表します。 既定値は -1 です。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**dbid**|**smallint**|このプランに対応する [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントがコンパイルされたときに有効であったコンテキスト データベースの ID。 アドホック SQL ステートメントおよび準備された SQL ステートメントの場合、ステートメントがコンパイルされたデータベースの ID。<br /><br /> NULL 値は許可されます。|  
|**objectid**|**int**|ストアド プロシージャやユーザー定義関数など、クエリ プランのオブジェクトの ID。 アドホック バッチおよび準備されたバッチの場合、この列の値は **NULL** です。<br /><br /> NULL 値は許可されます。|  
|**number**|**smallint**|ストアド プロシージャに付けられた番号 (整数)。 たとえば、**orders** アプリケーションのプロシージャ グループの名前は、**orderproc;1**、**orderproc;2** のように指定されることがあります。 アドホック バッチおよび準備されたバッチの場合、この列の値は **NULL** です。<br /><br /> NULL 値は許可されます。|  
|**暗号**|**bit**|対応するプロシージャが暗号化されているかどうか。<br /><br /> 0 = 暗号化されていない<br /><br /> 1 = 暗号化されている<br /><br /> NULL 値は許可されません。|  
|**query_plan**|**nvarchar(max)**|*Plan_handle*で指定されたクエリ実行プランのコンパイル時のプラン表示表現を格納します。 プラン表示はテキスト形式です。 アドホック [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント、ストアド プロシージャ コール、ユーザー定義関数コールなどを含むバッチごとに、1 つのプランが生成されます。<br /><br /> NULL 値は許可されます。|  
  
## <a name="remarks"></a>解説  
 次の場合、**sys.dm_exec_text_query_plan** で返されるテーブルの **plan** 列にはプラン表示の出力は返されません。  
  
-   *Plan_handle*を使用して指定されたクエリプランがプランキャッシュから削除されている場合、返されるテーブルの**query_plan**列は null になります。 たとえば、プラン ハンドルがキャプチャされてから **sys.dm_exec_text_query_plan** に使用されるまでに遅延が生じると、クエリ プランがキャッシュから削除されることがあります。  
  
-   一括操作ステートメントや、8 KB よりも大きなサイズの文字列リテラルを含むステートメントなど、キャッシュされない [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントがいくつかあります。 これらのステートメントはキャッシュに存在しないため、**sys.dm_exec_text_query_plan** を使用してこれらのステートメントのプラン表示を取得することはできません。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)]バッチまたはストアドプロシージャにユーザー定義関数への呼び出し、または EXEC (*string*) を使用するなどの動的 SQL の呼び出しが含まれている場合、ユーザー定義関数のコンパイル済み XML プラン表示は、バッチまたはストアドプロシージャの dm_exec_text_query_plan によって返されるテーブルには含まれません **。** 代わりに、ユーザー定義関数に対応する*plan_handle*に対して、 **dm_exec_text_query_plan**の個別の呼び出しを行う必要があります。  
  
アドホッククエリで [簡易](../../relational-databases/query-processing-architecture-guide.md#SimpleParam) または [強制パラメーター](../../relational-databases/query-processing-architecture-guide.md#ForcedParam)化を使用する場合、 **query_plan** 列にはステートメントテキストのみが含まれ、実際のクエリプランは含まれません。 クエリ プランを返すには、**sys.dm_exec_text_query_plan** を呼び出して、準備されたパラメーター化クエリのプラン ハンドルを取得します。 クエリがパラメーター化されたかどうかを判断するには、[sys.syscacheobjects](../../relational-databases/system-compatibility-views/sys-syscacheobjects-transact-sql.md) ビューの **sql** 列、または [sys.dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md) 動的管理ビューの text 列を参照します。  
  
## <a name="permissions"></a>アクセス許可  
 **sys.dm_exec_text_query_plan** を実行するには、ユーザーは **sysadmin** 固定サーバー ロールのメンバーであるか、サーバーの VIEW SERVER STATE 権限が与えられている必要があります。  
  
## <a name="examples"></a>例  
  
### <a name="a-retrieving-the-cached-query-plan-for-a-slow-running-transact-sql-query-or-batch"></a>A. 実行速度の遅い Transact-sql クエリまたはバッチのキャッシュされたクエリプランを取得する  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バッチが、特定の  との接続において長時間実行されている場合は、このクエリやバッチの実行プランを取得して、遅延の原因を調べることができます。 次の例では、実行速度の遅いクエリまたはバッチのプラン表示を取得する方法を示します。  
  
> [!NOTE]  
> この例を実行するには、 *session_id* と *plan_handle* の値を実際のサーバー固有の値に置き換えます。  
  
 まず、`sp_who` ストアド プロシージャを使用して、クエリまたはバッチを実行しているプロセスのサーバー プロセス ID (SPID) を取得します。  
  
```sql  
USE master;  
GO  
EXEC sp_who;  
GO  
```  
  
 `sp_who` によって返される結果セットでは、SPID の値が `54` であることが示されます。 `sys.dm_exec_requests` 動的管理ビューで、この SPID を使用して次のクエリを実行すると、プラン ハンドルを取得できます。  
  
```sql  
USE master;  
GO  
SELECT * FROM sys.dm_exec_requests  
WHERE session_id = 54;  
GO  
```  
  
 **sys.dm_exec_requests** から返されるテーブルでは、実行速度の遅いクエリやバッチのプラン ハンドルが `0x06000100A27E7C1FA821B10600` であることが示されます。 次の例は、指定したプラン ハンドルのクエリ プランを返し、既定値 0 および -1 を使用してクエリまたはバッチ内のすべてのステートメントを返します。  
  
```sql  
USE master;  
GO  
SELECT query_plan   
FROM sys.dm_exec_text_query_plan (0x06000100A27E7C1FA821B10600,0,-1);  
GO  
```  
  
### <a name="b-retrieving-every-query-plan-from-the-plan-cache"></a>B. プランキャッシュからすべてのクエリプランを取得する  
 プラン キャッシュにあるすべてのクエリ プランのスナップショットを取得するには、`sys.dm_exec_cached_plans` 動的管理ビューに対してクエリを実行し、キャッシュにあるすべてのクエリ プランのプラン ハンドルを取得します。 プラン ハンドルは、`plan_handle` の `sys.dm_exec_cached_plans` 列に格納されます。 その後、次のように CROSS APPLY 演算子を使用して、プラン ハンドルを `sys.dm_exec_text_query_plan` に渡します。 現在プランキャッシュにある各プランのプラン表示出力は、 `query_plan` 返されるテーブルの列にあります。  
  
```sql  
USE master;  
GO  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp   
CROSS APPLY sys.dm_exec_text_query_plan(cp.plan_handle, DEFAULT, DEFAULT);  
GO  
```  
  
### <a name="c-retrieving-every-query-plan-for-which-the-server-has-gathered-query-statistics-from-the-plan-cache"></a>C. サーバーがクエリ統計情報を収集したすべてのクエリプランをプランキャッシュから取得する  
 現在プラン キャッシュにあるクエリ プランのうち、サーバーで統計情報が収集されたすべてのクエリ プランのスナップショットを取得するには、`sys.dm_exec_query_stats` 動的管理ビューに対してクエリを実行し、キャッシュにあるこれらのプランのプラン ハンドルを取得します。 プラン ハンドルは、`plan_handle` の `sys.dm_exec_query_stats` 列に格納されます。 その後、次のように CROSS APPLY 演算子を使用して、プラン ハンドルを `sys.dm_exec_text_query_plan` に渡します。 各プランのプラン表示出力は、返されるテーブルの `query_plan` 列に格納されます。  
  
```sql  
USE master;  
GO  
SELECT * FROM sys.dm_exec_query_stats AS qs   
CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, qs.statement_start_offset, qs.statement_end_offset);  
GO  
```  
  
### <a name="d-retrieving-information-about-the-top-five-queries-by-average-cpu-time"></a>D. 平均 CPU 時間による上位5つのクエリに関する情報の取得  
 次の例では、上位 5 つのクエリにかかった平均 CPU 時間とクエリ プランを返します。 **sys.dm_exec_text_query_plan** 関数で、既定値 0 および -1 を使用してクエリ プランのバッチ内のすべてのステートメントを返します。  
  
```sql  
SELECT TOP 5 total_worker_time/execution_count AS [Avg CPU Time],  
Plan_handle, query_plan   
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, 0, -1)  
ORDER BY total_worker_time/execution_count DESC;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [dm_exec_query_plan &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)  
