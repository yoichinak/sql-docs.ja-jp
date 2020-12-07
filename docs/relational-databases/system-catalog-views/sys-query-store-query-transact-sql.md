---
description: sys.query_store_query (Transact-sql)
title: sys.query_store_query (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 01/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- QUERY_STORE_QUERY
- SYS.QUERY_STORE_QUERY_TSQL
- SYS.QUERY_STORE_QUERY
- QUERY_STORE_QUERY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_query catalog view
- sys.query_store_query catalog view
ms.assetid: bdee149e-7556-4fc3-8242-925dd4b7b6ac
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1099243569f74cc5c50c90de1ec7bf35a5c53d51
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "92005814"
---
# <a name="sysquery_store_query-transact-sql"></a>sys.query_store_query (Transact-sql)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

  クエリと、それに関連付けられた全体的な集計されたランタイム実行統計に関する情報を格納します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**query_id**|**bigint**|主キー|  
|**query_text_id**|**bigint**|外部キー。 [Sys.query_store_query_text &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)への結合|  
|**context_settings_id**|**bigint**|外部キー。 [Sys.query_context_settings &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)に結合します。<br/>**注:** Azure Synapse Analytics は常にゼロ (0) を返します。|  
|**object_id**|**bigint**|クエリが含まれるデータベースオブジェクトの ID (ストアドプロシージャ、トリガー、CLR UDF/UDAgg など)。 クエリがデータベースオブジェクト (アドホッククエリ) の一部として実行されない場合は0です。<br/>**注:** Azure Synapse Analytics は常にゼロ (0) を返します。|  
|**batch_sql_handle**|**varbinary(64)**|クエリが含まれているステートメントバッチの ID。 クエリが一時テーブルまたはテーブル変数を参照する場合にのみ設定されます。<br/>**注:** Azure Synapse Analytics は常に *NULL*を返します。|  
|**query_hash**|**binary (8)**|論理クエリツリーに基づく個々のクエリの MD5 ハッシュ。 オプティマイザーヒントを含めます。|  
|**is_internal_query**|**bit**|クエリが内部的に生成されました。<br/>**注:** Azure Synapse Analytics は常にゼロ (0) を返します。|  
|**query_parameterization_type**|**tinyint**|パラメーター化の種類:<br /><br /> 0 - なし<br /><br /> 1-ユーザー<br /><br /> 2-単純<br /><br /> 3-強制<br/>**注:** Azure Synapse Analytics は常にゼロ (0) を返します。|  
|**query_parameterization_type_desc**|**nvarchar(60)**|パラメーター化の型の説明テキストです。<br/>**注:** Azure Synapse Analytics は常に *None*を返します。|  
|**initial_compile_start_time**|**datetimeoffset**|コンパイルの開始時刻。|  
|**last_compile_start_time**|**datetimeoffset**|コンパイルの開始時刻。|  
|**last_execution_time**|**datetimeoffset**|[最終実行時間] は、クエリ/プランの最後の終了時刻を示します。|  
|**last_compile_batch_sql_handle**|**varbinary(64)**|クエリが最後に使用された最後の SQL バッチのハンドル。 バッチの全文を取得するために、 [transact-sql&#41;&#40;sys.dm_exec_sql_text ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md) に入力として指定できます。<br/>**注:** Azure Synapse Analytics は常に *NULL*を返します。|  
|**last_compile_batch_offset_start**|**bigint**|Last_compile_batch_sql_handle と共に sys.dm_exec_sql_text に提供できる情報。<br/>**注:** Azure Synapse Analytics は常にゼロ (0) を返します。|
|**last_compile_batch_offset_end**|**bigint**|Last_compile_batch_sql_handle と共に sys.dm_exec_sql_text に提供できる情報。<br/>**注:** Azure Synapse Analytics は常にゼロ (0) を返します。|  
|**count_compiles**|**bigint**|コンパイルの統計情報。<br/>**注:** Azure Synapse Analytics は常に1を返します。|  
|**avg_compile_duration**|**float**|ミリ秒単位のコンパイル統計。|  
|**last_compile_duration**|**bigint**|ミリ秒単位のコンパイル統計。|  
|**avg_bind_duration**|**float**|統計情報をマイクロ秒単位でバインドします。<br/>**注:** Azure Synapse Analytics は常にゼロ (0) を返します。|  
|**last_bind_duration**|**bigint**|バインディングの統計。<br/>**注:** Azure Synapse Analytics は常にゼロ (0) を返します。|  
|**avg_bind_cpu_time**|**float**|バインディングの統計。<br/>**注:** Azure Synapse Analytics は常にゼロ (0) を返します。|  
|**last_bind_cpu_time**|**bigint**|バインディングの統計。<br/>**注:** Azure Synapse Analytics は常にゼロ (0) を返します。|  
|**avg_optimize_duration**|**float**|マイクロ秒単位の最適化統計。<br/>**注:** Azure Synapse Analytics は常にゼロ (0) を返します。|
|**last_optimize_duration**|**bigint**|最適化の統計。<br/>**注:** Azure Synapse Analytics は常にゼロ (0) を返します。|
|**avg_optimize_cpu_time**|**float**|マイクロ秒単位の最適化統計。<br/>**注:** Azure Synapse Analytics は常にゼロ (0) を返します。|
|**last_optimize_cpu_time**|**bigint**|最適化の統計。<br/>**注:** Azure Synapse Analytics は常にゼロ (0) を返します。|
|**avg_compile_memory_kb**|**float**|メモリの統計情報をコンパイルします。<br/>**注:** Azure Synapse Analytics は常にゼロ (0) を返します。|
|**last_compile_memory_kb**|**bigint**|メモリの統計情報をコンパイルします。<br/>**注:** Azure Synapse Analytics は常にゼロ (0) を返します。|
|**max_compile_memory_kb**|**bigint**|メモリの統計情報をコンパイルします。<br/>**注:** Azure Synapse Analytics は常にゼロ (0) を返します。|
|**is_clouddb_internal_query**|**bit**|オンプレミスでは常に 0 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] です。<br/>**注:** Azure Synapse Analytics は常にゼロ (0) を返します。|
  
## <a name="permissions"></a>アクセス許可  
 **VIEW DATABASE STATE**権限が必要です。  
  
## <a name="see-also"></a>参照  
 [sys.database_query_store_options &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_runtime_stats_interval &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [クエリのストアを使用した、パフォーマンスの監視](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [クエリ ストアのストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
  
