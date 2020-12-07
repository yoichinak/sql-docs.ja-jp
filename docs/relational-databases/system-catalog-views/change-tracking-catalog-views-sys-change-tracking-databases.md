---
description: カタログビューの Change Tracking-sys.change_tracking_databases
title: sys.change_tracking_databases (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- change_tracking_databases
- sys.change_tracking_databases_TSQL
- sys.change_tracking_databases
- change_tracking_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.change_tracking_databases
- change tracking [SQL Server], sys.change_tracking_databases
ms.assetid: bb233baa-2991-4904-a0eb-3772b81121a4
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 05421e215b41fcf0f1be93b189873c3f0d2aa51c
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810368"
---
# <a name="change-tracking-catalog-views---syschange_tracking_databases"></a>カタログビューの Change Tracking-sys.change_tracking_databases
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  変更の追跡が有効なデータベースごとに 1 行のデータを返します。  

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|database_id|**int**|データベースの ID です。 これは、のインスタンス内で一意です [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|is_auto_cleanup_on|**bit**|構成された保有期間が経過した後に、変更追跡データが自動的にクリーンアップされるかどうかを示します。<br /><br /> 0 = オフ<br /><br /> 1 = On|  
|retention_period|**int**|自動クリーンアップが使用されている場合に、変更追跡データをデータベースに保持する期間を示します。|  
|retention_period_units_desc|**nvarchar(60)**|保有期間の説明を指定します。<br /><br /> 分<br /><br /> 時間<br /><br /> 日間|  
|retention_period_units|**tinyint**|保有期間の時間の単位です。<br /><br /> 1 = 分<br /><br /> 2 = 時間<br /><br /> 3 = 日|  
  
## <a name="permissions"></a>アクセス許可  
 sys.change_tracking_databases には、sys.databases に行われるのと同じ権限チェックが行われます。 sys.change_tracking_databases の呼び出し元がデータベースの所有者でない場合、対応する行を表示するには、少なくとも、ALTER ANY DATABASE または VIEW ANY DATABASE のサーバー レベルの権限か、master データベースまたは現在のデータベースの CREATE DATABASE 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [Change Tracking カタログビュー &#40;Transact-sql&#41;](./catalog-views-transact-sql.md)   
 [データ変更の追跡 &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
