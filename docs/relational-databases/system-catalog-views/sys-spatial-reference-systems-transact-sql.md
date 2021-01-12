---
description: sys.spatial_reference_systems (Transact-sql)
title: sys.spatial_reference_systems (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- spatial_reference_systems_TSQL
- sys.spatial_reference_systems_TSQL
- sys.spatial_reference_systems
- spatial_reference_systems
dev_langs:
- TSQL
helpviewer_keywords:
- sys.spatial_reference_systems catalog view
- spatial_reference_systems
ms.assetid: 3c9bc120-67c3-463f-9e24-29fd623f25a0
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d968fc9ccb4d54e5345250477d72281152b29f68
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98100189"
---
# <a name="sysspatial_reference_systems-transact-sql"></a>sys.spatial_reference_systems (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でサポートされている空間参照系 (SRID) の一覧を表示します。  

  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|spatial_reference_id|**int**|でサポートされている SRID [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|authority_name|**nvarchar(128)**|SRID の機関。|  
|authorized_spatial_reference_id|**int**|**Authority_name** のという名前の機関によって指定された SRID。|  
|well_known_text|**nvarchar (4000)**|SRID の WKT 表現。|  
|unit_of_measure|**nvarchar(128)**|測定単位の名前。|  
|unit_conversion_factor|**float**|メートル単位の長さ。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
  
