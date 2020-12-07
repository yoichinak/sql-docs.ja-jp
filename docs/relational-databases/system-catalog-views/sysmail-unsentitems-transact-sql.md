---
description: sysmail_unsentitems (Transact-SQL)
title: sysmail_unsentitems (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_unsentitems_TSQL
- sysmail_unsentitems
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_unsentitems database mail view
ms.assetid: 993c12da-41e5-4e53-a188-0323feb70c67
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7ef61a0c08d1ddc2e3a268571521b4da47cee90f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543986"
---
# <a name="sysmail_unsentitems-transact-sql"></a>sysmail_unsentitems (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  **未送信**または**再試行**中の状態のデータベースメールメッセージごとに1行の情報を格納します。 未送信または再試行の状態のメッセージは、メールキューに残ります。いつでも送信できます。 メッセージは、次の理由により、 **未送信** 状態になることがあります。  
  
-   メッセージが新しく、メール キューに挿入されていても、データベース メールが他のメッセージの処理中でこのメッセージに達していない。  
  
-   データベース メール外部プログラムが実行されておらず、メールが送信されていない  
  
 メッセージの **再試行** の状態は次のようになります。  
  
-   データベース メールでメッセージの送信が試行されたが、SMTP メール サーバーに接続できなかった。 データベースメールは、メッセージを送信したプロファイルに割り当てられた他のデータベースメールアカウントを使用してメッセージの送信を試行し続けます。 メールを送信できるアカウントがない場合、データベースメールは、 **アカウントの再試行待ち時間** パラメーターに構成されている時間が経過するまで待機してから、メッセージの送信を再試行します。 データベースメールは、 **アカウントの再試行** 回数のパラメーターを使用して、メッセージの送信を試行する回数を決定します。 データベースメールがメッセージを送信しようとしている間は、メッセージの **再試行** 状態が保持されます。  
  
 このビューは、送信待ちメッセージの数と、それらのメール キューでの待機時間を確認する場合に使用できます。 通常、 **未送信** のメッセージの数は少なくなります。 通常の操作中にベンチマークテストを実行して、メッセージキュー内の適切な数のメッセージを操作に使用します。  
  
 データベースメールによって処理されるすべてのメッセージを表示するには [sysmail_allitems &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)を使用します。 失敗した状態のメッセージだけを表示するには、 [sysmail_faileditems &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)を使用します。 送信されたメッセージだけを表示するには、 [sysmail_sentitems &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md)を使用します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**mailitem_id**|**int**|メールキュー内のメールアイテムの識別子。|  
|**profile_id**|**int**|メッセージの送信に使用されるプロファイルの識別子。|  
|**recipients**|**varchar(max)**|メッセージの受信者の電子メールアドレス。|  
|**copy_recipients**|**varchar(max)**|メッセージのコピーを受信するユーザーの電子メールアドレス。|  
|**blind_copy_recipients**|**varchar(max)**|メッセージのコピーを受信したが、その名前がメッセージヘッダーに表示されない電子メールアドレス。|  
|**subject**|**nvarchar (510)**|メッセージの件名行。|  
|**body**|**varchar(max)**|メッセージの本文|  
|**body_format**|**varchar (20)**|メッセージの本文形式。 指定できる値は、 **TEXT** と **HTML**です。|  
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
|**send_request_user**|**sysname**|メッセージを送信したユーザー。 これは、メッセージの [ **差出人** ] フィールドではなく、データベースメールプロシージャのユーザーコンテキストです。|  
|**sent_account_id**|**int**|メッセージの送信に使用されるデータベースメールアカウントの識別子。 このビューでは常に NULL です。|  
|**sent_status**|**varchar (8)**|データベースメールがメールを送信しようとしていない場合は、 **送信** されません。 データベースメールがメッセージの送信に失敗したが、再試行している場合は、 **再試行** されます。|  
|**sent_date**|**datetime**|データベースメールが最後にメールを送信しようとした日付と時刻。 データベース メールでメッセージの送信が試行されていない場合は NULL になります。|  
|**last_mod_date**|**datetime**|行が最後に変更された日付と時刻。|  
|**last_mod_user**|**sysname**|行を最後に変更したユーザー。|  
  
## <a name="remarks"></a>解説  
 データベース メールのトラブルシューティングを行うとき、このビューでは送信済みのメッセージ数とメッセージの待機時間を確認できるので、問題の性質を特定するのに役立ちます。 メッセージが 1 つも送信されていない場合は、データベース メール外部プログラムが動作していないか、ネットワークの問題によってデータベース メールから SMTP サーバーへの接続に障害が発生している可能性があります。 未送信のメッセージの多くが同じ **profile_id**を持っている場合は、SMTP サーバーに問題がある可能性があります。 プロファイルにアカウントを追加することを検討してください。 メッセージが送信されているにもかかわらず、メッセージがキューに過剰に時間を費やしている場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必要なメッセージの量を処理するためにより多くのリソースが必要になることがあります。  
  
## <a name="permissions"></a>アクセス許可  
 **Sysadmin**固定サーバーロールおよび**databasemailuserrole**データベースロールに付与されます。 **Sysadmin**固定サーバーロールのメンバーによって実行されると、このビューにはすべての**未送信**または**再試行**中のメッセージが表示されます。 他のすべてのユーザーには、送信した **未送信** または **再試行** 中のメッセージのみが表示されます。  
  
  
