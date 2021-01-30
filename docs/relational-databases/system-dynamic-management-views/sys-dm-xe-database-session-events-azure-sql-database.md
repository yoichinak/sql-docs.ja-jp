---
description: sys.dm_xe_database_session_events (Azure SQL Database)
title: sys.dm_xe_database_session_events
titleSuffix: Azure SQL Database
ms.date: 06/10/2016
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: reference
ms.assetid: 9e985a19-f93f-4c56-b644-12c529298011
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: = azuresqldb-current
ms.custom: seo-lt-2019
ms.openlocfilehash: 4c96b6596c01410f9cea5d0e3183f599d1031c26
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99131154"
---
# <a name="sysdm_xe_database_session_events-azure-sql-database"></a>sys.dm_xe_database_session_events (Azure SQL Database)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  セッション イベントに関する情報を返します。 イベントは、個別の実行ポイントです。 イベントに述語を適用すると、イベントに必要な情報が含まれていない場合に、イベントの発生を防ぐことができます。  
  
||  
|-|  
|**に適用さ** れます: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 およびそれ以降のすべてのバージョン。|  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary (8)**|イベントセッションのメモリアドレス。 NULL 値は許可されません。|  
|event_name|**nvarchar(60)**|アクションが関連付けられているイベントの名前。 NULL 値は許可されません。|  
|event_package_guid|**uniqueidentifier**|イベントを含むパッケージの GUID。 NULL 値は許可されません。|  
|event_predicate|**nvarchar(2048)**|イベントに適用される述語ツリーの XML 表現。 NULL 値が許可されます。|  
  
## <a name="permissions"></a>アクセス許可  
 VIEW DATABASE STATE 権限が必要です。  
  
### <a name="relationship-cardinalities"></a>リレーションシップ基数  
  
|差出人|終了|リレーションシップ|  
|----------|--------|------------------|  
|sys.dm_xe_database_session_events sys.dm_xe_database_session_events.event_session_address|sys.dm_xe_database_sessions。アドレス|多対一|  
|event_package_guid、_xe_database_session_events、_xe_database_session_events. event_name|sys.dm_xe_objects.name、sys.dm_xe_objects.package_guid|多対一|  
  
  
