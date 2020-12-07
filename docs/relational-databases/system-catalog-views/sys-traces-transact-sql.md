---
description: sys.traces (Transact-SQL)
title: sys. トレース (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- traces
- sys.traces_TSQL
- sys.traces
- traces_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.traces catalog view
ms.assetid: 4a03be22-b7da-4e2a-97ff-94bed890a620
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 31de0333847573b46872cfa5a3441dd92820151f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544953"
---
# <a name="systraces-transact-sql"></a>sys.traces (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  システム上で現在実行中のトレースは、の **トレース** カタログビューに含まれています。 このビューは、 **fn_trace_getinfo** 関数の代わりとして使用されます。  
  
 サポートされているトレースイベントの完全な一覧については、「 [SQL Server イベントクラスのリファレンス](../../relational-databases/event-classes/sql-server-event-class-reference.md)」を参照してください。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに拡張イベントカタログビューを使用します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|トレース ID。|  
|**status**|**int**|トレースの状態。<br /><br /> 0 = 停止<br /><br /> 1 = 実行中|  
|**path**|**nvarchar(260)**|トレースファイルのパス。 トレースが行セットトレースの場合、この値は null になります。|  
|**max_size**|**bigint**|トレース ファイル サイズの上限 (MB 単位)。 トレースが行セットトレースの場合、この値は null になります。|  
|**stop_time**|**datetime**|実行中のトレースを停止する時刻。|  
|**max_files**|**int**|ロールオーバー ファイルの最大数。 最大数が設定されていない場合、この値は null になります。|  
|**is_rowset**|**bit**|1 = 行セットトレース。|  
|**is_rollover**|**bit**|1 = ロールオーバーオプションが有効になっています。|  
|**is_shutdown**|**bit**|1 = シャットダウンオプションが有効になっています。|  
|**is_default**|**bit**|1 = 既定のトレース。|  
|**buffer_count**|**int**|トレースによって使用されるメモリ内バッファーの数。|  
|**buffer_size**|**int**|各バッファーのサイズ (KB)。|  
|**file_position**|**bigint**|最後のトレース ファイルの位置。 トレースが行セットトレースの場合、この値は null になります。|  
|**reader_spid**|**int**|行セットトレースリーダーのセッション ID。 トレースがファイルトレースの場合、この値は null になります。|  
|**start_time**|**datetime**|トレースの開始日時。|  
|**last_event_time**|**datetime**|最後にイベントが発生した時刻。|  
|**event_count**|**bigint**|発生したイベントの総数。|  
|**dropped_event_count**|**int**|削除されたイベントの合計数。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [trace_categories &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-categories-transact-sql.md)   
 [trace_columns &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-columns-transact-sql.md)   
 [trace_events &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-events-transact-sql.md)   
 [trace_event_bindings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-event-bindings-transact-sql.md)   
 [trace_subclass_values &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-subclass-values-transact-sql.md)  
  
  
