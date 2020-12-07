---
description: IHcolumns (Transact-sql)
title: IHcolumns (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHcolumns_TSQL
- IHcolumns
dev_langs:
- TSQL
helpviewer_keywords:
- IHcolumns system table
ms.assetid: 5bb027e5-5279-487b-9c33-5f402987253c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a27e72b46fed5f814e91d447abf30c9c905cba4d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540984"
---
# <a name="ihcolumns-transact-sql"></a>IHcolumns (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **IHcolumns**システムテーブルには、パブリッシュされた列ごとに1つの行が含まれています。 このテーブルは、SQL&#xA0;Server 以外のパブリッシャーの列のデータ型がパブリッシュされたときの表示方法を定義するために使用されます。これにより、実質的に、SQL&#xA0;Server 以外のデータベース管理システム (DBMS) と SQL&#xA0;Server の間でデータ型をマップします。 このテーブルは、ディストリビューションデータベースに格納されます。  
  
## <a name="definition"></a>定義  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**column_id**|**int**|パブリッシュされた列を識別します。|  
|**publishercolumn_id**|**int**|パブリッシュされた列を、 [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) システムテーブルに格納されている列のメタデータに関連付けます。|  
|**name**|**sysname**|列名を指定します。|  
|**article_id**|**int**|列が属しているアーティクルを識別します。|  
|**column_ordinal**|**int**|順序に基づいた列の識別子。|  
|**mapped_type**|**tinyint**|サブスクライバーのマップ先となる列のデータ型です。|  
|**mapped_length**|**bigint**|サブスクライバーの列の長さです。|  
|**mapped_prec**|**int**|サブスクライバーの列の有効桁数です。|  
|**mapped_scale**|**int**|サブスクライバーの列の小数点以下桁数です。|  
|**mapped_nullable**|**bit**|サブスクライバーの列で NULL 値を許容するかどうかを示します。 **1** は null 値が許容されることを示します。|  
  
## <a name="see-also"></a>参照  
 [異種データベース レプリケーション](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーションビュー &#40;Transact-sql&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_articlecolumn (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sysarticlecolumns &#40;システムビュー&#41; &#40;Transact-sql&#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)   
 [sysarticlecolumns &#40;Transact-sql&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
