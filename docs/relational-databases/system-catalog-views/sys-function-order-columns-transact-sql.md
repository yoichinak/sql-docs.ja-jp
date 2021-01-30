---
description: sys.function_order_columns (Transact-SQL)
title: sys.function_order_columns (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- function_order_columns
- sys.function_order_columns_TSQL
- function_order_columns_TSQL
- sys.function_order_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.function_order_columns catalog view
ms.assetid: 29287973-3125-4d35-8ca9-92cb45828854
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: d66bf0eebbe2eb37c95a06cd03f07e2b8e2471f9
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99191442"
---
# <a name="sysfunction_order_columns-transact-sql"></a>sys.function_order_columns (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  共通言語ランタイム (CLR) テーブル値関数の **ORDER** 式の一部である列ごとに1行の値を返します。  

  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|順序が定義されているオブジェクト (CLR テーブル値関数) の ID です。|  
|**order_column_id**|**int**|順序列の ID です **order_column_id** は **object_id** 内でのみ一意です。<br /><br /> **order_column_id** は、順序付けにおけるこの列の位置を表します。|  
|**column_id**|**int**|**Object_id** 内の列の ID。<br /><br /> **column_id** は **object_id** 内でのみ一意です。|  
|**is_descending**|**bit**|1 = 順序列には、降順の並べ替え方向があります。<br /><br /> 0 = 順序列には昇順の並べ替え方向があります。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
