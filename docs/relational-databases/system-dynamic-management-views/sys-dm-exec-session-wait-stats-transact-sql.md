---
description: sys.dm_exec_session_wait_stats (Transact-sql)
title: sys.dm_exec_session_wait_stats (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sys.dm_exec_session_wait_stats
- sys.dm_exec_session_wait_stats_tsql
- dm_exec_session_wait_stats
- dm_exec_session_wait_stats_tsql
helpviewer_keywords:
- sys.dm_exec_session_wait_stats
ms.assetid: df84842a-71eb-4fda-b448-5953cf9985dc
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: f909ebd3f604fc8c56b08cadc1e70915da061de7
ms.sourcegitcommit: b1cec968b919cfd6f4a438024bfdad00cf8e7080
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2021
ms.locfileid: "99236887"
---
# <a name="sysdm_exec_session_wait_stats-transact-sql"></a>sys.dm_exec_session_wait_stats (Transact-sql)

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

  各セッションで実行されたスレッドによって検出されたすべての待機に関する情報を返します。 このビューを使用すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セッション、および特定のクエリとバッチに関するパフォーマンスの問題を診断できます。  このビューでは、 [sys.dm_os_wait_stats &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md) に対して集計されたものと同じ情報が返されますが、 **session_id** 番号も表示されます。  
  
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sssql16-md](../../includes/sssql16-md.md)] 以降)。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|セッションの id。|  
|wait_type|**nvarchar(60)**|待機の種類の名前。 詳細については、「[sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)」を参照してください。|  
|waiting_tasks_count|**bigint**|この待機の種類における待機の数。 このカウンターは、待機が開始するたび増加します。|  
|wait_time_ms|**bigint**|この待機の種類における総待機時間 (ミリ秒単位)。 この時間には signal_wait_time_ms が含まれます。|  
|max_wait_time_ms|**bigint**|この待機の種類における最大待機時間。|  
|signal_wait_time_ms|**bigint**|待機スレッドがシグナルを受け取ってから実行を開始するまでの時間。|  
  
## <a name="remarks"></a>解説  
 この DMV は、セッションが開かれたとき、またはセッションがリセットされたとき (接続プールがある場合) に、セッションの情報をリセットします。  
  
 待機の種類の詳細については、「 [sys.dm_os_wait_stats &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 ユーザーがサーバーに対する **VIEW SERVER STATE** 権限を持っている場合、ユーザーにはのインスタンスで実行中のすべてのセッションが表示されます。それ以外の場合、ユーザーには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 現在のセッションのみが表示されます。  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [SQL Server オペレーティングシステム関連の動的管理ビュー &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)  
 
