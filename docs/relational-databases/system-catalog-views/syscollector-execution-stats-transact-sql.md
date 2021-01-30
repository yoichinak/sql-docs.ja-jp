---
description: syscollector_execution_stats (Transact-SQL)
title: syscollector_execution_stats (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- syscollector_execution_stats
- syscollector_execution_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syscollector_execution_stats view
- data collector view
ms.assetid: 23e35ac5-fbbf-4922-970c-f4fac44c1263
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 54a56a6a9bdb2e5ad783d2e860c0b3415d4ddf7c
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99199721"
---
# <a name="syscollector_execution_stats-transact-sql"></a>syscollector_execution_stats (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  コレクションセットまたはパッケージのタスクの実行に関する情報を提供します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**log_id**|**bigint**|各コレクション セットの実行を識別します。 このビューを他の詳細ログと結合するために使用します。 NULL 値は許可されません。|  
|**task_name**|**nvarchar(128)**|この情報の対象となるコレクションセットまたはパッケージタスクの名前。 NULL 値は許可されません。|  
|**execution_row_count_in**|**int**|データフローの開始時に処理された行の数。 NULL 値が許可されます。|  
|**execution_row_count_out**|**int**|データ フローの最後に処理される行数です。 NULL 値が許可されます。|  
|**execution_row_count_errors**|**int**|データ フロー中に失敗した行数です。 NULL 値が許可されます。|  
|**execution_time_ms**|**int**|タスクの完了に必要な時間 (ミリ秒単位)。 NULL 値が許可されます。|  
|**log_time**|**datetime**|この情報がログに記録された時刻。 NULL 値は許可されません。|  
  
## <a name="permissions"></a>アクセス許可  
 **Dc_operator** に対する SELECT 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [データ コレクター ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [データ コレクターのビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)  
  
  
