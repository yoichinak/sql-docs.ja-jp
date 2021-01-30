---
description: sys.dm_xe_database_session_targets (Azure SQL Database)
title: sys.dm_xe_database_session_targets
titleSuffix: Azure SQL Database
ms.date: 06/10/2016
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: reference
ms.assetid: 7f353e2a-f8fc-4366-97e4-aa1c49eadaf4
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: = azuresqldb-current
ms.custom: seo-dt-2019
ms.openlocfilehash: 0012b735fe99a2ef68989ee0b714a86e9efc0892
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99130268"
---
# <a name="sysdm_xe_database_session_targets-azure-sql-database"></a>sys.dm_xe_database_session_targets (Azure SQL Database)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  セッション ターゲットに関する情報を返します。  
  
||  
|-|  
|**適用対象**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 および将来のすべてのバージョン。|  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary (8)**|イベントセッションのメモリアドレス。 には、sys.dm_xe_database_sessions との多対一のリレーションシップがあります。 NULL 値は許可されません。|  
|target_name|**nvarchar(60)**|セッション内のターゲットの名前。 NULL 値は許可されません。|  
|target_package_guid|**uniqueidentifier**|ターゲットを含むパッケージの GUID。 NULL 値は許可されません。|  
|execution_count|**bigint**|セッションに対してターゲットが実行された回数。 NULL 値は許可されません。|  
|execution_duration_ms|**bigint**|ターゲットが実行された時間の合計 (ミリ秒単位)。 NULL 値は許可されません。|  
|target_data|**nvarchar(max)**|イベント集計情報など、ターゲットが保持するデータ。 NULL 値が許可されます。|  
  
## <a name="permissions"></a>アクセス許可  
 VIEW DATABASE STATE 権限が必要です。  
  
### <a name="relationship-cardinalities"></a>リレーションシップ基数  
  
|差出人|終了|リレーションシップ|  
|----------|--------|------------------|  
|sys.dm_xe_database_session_targets sys.dm_xe_database_session_targets.event_session_address|sys.dm_xe_database_sessions。アドレス|多対一|  
  
  
