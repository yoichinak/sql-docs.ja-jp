---
description: MSmerge_current_partition_mappings
title: MSmerge_current_partition_mappings |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_current_partition_mappings
- MSmerge_current_partition_mappings_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_current_partition_mappings system table
ms.assetid: a3088840-5a30-40f5-8e8a-aa03afc4905f
author: cawrites
ms.author: chadam
ms.openlocfilehash: 89ac58572c4e0888a9313542483ea542875a41b8
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98091426"
---
# <a name="msmerge_current_partition_mappings"></a>MSmerge_current_partition_mappings
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_current_partition_mappings** テーブルには、特定の変更された行が属しているパーティション id ごとに1つの行が格納されます。 このテーブルは、パブリケーションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publication_number**|**smallint**|**Sysmergepublications** に格納されているパブリケーション番号。|  
|**tablenick**|**int**|パブリッシュされたテーブルのニックネーム。|  
|**rowguid**|**uniqueidentifier**|指定された行の行識別子。|  
|**partition_id**|**int**|行が属するパーティションの ID。 行の変更がすべてのサブスクライバーに関連する場合、値は-1 です。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
