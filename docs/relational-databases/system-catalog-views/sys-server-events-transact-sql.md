---
description: server_events (Transact-sql)
title: server_events (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f451456320e7248f48be5a9b7233f1a6cf5b2968
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551383"
---
# <a name="sysserver_events-transact-sql"></a>server_events (Transact-sql)
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
  
  
