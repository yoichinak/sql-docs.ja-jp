---
description: query_context_settings (Transact-sql)
title: query_context_settings (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/29/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- QUERY_CONTEXT_SETTINGS_TSQL
- SYS.QUERY_CONTEXT_SETTINGS_TSQL
- SYS.QUERY_CONTEXT_SETTINGS
- QUERY_CONTEXT_SETTINGS
dev_langs:
- TSQL
helpviewer_keywords:
- sys.query_context_settings catalog view
ms.assetid: 3c1887df-6bd8-491e-82fc-d25ad9589faf
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ce442458968fe21fc8ac84008bf33e823c2f3876
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542496"
---
# <a name="sysquery_context_settings-transact-sql"></a>query_context_settings (Transact-sql)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

  クエリに関連付けられたコンテキスト設定に影響するセマンティクスに関する情報を格納します。 では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クエリのセマンティクスに影響を与える (クエリの正しい結果を定義する) いくつかのコンテキスト設定が使用できます。 異なる設定でコンパイルされた同じクエリテキストでは、(基になるデータに応じて) 異なる結果が生成される場合があります。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**context_settings_id**|**bigint**|主キー この値は、Showplan XML for queries で公開されています。|  
|**set_options**|**varbinary (8)**|いくつかの SET オプションの状態を反映するビットマスク。 詳細については、「 [sys. dm_exec_plan_attributes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md)」を参照してください。|  
|**language_id**|**smallint**|言語の id。 詳細については、「 [sys.sys言語 &#40;transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)」を参照してください。|  
|**date_format**|**smallint**|日付の形式。 詳しくは、「[SET DATEFORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/set-dateformat-transact-sql.md)」をご覧ください。|  
|**date_first**|**tinyint**|日付の最初の値。 詳しくは、「[SET DATEFIRST &#40;Transact-SQL&#41;](../../t-sql/statements/set-datefirst-transact-sql.md)」をご覧ください。|  
|**status**|**varbinary (2)**|クエリが実行されたクエリまたはコンテキストの種類を示すビットマスクフィールドです。 <br />列の値は、複数のフラグの組み合わせにすることができます (16 進数で表現)。<br /><br /> 0x0-通常のクエリ (特定のフラグなし)<br /><br /> 0x1-カーソル Api ストアドプロシージャのいずれかを使用して実行されたクエリ<br /><br /> 0x2-通知のクエリ<br /><br /> 0x4-内部クエリ<br /><br /> 0x8-汎用パラメーター化を使用しない自動パラメーター化クエリ<br /><br /> 0x10-カーソルフェッチ更新クエリ<br /><br /> 0x20-カーソル更新要求で使用されているクエリ<br /><br /> 0x40-カーソルを開いたときに最初の結果セットが返される (Cursor Auto Fetch)<br /><br /> 0x80-暗号化されたクエリ<br /><br /> 0x100-行レベルのセキュリティ述語のコンテキストでのクエリ|  
|**required_cursor_options**|**int**|カーソルの種類など、ユーザーによって指定されたカーソルオプション。|  
|**acceptable_cursor_options**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がステートメントの実行をサポートするために暗黙的に変換できるカーソル オプションです。|  
|**merge_action_type**|**smallint**|**MERGE**ステートメントの結果として使用されるトリガー実行プランの種類です。<br /><br /> 0は、非トリガープラン、 **merge**ステートメントの結果として実行されないトリガープラン、または**DELETE**アクションのみを指定する**merge**ステートメントの結果として実行されるトリガープランを示します。<br /><br /> 1は、 **MERGE**ステートメントの結果として実行される**INSERT**トリガープランを示します。<br /><br /> 2は、 **MERGE**ステートメントの結果として実行される**UPDATE**トリガープランを示します。<br /><br /> 3は、対応する**INSERT**または**UPDATE**アクションを含む**MERGE**ステートメントの結果として実行される**DELETE**トリガープランを示します。<br /><br /> <br /><br /> 連鎖アクションによって実行される入れ子になったトリガーの場合、この値は cascade の原因となった **MERGE** ステートメントのアクションです。|  
|**default_schema_id**|**int**|既定のスキーマの ID。完全に修飾されていない名前を解決するために使用されます。|  
|**is_replication_specific**|**bit**|レプリケーションに使用されます。|  
|**is_contained**|**varbinary (1)**|1は、包含データベースを示します。|  
  
## <a name="permissions"></a>アクセス許可  
 **VIEW DATABASE STATE**権限が必要です。  
  
## <a name="see-also"></a>参照  
 [database_query_store_options &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [query_store_plan &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [query_store_query &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [query_store_query_text &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [query_store_runtime_stats &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [query_store_wait_stats &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)   
 [query_store_runtime_stats_interval &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [クエリのストアを使用した、パフォーマンスの監視](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [クエリ ストアのストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
  
