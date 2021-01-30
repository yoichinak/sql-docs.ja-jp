---
description: IHpublishercolumnindexes (Transact-SQL)
title: IHpublishercolumnindexes (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- IHpublishercolumnindexes
- IHpublishercolumnindexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishercolumnindexes system table
ms.assetid: 95b95a1d-b502-4838-825f-82a456487e25
author: cawrites
ms.author: chadam
ms.openlocfilehash: 13d7e4240b86950b21889f660d9e228eb09552e7
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99201671"
---
# <a name="ihpublishercolumnindexes-transact-sql"></a>IHpublishercolumnindexes (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **IHpublishercolumnindexes** システムテーブルは、 [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md)システムテーブル内の非 SQL Server パブリケーションの列を [IHpublisherindexes](../../relational-databases/system-tables/ihpublisherindexes-transact-sql.md)システムテーブルのインデックスにマップします。 このテーブルは、ディストリビューションデータベースに格納されます。  
  
## <a name="definition"></a>定義  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**int**|[IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md)から、関連付けられたインデックスを持つ列を識別します。|  
|**publisherindex_id**|**int**|列に関連付けられている [IHpublisherindexes](../../relational-databases/system-tables/ihpublisherindexes-transact-sql.md) テーブルのインデックスを識別します。|  
|**indid**|**int**|パブリッシュされたテーブル内の列の位置を示します。|  
  
## <a name="see-also"></a>参照  
 [異種データベース レプリケーション](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
