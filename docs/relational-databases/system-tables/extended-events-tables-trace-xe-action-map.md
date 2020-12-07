---
description: 拡張イベント テーブル - trace_xe_action_map
title: trace_xe_action_map (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- trace_xe_action_map_TSQL
- trace_xe_action_map
dev_langs:
- TSQL
helpviewer_keywords:
- extended events [SQL Server], tables
- trace_xe_action_map
ms.assetid: 208a1413-ce7f-4521-b765-d74723627302
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5f3b742741d3add5b54c07d3cec4f47bbd919e2d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540417"
---
# <a name="extended-events-tables---trace_xe_action_map"></a>拡張イベント テーブル - trace_xe_action_map
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  SQL トレース列 ID に割り当てられている拡張イベントのアクションごとに 1 行のデータを格納します。 このテーブルは、sys スキーマの master データベースに格納されます。  
  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|trace_column_id|**smallint**|マップされる SQL トレース列の ID。|  
|package_name|**nvarchar(60)**|マップされたアクションがある拡張イベント パッケージの名前です。|  
|xe_action_name|**nvarchar(60)**|SQL トレース列にマップされる拡張イベントアクションの名前です。|  
  
## <a name="remarks"></a>解説  
 次のクエリを使用して、SQL トレース列に相当する拡張イベントアクションを特定できます。  
  
```  
SELECT tc.name AS trace_column, am.package_name, am.xe_action_name  
FROM sys.trace_columns AS tc  
INNER JOIN sys.trace_xe_action_map AS am  
   ON tc.trace_column_id = am.trace_column_id  
```  
  
 アクションにマップされない SQL トレース列は、テーブルには含まれません。  
  
## <a name="see-also"></a>参照  
 [trace_xe_event_map &#40;Transact-SQL&#41;](../../relational-databases/system-tables/extended-events-tables-trace-xe-event-map.md)  
  
  
