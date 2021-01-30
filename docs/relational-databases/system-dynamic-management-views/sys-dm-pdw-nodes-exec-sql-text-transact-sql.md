---
title: sys.dm_pdw_nodes_exec_sql_text (Transact-sql) |Microsoft Docs
description: 指定された sql_handle によって識別される SQL バッチのテキストを返す動的管理ビュー。
ms.custom: ''
ms.date: 10/14/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: reference
dev_langs:
- TSQL
ms.assetid: ''
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest
ms.openlocfilehash: 4e66c08b7e4a4a179a53c853e2802759f0627471
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99140473"
---
# <a name="syspdw_nodes_dm_exec_sql_text-transact-sql"></a>sys.pdw_nodes_dm_exec_sql_text (Transact-sql)
[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

指定された *sql_handle* によって識別される SQL バッチのテキストを返します。 このテーブル値関数は、システム関数 **fn_get_sql** に代わるものです。  
   
## <a name="table-returned"></a>返されたテーブル  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**pdw_node_id**|**int**|ノードに関連付けられている一意の数値 ID。|
|**dbid**|**smallint**|データベースの ID。<br /><br /> 計画外および準備された SQL ステートメントの場合、ステートメントがコンパイルされたデータベースの ID。|  
|**objectid**|**int**|オブジェクトの ID。<br /><br /> アドホック SQL ステートメントおよび準備された SQL ステートメントの場合は NULL になります。|  
|**number**|**smallint**|番号付きストアド プロシージャの場合、ストアド プロシージャの番号。 詳細については、「 [sys.numbered_procedures &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-numbered-procedures-transact-sql.md)」を参照してください。<br /><br /> アドホック SQL ステートメントおよび準備された SQL ステートメントの場合は NULL になります。|  
|**暗号**|**bit**|1: SQL テキストは暗号化されています。<br /><br /> 0: SQL テキストは暗号化されていません。|  
|**text**|**nvarchar(max)**|SQL クエリのテキスト。<br /><br /> 暗号化されているオブジェクトの場合は NULL になります。|  

## <a name="remarks"></a>コメント  
[Sys.dm_exec_sql_text](./sys-dm-exec-sql-text-transact-sql.md)の同じ解説が適用されます。  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する **sysadmin** サーバーロールまたは権限が必要 `VIEW SERVER STATE` です。  
  
## <a name="see-also"></a>関連項目  
 [Azure Synapse Analytics と並列データウェアハウスの動的管理ビュー &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  

  ## <a name="next-steps"></a>次のステップ
 開発に関するその他のヒントについては、「 [Azure Synapse Analytics の開発の概要](/azure/sql-data-warehouse/sql-data-warehouse-overview-develop)」を参照してください。