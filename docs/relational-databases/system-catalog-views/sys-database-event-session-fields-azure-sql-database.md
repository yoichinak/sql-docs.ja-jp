---
description: sys.database_event_session_fields (Azure SQL Database)
title: database_event_session_fields (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
ms.assetid: 9b5c94d6-612c-4e0f-976d-ac6ba55da3ac
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 04479cb0def838e87c472bf17cffc282af298ee7
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537419"
---
# <a name="sysdatabase_event_session_fields-azure-sql-database"></a>sys.database_event_session_fields (Azure SQL Database)
[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

  イベントおよびターゲットに明示的に設定されたカスタマイズ可能な列ごとに 1 行のデータを返します。  
  
||  
|-|  
|**に適用さ**れます: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 およびそれ以降のすべてのバージョン。|  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|イベントセッションの ID。 NULL 値は許可されません。|  
|object_id|**int**|このフィールドに関連付けられているオブジェクトの ID。 NULL 値は許可されません。|  
|name|**sysname**|フィールドの名前。 NULL 値は許可されません。|  
|値|**sql_variant**|フィールドの値。 NULL 値は許可されません。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW DATABASE STATE 権限が必要です。  
  
## <a name="remarks"></a>解説  
 このビューには、次のリレーションシップ基数があります。  
  
| From | 終了 | リレーションシップ |
| ---- | -- | ------------ |
|database_event_session_actions。 event_session_id|database_event_sessions。 event_session_id|多対一|  
|database_event_session_actions。 event_id<br /><br /> database_event_session_actions。 object_id<br /><br /> database_event_session_actions。 event_session_id|database_event_session_events。 event_session_id<br /><br /> database_event_session_events。 event_id|多対一|  
|database_event_session_actions。 event_session_id<br /><br /> database_event_session_actions。 object_id|database_event_session_targets。 event_session_id<br /><br /> database_event_session_targets。 target_id|多対一|  
  
## <a name="see-also"></a>参照  
 [拡張イベント](../../relational-databases/extended-events/extended-events.md)  
  
  
