---
description: sys.server_trigger_events (Transact-SQL)
title: sys.server_trigger_events (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sys.server_trigger_events_TSQL
- server_trigger_events_TSQL
- sys.server_trigger_events
- server_trigger_events
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_trigger_events catalog view
ms.assetid: be7d8a59-3c00-4f1b-b4b0-3dcd5572e002
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: b18217ea444862555c10f4954dab004e0b7a1b55
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99198547"
---
# <a name="sysserver_trigger_events-transact-sql"></a>sys.server_trigger_events (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  サーバー レベル (同期) トリガーが起動されるイベントごとに 1 行のデータを格納します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**継承された列**||[Sys.server_events](../../relational-databases/system-catalog-views/sys-server-events-transact-sql.md)からすべての列を継承します。|  
|**is_first**|**bit**|トリガーは、このイベントに対して最初に起動するようにマークされています。|  
|**is_last**|**bit**|トリガーは、このイベントに対して最後に起動されるようにマークされています。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
