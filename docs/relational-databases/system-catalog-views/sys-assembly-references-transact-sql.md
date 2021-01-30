---
description: sys.assembly_references (Transact-sql)
title: sys.assembly_references (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- assembly_references
- sys.assembly_references_TSQL
- assembly_references_TSQL
- sys.assembly_references
dev_langs:
- TSQL
helpviewer_keywords:
- sys.assembly_references catalog view
ms.assetid: 50a5ed42-2d5b-4a11-a0d2-9a02241b078d
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 76f85ecf69c22e2f8f372f2b62e11aef86a0edd1
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99189330"
---
# <a name="sysassembly_references-transact-sql"></a>sys.assembly_references (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  1 つのアセンブリが直接他方を参照している、アセンブリのペアごとに 1 行のデータを保持します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**assembly_id**|**int**|この参照が属するアセンブリの ID。|  
|**referenced_assembly_id**|**int**|参照されているアセンブリの ID です。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [CLR アセンブリカタログビュー &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/clr-assembly-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [ASSEMBLYPROPERTY &#40;Transact-sql&#41;](../../t-sql/functions/assemblyproperty-transact-sql.md)  
  
  
