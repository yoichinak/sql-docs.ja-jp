---
description: メッセージ (エラー用) のカタログ ビュー - sys.messages
title: sys. messages (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- messages_TSQL
- sys.messages_TSQL
- sys.messages
- messages
dev_langs:
- TSQL
helpviewer_keywords:
- error messages [SQL Server]
- sys.messages catalog view
- error numbers [SQL Server]
ms.assetid: 8c16ecdf-68f4-4a2a-b594-086e3344e58a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 30cfb208d709f19743216369b23e6b7bef9dfc38
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810398"
---
# <a name="messages-for-errors-catalog-views---sysmessages"></a>メッセージ (エラー用) のカタログ ビュー - sys.messages
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  システム定義メッセージとユーザー定義メッセージの両方について、システム内のエラーメッセージの **message_id** または **language_id** ごとに1行の値を格納します。 詳細については、「[sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)」を参照してください。  
   
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**message_id**|**int**|メッセージの ID。 これはサーバー内で一意です。 5万未満のメッセージ Id はシステムメッセージです。|  
|**language_id**|**smallint**|**Sys.syslanguages**で定義されているように、**テキスト**内のテキストが使用される言語 ID。 これは、指定された **message_id**に対して一意です。|  
|**severity**|**tinyint**|メッセージの重大度レベル (1 ~ 25)。 これは、 **message_id**内のすべてのメッセージ言語で同じです。|  
|**is_event_logged**|**bit**|1 = メッセージは、エラーが発生するとイベントがログに記録されます。 これは、 **message_id**内のすべてのメッセージ言語で同じです。|  
|**text**|**nvarchar(2048)**|対応する **language_id** がアクティブな場合に使用されるメッセージのテキスト。|  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [THROW &#40;Transact-SQL&#41;](../../t-sql/language-elements/throw-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [エラーのメッセージ &#40;&#41; カタログビュー &#40;Transact-sql&#41;]()   
 [例外メッセージボックスのプログラミング](/previous-versions/sql/sql-server-2016/ms166343(v=sql.130))   
 [エラーメッセージ](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [データベース エンジンのイベントとエラー](../../relational-databases/errors-events/database-engine-events-and-errors.md)  
  
