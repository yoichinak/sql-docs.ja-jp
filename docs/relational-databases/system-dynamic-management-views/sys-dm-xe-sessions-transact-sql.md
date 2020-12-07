---
description: sys.dm_xe_sessions (Transact-SQL)
title: dm_xe_sessions (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_xe_sessions_TSQL
- dm_xe_sessions
- sys.dm_xe_sessions_TSQL
- sys.dm_xe_sessions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_sessions dynamic management view
- extended events [SQL Server], views
ms.assetid: defd6efb-9507-4247-a91f-dc6ff5841e17
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 16e1b53b91e5c1dca0bfd1b9bab49ad5e129e9c2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543807"
---
# <a name="sysdm_xe_sessions-transact-sql"></a>sys.dm_xe_sessions (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  アクティブな拡張イベントセッションに関する情報を返します。 このセッションは、イベント、アクション、およびターゲットのコレクションです。  
    
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|address|**varbinary (8)**|セッションのメモリアドレス。 アドレスはローカルシステム全体で一意です。 NULL 値は許可されません。|  
|name|**nvarchar (256)**|セッションの名前。 名前はローカルシステム全体で一意です。 NULL 値は許可されません。|  
|pending_buffers|**int**|処理を保留しているバッファーの最大数。 NULL 値は許可されません。|  
|total_regular_buffers|**int**|セッションに関連付けられている標準バッファーの合計数。 NULL 値は許可されません。<br /><br /> 注: ほとんどの場合、通常のバッファーが使用されます。 これらのバッファーは、多数のイベントを保持するのに十分なサイズです。 通常は、各セッションに 3 つ以上のバッファーがあります。 標準バッファーの数は、MEMORY_PARTITION_MODE オプションによって設定されるメモリのパーティション分割に基づいて、サーバーで自動的に決定されます。 標準バッファーのサイズは、MAX_MEMORY オプションの値 (既定では 4 MB) をバッファーの数で割った値になります。 MEMORY_PARTITION_MODE と MAX_MEMORY オプションの詳細については、「 [CREATE EVENT SESSION &#40;transact-sql&#41;](../../t-sql/statements/create-event-session-transact-sql.md)」を参照してください。|  
|regular_buffer_size|**bigint**|通常のバッファーサイズ (バイト単位)。 NULL 値は許可されません。|  
|total_large_buffers|**int**|大きなバッファーの合計数。 NULL 値は許可されません。<br /><br /> メモ: 大きなバッファーは、イベントが通常のバッファーより大きい場合に使用されます。 この目的のために明示的に確保されています。 ラージ バッファーは、イベント セッションが開始されるときに割り当てられ、サイズは MAX_EVENT_SIZE オプションによって決まります。 MAX_EVENT_SIZE オプションの詳細については、「 [CREATE EVENT SESSION &#40;transact-sql&#41;](../../t-sql/statements/create-event-session-transact-sql.md)」を参照してください。|  
|large_buffer_size|**bigint**|ラージ バッファーのサイズ (バイト単位)。 NULL 値は許可されません。|  
|total_buffer_size|**bigint**|セッションのイベントを格納するためのメモリ バッファーの合計サイズ (バイト単位)。 NULL 値は許可されません。|  
|buffer_policy_flags|**int**|すべてのバッファーがいっぱいになり、新しいイベントが発生した場合のセッションイベントバッファーの動作を示すビットマップ。 NULL 値は許可されません。|  
|buffer_policy_desc|**nvarchar (256)**|すべてのバッファーがいっぱいになっているときに新しいイベントが発生した場合のセッション イベント バッファーの動作を示す説明。  NULL 値は許可されません。 buffer_policy_desc には、次のいずれかを指定できます。<br /><br /> イベントの削除<br /><br /> イベントを削除しない<br /><br /> フルバッファーの削除<br /><br /> 新しいバッファーの割り当て|  
|flags|**int**|セッションに設定されているフラグを示すビットマップ。 NULL 値は許可されません。|  
|flag_desc|**nvarchar (256)**|セッションに設定されているフラグの説明。  NULL 値は許可されません。 flag_desc は、次の任意の組み合わせにすることができます。<br /><br /> 閉じるときにバッファーをフラッシュする<br /><br /> 専用ディスパッチャー<br /><br /> 再帰イベントを許可する|  
|dropped_event_count|**int**|バッファーがいっぱいになったときに削除されたイベントの数。 バッファーポリシーが [Drop full buffer] または [Do not drop events] の場合、この値は **0** です。 NULL 値は許可されません。|  
|dropped_buffer_count|**int**|バッファーがいっぱいのときに削除されたバッファーの数。 バッファーポリシーが "Drop event" に設定されている場合、または "Do not drop events" に設定されている場合、この値は **0** になります。 NULL 値は許可されません。|  
|blocked_event_fire_time|**int**|バッファーがいっぱいになったときにイベントの実行がブロックされた時間の長さ。 バッファーポリシーが [Drop full buffer] または [Drop event] の場合、この値は **0** になります。 NULL 値は許可されません。|  
|create_time|**datetime**|セッションが作成された時刻。 NULL 値は許可されません。|  
|largest_event_dropped_size|**int**|セッション バッファーに収まらなかった最大のイベントのサイズ。 NULL 値は許可されません。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

