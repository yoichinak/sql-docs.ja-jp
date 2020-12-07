---
description: transmission_queue (Transact-sql)
title: transmission_queue (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- transmission_queue
- sys.transmission_queue_TSQL
- sys.transmission_queue
- transmission_queue_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.transmission_queue catalog view
ms.assetid: f3515d1a-be8f-4a27-8058-8865f0919838
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7b0a45de2a9eb967151bf0850556469fe857db5c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544939"
---
# <a name="systransmission_queue-transact-sql"></a>transmission_queue (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  このカタログ ビューは、転送キュー内のメッセージごとに 1 行のデータを格納します。ビューの内容を次の表に示します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**conversation_handle**|**uniqueidentifier**|このメッセージが属するメッセージ交換の識別子。 NULL 値は許容されません。|  
|**to_service_name**|**nvarchar (256)**|このメッセージの対象となるサービスの名前。 NULLABLE.|  
|**to_broker_instance**|**nvarchar(128)**|このメッセージの送信先となるサービスをホストするブローカーの識別子。 NULLABLE.|  
|**from_service_name**|**nvarchar (256)**|このメッセージの差出人となるサービスの名前。 NULLABLE.|  
|**service_contract_name**|**nvarchar (256)**|このメッセージのメッセージ交換が従うコントラクトの名前。 NULLABLE.|  
|**enqueue_time**|**datetime**|メッセージがキューに入った時刻。 この値には、インスタンスのローカルのタイム ゾーンに関係なく UTC が使用されます。 NULL 値は許容されません。|  
|**message_sequence_number**|**bigint**|メッセージのシーケンス番号。 NULL 値は許容されません。|  
|**message_type_name**|**nvarchar (256)**|メッセージの種類の名前。 NULLABLE.|  
|**is_conversation_error**|**bit**|このメッセージがエラーメッセージであるかどうか。<br /><br /> 0 = エラーメッセージではありません。<br /><br /> 1 = エラー メッセージです。<br /><br /> NULL 値は許容されません。|  
|**is_end_of_dialog**|**bit**|このメッセージがメッセージ交換の終了メッセージかどうかを示します。 NULL 値は許容されません。<br /><br /> 0 = メッセージ交換の終了メッセージではありません。<br /><br /> 1 = メッセージ交換の最後のメッセージです。<br /><br /> NULL 値は許容されません。|  
|**message_body**|**varbinary(max)**|メッセージの本文。 NULLABLE.|  
|**transmission_status**|**nvarchar (4000)**|メッセージがキューにある理由。 これは通常、メッセージ送信が失敗した理由を示すエラー メッセージです。 空白の場合、メッセージはまだ送信されていません。 NULLABLE.|  
|**priority**|**tinyint**|このメッセージに割り当てられている優先度レベル。 NULL 値は許容されません。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
  
