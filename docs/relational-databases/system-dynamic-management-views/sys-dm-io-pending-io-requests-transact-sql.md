---
description: sys.dm_io_pending_io_requests (Transact-SQL)
title: dm_io_pending_io_requests (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_io_pending_io_requests
- dm_io_pending_io_requests
- dm_io_pending_io_requests_TSQL
- sys.dm_io_pending_io_requests_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_io_pending_io_requests dynamic management view
ms.assetid: d1fb46dd-5c74-4c04-9ecf-8934b1bedb5b
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7e61b234942d6e486886ae8238db8b9c68e65385
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89532533"
---
# <a name="sysdm_io_pending_io_requests-transact-sql"></a>sys.dm_io_pending_io_requests (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で保留中の I/O 要求ごとに 1 行のデータを返します。  
  
> [!NOTE]  
>  またはからこれを呼び出すに [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] は [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 、 **dm_pdw_nodes_io_pending_io_requests**という名前を使用します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**io_completion_request_address**|**varbinary (8)**|IO 要求のメモリアドレス。 NULL 値は許可されません。|  
|**io_type**|**nvarchar(60)**|保留中の I/O 要求の種類。 NULL 値は許可されません。|  
|**io_pending_ms_ticks**|**bigint**|内部使用のみです。 NULL 値は許可されません。| 
|**io_pending**|**int**|I/o 要求が Windows によって保留されているか、完了しているかを示します。 I/o 要求は、Windows が要求を完了しているにもかかわらず、i/o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 要求を処理してこの一覧から削除するコンテキストスイッチをまだ実行していない場合でも保留状態になることがあります。 NULL 値は許可されません。|  
|**io_completion_routine_address**|**varbinary (8)**|I/O 要求が完了したときに呼び出される内部関数。 NULL 値が許可されます。|  
|**io_user_data_address**|**varbinary (8)**|内部使用のみです。 NULL 値が許可されます。|  
|**scheduler_address**|**varbinary (8)**|この i/o 要求が発行されたスケジューラ。 I/o 要求は、スケジューラの保留中の i/o の一覧に表示されます。 詳細については、「 [sys. dm_os_schedulers &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md)」を参照してください。 NULL 値は許可されません。|  
|**io_handle**|**varbinary (8)**|I/o 要求で使用されるファイルのファイルハンドル。 NULL 値が許可されます。|  
|**io_offset**|**bigint**|I/O 要求のオフセット。 NULL 値は許可されません。|  
|**io_handle_path**|**nvarchar (256)**| I/o 要求で使用されるファイルのパス。 NULL 値が許可されます。|
|**pdw_node_id**|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> このディストリビューションが配置されているノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可  

で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium レベルでは、データベースの権限が必要です `VIEW DATABASE STATE` 。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Standard レベルおよび Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [I O 関連の動的管理ビューおよび関数 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


