---
description: dm_exec_query_plan (Transact-sql)
title: dm_exec_query_plan (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_query_plan_TSQL
- sys.dm_exec_query_plan
- dm_exec_query_plan
- sys.dm_exec_query_plan_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_plan dynamic management function
ms.assetid: e26f0867-9be3-4b2e-969e-7f2840230770
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 741cfebb7eb50e37512a5778691ab61700f9d98e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548553"
---
# <a name="sysdm_exec_query_plan-transact-sql"></a>dm_exec_query_plan (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

プラン ハンドルで指定されたバッチのプラン表示を XML 形式で返します。 プラン ハンドルで指定するプランは、キャッシュ内のもの、または現在実行中のものを指定できます。  
  
プラン表示の XML スキーマは、 [この Microsoft Web サイト](https://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409)で公開されており、利用できます。 また、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がインストールされているディレクトリからも入手できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sys.dm_exec_query_plan(plan_handle)  
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
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**dbid**|**smallint**|このプランに対応する [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントがコンパイルされたときに有効であったコンテキスト データベースの ID。 アドホック SQL ステートメントおよび準備された SQL ステートメントの場合、ステートメントがコンパイルされたデータベースの ID。<br /><br /> NULL 値は許可されます。|  
|**objectid**|**int**|ストアド プロシージャやユーザー定義関数など、クエリ プランのオブジェクトの ID。 アドホック バッチおよび準備されたバッチの場合、この列の値は **NULL** です。<br /><br /> NULL 値は許可されます。|  
|**number**|**smallint**|ストアド プロシージャに付けられた番号 (整数)。 たとえば、**orders** アプリケーションのプロシージャ グループの名前は、**orderproc;1**、**orderproc;2** のように指定されることがあります。 アドホック バッチおよび準備されたバッチの場合、この列の値は **NULL** です。<br /><br /> NULL 値は許可されます。|  
|**暗号**|**bit**|対応するプロシージャが暗号化されているかどうか。<br /><br /> 0 = 暗号化されていない<br /><br /> 1 = 暗号化されている<br /><br /> NULL 値は許可されません。|  
|**query_plan**|**xml**|*Plan_handle*で指定されたクエリ実行プランのコンパイル時のプラン表示表現を格納します。 プラン表示は XML 形式です。 アドホック [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント、ストアド プロシージャ コール、ユーザー定義関数コールなどを含むバッチごとに、1 つのプランが生成されます。<br /><br /> NULL 値は許可されます。|  
  
## <a name="remarks"></a>解説  
 次の場合、**sys.dm_exec_query_plan** で返されるテーブルの **query_plan** 列にはプラン表示の出力は返されません。  
  
-   *Plan_handle*を使用して指定されたクエリプランがプランキャッシュから削除されている場合、返されるテーブルの**query_plan**列は null になります。 たとえば、プラン ハンドルがキャプチャされてから **sys.dm_exec_query_plan** に使用されるまでに遅延が生じると、クエリ プランがキャッシュから削除されることがあります。  
  
-   一括操作ステートメントや、8 KB よりも大きなサイズの文字列リテラルを含むステートメントなど、キャッシュされない [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントがいくつかあります。 これらのステートメントはキャッシュに存在しないため、バッチが現在実行中でない限り、**sys.dm_exec_query_plan** を使用してこれらのステートメントの XML プラン表示を取得することはできません。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)]バッチまたはストアドプロシージャにユーザー定義関数への呼び出し、または EXEC (*string*) を使用するなどの動的 SQL の呼び出しが含まれている場合、ユーザー定義関数のコンパイル済み XML プラン表示は、バッチまたはストアドプロシージャの dm_exec_query_plan によって返されるテーブルには含まれません **。** 代わりに、ユーザー定義関数に対応するプランハンドルに対して、 **dm_exec_query_plan** の個別の呼び出しを行う必要があります。  
  
 アドホック クエリで簡易または強制のパラメーター化を行う場合、**query_plan** 列にはステートメント テキストのみが格納され、実際のクエリ プランは格納されません。 クエリ プランを返すには、**sys.dm_exec_query_plan** を呼び出して、準備されたパラメーター化クエリのプラン ハンドルを取得します。 クエリがパラメーター化されたかどうかを判断するには、[sys.syscacheobjects](../../relational-databases/system-compatibility-views/sys-syscacheobjects-transact-sql.md) ビューの **sql** 列、または [sys.dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md) 動的管理ビューの text 列を参照します。  
  
> [!NOTE] 
> **Xml**データ型で許可されている入れ子になったレベルの数に制限があるため、 **dm_exec_query_plan**は入れ子になった要素の128レベル以上のクエリプランを返すことができません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の以前のバージョンでは、この条件が原因でクエリ プランが返されず、エラー 6335 が生成されます。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]Service Pack 2 以降のバージョンでは、 **query_plan**列には NULL が返されます。   
> [Dm_exec_text_query_plan &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-text-query-plan-transact-sql.md)動的管理関数を使用すると、クエリプランの出力をテキスト形式で返すことができます。  
  
## <a name="permissions"></a>アクセス許可  
 **Dm_exec_query_plan**を実行するには、ユーザーが**sysadmin**固定サーバーロールのメンバーであるか、またはサーバーに対する権限を持っている必要があります。 `VIEW SERVER STATE`  
  
## <a name="examples"></a>例  
 次の例は、**sys.dm_exec_query_plan** 動的管理ビューの使用方法を示しています。  
  
 XML プラン表示を表示するには、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のクエリ エディターで次のクエリを実行した後、**sys.dm_exec_query_plan** によって返されるテーブルの **query_plan** 列で **[ShowPlanXML]** をクリックします。 XML プラン表示は、[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] の概要ペインに表示されます。 XML プラン表示をファイルに保存するには、[ **query_plan** ] 列の [ **showplan XML** ] を右クリックし、[結果に名前を付け**て保存**] をクリックします。ファイルの名前を sqlplan のように指定します ( \<*file_name*> 例: myxmlshowplan. sqlplan)。  
  
### <a name="a-retrieve-the-cached-query-plan-for-a-slow-running-transact-sql-query-or-batch"></a>A. 実行速度の遅い Transact-sql クエリまたはバッチのキャッシュされたクエリプランを取得する  
 アドホック バッチ、ストアド プロシージャ、ユーザー定義関数などの各種 [!INCLUDE[tsql](../../includes/tsql-md.md)] バッチのクエリ プランは、プラン キャッシュと呼ばれるメモリ領域にキャッシュされます。 キャッシュされたそれぞれのクエリ プランは、プラン ハンドルと呼ばれる一意識別子で識別されます。 **sys.dm_exec_query_plan** 動的管理ビューでは、このプラン ハンドルを指定して、特定の [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリまたはバッチの実行プランを取得できます。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バッチが、特定の  との接続において長時間実行されている場合は、このクエリやバッチの実行プランを取得して、遅延の原因を調べることができます。 次の例では、実行速度の遅いクエリまたはバッチに対して XML プラン表示を取得する方法を示します。  
  
> [!NOTE]  
>  この例を実行するには、 *session_id* と *plan_handle* の値を実際のサーバー固有の値に置き換えます。  
  
 まず、`sp_who` ストアド プロシージャを使用して、クエリまたはバッチを実行しているプロセスのサーバー プロセス ID (SPID) を取得します。  
  
```sql  
USE master;  
GO  
exec sp_who;  
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
  
 **Dm_exec_requests**によって返されるテーブルは、実行速度の遅いクエリまたはバッチのプランハンドルがであることを示します。これは、次のように、を使用して、 `0x06000100A27E7C1FA821B10600` *plan_handle* `sys.dm_exec_query_plan` 実行プランを XML 形式で取得するための plan_handle 引数として指定できます。 実行速度の遅いクエリまたはバッチの XML 形式の実行プランは、`sys.dm_exec_query_plan` によって返されるテーブルの **query_plan** 列に格納されます。  
  
```sql  
USE master;  
GO  
SELECT * 
FROM sys.dm_exec_query_plan (0x06000100A27E7C1FA821B10600);  
GO  
```  
  
### <a name="b-retrieve-every-query-plan-from-the-plan-cache"></a>B. プランキャッシュからすべてのクエリプランを取得する  
 プラン キャッシュにあるすべてのクエリ プランのスナップショットを取得するには、`sys.dm_exec_cached_plans` 動的管理ビューに対してクエリを実行し、キャッシュにあるすべてのクエリ プランのプラン ハンドルを取得します。 プラン ハンドルは、`plan_handle` の `sys.dm_exec_cached_plans` 列に格納されます。 その後、次のように CROSS APPLY 演算子を使用して、プラン ハンドルを `sys.dm_exec_query_plan` に渡します。 現在プラン キャッシュにある各プランの XML プラン表示の出力は、返されるテーブルの `query_plan` 列に格納されます。  
  
```sql  
USE master;  
GO  
SELECT * 
FROM sys.dm_exec_cached_plans AS cp 
CROSS APPLY sys.dm_exec_query_plan(cp.plan_handle);  
GO  
```  
  
### <a name="c-retrieve-every-query-plan-for-which-the-server-has-gathered-query-statistics-from-the-plan-cache"></a>C. サーバーがクエリ統計情報を収集したすべてのクエリプランをプランキャッシュから取得します。  
 現在プラン キャッシュにあるクエリ プランのうち、サーバーで統計情報が収集されたすべてのクエリ プランのスナップショットを取得するには、`sys.dm_exec_query_stats` 動的管理ビューに対してクエリを実行し、キャッシュにあるこれらのプランのプラン ハンドルを取得します。 プラン ハンドルは、`plan_handle` の `sys.dm_exec_query_stats` 列に格納されます。 その後、次のように CROSS APPLY 演算子を使用して、プラン ハンドルを `sys.dm_exec_query_plan` に渡します。 現在プラン キャッシュにある、収集された統計情報に関連する各プランの XML プラン表示の出力は、返されるテーブルの `query_plan` 列に格納されます。  
  
```sql  
USE master;  
GO  
SELECT * 
FROM sys.dm_exec_query_stats AS qs 
CROSS APPLY sys.dm_exec_query_plan(qs.plan_handle);  
GO  
```  
  
### <a name="d-retrieve-information-about-the-top-five-queries-by-average-cpu-time"></a>D. 平均 CPU 時間に基づく上位 5 つのクエリに関する情報を取得する  
 次の例では、上位 5 つのクエリにかかった平均 CPU 時間とプランを返します。  
  
```sql  
SELECT TOP 5 total_worker_time/execution_count AS [Avg CPU Time],  
   plan_handle, query_plan   
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_query_plan(qs.plan_handle)  
ORDER BY total_worker_time/execution_count DESC;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)   
 [dm_exec_query_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [プラン表示の論理操作と物理操作のリファレンス](../../relational-databases/showplan-logical-and-physical-operators-reference.md)   
 [dm_exec_text_query_plan &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-text-query-plan-transact-sql.md)  
  
  
