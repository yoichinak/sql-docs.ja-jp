---
description: cdc. index_columns (Transact-sql)
title: cdc. index_columns (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc.index_columns_TSQL
- cdc.index_columns
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.index_columns
ms.assetid: 256ec8a5-3031-40a8-9fdb-99db42ea453d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5cf09c3a66a3db1b7275dfe8017d953aaf57b42d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544641"
---
# <a name="cdcindex_columns-transact-sql"></a>cdc. index_columns (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  変更テーブルに関連付けられている各インデックス列に対して1行の値を返します。 インデックス列は、ソーステーブル内の行を一意に識別するために、変更データキャプチャによって使用されます。 既定では、ソース テーブルの主キー列が含まれます。 ただし、ソース テーブルに対して変更データ キャプチャを有効にする際、ソース テーブルの一意のインデックスが指定された場合は、代わりにそのインデックスの列が使用されます。 差分変更の追跡が有効になっている場合、ソーステーブルには主キーまたは一意のインデックスが必要です。 詳細については、「 [sys. sp_cdc_enable_table &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)」を参照してください。  
  
 システムテーブルに対して直接クエリを実行しないことをお勧めします。 代わりに、 [sp_cdc_help_change_data_capture](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md) ストアドプロシージャを実行します。  

  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|変更テーブルの ID。|  
|**column_name**|**sysname**|インデックス列の名前。|  
|**index_ordinal**|**tinyint**|インデックス内の列の 1 から始まる序数。|  
|**column_id**|**int**|ソーステーブル内の列の ID。|  
  
## <a name="see-also"></a>参照  
 [cdc. change_tables &#40;Transact-sql&#41;](../../relational-databases/system-tables/cdc-change-tables-transact-sql.md)  
  
  
