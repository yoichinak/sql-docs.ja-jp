---
description: sys.database_event_session_events (Azure SQL Database)
title: sys.database_event_session_events (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
ms.assetid: f4c9eb0a-173c-4c66-8dd8-6f7176b2657f
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c237064fedc0c697f8bd20a01317e43ac37fe4f5
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98102808"
---
# <a name="sysdatabase_event_session_events-azure-sql-database"></a>sys.database_event_session_events (Azure SQL Database)
[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

  イベント セッションのイベントごとに行を返します。  
  
||  
|-|  
|**に適用さ** れます: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 およびそれ以降のすべてのバージョン。|  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|イベントセッションの ID。 NULL 値は許可されません。|  
|event_id|**int**|イベントの ID。 この ID は、イベントセッションオブジェクト内で一意です。 NULL 値は許可されません。|  
|name|**sysname**|イベントの名前です。 NULL 値は許可されません。|  
|パッケージ|**sysname**|イベントを含むイベント パッケージの名前。 NULL 値は許可されません。|  
|name|**sysname**|イベントが格納されているモジュールの名前。 NULL 値は許可されません。|  
|predicate|**nvarchar (3000)**|イベントに適用される述語式。 NULL 値が許可されます。|  
|predicate_xml|**nvarchar (3000)**|イベントに適用される XML 述語式。 NULL 値が許可されます。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW DATABASE STATE 権限が必要です。  
  
## <a name="remarks"></a>解説  
 このビューには、次のリレーションシップ基数があります。  
  
| 差出人 | 終了 | Relationship |
| ---- | -- | ------------ |
|sys.database_event_session_events sys.database_event_session_events.event_session_id|sys.database_event_sessions sys.database_event_sessions.event_session_id|多対一|  
  
## <a name="see-also"></a>参照  
 [拡張イベント](../../relational-databases/extended-events/extended-events.md)  
  
  
