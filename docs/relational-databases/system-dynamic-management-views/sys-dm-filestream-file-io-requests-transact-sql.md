---
description: sys.dm_filestream_file_io_requests (Transact-SQL)
title: dm_filestream_file_io_requests (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_filestream_file_io_requests
- dm_filestream_file_io_requests
- sys.dm_filestream_file_io_requests_TSQL
- dm_filestream_file_io_requests_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_filestream_file_io_requests catalog view
ms.assetid: d41e39a5-14d5-4f3d-a2e3-a822b454c1ed
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9f4f675f0022b3afeeaccbdc6e907b5ce1c17ca7
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543895"
---
# <a name="sysdm_filestream_file_io_requests-transact-sql"></a>sys.dm_filestream_file_io_requests (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定した時点で名前空間の所有者 (NSO) によって処理されている i/o 要求の一覧を表示します。  
  
|Column|種類|説明|  
|------------|----------|-----------------|  
|**request_context_address**|**varbinary (8)**|ドライバーからの I/O 要求を含む NSO メモリ ブロックの内部アドレスを示します。 NULL 値は許可されません。|  
|**current_spid**|**smallint**|現在の SQL Server の接続のシステムプロセス id (SPID) を表示します。 NULL 値は許可されません。|  
|**request_type**|**nvarchar(60)**|I/o 要求パケット (IRP) の種類を示します。 使用できる要求の種類は、REQ_PRE_CREATE、REQ_POST_CREATE、REQ_RESOLVE_VOLUME、REQ_GET_VOLUME_INFO、REQ_GET_LOGICAL_NAME、REQ_GET_PHYSICAL_NAME、REQ_PRE_CLEANUP、REQ_POST_CLEANUP、REQ_CLOSE、REQ_FSCTL、REQ_QUERY_INFO、REQ_SET_INFO、REQ_ENUM_DIRECTORY、REQ_QUERY_SECURITY、REQ_SET_SECURITY です。 Null 値はありません|  
|**request_state**|**nvarchar(60)**|NSO の i/o 要求の状態を表示します。 REQ_STATE_RECEIVED、REQ_STATE_INITIALIZED、REQ_STATE_ENQUEUED、REQ_STATE_PROCESSING、REQ_STATE_FORMATTING_RESPONSE、REQ_STATE_SENDING_RESPONSE、REQ_STATE_COMPLETING、および REQ_STATE_COMPLETED のいずれかの値になります。 NULL 値は許可されません。|  
|**request_id**|**int**|ドライバーによってこの要求に割り当てられた一意の要求 ID が表示されます。 NULL 値は許可されません。|  
|**irp_id**|**int**|一意の IRP ID を表示します。 これは、特定の IRP に関連するすべての I/O 要求を識別する場合に役立ちます。 NULL 値は許可されません。|  
|**handle_id**|**int**|名前空間ハンドル ID が指定されました。 これは NSO 固有の識別子で、インスタンス内で一意です。 NULL 値は許可されません。|  
|**client_thread_id**|**varbinary (8)**|要求元のクライアントアプリケーションのスレッド ID が表示されます。<br /><br /> 警告これは、クライアントアプリケーションが SQL Server と同じコンピューター上で実行されている場合にのみ意味があります。 ** \* \* \* \* ** クライアントアプリケーションがリモートで実行されている場合、 **client_thread_id** には、リモートクライアントの代わりに動作するシステムプロセスのスレッド id が表示されます。<br /><br /> NULL 値が許可されます。|  
|**client_process_id**|**varbinary (8)**|クライアントアプリケーションが SQL Server と同じコンピューター上で実行されている場合に、クライアントアプリケーションのプロセス ID を表示します。 リモート クライアントの場合は、クライアント アプリケーションの代わりに動作しているシステム プロセス ID を示します。 NULL 値が許可されます。|  
|**handle_context_address**|**varbinary (8)**|クライアントのハンドルに関連付けられた内部 NSO 構造体のアドレスを表示します。 NULL 値が許可されます。|  
|**filestream_transaction_id**|**varbinary (128)**|指定したハンドルと、このハンドルに関連付けられているすべての要求に関連付けられているトランザクションの ID を表示します。 **Get_filestream_transaction_context**関数によって返される値です。 NULL 値が許可されます。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;の Filestream および FileTable の動的管理ビュー ](../../relational-databases/system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)  
  
  
