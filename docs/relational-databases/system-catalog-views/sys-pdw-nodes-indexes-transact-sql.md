---
description: sys.pdw_nodes_indexes (Transact-sql)
title: sys.pdw_nodes_indexes (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: reference
dev_langs:
- TSQL
ms.assetid: 261bcb7f-a906-4979-b274-bc5f1aa66426
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest'
ms.openlocfilehash: a9fee9ec599444091e0543b0ed7e4fd326fdaa02
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99186508"
---
# <a name="syspdw_nodes_indexes-transact-sql"></a>sys.pdw_nodes_indexes (Transact-sql)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  のインデックスを返し [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ます。  
  
|列名|データ型|説明|Range|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|このインデックスが所属するオブジェクトの id。||  
|name|**sysname**|インデックス名。 Name は、オブジェクト内でのみ一意です。 NULL = ヒープ||  
|index_id|**int**|インデックスの id。 index_id は、オブジェクト内でのみ一意です。<br /><br /> 0 = ヒープ<br /><br /> 1 = クラスター化インデックス<br /><br /> > 1 = 非クラスター化インデックス||  
|type|**tinyint**|インデックスの種類:<br /><br /> 0 = ヒープ<br /><br /> 1 = クラスター化<br /><br /> 2 = 非クラスター化<br /><br /> 5 = クラスター化 xVelocity メモリ最適化列ストアインデックス|  
|type_desc|**nvarchar(60)**|インデックスの種類の説明:<br /><br /> HEAP<br /><br /> CLUSTERED<br /><br /> NONCLUSTERED<br /><br /> クラスター化列ストア||  
|is_unique|**bit**|0 = インデックスは一意ではありません。|常に 0 です。|  
|data_space_id|**int**|このインデックスのデータ領域の id。 データ領域は、ファイル グループまたはパーティション構成です。<br /><br /> 0 = object_id はテーブル値関数です。||  
|ignore_dup_key|**bit**|0 = IGNORE_DUP_KEY はオフです。|常に 0 です。|  
|is_primary_key|**bit**|1 = インデックスは PRIMARY KEY 制約の一部です。|常に 0 です。|  
|is_unique_constraint|**bit**|1 = インデックスは UNIQUE 制約の一部です。|常に 0 です。|  
|fill_factor|**tinyint**|> 0 = インデックスが作成または再構築されたときに使用される FILLFACTOR のパーセンテージ。<br /><br /> 0 = 既定値|常に 0 です。|  
|is_padded|**bit**|0 = PADINDEX はオフです。|常に 0 です。|  
|is_disabled|**bit**|1 = インデックスは無効です。<br /><br /> 0 = インデックスは無効になっていません。||  
|is_hypothetical|**bit**|0 = インデックスは仮想的ではありません。|常に 0 です。|  
|allow_row_locks|**bit**|1 = インデックスは行ロックを許可します。|常に1です。|  
|allow_page_locks|**bit**|1 = インデックスはページロックを許可します。|常に1です。|  
|has_filter|**bit**|0 = インデックスにフィルターがありません。|常に 0 です。|  
|filter_definition|**nvarchar(max)**|フィルター選択されたインデックスに含まれる行のサブセットの式。|常に NULL です。|  
|pdw_node_id|**int**|ノードの一意識別子 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 。|NOT NULL|  
  
## <a name="permissions"></a>アクセス許可  
 CONTROL SERVER 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [Azure Synapse Analytics と Parallel Data Warehouse のカタログ ビュー](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
