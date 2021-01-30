---
description: sys.sysforeignkeys (Transact-sql)
title: sys.sysforeignkeys (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sysforeignkeys
- sys.sysforeignkeys
- sys.sysforeignkeys_TSQL
- sysforeignkeys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysforeignkeys system table
- sys.sysforeignkeys compatibility view
ms.assetid: 41544236-1c46-4501-be88-18c06963b6e8
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: edbb686df3d410b6049bca2799e0f10b2ff07db8
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99158528"
---
# <a name="syssysforeignkeys-transact-sql"></a>sys.sysforeignkeys (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  データベース中のテーブルの定義内にある、FOREIGN KEY 制約に関する情報を保持します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**constid**|**int**|外部キー制約の ID。|  
|**fkeyid**|**int**|FOREIGN KEY 制約を持つテーブルのオブジェクト ID。|  
|**rkeyid**|**int**|FOREIGN KEY 制約で参照されているテーブルのオブジェクト ID。|  
|**fkey**|**smallint**|参照している列の ID。|  
|**rkey**|**smallint**|参照されている列の ID。|  
|**keyno**|**smallint**|参照列リスト内の列の位置。|  
  
## <a name="see-also"></a>参照  
 [システムビューへのシステムテーブルのマッピング &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [互換性ビュー &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
