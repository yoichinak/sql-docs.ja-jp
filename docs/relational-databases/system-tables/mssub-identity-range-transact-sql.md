---
description: MSsub_identity_range (Transact-SQL)
title: MSsub_identity_range (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- MSsub_identity_range_TSQL
- MSsub_identity_range
dev_langs:
- TSQL
helpviewer_keywords:
- MSsub_identity_range system table
ms.assetid: 26e20d28-14ed-44fc-af3b-4de386de4bb8
author: cawrites
ms.author: chadam
ms.openlocfilehash: b57fc0593298e38f6db8969e742127c007411246
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99156798"
---
# <a name="mssub_identity_range-transact-sql"></a>MSsub_identity_range (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSsub_identity_range** テーブルでは、サブスクリプションの id 範囲管理がサポートされています。 このテーブルは、subscription データベースに保存されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**objid**|**int**|レプリケーションで管理される ID 列を持つテーブルの ID です。|  
|**range**|**bigint**|サブスクライバーで調整によって割り当てられる連続する id 値の範囲のサイズを制御します。|  
|**last_seed**|**bigint**|現在の範囲の下限。|  
|**threshold**|**int**|ディストリビューション エージェントがどの時点で新しい ID 範囲を割り当てるかを制御するパーセンテージの値です。 [ *しきい* 値] で指定した値のパーセンテージが使用されると、ディストリビューションエージェントによって新しい id 範囲が作成されます。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
