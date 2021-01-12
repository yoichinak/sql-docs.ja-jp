---
description: MSmerge_dynamic_snapshots (Transact-SQL)
title: MSmerge_dynamic_snapshots (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_dynamic_snapshots_TSQL
- MSmerge_dynamic_snapshots
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_dynamic_snapshots system table
ms.assetid: a5592b3c-731b-4fc9-ae4b-2602ed78248e
author: cawrites
ms.author: chadam
ms.openlocfilehash: 10d3e082032daa3782e15caa20d43e8eb4130bd5
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98091425"
---
# <a name="msmerge_dynamic_snapshots-transact-sql"></a>MSmerge_dynamic_snapshots (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_dynamic_snapshots** テーブルでは、パラメーター化された行フィルターを使用して、マージパブリケーションに対して定義されている各パーティションのフィルター選択されたデータスナップショットの場所を追跡します。 このテーブルは、 **パブリケーション** データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**partition_id**|**int**|マージ パーティションの ID。|  
|**dynamic_snapshot_location**|**nvarchar (255)**|パーティションのフィルター選択されたデータスナップショットの場所です。|  
|**last_updated**|**datetime**|フィルター選択されたデータスナップショットが更新された日付。|  
  
## <a name="see-also"></a>参照  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
