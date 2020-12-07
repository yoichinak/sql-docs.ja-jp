---
description: IHpublishercolumns (Transact-SQL)
title: IHpublishercolumns (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublishercolumns
- IHpublishercolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishercolumns system table
ms.assetid: a5347750-224c-40d9-ae12-57e7213b7db9
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 49d4da72bc68d375b7c918768b656e025c4dc6f2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89524996"
---
# <a name="ihpublishercolumns-transact-sql"></a>IHpublishercolumns (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **IHpublishercolumns**システムテーブルは、パブリッシャーに格納されているメタデータを表します。 このテーブルには、現在のディストリビューターを使用して SQL Server 以外のパブリッシャーからレプリケートされた列ごとに1つの行が含まれています。 **IHpublishercolumns**のデータ型情報は、データのパブリッシュ元である非 SQL Server データベース管理システム (DBMS) に固有です。 このテーブルは、ディストリビューションデータベースに格納されます。  
  
## <a name="definition"></a>定義  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**int**|パブリッシュされた列を識別します。|  
|**table_id**|**int**|列が属している [IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md) からソーステーブルを識別します。|  
|**publisher_id**|**smallint**|列がパブリッシュされる SQL Server 以外のパブリッシャーを指定します。|  
|**name**|**sysname**|パブリッシュされた列の名前。|  
|**column_ordinal**|**int**|順序に基づいた列の識別子。|  
|**type**|**varchar(255)**|パブリッシャーのソース列の列のデータ型です。|  
|**length**|**bigint**|パブリッシャーのソース列の長さ。|  
|**prec**|**int**|パブリッシャーのソース列の有効桁数です。|  
|**scale**|**int**|パブリッシャーのソース列の小数点以下桁数です。|  
|**isnullable**|**bit**|列で NULL 値を許容するかどうかを示します。 **1** は null 値が許容されることを示します。|  
|**iscaptured**|**bit**|列にトリガーが存在するかどうかを示します。これは、の列がアーティクルにパブリッシュされていない場合でも存在する可能性があります。 値 **1** は、列にトリガーが存在することを意味します。|  
  
## <a name="see-also"></a>参照  
 [異種データベース レプリケーション](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーションビュー &#40;Transact-sql&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sysarticlecolumns &#40;システムビュー&#41; &#40;Transact-sql&#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)   
 [sysarticlecolumns &#40;Transact-sql&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
