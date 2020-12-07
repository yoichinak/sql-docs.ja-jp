---
description: sysmail_delete_mailitems_sp (Transact-SQL)
title: sysmail_delete_mailitems_sp (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_delete_mailitems_sp_TSQL
- sysmail_delete_mailitems_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_mailitems_sp
ms.assetid: f87c9f4a-bda1-4bce-84b2-a055a3229ecd
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a1bcfc2bbd5069e50399eaa6b23fc69938ec6a05
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538501"
---
# <a name="sysmail_delete_mailitems_sp-transact-sql"></a>sysmail_delete_mailitems_sp (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  データベースメール内部テーブルから電子メールメッセージを完全に削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sysmail_delete_mailitems_sp  [ [ @sent_before = ] 'sent_before' ]  
    [ , [ @sent_status = ] 'sent_status' ]  
```  
  
## <a name="arguments"></a>引数  
`[ \@sent_before = ] 'sent_before'`*Sent_before*引数として指定された日付と時刻までの電子メールを削除します。 *sent_before* は **datetime** で、既定値は NULL です。 NULL はすべての日付を表します。  
  
`[ \@sent_status = ] 'sent_status'`*Sent_status*によって指定された種類の電子メールを削除します。 *sent_status* は **varchar (8)** で、既定値はありません。 有効なエントリは、 **送信済み**、 **未送信**、 **再試行**中、および **失敗**です。 NULL はすべての状態を表します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 データベースメールメッセージとその添付ファイルは、 **msdb** データベースに格納されます。 **Msdb**が予想以上に大きくなり、組織のドキュメント保持プログラムに準拠するように、メッセージを定期的に削除する必要があります。 データベースメールテーブルから電子メールメッセージを完全に削除するには、 **sysmail_delete_mailitems_sp** ストアドプロシージャを使用します。 日時を指定する引数を使用すると、古い電子メールだけを削除できます。 この場合、引数で指定した日時より前の電子メールが削除されます。 もう1つの省略可能な引数を使用すると、 **sent_status** の引数として指定された特定の種類の電子メールのみを削除できます。 ** \@ Sent_before**または** \@ sent_status**の引数を指定する必要があります。 すべてのメッセージを削除するには、 ** \@ sent_before = getdate ()** を使用します。  
  
 電子メールを削除すると、そのメッセージに関係する添付ファイルも削除されます。 電子メールを削除しても、 **sysmail_event_log**内の対応するエントリは削除されません。 [Sysmail_delete_log_sp](../../relational-databases/system-stored-procedures/sysmail-delete-log-sp-transact-sql.md)を使用して、ログから項目を削除します。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、このストアドプロシージャは、 **sysadmin** 固定サーバーロールおよび **databasemailuserrole**のメンバーに対して実行するために許可されています。 **Sysadmin**固定サーバーロールのメンバーは、このプロシージャを実行して、すべてのユーザーが送信した電子メールを削除できます。 **Databasemailuserrole**のメンバーは、そのユーザーによって送信された電子メールのみを削除できます。  
  
## <a name="examples"></a>例  
  
### <a name="a-deleting-all-e-mails"></a>A. すべての電子メールを削除する  
 次の例では、データベース メール システムにあるすべての電子メールを削除します。  
  
```  
DECLARE @GETDATE datetime  
SET @GETDATE = GETDATE();  
EXECUTE msdb.dbo.sysmail_delete_mailitems_sp @sent_before = @GETDATE;  
GO  
```  
  
### <a name="b-deleting-the-oldest-e-mails"></a>B. 最も古いメールを削除する  
 次の例では、データベースメールログでよりも古い電子メールを削除し `October 9, 2005` ます。  
  
```  
EXECUTE msdb.dbo.sysmail_delete_mailitems_sp   
    @sent_before = 'October 9, 2005' ;  
GO  
```  
  
### <a name="c-deleting-all-e-mails-of-a-certain-type"></a>C. 特定の種類のすべての電子メールを削除する  
 次の例では、データベースメールログ内の失敗したすべての電子メールを削除します。  
  
```  
EXECUTE msdb.dbo.sysmail_delete_mailitems_sp   
    @sent_status = 'failed' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sysmail_allitems &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)   
 [sysmail_event_log &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)   
 [sysmail_mailattachments &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sysmail-mailattachments-transact-sql.md)   
 [データベース メール メッセージやイベント ログをアーカイブする SQL Server エージェント ジョブの作成](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)  
  
  
