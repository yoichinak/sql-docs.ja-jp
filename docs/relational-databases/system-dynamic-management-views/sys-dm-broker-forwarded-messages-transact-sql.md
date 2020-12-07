---
description: sys.dm_broker_forwarded_messages (Transact-SQL)
title: dm_broker_forwarded_messages (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_broker_forwarded_messages
- dm_broker_forwarded_messages
- sys.dm_broker_forwarded_messages_TSQL
- dm_broker_forwarded_messages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_broker_forwarded_messages dynamic management view
ms.assetid: 5576376d-6364-417a-8475-aa770e060845
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1b167baced0acda08234b4240bc362c602f327f9
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544790"
---
# <a name="sysdm_broker_forwarded_messages-transact-sql"></a>sys.dm_broker_forwarded_messages (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  のインスタンス [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が転送処理中であることを Service Broker メッセージごとに1行の値を返します。  
  

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**conversation_id**|**uniqueidentifier**|このメッセージが属しているメッセージ交換の ID。 NULLABLE.|  
|**is_initiator**|**bit**|メッセージがメッセージ交換の発信側から送信されたものかどうかを示します。  NULLABLE.<br /><br /> 0 = イニシエーターからのものではない<br /><br /> 1 = 発信側から|  
|**to_service_name**|**nvarchar(512)**|このメッセージが送信されるサービスの名前。 NULLABLE.|  
|**to_broker_instance**|**nvarchar(512)**|このメッセージが送信されるサービスをホストするブローカーの識別子。 NULLABLE.|  
|**from_service_name**|**nvarchar(512)**|このメッセージの差出人となるサービスの名前。 NULLABLE.|  
|**from_broker_instance**|**nvarchar(512)**|メッセージの送信元となるサービスをホストしているブローカーの識別子。 NULLABLE.|  
|**adjacent_broker_address**|**nvarchar(512)**|このメッセージが送信されるネットワークアドレス。 NULLABLE.|  
|**message_sequence_number**|**bigint**|ダイアログボックス内のメッセージのシーケンス番号。 NULLABLE.|  
|**message_fragment_number**|**int**|ダイアログ メッセージが断片化している場合、このトランスポート メッセージに含まれるフラグメント番号。 NULLABLE.|  
|**hops_remaining**|**tinyint**|メッセージが最終送信先に届くまでに再転送される回数。 メッセージが転送されるたび、この数は 1 ずつ減少します。 NULLABLE.|  
|**time_to_live**|**int**|メッセージがアクティブなままになる最長時間。 この値が 0 に達すると、メッセージは破棄されます。 NULLABLE.|  
|**time_consumed**|**int**|メッセージが既にアクティブになっている時刻。 メッセージが転送されるたびに、メッセージの転送にかかる時間によって、この数が増加します。 NULL 値は許容されません。|  
|**message_id**|**uniqueidentifier**|メッセージの ID。 NULLABLE.|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Service Broker 関連の動的管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
  

