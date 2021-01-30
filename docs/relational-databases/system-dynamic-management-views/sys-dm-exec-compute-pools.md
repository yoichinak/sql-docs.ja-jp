---
description: sys.dm_exec_compute_pools (Transact-sql)
title: sys.dm_exec_compute_pools (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, big-data-clusters
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sys.dm_exec_compute_pools
- dm_exec_compute_pools_TSQL
- dm_exec_compute_pools
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_compute_pools dynamic management view
ms.assetid: ''
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: '>=sql-server-ver15||>=sql-server-linux-2017'
ms.openlocfilehash: 563bbedbf9a39a7cf1f3aeb6434f134bafb97d73
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99106186"
---
# <a name="sysdm_exec_compute_pools-transact-sql"></a>sys.dm_exec_compute_pools (Transact-sql)
[!INCLUDE[sqlserver2019](../../includes/applies-to-version/sqlserver2019.md)]

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|name|`sysname`|コンピューティングプールの名前。 NULL 値は許可されません。 `default`既定のコンピューティングプールに対してを返します。 |
|compute_pool_id|`int`|プールの一意の識別子。 このビューのキー。|  
|location|`sysname`|SQL ビッグデータクラスター内のコントローラーへのエンドポイント。 NULL 値は許可されません。 |

## <a name="permissions"></a>アクセス許可

で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。

## <a name="see-also"></a>参照

[概要 [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ss-nover.md)] ](../../big-data-cluster/big-data-cluster-overview.md)
