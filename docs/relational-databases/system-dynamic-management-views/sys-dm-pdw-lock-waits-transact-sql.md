---
description: sys.dm_pdw_lock_waits (Transact-sql)
title: sys.dm_pdw_lock_waits (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8ef966f8-d14e-40d3-9626-3508ada9b8fb
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 0e3ddfbf5c6bb0aaa06a28091bce99c90bf4beb6
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035355"
---
# <a name="sysdm_pdw_lock_waits-transact-sql"></a>sys.dm_pdw_lock_waits (Transact-sql)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  ロックを待機している要求に関する情報を保持します。  
  
|列名|データ型|説明|Range|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**bigint**|待機リスト内の要求の位置。|0から始まる序数。 これは、すべての待機エントリで一意ではありません。|  
|session_id|**nvarchar(32)**|待機状態が発生したセッションの ID。|[Transact-sql&#41;&#40;sys.dm_pdw_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)の session_id を参照してください。|  
|type|**nvarchar (255)**|このエントリが表す待機の種類。|指定できる値<br /><br /> 共有<br /><br /> SharedUpdate<br /><br /> ExclusiveUpdate<br /><br /> 排他的|  
|object_type|**nvarchar (255)**|待機の影響を受けるオブジェクトの種類。|指定できる値<br /><br /> OBJECT<br /><br /> DATABASE<br /><br /> SYSTEM<br /><br /> SCHEMA<br /><br /> APPLICATION|  
|object_name|**nvarchar (386)**|待機の影響を受けた、指定したオブジェクトの名前または GUID。|テーブルとビューは、3つの部分で構成される名前で表示されます。<br /><br /> インデックスと統計情報は、4つの部分で構成される名前で表示されます。<br /><br /> 名前、プリンシパル、およびデータベースは、文字列名です。|  
|request_id|**nvarchar(32)**|待機状態が発生した要求の ID。|要求の ID。<br /><br /> これは、読み込み要求の GUID です。|  
|request_time|**datetime**|ロックまたはリソースが要求された時刻。||  
|acquire_time|**datetime**|ロックまたはリソースが取得された時刻。||  
|state|**nvarchar (50)**|待機状態の状態。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**int**|待機中の項目の優先順位。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
  
## <a name="see-also"></a>参照  
 [Azure Synapse Analytics と並列データウェアハウスの動的管理ビュー &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
