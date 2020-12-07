---
description: sp_create_plan_guide_from_handle (Transact-sql)
title: sp_create_plan_guide_from_handle (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_create_plan_guide_from_handle_TSQL
- sp_create_plan_guide_from_handle
dev_langs:
- TSQL
helpviewer_keywords:
- sp_create_plan_guide_from_handle
ms.assetid: 02cfb76f-a0f9-4b42-a880-1c3e7d64fe41
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ddb185ca0a5cf0e7abe0e51992d3e607555a9ea1
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543622"
---
# <a name="sp_create_plan_guide_from_handle-transact-sql"></a>sp_create_plan_guide_from_handle (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  プラン キャッシュ内のクエリ プランから 1 つ以上のプラン ガイドを作成します。 このストアドプロシージャを使用すると、クエリオプティマイザーでは、指定されたクエリに対して常に特定のクエリプランを使用できます。 プラン ガイドの詳細については、「 [Plan Guides](../../relational-databases/performance/plan-guides.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sp_create_plan_guide_from_handle [ @name = ] N'plan_guide_name'  
    , [ @plan_handle = ] plan_handle  
    , [ [ @statement_start_offset = ] { statement_start_offset | NULL } ]  
```  
  
## <a name="arguments"></a>引数  
 [ @name =] N '*plan_guide_name*'  
 プランガイドの名前を指定します。 プラン ガイド名は現在のデータベースに対して有効です。 *plan_guide_name* は、 [識別子](../../relational-databases/databases/database-identifiers.md) の規則に従っている必要があり、番号記号 (#) で始めることはできません。 *Plan_guide_name*の最大長は124文字です。  
  
 [ @plan_handle =] *plan_handle*  
 プラン キャッシュのバッチを識別します。 *plan_handle* は **varbinary (64)** です。 *plan_handle* は、 [dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md) 動的管理ビューから取得できます。  
  
 [ @statement_start_offset =] { *statement_start_offset* |NULL}]  
 指定された *plan_handle*のバッチ内でのステートメントの開始位置を識別します。 *statement_start_offset* は **int**,、既定値は NULL です。  
  
 ステートメントオフセットは、 [dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md) 動的管理ビューの statement_start_offset 列に対応しています。  
  
 NULL を指定した場合や、ステートメント オフセットを指定しない場合は、指定したプラン ハンドルのクエリ プランを使用してバッチ内の各ステートメントに対してプラン ガイドが作成されます。 結果として得られるプランガイドは、USE PLAN クエリヒントを使用して特定のプランを強制的に使用するプランガイドに相当します。  
  
## <a name="remarks"></a>解説  
 すべての種類のステートメントに対してプラン ガイドを作成できるわけではありません。 プラン ガイドを作成できないステートメントがバッチ内にあった場合、そのステートメントは無視されて、バッチ内の次のステートメントが処理されます。 ステートメントが同じバッチ内で複数回出現する場合は、最後に発生したプランが有効になり、ステートメントの前のプランは無効になります。 プランガイドでバッチ内のステートメントを使用できない場合、エラー10532が発生し、ステートメントは失敗します。 このエラーを回避するため、常に sys.dm_exec_query_stats 動的管理ビューからプラン ハンドルを取得することをお勧めします。  
  
> [!IMPORTANT]  
>  sp_create_plan_guide_from_handle では、プラン キャッシュに含まれているとおりのプランに基づいてプラン ガイドが作成されます。 したがって、バッチ テキスト、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント、および XML プラン表示が、プラン キャッシュから結果のプラン ガイドに文字単位で (クエリに渡されたリテラル値も含め) 取り込まれます。 これらのテキスト文字列には、データベースのメタデータに格納されている機密情報が含まれている場合があります。 適切な権限を持つユーザーは、の plan_guides カタログビューおよび [ **プランガイドのプロパティ** ] ダイアログボックスを使用して、この情報を表示できます [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。 プランガイドによって機密情報が公開されないようにするには、プランキャッシュから作成されたプランガイドを確認することをお勧めします。  
  
## <a name="creating-plan-guides-for-multiple-statements-within-a-query-plan"></a>クエリプラン内の複数のステートメントに対してプランガイドを作成する  
 sp_create_plan_guide_from_handle では、sp_create_plan_guide と同様に、対象となるバッチやモジュールのクエリ プランがプラン キャッシュから削除されます。 これは、新しいプラン ガイドがすべてのユーザーによって使用されるようにするための措置です。 1つのクエリプラン内の複数のステートメントに対してプランガイドを作成する場合は、明示的なトランザクションですべてのプランガイドを作成することによって、キャッシュからプランの削除を延期できます。 これにより、そのトランザクションが完了して、指定した各ステートメントのプラン ガイドが作成されるまで、プランがキャッシュに保持されます。 例 B を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 `VIEW SERVER STATE` 権限が必要です。 その他、sp_create_plan_guide_from_handle を使用して作成するプラン ガイドごとに必要な個々の権限があります。 OBJECT 型のプランガイドを作成するには `ALTER` 、参照先のオブジェクトに対する権限が必要です。 SQL または TEMPLATE 型のプランガイドを作成するには `ALTER` 、現在のデータベースに対する権限が必要です。 作成されるプランガイドの種類を決定するには、次のクエリを実行します。  
  
```sql  
SELECT cp.plan_handle, sql_handle, st.text, objtype   
FROM sys.dm_exec_cached_plans AS cp  
JOIN sys.dm_exec_query_stats AS qs ON cp.plan_handle = qs.plan_handle  
CROSS APPLY sys.dm_exec_sql_text(sql_handle) AS st;  
```  
  
 プランガイドを作成するステートメントが含まれている行で、結果セットの列を確認し `objtype` ます。 値がの場合は `Proc` 、プランガイドが OBJECT 型であることを示します。 やなどの他の値 `AdHoc` は `Prepared` 、プランガイドが SQL 型であることを示します。  
  
## <a name="examples"></a>例  
  
### <a name="a-creating-a-plan-guide-from-a-query-plan-in-the-plan-cache"></a>A. プラン キャッシュ内のクエリ プランからプラン ガイドを作成する  
 次の例では、プランキャッシュからクエリプランを指定することにより、1つの SELECT ステートメントに対してプランガイドを作成します。 まず、プラン ガイドを作成する単純な `SELECT` ステートメントを実行します。 次に、動的管理ビューの `sys.dm_exec_sql_text` および `sys.dm_exec_text_query_plan` を使用してこのクエリのプランを調べます。 その後、クエリに関連付けられているプランキャッシュでクエリプランを指定することによって、クエリに対してプランガイドが作成されます。 この例の最後のステートメントは、プラン ガイドが存在することを確認します。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT WorkOrderID, p.Name, OrderQty, DueDate  
FROM Production.WorkOrder AS w   
JOIN Production.Product AS p ON w.ProductID = p.ProductID  
WHERE p.ProductSubcategoryID > 4  
ORDER BY p.Name, DueDate;  
GO  
-- Inspect the query plan by using dynamic management views.  
SELECT * FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_sql_text(sql_handle)  
CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, qs.statement_start_offset, qs.statement_end_offset) AS qp  
WHERE text LIKE N'SELECT WorkOrderID, p.Name, OrderQty, DueDate%';  
GO  
-- Create a plan guide for the query by specifying the query plan in the plan cache.  
DECLARE @plan_handle varbinary(64);  
DECLARE @offset int;  
SELECT @plan_handle = plan_handle, @offset = qs.statement_start_offset  
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_sql_text(sql_handle) AS st  
CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, qs.statement_start_offset, qs.statement_end_offset) AS qp  
WHERE text LIKE N'SELECT WorkOrderID, p.Name, OrderQty, DueDate%';  
  
EXECUTE sp_create_plan_guide_from_handle   
    @name =  N'Guide1',  
    @plan_handle = @plan_handle,  
    @statement_start_offset = @offset;  
GO  
-- Verify that the plan guide is created.  
SELECT * FROM sys.plan_guides  
WHERE scope_batch LIKE N'SELECT WorkOrderID, p.Name, OrderQty, DueDate%';  
GO  
```  
  
### <a name="b-creating-multiple-plan-guides-for-a-multistatement-batch"></a>B. 複数のステートメントで構成されるバッチに対して複数のプラン ガイドを作成する  
 次の例では、ステートメントバッチ内の2つのステートメントに対してプランガイドを作成します。 プランガイドは、明示的なトランザクション内に作成されます。これにより、最初のプランガイドが作成された後に、バッチのクエリプランがプランキャッシュから削除されることはありません。 まず、複数のステートメントで構成されるバッチを実行します。 バッチのプランは、動的管理ビューを使用して検査されます。 バッチ内の各ステートメントの行が返されることに注意してください。 次に、パラメーターを指定することにより、バッチ内の最初と3番目のステートメントに対してプランガイドが作成され `@statement_start_offset` ます。 この例の最後のステートメントでは、プランガイドが存在することを確認します。  
  
 [!code-sql[PlanGuides#Create_From_Handle2](../../relational-databases/system-stored-procedures/codesnippet/tsql/sp-create-plan-guide-fro_1.sql)]  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースエンジン ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [dm_exec_query_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 [プランガイド](../../relational-databases/performance/plan-guides.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [dm_exec_sql_text &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [dm_exec_text_query_plan &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-text-query-plan-transact-sql.md)   
 [sp_control_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md)  
  
  
