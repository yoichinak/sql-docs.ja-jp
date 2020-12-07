---
description: sysmail_faileditems (Transact-sql)
title: sysmail_faileditems (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_faileditems
- sysmail_faileditems_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_faileditems database mail view
ms.assetid: a31562c5-358e-4cfc-a72d-b3faccc53851
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6c86c282b80c346c4d9378c9488e0503bbb85212
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548917"
---
# <a name="sysmail_faileditems-transact-sql"></a>sysmail_faileditems (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **失敗した**状態のデータベースメールメッセージごとに1行の情報を格納します。 このビューは、正しく送信されなかったメッセージを特定するときに使用できます。  
  
 データベースメールによって処理されるすべてのメッセージを表示するには [sysmail_allitems &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)を使用します。 未送信のメッセージだけを表示するには、 [sysmail_unsentitems &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md)を使用します。 送信されたメッセージだけを表示するには、 [sysmail_sentitems &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md)を使用します。 電子メールの添付ファイルを表示するには、 [sysmail_mailattachments &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sysmail-mailattachments-transact-sql.md)を使用します。  
  
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
|**Attachment_encoding**|**varchar (20)**|メールの添付ファイルの種類。|  
|**クエリ**|**varchar(max)**|メールプログラムによって実行されるクエリ。|  
|**execute_query_database**|**sysname**|メールプログラムによってクエリが実行されたデータベースコンテキスト。|  
|**attach_query_result_as_file**|**bit**|値が0の場合、クエリ結果は、本文の内容の後に電子メールメッセージの本文に含まれていました。 値が 1 の場合、結果が添付ファイルとして返されたことを示します。|  
|**query_result_header**|**bit**|値が1の場合、クエリ結果には列ヘッダーが含まれます。 値が 0 の場合、クエリの結果に列のヘッダーが含まれていないことを示します。|  
|**query_result_width**|**int**|メッセージの **query_result_width** パラメーター。|  
|**query_result_separator**|**char(1)**|クエリの出力で列の区切りに使用された文字。|  
|**exclude_query_output**|**bit**|メッセージの **exclude_query_output** パラメーター。 詳細については、「 [sp_send_dbmail &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md)」を参照してください。|  
|**append_query_error**|**bit**|メッセージの **append_query_error** パラメーター。 0 は、クエリにエラーがあった場合、データベース メールで電子メール メッセージが送信されないことを示します。|  
|**send_request_date**|**datetime**|メッセージがメールキューに置かれた日付と時刻。|  
|**send_request_user**|**sysname**|メッセージを送信したユーザー。 これは、メッセージの From: フィールドではなく、データベースメールプロシージャのユーザーコンテキストです。|  
|**sent_account_id**|**int**|メッセージの送信に使用されるデータベースメールアカウントの識別子。 このビューでは常に NULL です。|  
|**sent_status**|**varchar (8)**|メールの状態。 このビューでは常に **失敗しました** 。|  
|**sent_date**|**datetime**|メッセージがメールキューから削除された日付と時刻。|  
|**last_mod_date**|**datetime**|行が最後に変更された日付と時刻。|  
|**last_mod_user**|**sysname**|行を最後に変更したユーザー。|  
  
## <a name="remarks"></a>解説  
 データベースメールによって送信されなかったメッセージを表示するには、 **sysmail_faileditems** ビューを使用します。 データベース メールのトラブルシューティングを行うとき、このビューでは送信されなかったメッセージの属性を確認できるので、問題の性質を特定するのに役立ちます。 失敗の理由を確認するには、失敗したメッセージのエントリを [ [sysmail_event_log &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md) ビューで確認します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sysadmin**固定サーバーロールおよび**databasemailuserrole**データベースロールに付与されます。 **Sysadmin**固定サーバーロールのメンバーによって実行されると、このビューには失敗したすべてのメッセージが表示されます。 他のすべてのユーザーには、送信した失敗したメッセージのみが表示されます。  
  
  
