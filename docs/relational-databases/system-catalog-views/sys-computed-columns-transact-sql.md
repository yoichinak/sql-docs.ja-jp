---
description: sys.computed_columns (Transact-sql)
title: sys.computed_columns (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.computed_columns_TSQL
- sys.computed_columns
- computed_columns_TSQL
- computed_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.computed_columns catalog view
ms.assetid: c962c619-e18f-4315-9251-8d9862462299
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a7dbe7e9176605dea875e1846b72e1f00301be55
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98100708"
---
# <a name="syscomputed_columns-transact-sql"></a>sys.computed_columns (Transact-sql)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  列が計算列である場合は、その列の行が格納され **ます。**  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**\<Inherited columns>**||**Sys.computed_columns** ビューでは、すべての列が返されます、**列、ビュー** です。 また、以下に示す追加の列も返されます。 **Sys.computed_columns** ビューが **sys** から継承する列の説明については、「 [sys &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)」を参照してください。 **Sys.computed_columns** ビューでは、 **is_computed** 列の値は常に1に設定されます。|  
|**カスタム**|**nvarchar(max)**|この計算列を定義する SQL テキスト。|  
|**uses_database_collation**|**bit**|1 = 列の定義は、正しい評価のために、データベースの既定の照合順序に依存します。それ以外の場合は0です。 このような依存関係によって、データベースの既定の照合順序を変更できなくなります。|  
|**is_persisted**|**bit**|計算列は保持されます。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
