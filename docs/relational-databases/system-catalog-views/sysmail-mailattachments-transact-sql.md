---
description: sysmail_mailattachments (Transact-sql)
title: sysmail_mailattachments (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_mailattachments_TSQL
- sysmail_mailattachments
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_mailattachments database mail view
ms.assetid: aee87059-a4c1-459a-a95c-641b4e3f0e73
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f3f29f688e750b853c288c901cd81b9891a285c8
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542396"
---
# <a name="sysmail_mailattachments-transact-sql"></a>sysmail_mailattachments (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  データベースメールに送信された添付ファイルごとに1行のデータを格納します。 データベースメールの添付ファイルに関する情報が必要な場合は、このビューを使用します。 データベースメールによって処理されるすべての電子メールを確認するには [sysmail_allitems &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)を使用します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**attachment_id**|**int**|添付ファイルの識別子。|  
|**mailitem_id**|**int**|添付ファイルが含まれていたメール アイテムの識別子。|  
|**ファイル名**|**nvarchar (520)**|添付ファイルのファイル名。 **Attach_query_result**が1で**query_attachment_filename**が NULL の場合、データベースメールによって任意のファイル名が作成されます。|  
|**filesize**|**int**|添付ファイルのサイズ (バイト単位)。|  
|**資料**|**varbinary(max)**|添付ファイルのコンテンツ。|  
|**last_mod_date**|**datetime**|行が最後に変更された日付と時刻。|  
|**last_mod_user**|**sysname**|行を最後に変更したユーザー。|  
  
## <a name="remarks"></a>解説  
 データベースメールのトラブルシューティングを行う場合は、このビューを使用して添付ファイルのプロパティを表示します。  
  
 システムテーブルに格納されている添付ファイルは、 **msdb** データベースのサイズが大きくなる可能性があります。 **Sysmail_delete_mailitems_sp**を使用して、メールアイテムとそれに関連付けられている添付ファイルを削除します。 詳細については、「 [データベースメールメッセージとイベントログをアーカイブするための SQL Server エージェントジョブの作成](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 **Sysadmin**固定サーバーロールおよび**databasemailuserrole**データベースロールに付与されます。 **Sysadmin**固定サーバーロールのメンバーによって実行されると、このビューにはすべての添付ファイルが表示されます。 他のすべてのユーザーには、送信したメッセージの添付ファイルのみが表示されます。  
  
## <a name="see-also"></a>参照  
 [sysmail_allitems &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)   
 [sysmail_faileditems &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)   
 [sysmail_sentitems &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md)   
 [sysmail_unsentitems &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md)   
 [sysmail_event_log &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)  
  
  
