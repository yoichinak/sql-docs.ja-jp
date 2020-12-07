---
description: syscollector_execution_log_full (Transact-sql)
title: syscollector_execution_log_full (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syscollector_execution_log_full
- syscollector_execution_log_full_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data collector view
- syscollector_execution_log_full view
ms.assetid: 6c8db22d-2e4c-4b7c-ac5a-8762ef1b175b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b60d6f7efb33398789795753f8921ad9d5c55d1f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546752"
---
# <a name="syscollector_execution_log_full-transact-sql"></a>syscollector_execution_log_full (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  実行ログがいっぱいになったときのコレクションセットまたはパッケージに関する情報を提供します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|log_id|**bigint**|各コレクション セットの実行を識別します。 このビューを他の詳細ログと結合するために使用します。 NULL 値が許可されます。|  
|parent_log_id|**bigint**|親パッケージまたはコレクションセットを識別します。 NULL 値は許可されません。 Id は親子関係にチェーンされています。これにより、どのパッケージがどのコレクションセットによって開始されたかを判断できます。 このビューでは、ログエントリが親子リンクによってグループ化され、呼び出しチェーンが明確に表示されるようにパッケージの名前にインデントがされます。|  
|name|**nvarchar (4000)**|このログエントリが表すコレクションセットまたはパッケージの名前。 NULL 値が許可されます。|  
|status|**smallint**|コレクションセットまたはコレクションパッケージの現在の状態を示します。 NULL 値が許可されます。<br /><br /> 値は次のとおりです。<br /><br /> 0 = 実行中<br /><br /> 1 = 完了<br /><br /> 2 = 失敗|  
|runtime_execution_mode|**smallint**|コレクションセットアクティビティがデータの収集またはデータのアップロードを行っているかどうかを示します。 NULL 値が許可されます。|  
|start_time|**datetime**|コレクションセットまたはパッケージが開始された時刻。 NULL 値が許可されます。|  
|last_iteration_time|**datetime**|継続的に実行されるパッケージの場合、パッケージが最後にスナップショットをキャプチャした時刻。 NULL 値が許可されます。|  
|finish_time|**datetime**|完了したパッケージとコレクションセットの実行が完了した時刻。 NULL 値が許可されます。|  
|duration|**int**|パッケージまたはコレクションセットが実行されている時間 (秒単位)。 NULL 値が許可されます。|  
|failure_message|**nvarchar(2048)**|コレクションセットまたはパッケージが失敗した場合は、そのコンポーネントの最新のエラーメッセージ。 NULL 値が許可されます。 詳細なエラー情報を取得するには、 [fn_syscollector_get_execution_details &#40;transact-sql&#41;](../../relational-databases/system-functions/fn-syscollector-get-execution-details-transact-sql.md) 関数を使用します。|  
|operator|**nvarchar(128)**|コレクションセットまたはパッケージを開始したユーザーを識別します。 NULL 値が許可されます。|  
|package_execution_id|**uniqueidentifier**|[!INCLUDE[ssIS](../../includes/ssis-md.md)] ログ テーブルへのリンクを提供します。 NULL 値が許可されます。|  
|collection_set_id|**int**|Msdb のデータコレクション構成テーブルへのリンクを提供します。 NULL 値が許可されます。|  
  
## <a name="permissions"></a>アクセス許可  
 **Dc_operator**に SELECT が必要です。  
  
## <a name="see-also"></a>参照  
 [データ コレクター ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [データ コレクターのビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)  
  
  
