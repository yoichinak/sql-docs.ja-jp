---
description: IHpublisherconstraints (Transact-sql)
title: IHpublisherconstraints (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublisherconstraints
- IHpublisherconstraints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublisherconstraints system table
ms.assetid: 537b1e1a-7228-4680-aa27-5ad7072ea01e
author: cawrites
ms.author: chadam
ms.openlocfilehash: d53c7bdee115715b8513356f02a3afddc75ec118
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98092459"
---
# <a name="ihpublisherconstraints-transact-sql"></a>IHpublisherconstraints (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **IHpublisherconstraints** システムテーブルには、現在のディストリビューターを使用して SQL Server 以外のパブリッシャーからレプリケートされた制約ごとに1つの行が含まれています。 このテーブルは、ディストリビューションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisherconstraint_id**|**int**|パブリッシュされた制約を識別します。|  
|**table_id**|**int**|制約が属している [IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md) からテーブルを識別します。|  
|**publisher_id**|**smallint**|列がパブリッシュされる SQL Server 以外のパブリッシャーを指定します。|  
|**名前**|**Sysname**|パブリッシュされた制約の名前です。|  
|**Type**|**nvarchar (255)**|[IHconstrainttypes](../../relational-databases/system-tables/ihconstrainttypes-transact-sql.md)システムテーブルからサポートされている制約の種類。|  
  
## <a name="see-also"></a>参照  
 [異種データベース レプリケーション](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
