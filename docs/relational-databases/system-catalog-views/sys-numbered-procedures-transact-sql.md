---
description: sys.numbered_procedures (Transact-SQL)
title: numbered_procedures (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.numbered_procedures_TSQL
- numbered_procedures
- sys.numbered_procedures
- numbered_procedures_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.numbered_procedures catalog view
ms.assetid: 5b6d6498-bac6-4266-94b9-d16ef5089cf0
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b849c5f2d02af85f3cab09dfc0cef05a5df8cac1
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539618"
---
# <a name="sysnumbered_procedures-transact-sql"></a>sys.numbered_procedures (Transact-SQL)
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

  番号付きプロシージャとして作成された SQL Server ストアドプロシージャごとに1行の値を格納します。 この場合、ベース (number = 1) ストアドプロシージャの行は表示されません。 基本ストアドプロシージャのエントリは、 **sys. objects** や **sys. プロシージャ**などのビューにあります。  
  
> [!IMPORTANT]  
>  番号付きプロシージャは非推奨とされます。 番号付きプロシージャの使用は推奨されません。 このカタログビューを使用するクエリがコンパイルされると、DEPRECATION_ANNOUNCEMENT イベントが発生します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ストアドプロシージャのオブジェクトの ID。|  
|**procedure_number**|**smallint**|オブジェクト内のこのプロシージャの数 (2 以上)。|  
|**カスタム**|**nvarchar(max)**|このプロシージャを定義する SQL Server テキスト。<br /><br /> NULL = 暗号化されています。|  
  
> [!NOTE]  
>  XML および CLR パラメーターは、番号付きプロシージャではサポートされていません。  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
