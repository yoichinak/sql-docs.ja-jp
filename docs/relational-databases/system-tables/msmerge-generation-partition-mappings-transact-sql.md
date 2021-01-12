---
title: MSmerge_generation_partition_mappings (T-sql)
description: マージパブリケーションのパーティションに対する変更を追跡するために使用される MSmerge_generation_partition_mappings ストアドプロシージャについて説明します。
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_generation_partition_mappings_TSQL
- MSmerge_generation_partition_mappings
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_generation_partition_mappings system table
ms.assetid: 443a4024-ce48-4772-9ee5-95bd6fb6476b
author: cawrites
ms.author: chadam
ms.openlocfilehash: 7e4bc8d5e833f5ca4c9c19c81985f744c497dfcd
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98102061"
---
# <a name="msmerge_generation_partition_mappings-transact-sql"></a>MSmerge_generation_partition_mappings (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_generation_partition_mappings** テーブルは、マージパブリケーションのパーティションに対する変更を追跡するために使用されます。 このテーブルは、パブリケーションデータベースおよび scubscription データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publication_number**|**smallint**|マージ パブリケーションを識別します。|  
|**generation**|**bigint**|生成値。|  
|**partition_id**|**int**|パーティションを識別します。|  
|**changecount**|**int**|パーティションが変更された回数。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
