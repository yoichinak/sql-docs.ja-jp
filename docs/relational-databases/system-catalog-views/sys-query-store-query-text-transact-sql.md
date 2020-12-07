---
description: sys.query_store_query_text (Transact-sql)
title: sys.query_store_query_text (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 01/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.QUERY_STORE_QUERY_TEXT
- QUERY_STORE_QUERY_TEXT
- SYS.QUERY_STORE_QUERY_TEXT_TSQL
- QUERY_STORE_QUERY_TEXT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.query_store_query_text catalog view
- query_store_query_text catalog view
ms.assetid: f7032fa0-7c16-4492-bb82-685806c63a8c
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2d0dd52ae5c84ab13266bc1c90f81a3d9b2ad869
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "92005623"
---
# <a name="sysquery_store_query_text-transact-sql"></a>sys.query_store_query_text (Transact-sql)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)]クエリのテキストと SQL ハンドルを格納します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**query_text_id**|**bigint**|主キー|  
|**query_sql_text**|**nvarchar(max)**|ユーザーが指定したクエリの SQL テキスト。 には、空白、ヒント、およびコメントが含まれています。 クエリ テキストの前後のコメントとスペースは無視されます。 テキスト内のコメントとスペースは無視されません。|  
|**statement_sql_handle**|**vabinary (64)**|個々のクエリの SQL ハンドル。|  
|**is_part_of_encrypted_module**|**bit**|クエリテキストは、暗号化されたモジュールの一部です。<br/>**注:** Azure Synapse Analytics は常にゼロ (0) を返します。|
|**has_restricted_text**|**bit**|クエリテキストには、パスワードまたはその他の unmentionable 語が含まれています。<br/>**注:** Azure Synapse Analytics は常にゼロ (0) を返します。|
  
## <a name="permissions"></a>アクセス許可  
 **VIEW DATABASE STATE**権限が必要です。  
  
## <a name="see-also"></a>参照  
 [sys.database_query_store_options &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_runtime_stats &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats_interval &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [クエリのストアを使用した、パフォーマンスの監視](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [クエリ ストアのストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
  
