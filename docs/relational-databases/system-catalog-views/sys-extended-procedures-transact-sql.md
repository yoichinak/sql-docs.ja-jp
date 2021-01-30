---
description: sys.extended_procedures (Transact-SQL)
title: sys.extended_procedures (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- extended_procedures
- sys.extended_procedures
- sys.extended_procedures_TSQL
- extended_procedures_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.extended_procedures catalog view
ms.assetid: 310e0f87-0044-4fdf-bd12-51a723a74ce6
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: c148fb0bd8aa9af0f49a6d6e7d5a239af00b64e1
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99203829"
---
# <a name="sysextended_procedures-transact-sql"></a>sys.extended_procedures (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  拡張ストアドプロシージャであるオブジェクトごとに1行の値を格納 **し** ます。型 = X。拡張ストアドプロシージャは、 **master** データベースにインストールされるので、データベースコンテキストからのみ表示されます。 他のデータベースコンテキストの **sys.extended_procedures** ビューからを選択すると、空の結果セットが返されます。  

  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**\<Columns inherited from sys.objects>**||このビューが継承する列の一覧については、「 [sys. objects &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)」を参照してください。|  
|**dll_name**|**nvarchar(260)**|この拡張ストアドプロシージャの DLL の名前 (パスを含む)。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
