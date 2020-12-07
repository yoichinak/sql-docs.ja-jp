---
description: dm_exec_cached_plans (Transact-sql)
title: dm_exec_cached_plans (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_cached_plans
- dm_exec_cached_plans
- dm_exec_cached_plans_TSQL
- sys.dm_exec_cached_plans_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_cached_plans dynamic management view
ms.assetid: 95b707d3-3a93-407f-8e88-4515d4f2039d
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 02e10051c13f55b703e0f45ab2b657d7f0d66230
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542204"
---
# <a name="sysdm_exec_cached_plans-transact-sql"></a>dm_exec_cached_plans (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  クエリ実行を高速化するため [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でキャッシュされた各クエリ プランについての行を返します。 この動的管理ビューを使用して、キャッシュされたクエリ プラン、キャッシュされたクエリ テキスト、キャッシュされたプランが確保するメモリの量、およびキャッシュされたプランの再利用回数を参照できます。  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] では、動的管理ビューは、データベースの包含に影響する情報を公開することも、ユーザーがアクセスできる他のデータベースに関する情報を公開することもできません。 この情報を公開しないように、接続されたテナントに属していないデータを含むすべての行がフィルターで除外されます。さらに、列 **memory_object_address** および **pool_id** の値はフィルター処理されます。列の値が NULL に設定されています。  
  
> [!NOTE]  
>  またはからこれを呼び出すに [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] は [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 、 **dm_pdw_nodes_exec_cached_plans**という名前を使用します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|bucketid|**int**|エントリをキャッシュするハッシュ バケットの ID。 値の範囲は、0 からキャッシュの種類によって決まっているハッシュ テーブルのサイズまでです。<br /><br /> SQL プランおよびオブジェクト プランのキャッシュでは、ハッシュ テーブルのサイズが 32 ビット システムで最大 10007、64 ビット システムで最大 40009 です。 Bound Trees のキャッシュでは、ハッシュ テーブルのサイズが 32 ビット システムで最大 1009、64 ビット システムで最大 4001 です。 拡張ストアド プロシージャのキャッシュでは、ハッシュ テーブルのサイズが 32 ビット システムでも 64 ビット システムでも 127 です。|  
|refcounts|**int**|このキャッシュ オブジェクトを参照しているキャッシュ オブジェクトの数。 エントリをキャッシュするには、**refcounts** を 1 以上にする必要があります。|  
|usecounts|**int**|キャッシュ オブジェクトが検索された回数。 パラメーター化クエリがキャッシュ内のプランを検索したときは増加しません。 プラン表示を使用しているときは複数回増加できます。|  
|size_in_bytes|**int**|キャッシュ オブジェクトによって使用されたバイト数。|  
|memory_object_address|**varbinary (8)**|キャッシュ エントリのメモリ アドレス。 この値は、[sys.dm_os_memory_objects](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md) と併用してキャッシュされたプランのメモリ内訳を取得したり、[sys.dm_os_memory_cache_entries](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-entries-transact-sql.md) と併用してエントリをキャッシュするコストを取得したりできます。|  
|cacheobjtype|**nvarchar (34)**|キャッシュ内のオブジェクトの種類。 値は次のいずれかになります。<br /><br /> Compiled Plan<br /><br /> Compiled Plan Stub<br /><br /> Parse Tree<br /><br /> Extended Proc<br /><br /> CLR Compiled Func<br /><br /> CLR Compiled Proc|  
|objtype|**nvarchar (16)**|オブジェクトの種類。 有効な値とそれに対応する説明を次に示します。<br /><br /> Proc: ストアドプロシージャ<br />準備完了: 準備されたステートメント<br />アドホック: アドホッククエリ。 [!INCLUDE[tsql](../../includes/tsql-md.md)]リモートプロシージャ呼び出しとしてではなく**osql**または**sqlcmd**を使用して、言語イベントとして送信されたを示します。<br />ReplProc: レプリケーション-フィルター-プロシージャ<br />トリガー: トリガー<br />ビュー: 表示<br />既定値: 既定<br />UsrTab: User テーブル<br />SysTab: システムテーブル<br />Check: CHECK 制約<br />ルール: ルール|  
|plan_handle|**varbinary(64)**|インメモリ プランの識別子。 この識別子は一時的なもので、プランがキャッシュに残っている間だけ一定の値になります。 この値は、次の動的管理関数で使用できます。<br /><br /> [sys.dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)<br /><br /> [sys.dm_exec_query_plan](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)<br /><br /> [sys.dm_exec_plan_attributes](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md)|  
|pool_id|**int**|このプランのメモリ使用量の大部分を占めるリソース プールの ID。|  
|pdw_node_id|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> このディストリビューションが配置されているノードの識別子。|  
  
 <sup>1</sup>  
  
## <a name="permissions"></a>アクセス許可

で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium レベルでは、データベースの権限が必要です `VIEW DATABASE STATE` 。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Standard レベルおよび Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   

## <a name="examples"></a>例  
  
### <a name="a-returning-the-batch-text-of-cached-entries-that-are-reused"></a>A. 再利用されたキャッシュエントリのバッチテキストを返す  
 次の例は、複数回使用されたすべてのキャッシュ エントリの SQL テキストを返します。  
  
```sql  
SELECT usecounts, cacheobjtype, objtype, text   
FROM sys.dm_exec_cached_plans   
CROSS APPLY sys.dm_exec_sql_text(plan_handle)   
WHERE usecounts > 1   
ORDER BY usecounts DESC;  
GO  
```  
  
### <a name="b-returning-query-plans-for-all-cached-triggers"></a>B. キャッシュされたすべてのトリガーのクエリプランを返す  
 次の例は、キャッシュされたすべてのトリガーのクエリ プランを返します。  
  
```sql  
SELECT plan_handle, query_plan, objtype   
FROM sys.dm_exec_cached_plans   
CROSS APPLY sys.dm_exec_query_plan(plan_handle)   
WHERE objtype ='Trigger';  
GO  
```  
  
### <a name="c-returning-the-set-options-with-which-the-plan-was-compiled"></a>C. プランがコンパイルされた SET オプションを取得する  
 次の例は、プランをコンパイルした SET オプションを返します。 `sql_handle`プランのも返されます。 PIVOT 演算子は、 `set_options` `sql_handle` 属性と属性を行ではなく列として出力するために使用されます。 で返される値の詳細については `set_options` 、「 [sys. Dm_exec_plan_attributes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md)」を参照してください。  
  
```sql  
SELECT plan_handle, pvt.set_options, pvt.sql_handle  
FROM (  
      SELECT plan_handle, epa.attribute, epa.value   
      FROM sys.dm_exec_cached_plans   
      OUTER APPLY sys.dm_exec_plan_attributes(plan_handle) AS epa  
      WHERE cacheobjtype = 'Compiled Plan'  
      ) AS ecpa   
PIVOT (MAX(ecpa.value) FOR ecpa.attribute IN ("set_options", "sql_handle")) AS pvt;  
GO  
```  
  
### <a name="d-returning-the-memory-breakdown-of-all-cached-compiled-plans"></a>D. キャッシュされたすべてのコンパイル済みプランのメモリ内訳を返す  
 次の例は、キャッシュにあるすべてのコンパイル済みプランのメモリ内訳を返します。  
  
```sql  
SELECT plan_handle, ecp.memory_object_address AS CompiledPlan_MemoryObject,   
    omo.memory_object_address, type, page_size_in_bytes   
FROM sys.dm_exec_cached_plans AS ecp   
JOIN sys.dm_os_memory_objects AS omo   
    ON ecp.memory_object_address = omo.memory_object_address   
    OR ecp.memory_object_address = omo.parent_address  
WHERE cacheobjtype = 'Compiled Plan';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [実行関連の動的管理ビューおよび関数 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [dm_exec_query_plan &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)   
 [dm_exec_plan_attributes &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md)   
 [dm_exec_sql_text &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [dm_os_memory_objects &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md)   
 [dm_os_memory_cache_entries &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-entries-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)  
  
  


