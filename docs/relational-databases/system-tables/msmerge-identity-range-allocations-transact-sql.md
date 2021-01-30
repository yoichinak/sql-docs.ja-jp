---
description: MSmerge_identity_range_allocations (Transact-sql)
title: MSmerge_identity_range_allocations (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- MSmerge_identity_range_allocations
- MSmerge_identity_range_allocations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_identity_range_allocations system table
ms.assetid: 6362e35e-0ab3-4638-855b-1ce013f5fd6d
author: cawrites
ms.author: chadam
ms.openlocfilehash: c86e1c65af5852d08ea3e1bd331ab04be8c5a5ab
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99209609"
---
# <a name="msmerge_identity_range_allocations-transact-sql"></a>MSmerge_identity_range_allocations (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_identity_range_allocations** テーブルは、パブリッシュされたアーティクルについて、パブリッシャーとサブスクライバーの両方に対する id 範囲の割り当ての履歴を追跡するために使用されます。 このテーブルは、ディストリビューションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|パブリッシャーの ID。|  
|**publisher_db**|**nvarchar(128)**|パブリケーションデータベースの名前です。|  
|**レプリケーション**|**nvarchar(128)**|パブリケーションの名前を指定します。|  
|**記事**|**nvarchar(128)**|アーティクルの名前です。|  
|**サブスクライバ**|**nvarchar(128)**|サブスクライバーの名前です。|  
|**subscriber_db**|**nvarchar(128)**|サブスクリプションデータベースの名前。|  
|**is_pub_range**|**bit**|Id 範囲がパブリッシャーに割り当てられているかどうかを示します。|  
|**ranges_allocated**|**tinyint**|割り当てられている ID 範囲の数です。|  
|**range_begin**|**数値 (38)**|範囲の開始値。|  
|**range_end**|**数値 (38)**|範囲内の最後の値。|  
|**next_range_begin**|**数値 (38)**|次の範囲で割り当てられる開始値です。|  
|**next_range_end**|**数値 (38)**|割り当てられる次の範囲の最後の値。|  
|**max_used**|**数値 (38)**|使用されている最大 ID 値です。|  
|**time_of_allocation**|**datetime**|割り当てが行われた時刻。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
