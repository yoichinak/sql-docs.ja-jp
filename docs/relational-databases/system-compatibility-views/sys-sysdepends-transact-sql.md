---
description: sys.sysdepends (Transact-SQL)
title: sys.sys依存 (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sys.sysdepends_TSQL
- sysdepends
- sysdepends_TSQL
- sys.sysdepends
dev_langs:
- TSQL
helpviewer_keywords:
- sysdepends system table
- sys.sysdepends compatibility view
ms.assetid: f9c182cb-386f-4e72-859f-9f1115b389f9
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 75cd326cb42798f6541ea1d40cb962b92bf617e1
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99201387"
---
# <a name="syssysdepends-transact-sql"></a>sys.sysdepends (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  データベース内のオブジェクト (ビュー、プロシージャ、トリガー) 間の従属情報と、その定義に含まれるオブジェクト (テーブル、ビュー、プロシージャ) を格納します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|オブジェクト ID|  
|**depid**|**int**|従属しているオブジェクトの ID。|  
|**number**|**smallint**|プロシージャ番号。|  
|**depnumber**|**smallint**|従属しているプロシージャ番号。|  
|**status**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**deptype**|**tinyint**|依存オブジェクトの種類を識別します。<br /><br /> 0 = オブジェクトまたは列 (非スキーマ バインド参照のみ)<br /><br /> 1 = オブジェクトまたは列 (スキーマバインド参照)|  
|**depdbid**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**depsiteid**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**selall**|**bit**|1 = オブジェクトは SELECT * ステートメントで使用されます。<br /><br /> 0 = いいえ。|  
|**resultobj**|**bit**|1 = オブジェクトが更新されています。<br /><br /> 0 = いいえ。|  
|**readobj**|**bit**|1 = オブジェクトが読み取られています。<br /><br /> 0 = いいえ。|  
  
## <a name="see-also"></a>参照  
 [システムビューへのシステムテーブルのマッピング &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [互換性ビュー &#40;Transact-sql&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)   
 [sp_depends &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-depends-transact-sql.md)   
 [sys.sql_dependencies &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md)  
  
  
