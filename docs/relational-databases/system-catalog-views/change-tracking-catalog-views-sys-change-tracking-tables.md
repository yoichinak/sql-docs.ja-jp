---
description: カタログビューの Change Tracking-sys.change_tracking_tables
title: sys.change_tracking_tables (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- change_tracking_tables_TSQL
- sys.change_tracking_tables
- change_tracking_tables
- sys.change_tracking_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- change tracking [SQL Server], sys.change_tracking_tables
- sys.change_tracking_tables
ms.assetid: 97ec69b6-0d49-4d98-82f0-d3e77ba1ad2b
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9f0fb1b5ad1c004f1f4aba688c29138282b71f38
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809618"
---
# <a name="change-tracking-catalog-views---syschange_tracking_tables"></a>カタログビューの Change Tracking-sys.change_tracking_tables
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  変更の追跡が有効な現在のデータベース内のテーブルごとに 1 行のデータを返します。  
   
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|object_id|**int**|変更ジャーナルを持つテーブルの ID。 テーブルは、変更の追跡が現在無効になっている場合でも、変更ジャーナルを持つことができます。<br /><br /> テーブル ID はデータベース内で一意です。|  
|is_track_columns_updated_on|**bit**|テーブルに対する変更の追跡の現在の状態。<br /><br /> 0 = OFF<br /><br /> 1 = ON|  
|begin_version|**bigint**|テーブルで変更の追跡が開始されたときのデータベースのバージョン。 このバージョンは、通常、変更の追跡が有効になったことを示しますが、テーブルが切り捨てられた場合、この値はリセットされます。|  
|cleanup_version|**bigint**|クリーンアップによって変更追跡情報が削除された可能性のあるバージョン。|  
|min_valid_version|**bigint**|テーブルで使用できる変更追跡情報の有効な最小バージョン。<br /><br /> この行に関連付けられているテーブルから変更を取得する場合、last_sync_version には、この列に表示されるバージョンと同じ値か、それよりも大きい値を指定する必要があります。 詳細については、「 [CHANGE_TRACKING_MIN_VALID_VERSION &#40;transact-sql&#41;](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md)」を参照してください。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [CHANGE_TRACKING_MIN_VALID_VERSION &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md)   
 [Change Tracking カタログビュー &#40;Transact-sql&#41;](./catalog-views-transact-sql.md)   
 [データ変更の追跡 &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
