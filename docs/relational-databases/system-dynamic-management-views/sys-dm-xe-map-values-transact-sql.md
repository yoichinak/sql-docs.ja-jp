---
description: dm_xe_map_values (Transact-sql)
title: dm_xe_map_values (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_xe_map_values
- dm_xe_map_values
- dm_xe_map_values_TSQL
- sys.dm_xe_map_values_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_map_values dynamic management view
- xe
ms.assetid: c0c5dd7e-9cee-47e2-b65a-88194c00aa1f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 235f6d9bf0d84985d9749f9cae5ee2b93460feae
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546361"
---
# <a name="sysdm_xe_map_values-transact-sql"></a>dm_xe_map_values (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ユーザーによる判読が可能なテキストに対する内部数値キーのマッピングを返します。  
 
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|name|**nvarchar (256)**|マップの名前。 名前はローカルシステム全体で一意です。 NULL 値は許可されません。|  
|object_package_guid|**uniqueidentifier**|マップを含むパッケージの GUID。 NULL 値は許可されません。|  
|map_key|**int**|内部キー値。 NULL 値は許可されません。|  
|map_value|**nvarchar (3072)**|キー値の説明。 NULL 値は許可されません。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
### <a name="relationship-cardinalities"></a>リレーションシップ基数  
  
|From|終了|リレーションシップ|  
|----------|--------|------------------|  
|dm_xe_map_values.object_package_guid<br /><br /> dm_xe_map_values.name|sys.dm_xe_objects.package_guid<br /><br /> sys.dm_xe_objects.name|多対一| 
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

