---
description: sys.trigger_events (Transact-sql)
title: sys.trigger_events (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- trigger_events_TSQL
- trigger_events
- sys.trigger_events
- sys.trigger_events_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trigger_events catalog view
ms.assetid: 92540447-131c-491c-b033-c064c7d950e1
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2c6e0067e7e92e0f375c4fc0d735a3bb3f466021
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99188817"
---
# <a name="systrigger_events-transact-sql"></a>sys.trigger_events (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  トリガーが起動されるイベントごとに 1 行のデータを保持します。  
  
> [!NOTE]  
>  **sys.trigger_events** は、イベント通知には適用されません。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**\<Columns inherited from sys.events>**|適用なし|**Object_id**、**型**、 **type_desc** 列を、 [sys. events](../../relational-databases/system-catalog-views/sys-events-transact-sql.md)から継承します。|  
|**is_first**|**bit**|トリガーは、このイベントに対して最初に起動するようにマークされています。|  
|**is_last**|**bit**|トリガーは、このイベントに対して最後に起動されるようにマークされています。|  
|**event_group_type**|**int**|トリガーが作成されるイベントグループ。イベントグループに作成されていない場合は null。|  
|**event_group_type_desc**|**nvarchar(60)**|トリガーが作成されるイベントグループの説明です。イベントグループに作成されていない場合は null になります。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
