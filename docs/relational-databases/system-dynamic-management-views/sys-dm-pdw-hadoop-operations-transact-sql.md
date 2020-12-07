---
description: sys.dm_pdw_hadoop_operations (Transact-sql)
title: sys.dm_pdw_hadoop_operations (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5d2337d4-e2c7-48de-9c26-cdc7e6eb5d55
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: d86092480b71c6971a72f70fe8b00b4fd10c497e
ms.sourcegitcommit: 32135463a8494d9ed1600a58f51819359e3c09dc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2020
ms.locfileid: "91834361"
---
# <a name="sysdm_pdw_hadoop_operations-transact-sql"></a>sys.dm_pdw_hadoop_operations (Transact-sql)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  外部 Hadoop テーブルに対するクエリの実行の一部として Hadoop にプッシュされるマップ削減ジョブごとに1行の情報を格納 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] します。 各 map reduce ジョブは、クエリ内のいずれかの述語を表します。 これは、Hadoop の外部テーブルに対するクエリに対して述語のプッシュダウンが有効になっている場合にのみ使用されます。  
  
|列名|データ型|説明|Range|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|この外部 Hadoop 操作の ID。|[Sys.dm_pdw_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)の ID と同じです。|  
|step_index|**int**|この Hadoop 操作を参照するクエリステップのインデックス。|[Sys.dm_pdw_request_steps &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)の step_index と同じです。|  
|operation_type|**nvarchar (255)**|外部操作の種類を記述します。|' 外部 Hadoop 操作 '|  
|operation_name|**nvarchar (4000)**|マップ削減ジョブのジョブ ID。 これは、ジョブを送信した後に Hadoop によって返され [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ます。||  
|map_progress|**float**|マップジョブによってこれまでに使用された入力データの割合。|、0、および100の間の浮動小数点数。|  
|reduce_progress|**int**|完了した reduce ジョブの割合。|、0、および100の間の浮動小数点数。|  
  
## <a name="see-also"></a>参照  
 [システムビュー &#40;Transact-sql&#41;](../../t-sql/language-reference.md)  
  
