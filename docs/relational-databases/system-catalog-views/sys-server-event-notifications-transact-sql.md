---
description: sys.server_event_notifications (Transact-sql)
title: sys.server_event_notifications (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- server_event_notifications
- sys.server_event_notifications
- sys.server_event_notifications_TSQL
- server_event_notifications_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_event_notifications catalog view
ms.assetid: 1a83a044-3130-4551-95ca-162525846ff5
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 0fa3a705df518fa57917da989540a8b97f849a9c
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99172678"
---
# <a name="sysserver_event_notifications-transact-sql"></a>sys.server_event_notifications (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  サーバーレベルのイベント通知オブジェクトごとに1行の値を返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|サーバーイベント通知名。 は、すべてのサーバーレベルのイベント通知に対して一意です。|  
|**object_id**|**int**|オブジェクト ID 番号。 は、 **master** データベース内で一意です。|  
|**parent_class**|**tinyint**|親のクラス。 常に 100 = サーバーです。|  
|**parent_class_desc**|**nvarchar(60)**|親のクラスの説明です。 常にサーバーです。|  
|**parent_id**|**int**|は常に0です。|  
|**create_date**|**datetime**|作成日。|  
|**modify_date**|**datetime**|オブジェクトが ALTER ステートメントを使用して最後に変更された日付です。|  
|**service_name**|**nvarchar (256)**|通知の送信先のサービスの名前です。|  
|**broker_instance**|**nvarchar(128)**|指定された通知先サービスが定義されている Service Broker です。|  
|**creator_sid**|**varbinary(85)**|イベント通知を作成するステートメントを実行するログインの SID。 WITH FAN_IN がイベント通知定義に指定されていない場合は NULL になります。|  
|**principal_id**|**int**|これを所有しているサーバー プリンシパルの ID です。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
