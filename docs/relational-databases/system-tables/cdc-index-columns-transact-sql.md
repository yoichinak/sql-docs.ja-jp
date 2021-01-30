---
description: cdc.index_columns (Transact-sql)
title: cdc.index_columns (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- cdc.index_columns_TSQL
- cdc.index_columns
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.index_columns
ms.assetid: 256ec8a5-3031-40a8-9fdb-99db42ea453d
author: cawrites
ms.author: chadam
ms.openlocfilehash: 0eeac23e94fa1927e5b5efd573fd19fb8935d6f4
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99183300"
---
# <a name="cdcindex_columns-transact-sql"></a>cdc.index_columns (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  変更テーブルに関連付けられている各インデックス列に対して1行の値を返します。 インデックス列は、ソーステーブル内の行を一意に識別するために、変更データキャプチャによって使用されます。 既定では、ソース テーブルの主キー列が含まれます。 ただし、ソース テーブルに対して変更データ キャプチャを有効にする際、ソース テーブルの一意のインデックスが指定された場合は、代わりにそのインデックスの列が使用されます。 差分変更の追跡が有効になっている場合、ソーステーブルには主キーまたは一意のインデックスが必要です。 詳細については、「 [sys.sp_cdc_enable_table &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)」を参照してください。  
  
 システムテーブルに対して直接クエリを実行しないことをお勧めします。 代わりに、 [sys.sp_cdc_help_change_data_capture](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md) ストアドプロシージャを実行します。  

  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|変更テーブルの ID。|  
|**column_name**|**sysname**|インデックス列の名前。|  
|**index_ordinal**|**tinyint**|インデックス内の列の 1 から始まる序数。|  
|**column_id**|**int**|ソーステーブル内の列の ID。|  
  
## <a name="see-also"></a>参照  
 [cdc.change_tables &#40;Transact-sql&#41;](../../relational-databases/system-tables/cdc-change-tables-transact-sql.md)  
  
  
