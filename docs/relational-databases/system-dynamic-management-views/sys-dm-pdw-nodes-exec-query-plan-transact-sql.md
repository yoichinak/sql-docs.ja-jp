---
title: sys.dm_pdw_nodes_exec_query_plan (Transact-sql) |Microsoft Docs
description: プランハンドルで指定されたバッチのプラン表示を XML 形式で返す動的管理ビュー。 プラン ハンドルで指定するプランは、キャッシュ内のもの、または現在実行中のものを指定できます。
ms.custom: ''
ms.date: 10/14/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ''
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 06c5acb9480f52d0cadf84c54aa39bbc9bae12d9
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584938"
---
# <a name="syspdw_nodes_dm_exec_query_plan-transact-sql"></a>sys.pdw_nodes_dm_exec_query_plan (Transact-sql)
[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

プラン ハンドルで指定されたバッチのプラン表示を XML 形式で返します。 プラン ハンドルで指定するプランは、キャッシュ内のもの、または現在実行中のものを指定できます。  

> [!note] 
> Synapse SQL では、クエリに空白を追加すると、クエリハッシュが再計算され、以前にキャッシュされた実行プランが再利用されないクエリの変更として構成されます。


## <a name="table-returned"></a>返されたテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**pdw_node_id**|**int**|ノードに関連付けられている一意の数値 ID。| 
|**dbid**|**smallint**|このプランに対応する [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントがコンパイルされたときに有効であったコンテキスト データベースの ID。 計画外および準備された SQL ステートメントの場合、ステートメントがコンパイルされたデータベースの ID。<br /><br /> NULL 値は許可されます。|  
|**objectid**|**int**|ストアド プロシージャやユーザー定義関数など、クエリ プランのオブジェクトの ID。 アドホック バッチおよび準備されたバッチの場合、この列の値は **NULL** です。<br /><br /> NULL 値は許可されます。|  
|**number**|**smallint**|ストアド プロシージャに付けられた番号 (整数)。 アドホック バッチおよび準備されたバッチの場合、この列の値は **NULL** です。<br /><br /> NULL 値は許可されます。| 
|**暗号**|**bit**|対応するプロシージャが暗号化されているかどうか。<br /><br /> 0 = 暗号化されていない<br /><br /> 1 = 暗号化されている<br /><br /> NULL 値は許可されません。|  
|**query_plan**|**xml**|*Plan_handle* で指定されたクエリ実行プランのコンパイル時のプラン表示表現を格納します。 プラン表示は XML 形式です。 アドホック [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント、ストアド プロシージャ コール、ユーザー定義関数コールなどを含むバッチごとに、1 つのプランが生成されます。<br /><br /> NULL 値は許可されます。|  
  
## <a name="remarks"></a>注釈  
[Sys.dm_exec_query_plan](./sys-dm-exec-query-plan-transact-sql.md?view=sql-server-ver15)の同じ解説が適用されます。  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する **sysadmin** サーバーロールまたは権限が必要 `VIEW SERVER STATE` です。  
  
## <a name="see-also"></a>関連項目  
 [Azure Synapse Analytics と並列データウェアハウスの動的管理ビュー &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  

 ## <a name="next-steps"></a>次のステップ
 開発に関するその他のヒントについては、「 [Azure Synapse Analytics の開発の概要](/azure/sql-data-warehouse/sql-data-warehouse-overview-develop)」を参照してください。
