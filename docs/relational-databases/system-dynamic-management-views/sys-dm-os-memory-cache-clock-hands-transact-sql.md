---
description: sys.dm_os_memory_cache_clock_hands (Transact-SQL)
title: dm_os_memory_cache_clock_hands (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 12/21/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_cache_clock_hands_TSQL
- dm_os_memory_cache_clock_hands
- dm_os_memory_cache_clock_hands_TSQL
- sys.dm_os_memory_cache_clock_hands
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_cache_clock_hands dynamic management view
ms.assetid: 0660eddc-691c-425f-9d43-71151d644de7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 921a2c9e1b2f40c308c4f93b291d57ea1c39ef7f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543875"
---
# <a name="sysdm_os_memory_cache_clock_hands-transact-sql"></a>sys.dm_os_memory_cache_clock_hands (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  特定のキャッシュ クロックに関する各ハンドの状態を返します。  
  
> [!NOTE]  
>  またはからこれを呼び出すに [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] は [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 、 **dm_pdw_nodes_os_memory_cache_clock_hands**という名前を使用します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary (8)**|クロックに関連付けられたキャッシュのアドレス。 NULL 値は許可されません。|  
|**name**|**nvarchar (256)**|キャッシュの名前。 NULL 値は許可されません。|  
|**type**|**nvarchar(60)**|キャッシュストアの種類。 同じ種類のキャッシュが複数存在することが可能です。 NULL 値は許可されません。|  
|**clock_hand**|**nvarchar(60)**|手の種類。 これは、次のいずれかになります。<br /><br /> 外部<br /><br /> 内部<br /><br /> NULL 値は許可されません。|  
|**clock_status**|**nvarchar(60)**|クロックの状態。 これは、次のいずれかになります。<br /><br /> Suspended<br /><br /> 実行中<br /><br /> NULL 値は許可されません。|  
|**rounds_count**|**bigint**|エントリを削除するため、キャッシュ経由で行われたスイープの数。 NULL 値は許可されません。|  
|**removed_all_rounds_count**|**bigint**|すべてのスイープで削除されたエントリの数。 NULL 値は許可されません。|  
|**updated_last_round_count**|**bigint**|前回のスイープ中に更新されたエントリの数。 NULL 値は許可されません。|  
|**removed_last_round_count**|**bigint**|前回のスイープ中に削除されたエントリの数。 NULL 値は許可されません。|  
|**last_tick_time**|**bigint**|クロックハンドが最後に移動された時間 (ミリ秒単位)。 NULL 値は許可されません。|  
|**round_start_time**|**bigint**|前回のスイープの時間 (ミリ秒単位)。 NULL 値は許可されません。|  
|**last_round_start_time**|**bigint**|前のラウンドを完了するためにクロックが要した合計時間 (ミリ秒単位)。 NULL 値は許可されません。|  
|**pdw_node_id**|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> このディストリビューションが配置されているノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可  

で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium レベルでは、データベースの権限が必要です `VIEW DATABASE STATE` 。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Standard レベルおよび Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   
  
## <a name="remarks"></a>解説  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] メモリキャッシュと呼ばれる構造体のメモリに情報を格納します。 キャッシュには、データ、インデックス エントリ、コンパイル済みプロシージャ プランなど、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に関するさまざまな種類の情報が格納されます。 情報を再作成しないようにするために、メモリキャッシュは可能な限り長く保持され、通常はキャッシュから削除されます。これは、時間がかかりすぎている場合や、新しい情報のためにメモリ領域が必要な場合に、キャッシュから削除されます。 古い情報を削除するプロセスは、メモリスイープと呼ばれます。 メモリスイープは頻繁に発生するアクティビティですが、連続していません。 メモリ キャッシュのスイープはクロック アルゴリズムによって制御され、 各クロックは、両手と呼ばれる複数のメモリスイープを制御できます。 メモリキャッシュクロックハンドは、メモリスイープの1つの針の現在の場所です。  

## <a name="see-also"></a>参照  
 [SQL Server オペレーティングシステム関連の動的管理ビュー &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)    
 [dm_os_memory_cache_counters &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-counters-transact-sql.md)
  

