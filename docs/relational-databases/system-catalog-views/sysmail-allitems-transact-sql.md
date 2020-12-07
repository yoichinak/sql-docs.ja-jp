---
description: sysmail_allitems (Transact-sql)
title: sysmail_allitems (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_allitems_TSQL
- sysmail_allitems
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_allitems database mail view
ms.assetid: 21fb8432-7677-4435-902f-64a58bba4cbb
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9eb8d8b48203b047df830670eb88b0956d04c4dc
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537961"
---
# <a name="sysmail_allitems-transact-sql"></a>sysmail_allitems (Transact-sql)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  データベース メールで処理されたメッセージごとに 1 行のデータを格納します。 すべてのメッセージの状態を表示するには、このビューを使用します。  
  
 失敗した状態のメッセージだけを表示するには、 [sysmail_faileditems &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)を使用します。 未送信のメッセージだけを表示するには、 [sysmail_unsentitems &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md)を使用します。 送信されたメッセージだけを表示するには、 [sysmail_sentitems &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md)を使用します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**mailitem_id**|**int**|メールキュー内のメールアイテムの識別子。|  
|**profile_id**|**int**|メッセージの送信に使用されるプロファイルの識別子。|  
|**recipients**|**varchar(max)**|メッセージの受信者の電子メールアドレス。|  
|**copy_recipients**|**varchar(max)**|メッセージのコピーを受信するユーザーの電子メールアドレス。|  
|**blind_copy_recipients**|**varchar(max)**|メッセージのコピーを受信したが、その名前がメッセージヘッダーに表示されない電子メールアドレス。|  
|**subject**|**nvarchar (510)**|メッセージの件名行。|  
|**body**|**varchar(max)**|メッセージの本文|  
|**body_format**|**varchar (20)**|メッセージの本文形式。 可能な値は TEXT と HTML です。|  
|**importance**|**varchar (6)**|メッセージの **重要度** パラメーター。|  
|**区別**|**varchar (12)**|メッセージの **感度** パラメーター。|  
|**file_attachments**|**varchar(max)**|電子メール メッセージに添付されたファイル名の、セミコロン区切りの一覧。|  
|**attachment_encoding**|**varchar (20)**|メールの添付ファイルの種類。|  
|**query**|**varchar(max)**|メールプログラムによって実行されるクエリ。|  
|**execute_query_database**|**sysname**|メールプログラムによってクエリが実行されたデータベースコンテキスト。|  
|**attach_query_result_as_file**|**bit**|値が0の場合、クエリ結果は、本文の内容の後に電子メールメッセージの本文に含まれていました。 値が 1 の場合、結果が添付ファイルとして返されたことを示します。|  
|**query_result_header**|**bit**|値が1の場合、クエリ結果には列ヘッダーが含まれます。 値が 0 の場合、クエリの結果に列のヘッダーが含まれていないことを示します。|  
|**query_result_width**|**int**|メッセージの **query_result_width** パラメーター。|  
|**query_result_separator**|**char(1)**|クエリの出力で列の区切りに使用された文字。|  
|**exclude_query_output**|**bit**|メッセージの **exclude_query_output** パラメーター。 詳細については、「 [sp_send_dbmail &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md)」を参照してください。|  
|**append_query_error**|**bit**|メッセージの **append_query_error** パラメーター。 0 は、クエリにエラーがあった場合、データベース メールで電子メール メッセージが送信されないことを示します。|  
|**send_request_date**|**datetime**|メッセージがメールキューに置かれた日付と時刻。|  
|**send_request_user**|**sysname**|メッセージを送信したユーザー。 これは、メッセージの From: フィールドではなく、データベースメールプロシージャのユーザーコンテキストです。|  
|**sent_account_id**|**int**|メッセージの送信に使用されるデータベースメールアカウントの識別子。|  
|**sent_status**|**varchar (8)**|メールの状態。 設定可能な値は、次のとおりです。<br /><br /> **送信** 済み-メールが送信されました。<br /><br /> **未送信** -データベースメールはまだメッセージの送信を試みています。<br /><br /> データベースメール**再試行**しています。メッセージを送信できませんでしたが、もう一度送信しようとしています。<br /><br /> **失敗しました** -データベースメールはメッセージを送信できませんでした。|  
|**sent_date**|**datetime**|メッセージが送信された日時。|  
|**last_mod_date**|**datetime**|行が最後に変更された日付と時刻。|  
|**last_mod_user**|**sysname**|行を最後に変更したユーザー。|  
  
## <a name="remarks"></a>解説  
 データベースメールによって処理されたすべてのメッセージの状態を表示するには、 **sysmail_allitems** ビューを使用します。 データベース メールのトラブルシューティングを行うとき、このビューでは送信済みとそれ以外のメッセージの属性を比較できるので、問題の性質を特定するのに役立ちます。  
  
 このビューによって公開されるシステムテーブルにはすべてのメッセージが含まれているため、 **msdb** データベースのサイズが大きくなる可能性があります。 テーブルのサイズを小さくするために、古いメッセージをビューから定期的に削除します。 詳細については、「 [データベースメールメッセージとイベントログをアーカイブするための SQL Server エージェントジョブの作成](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 **Sysadmin**固定サーバーロールおよび**databasemailuserrole**データベースロールに付与されます。 **Sysadmin**固定サーバーロールのメンバーによって実行されると、このビューにはすべてのメッセージが表示されます。 他のすべてのユーザーには、送信したメッセージのみが表示されます。  
  
  
