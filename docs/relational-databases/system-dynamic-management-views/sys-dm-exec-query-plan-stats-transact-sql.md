---
description: dm_exec_query_plan_stats (Transact-sql)
title: dm_exec_query_plan_stats (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_exec_query_plan_stats
- sys.dm_exec_query_plan_stats_TSQL
- dm_exec_query_plan_stats_TSQL
- dm_exec_query_plan_stats
helpviewer_keywords:
- sys.dm_exec_query_plan_stats management view
ms.assetid: fdc7659e-df41-488e-b2b5-0d79734dfacb
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 0ab11e74205f47d50e927680081e8e13dfee37fb
ms.sourcegitcommit: 9be0047805ff14e26710cfbc6e10d6d6809e8b2c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "89042482"
---
# <a name="sysdm_exec_query_plan_stats-transact-sql"></a>dm_exec_query_plan_stats (Transact-sql)
[!INCLUDE[SQL Server 2019](../../includes/tsql-appliesto-ssver15-asdb-xxxx-xxx.md)]

以前にキャッシュされたクエリプランの前回の既知の実際の実行プランに相当するものを返します。

## <a name="syntax"></a>構文

```
sys.dm_exec_query_plan_stats(plan_handle)  
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
|**query_plan**|**xml**|*Plan_handle*で指定された実際のクエリ実行プランの最後に認識されたランタイム Showplan 表現を格納します。 プラン表示は XML 形式です。 アドホック [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント、ストアド プロシージャ コール、ユーザー定義関数コールなどを含むバッチごとに、1 つのプランが生成されます。<br /><br /> NULL 値は許可されます。| 

## <a name="remarks"></a>解説
これはオプトイン機能です。 サーバーレベルでを有効にするには、 [トレースフラグ](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 2451 を使用します。 データベースレベルでを有効にするには、 [ALTER DATABASE スコープ構成 &#40;transact-sql&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)の LAST_QUERY_PLAN_STATS オプションを使用します。

このシステム関数は、 **ライトウェイト** クエリ実行統計のプロファイルインフラストラクチャで動作します。 詳細については、「[クエリ プロファイリング インフラストラクチャ](../../relational-databases/performance/query-profiling-infrastructure.md)」を参照してください。  

プラン表示の出力には、 `sys.dm_exec_query_plan_stats` 次の情報が含まれています。
-  キャッシュされたプランで検出されたすべてのコンパイル時情報
-  操作ごとの実際の行数、クエリの CPU 時間と実行時間の合計、書き込みの警告、実際の DOP、使用されたメモリの最大値などのランタイム情報

次の条件下では、 **実際の実行プランに相当する** プラン表示出力が、返されたテーブルの **query_plan** 列に返され `sys.dm_exec_query_plan_stats` ます。  

-   このプランは、 [dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)にあります。     
    **AND**    
-   実行されているクエリは複雑であるか、リソースを消費しています。

次の条件下では、返されるテーブルの [ **query_plan** ] 列に、次のような**単純な<sup>1</sup> **プラン表示出力が返され `sys.dm_exec_query_plan_stats` ます。  

-   このプランは、 [dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)にあります。     
    **AND**    
-   クエリは単純であり、通常は OLTP ワークロードの一部として分類されます。

<sup>1</sup> は、ルートノードの演算子 (SELECT) のみを含む Showplan を参照します。

次の条件下では、からの **出力は返されません** `sys.dm_exec_query_plan_stats` 。

-   を使用して指定されたクエリプランは、 `plan_handle` プランキャッシュから削除されています。     
    **OR**    
-   最初の場所では、クエリプランをキャッシュできませんでした。 詳細については、「 [実行プランのキャッシュと再利用 ](../../relational-databases/query-processing-architecture-guide.md#execution-plan-caching-and-reuse)」を参照してください。
  
> [!NOTE] 
> **Xml**データ型で許可されている入れ子になったレベルの数に制限があるため、で `sys.dm_exec_query_plan` は、入れ子になった要素の128レベル以上を満たすクエリプランを返すことはできません。 以前のバージョンのでは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、この条件が原因でクエリプランが返されず、 [エラー 6335](../../relational-databases/errors-events/database-engine-events-and-errors.md#errors-6000-to-6999)が生成されます。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]Service Pack 2 以降のバージョンでは、 `query_plan` 列は NULL を返します。  

## <a name="permissions"></a>アクセス許可  
 サーバーに対する `VIEW SERVER STATE` 権限が必要です。  

## <a name="examples"></a>例  
  
### <a name="a-looking-at-last-known-actual-query-execution-plan-for-a-specific-cached-plan"></a>A. 特定のキャッシュされたプランに対する前回の既知の実際のクエリ実行プランの確認  
 次の例では、 **dm_exec_cached_plans**クエリを使用して、興味深い計画を見つけ、そのプランを出力からコピーします。 `plan_handle`  
  
```sql  
SELECT * FROM sys.dm_exec_cached_plans;  
GO  
```  
  
次に、最後に確認した実際のクエリ実行プランを取得するには、 `plan_handle` システム関数 **sys. dm_exec_query_plan_stats**でコピーしたを使用します。  
  
```sql  
SELECT * FROM sys.dm_exec_query_plan_stats(< copied plan_handle >);  
GO  
```   

### <a name="b-looking-at-last-known-actual-query-execution-plan-for-all-cached-plans"></a>B. キャッシュされたすべてのプランについて、最後に確認された実際のクエリ実行プランを確認する
  
```sql  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp
CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS st
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle) AS qps;  
GO  
```   

### <a name="c-looking-at-last-known-actual-query-execution-plan-for-a-specific-cached-plan-and-query-text"></a>C. 特定のキャッシュされたプランとクエリテキストに対する前回の既知の実際のクエリ実行プランの確認

```sql  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp
CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS st
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle) AS qps
WHERE st.text LIKE 'SELECT * FROM Person.Person%';  
GO  
```   

### <a name="d-look-at-cached-events-for-trigger"></a>D. トリガーのキャッシュされたイベントを確認する

```sql
SELECT *
FROM sys.dm_exec_cached_plans
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle)
WHERE objtype ='Trigger';
GO
```

## <a name="see-also"></a>参照
  [トレース フラグ](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [実行関連の動的管理ビュー &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  

