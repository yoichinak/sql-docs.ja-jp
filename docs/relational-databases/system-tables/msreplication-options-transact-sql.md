---
description: MSreplication_options (Transact-sql)
title: MSreplication_options (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- MSreplication_options
- MSreplication_options_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_options system table
ms.assetid: 23cf10d7-8bc1-4368-b5eb-e5576421e776
author: cawrites
ms.author: chadam
ms.openlocfilehash: e5df7d73eab0c5766468b59207b29ecb45e2e56e
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99199067"
---
# <a name="msreplication_options-transact-sql"></a>MSreplication_options (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSreplication_options** テーブルには、レプリケーションによって内部的に使用されるメタデータが格納されます。 このテーブルは、 **master** データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**optname**|**sysname**|内部使用のみ。|  
|**value**|**bit**|内部使用のみ。|  
|**major_version**|**int**|内部使用のみ。|  
|**minor_version**|**int**|内部使用のみ。|  
|**revision**|**int**|内部使用のみ。|  
|**install_failures**|**int**|内部使用のみ。|  
  
## <a name="see-also"></a>参照  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
