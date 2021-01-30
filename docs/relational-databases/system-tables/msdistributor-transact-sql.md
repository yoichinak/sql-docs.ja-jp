---
description: MSdistributor (Transact-sql)
title: MSdistributor (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- MSdistributor
- MSdistributor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistributor system table
ms.assetid: 981e9903-0b4b-4508-ac6d-2ee4c813a3d0
author: cawrites
ms.author: chadam
ms.openlocfilehash: c87acc9445317555444b8370d8d81a0c530555da
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99160384"
---
# <a name="msdistributor-transact-sql"></a>MSdistributor (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **Msdistributor** テーブルには、ディストリビューターのプロパティが含まれています。 このテーブルは、 **msdb** データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**property**|**sysname**|プロパティの名前|  
|**value**|**nvarchar (3000)**|プロパティの値。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
