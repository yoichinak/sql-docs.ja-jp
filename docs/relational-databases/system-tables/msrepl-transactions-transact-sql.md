---
description: MSrepl_transactions (Transact-sql)
title: MSrepl_transactions (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_transactions_TSQL
- MSrepl_transactions
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_transactions system table
ms.assetid: d325288d-47ae-4488-8799-122f7ab43459
author: cawrites
ms.author: chadam
ms.openlocfilehash: 6e9ca4af77c9cab4e64a515041e68e4eb3dae3b6
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98092413"
---
# <a name="msrepl_transactions-transact-sql"></a>MSrepl_transactions (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSrepl_transactions** テーブルには、レプリケートされたトランザクションごとに1つの行が含まれます。 このテーブルは、ディストリビューションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**int**|パブリッシャーデータベースの ID。|  
|**xact_id**|**varbinary(16)**|トランザクションの ID。|  
|**xact_seqno**|**varbinary(16)**|トランザクションのシーケンス番号。|  
|**entry_time**|**datetime**|トランザクションがディストリビューションデータベースに入力された時刻です。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
