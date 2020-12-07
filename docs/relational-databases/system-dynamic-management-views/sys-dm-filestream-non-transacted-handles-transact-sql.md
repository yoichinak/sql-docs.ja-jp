---
description: dm_filestream_non_transacted_handles (Transact-sql)
title: dm_filestream_non_transacted_handles (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_filestream_non_transacted_handles_TSQL
- dm_filestream_non_transacted_handles
- dm_filestream_non_transacted_handles_TSQL
- sys.dm_filestream_non_transacted_handles
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_filestream_non_transacted_handles dynamic management view
ms.assetid: 507ec125-67dc-450a-9081-94cde5444a92
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cde44e61d01f4995f1f3517f2144a36fff669177
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550265"
---
# <a name="sysdm_filestream_non_transacted_handles-transact-sql"></a>dm_filestream_non_transacted_handles (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  FileTable データに関連付けられている、現在開いている非トランザクションファイルハンドルを表示します。  
  
 このビューには、開かれているファイル ハンドルごとに 1 つの行が含まれています。 このビューのデータはサーバーのライブ内部状態に対応しているため、ハンドルを開いたり閉じたりすると、データは常に変化します。 このビューには、履歴情報は含まれていません。  
  
 詳細については、「 [FileTable の管理](../../relational-databases/blob/manage-filetables.md)」を参照してください。  
  
|**列**|**Type**|**説明**|  
|----------------|--------------|---------------------|  
|database_id|INT|ハンドルに関連付けられているデータベースの ID。|  
|object_id|INT|ハンドルが関連付けられている FileTable のオブジェクト ID。|  
|handle_id|INT|一意のハンドルコンテキスト識別子。 [Sp_kill_filestream_non_transacted_handles &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md)ストアドプロシージャが特定のハンドルを強制終了するために使用します。|  
|file_object_type|INT|ハンドルの型。 ハンドルを開くときの対象だった階層のレベル (つまりデータベースまたはアイテム) を示します。|  
|file_object_type_desc|nvarchar(120)|"UNDEFINED"、<br />"SERVER_ROOT"、<br />"DATABASE_ROOT"、<br />"TABLE_ROOT"、<br />"TABLE_ITEM"|  
|correlation_process_id|varbinary (8)|要求を発信したプロセスの一意の識別子を格納します。|  
|correlation_thread_id|varbinary (8)|要求を生成したスレッドの一意な識別子を格納します。|  
|file_context|varbinary (8)|このハンドルで使用されるファイル オブジェクトへのポインター。|  
|状態|INT|ハンドルの現在の状態。 アクティブ、終了、強制終了のいずれかになります。|  
|state_desc|nvarchar(120)|"ACTIVE"、<br />"CLOSED"、<br />キル|  
|current_workitem_type|INT|このハンドルが現在処理されている状態。|  
|current_workitem_type_desc|nvarchar(120)|"NoSetWorkItemType"、<br />"FFtPreCreateWorkitem",<br />"FFtGetPhysicalFileNameWorkitem",<br />"FFtPostCreateWorkitem"、<br />"FFtPreCleanupWorkitem",<br />"FFtPostCleanupWorkitem"、<br />"FFtPreCloseWorkitem"、<br />"FFtQueryDirectoryWorkItem"、<br />"FFtQueryInfoWorkItem"、<br />"FFtQueryVolumeInfoWorkItem",<br />"FFtSetInfoWorkitem"、<br />FFtWriteCompletionWorkitem|  
|fcb_id|bigint|FileTable ファイル制御ブロック ID。|  
|item_id|varbinary (892)|ファイルまたはディレクトリのアイテム ID。 通常、サーバーのルートのハンドルは NULL です。|  
|is_directory|bit|これはディレクトリです。|  
|item_name|nvarchar(512)|項目の名前。|  
|opened_file_name|nvarchar(512)|最初に要求されたパスを開いています。|  
|database_directory_name|nvarchar(512)|opened_file_name の一部で、データベースのディレクトリ名を表す部分。|  
|table_directory_name|nvarchar(512)|opened_file_name の一部で、テーブルのディレクトリ名を表す部分。|  
|remaining_file_name|nvarchar(512)|opened_file_name の一部で、残りのディレクトリ名を表す部分。|  
|open_time|DATETIME|ハンドルが開かれた時刻。|  
|flags|INT|ShareFlagsUpdatedToFcb = 0x1、<br />DeleteOnClose = 0x2、<br />NewFile = 0x4、<br />PostCreateDoneForNewFile = 0x8、<br />StreamFileOverwritten = 0x10、<br />RequestCancelled = 0x20、<br />NewFileCreationRolledBack = 0x40|  
|login_id|INT|ハンドルを開いたプリンシパルの ID。|  
|login_name|nvarchar(512)|ハンドルを開いたプリンシパルの名前。|  
|login_sid|varbinary(85)|ハンドルを開いたプリンシパルの SID。|  
|read_access|bit|読み取りアクセス用に開かれました。|  
|write_access|bit|書き込みアクセス用に開かれました。|  
|delete_access|bit|削除アクセス用に開かれました。|  
|share_read|bit|share_read を許可して開かれました。|  
|share_write|bit|Share_write 許可付きで開かれました。|  
|share_delete|bit|share_delete を許可して開かれました。|  
  
## <a name="see-also"></a>参照  
 [FileTable の管理](../../relational-databases/blob/manage-filetables.md)  
  
  
