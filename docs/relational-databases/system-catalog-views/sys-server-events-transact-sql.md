---
description: sys.server_events (Transact-sql)
title: sys.server_events (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- server_events_TSQL
- sys.server_events_TSQL
- server_events
- sys.server_events
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_events catalog view
ms.assetid: 996f6c9b-6426-4847-95d9-6b77541422be
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 350da163f64c09276cd57ebbf6c2c63b4e2e022c
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99188048"
---
# <a name="sysserver_events-transact-sql"></a>sys.server_events (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  サーバー レベルのイベント通知またはサーバー レベルの DDL トリガーが起動されるイベントごとに 1 行のデータを保持します。 列 **object_id** と **型** は、サーバーイベントを一意に識別します。  

  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|起動するサーバーレベルのイベント通知またはサーバーレベルの DDL トリガーの ID。|  
|**type**|**int**|イベント通知または DDL トリガーを起動させるイベントの種類。|  
|**type_desc**|**nvarchar(60)**|DDL トリガーまたはイベント通知を起動させるイベントの説明です。|  
|**event_group_type**|**int**|トリガーまたはイベント通知が作成されるイベントグループ。イベントグループに作成されていない場合は null。|  
|**event_group_type_desc**|**nvarchar(60)**|トリガーまたはイベント通知が作成されるイベントグループの説明。イベントグループに作成されていない場合は null になります。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
