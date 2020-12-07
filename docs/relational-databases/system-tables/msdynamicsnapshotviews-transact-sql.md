---
description: MSdynamicsnapshotviews (Transact-SQL)
title: MSdynamicsnapshotviews (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdynamicsnapshotviews_TSQL
- MSdynamicsnapshotviews
dev_langs:
- TSQL
helpviewer_keywords:
- MSdynamicsnapshotviews system table
ms.assetid: 4fc1822a-5d6e-4034-a2e2-363210232d3b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6a89b139970822482e8b0745d9ceeefe8bba3f94
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538273"
---
# <a name="msdynamicsnapshotviews-transact-sql"></a>MSdynamicsnapshotviews (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **Msdynamicsnapshotviews**テーブルは、スナップショットエージェントによって作成された一時フィルター選択されたすべてのデータスナップショットビューを追跡し、SQL Server エージェントまたはスナップショットエージェントが異常終了した場合に、ビューをクリーンアップするためにシステムによって使用されます。 このテーブルは、パブリケーションデータベースとサブスクリプションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**dynamic_snapshot_view_name**|**sysname**|一時的なフィルター選択されたデータ スナップショット ビューの名前です。|  
  
## <a name="see-also"></a>参照  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
