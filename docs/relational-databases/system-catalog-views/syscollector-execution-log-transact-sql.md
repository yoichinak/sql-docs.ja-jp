---
description: syscollector_execution_log (Transact-sql)
title: syscollector_execution_log (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- syscollector_execution_log_TSQL
- syscollector_execution_log
dev_langs:
- TSQL
helpviewer_keywords:
- data collector view
- syscollector_execution_log view
ms.assetid: 11554d64-0426-42ce-b7ce-5591f67864d2
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 1920cc669307230bd29acabd04e9ade88147261b
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99199740"
---
# <a name="syscollector_execution_log-transact-sql"></a>syscollector_execution_log (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  コレクション セットまたはコレクション パッケージの実行ログからの情報を提供します。   
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|log_id|**bigint**|各コレクション セットの実行を識別します。 このビューを他の詳細ログと結合するために使用します。 NULL 値は許可されません。|  
|parent_log_id|**bigint**|親パッケージまたはコレクションセットを識別します。 NULL 値は許可されません。 Id は親子関係にチェーンされています。これにより、どのパッケージがどのコレクションセットによって開始されたかを判断できます。 このビューでは、ログエントリが親子関係に基づいてグループ化され、呼び出しチェーンが明確に表示されるようにパッケージの名前がインデントされます。|  
|collection_set_id|**int**|このログエントリが表すコレクションセットまたはパッケージを識別します。 NULL 値は許可されません。|  
|collection_item_id|**int**|コレクション アイテムを識別します。 NULL 値が許可されます。|  
|start_time|**datetime**|コレクションセットまたはパッケージが開始された時刻。 NULL 値は許可されません。|  
|last_iteration_time|**datetime**|継続的に実行されるパッケージの場合、パッケージが最後にスナップショットをキャプチャした時刻。 NULL 値が許可されます。|  
|finish_time|**datetime**|完了したパッケージとコレクションセットの実行が完了した時刻。 NULL 値が許可されます。|  
|runtime_execution_mode|**smallint**|コレクションセットアクティビティがデータの収集またはデータのアップロードを行っているかどうかを示します。 NULL 値が許可されます。<br /><br /> 値は次のとおりです。<br /><br /> 0 = コレクション<br /><br /> 1 = アップロード|  
|status|**smallint**|コレクションセットまたはコレクションパッケージの現在の状態を示します。 NULL 値は許可されません。<br /><br /> 値は次のとおりです。<br /><br /> 0 = 実行中<br /><br /> 1 = 完了<br /><br /> 2 = 失敗|  
|operator|**nvarchar(128)**|コレクションセットまたはパッケージを開始したユーザーを識別します。 NULL 値は許可されません。|  
|package_id|**uniqueidentifier**|このログを生成したコレクション セットまたはコレクション パッケージを識別します。 NULL 値が許可されます。|  
|package_name|**nvarchar (4000)**|このログを生成したパッケージの名前。 NULL 値が許可されます。|  
|package_execution_id|**uniqueidentifier**|[!INCLUDE[ssIS](../../includes/ssis-md.md)] ログ テーブルへのリンクを提供します。 NULL 値が許可されます。|  
|failure_message|**nvarchar(2048)**|コレクションセットまたはパッケージが失敗した場合は、そのコンポーネントの最新のエラーメッセージ。 NULL 値が許可されます。 詳細なエラー情報を取得するには、 [fn_syscollector_get_execution_details &#40;transact-sql&#41;](../../relational-databases/system-functions/fn-syscollector-get-execution-details-transact-sql.md) 関数を使用します。|  
  
## <a name="permissions"></a>アクセス許可  
 Dc_operator に SELECT が必要です。  
  
## <a name="see-also"></a>参照  
 [データ コレクター ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [データ コレクターのビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)  
  
  
