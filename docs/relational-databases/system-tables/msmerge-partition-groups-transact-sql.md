---
description: MSmerge_partition_groups (Transact-SQL)
title: MSmerge_partition_groups (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_partition_groups_TSQL
- MSmerge_partition_groups
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_partition_groups system table
ms.assetid: 5d56d780-ee40-4afc-9c2a-d1723d86e430
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 80216729e7fd71c4a3089ac92e1a0d73bb234c65
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545666"
---
# <a name="msmerge_partition_groups-transact-sql"></a>MSmerge_partition_groups (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_partition_groups**テーブルには、特定のデータベースの事前計算済みパーティションごとに1つの行が格納されます。 表示される列に加えて、パラメーター化された行フィルターで使用される関数ごとに1つの列がこのテーブルに追加されます。 たとえば、フィルターで[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)関数が使用されている場合は、 **HOST_NAME_FN**という名前の列がテーブルに追加されます。 このパブリッシャーと同期した関数値の一意のセットごとに1つの行が格納されます。 これらすべての関数について、まったく同じ値と同期している 2 つ以上のサブスクライバーは、このテーブルの同じ行を共有しているので、同じパーティション ID を共有します。このテーブルは、パブリケーション データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**partition_id**|**int**|事前計算済みパーティションの一意な ID 番号を示す ID 列です。|  
|**publication_number**|**smallint**|**Sysmergepublications**に格納されているパブリケーション番号。|  
|**maxgen_whenadded**|**bigint**|このテーブルに行が挿入される時点で、パブリッシャーで把握している最も古い generation 値です。|  
|**using_partition_groups**|**bit**|パーティションが事前計算済みパーティションを使用するパブリケーションに属しているかどうかを示し、次のいずれかの値を指定できます。<br /><br /> **0** = パブリケーションは事前計算済みパーティションを使用しません。<br /><br /> **1** = パブリケーションは事前計算済みパーティションを使用します。<br /><br /> 詳細については、「[事前計算済みパーティションによるパラメーター化されたフィルターのパフォーマンス最適化](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)」を参照してください。|  
|**HOST_NAME_FN**|**nvarchar(128)**|パラメーター化された行フィルターを使用してパーティションを生成するときに指定される値。 詳しくは、「 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)」をご覧ください。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
